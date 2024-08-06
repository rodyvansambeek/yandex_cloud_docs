{% note warning %}

Этот метод API переопределит все параметры изменяемого объекта, которые не были явно переданы в запросе, на значения по умолчанию. Чтобы избежать этого, перечислите настройки, которые вы хотите изменить, в параметре `update_mask` (в виде массива строк `paths[]`).

{% cut "Формат перечисления настроек" %}

```yaml
"update_mask": {
    "paths": [
        "<настройка_1>",
        "<настройка_2>",
        ...
        "<настройка_N>"
    ]
}
```

{% endcut %}

{% endnote %}