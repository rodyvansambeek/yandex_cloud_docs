---
sourcePath: ru/ydb/ydb-docs-core/ru/core/best_practices/_includes/pk_scalability.md
---
# Выбор первичного ключа для максимальной производительности

Выбор колонок для первичного ключа таблицы оказывает определяющее влияние на возможности YDB по масштабированию нагрузки и повышению производительности.

Общие рекомендации по выбору первичного ключа:

* Следует избегать ситуаций, когда основная часть нагрузки приходится на одну [партицию](../../concepts/datamodel.md#partitioning) таблицы. Чем равномернее нагрузка распределяется по партициям, тем большая производительность может быть достигнута.
* Следует уменьшать количество партиций, которые могут быть затронуты в одном запросе. Более того, если запрос затрагивает не более одной партиции, то он выполняется по специальному упрощенному протоколу, что существенно увеличивает скорость и экономит ресурсы.

Все таблицы в {{ ydb-short-name }} отсортированы по возрастанию первичного ключа. Это означает, что запись в таблицу данных с монотонно возрастающим первичным ключом приведет к добавлению новых данные в конец таблицы. Так как {{ ydb-short-name }} разделяет таблицы на партиции по диапазонам ключей, вставки будут обрабатываться одним конкретным сервером, отвечающим за "последнюю" партицию. Сосредоточение нагрузки на одном сервере приведет к медленной загрузке данных и неэффективному использованию распределенной системы.
В качестве примера рассмотрим запись лога пользовательских событий в таблицу со схемой ```( timestamp, userid, userevent, PRIMARY KEY (timestamp, userid) )```.

```timestamp``` монотонно возрастает, как следствие, все записи будут записываться в конец таблицы и "последняя" партиция, которая отвечает за данный диапазон ключей, будет обслуживать все записи в таблицу. Это приведет к невозможности масштабирования нагрузки на запись, производительность будет ограничена одним процессом обслуживания этой партиции, и не будет расти с добавлением серверов в кластер.

В {{ ydb-short-name }} поддерживается автоматическое разделение партиции при достижении порогового размера или нагрузки. Но в рассматриваемом случае после разделения новая партиция начнет опять принимать всю нагрузку на запись, и ситуация повторится.

## Приемы, позволяющие равномерно распределить нагрузку по партициям таблицы {#balance-shard-load}

### Изменение порядка следования компонент ключа {#key-order}

Запись данных в таблицу со схемой ```( timestamp, userid, userevent, PRIMARY KEY (timestamp, userid) )``` приводит к неравномерной нагрузке на партиции таблицы из-за монотонно возрастающего первичного ключа. Изменение порядка следования компонент ключа таким образом, чтобы монотонно возрастающая часть не была первой компонентой, может помочь более равномерно распределить нагрузку. Если изменить схему таблицы на ```( timestamp, userid, userevent, PRIMARY KEY (userid, timestamp) )```, то при достаточном количестве пользователей, генерирующих события, запись в БД будет распределена по партициям более равномерно.

### Использование хеша от значений ключевых колонок в качестве первичного ключа {#key-hash}

Рассмотрим таблицу со схемой ```( timestamp, userid, userevent, PRIMARY KEY (userid, timestamp) )```. В качестве всего первичного ключа или его первой компоненты можно использовать хеш от исходного ключа, например так:

```
( HASH(timestamp, userid), timestamp, userid, userevent, PRIMARY KEY (HASH(userid), userid, timestamp) )
```

При правильном выборе функции хеширования строки будут распределены достаточно равномерно по всему пространству ключей, что в приведет к равномерной нагрузке на систему. При этом, наличие полей ```userid, timestamp``` в составе ключа после ```HASH(userid)``` сохраняет локальность и сортировку данных по времени для конкретного пользователя.

### Уменьшение количества партиций, затрагиваемых в одном запросе {#decrease-shards}

Предположим, что основной сценарий работы с данными таблицы — прочитать все события по конкретному ```userid```. Тогда при использовании схемы таблицы ```( timestamp, userid, userevent, PRIMARY KEY (timestamp, userid) )``` каждое чтение будет затрагивать все партиции таблицы. При этом, каждая партиция будет просканирована полностью, так как строки, относящиеся к конкретному ```userid```, расположены в заранее неизвестном порядке. Изменение порядка следования компонент ключа ```( timestamp, userid, userevent, PRIMARY KEY (userid, timestamp) )``` приведет к тому, что все строки, относящиеся к конкретному ```userid```, будут следовать друг за другом. Такое расположение строк положительно повлияет на скорость чтения информации по конкретному ```userid```.

## Значение NULL в ключевой колонке {#key-null}

В {{ ydb-short-name }} все колонки, включая ключевые, могут содержать значение NULL. Использование NULL в качестве значений в ключевых колонках не рекомендуется. По стандарту языка SQL (ISO/IEC&nbsp;9075) значение NULL нельзя сравнивать с другими значениями, вследствие чего использование лаконичных конструкции SQL с простыми операторами сравнения может приводить, например, к тому что, строки, содержащие значение NULL, могут быть пропущены при фильтрации.

## Ограничение размера строки {#limit-string}

Для достижения хорошей производительности не рекомендуется записывать в БД строки размером более 8 МБ и ключевые колонки размером более 2 КБ.