# Управление доступом {{ serverless-containers-name }}

В этом разделе вы узнаете:

* [на какие ресурсы можно назначить роль](#resources);
* [какие роли действуют в сервисе](#roles).

{% include [about-access-management](../../_includes/iam/about-access-management.md) %}

## На какие ресурсы можно назначить роль {#resources}

Роль можно назначить на [облако](../../resource-manager/concepts/resources-hierarchy.md#cloud), [каталог](../../resource-manager/concepts/resources-hierarchy.md#folder) и [контейнер](../concepts/container.md).

## Какие роли действуют в сервисе {#roles}

Ниже перечислены все роли, которые учитываются при проверке прав доступа в сервисе {{ serverless-containers-name }}.

{% include [cloud-roles](../../_includes/cloud-roles.md) %}

{% include [serverless-containers-roles-viewer](../../_includes/roles-serverless-containers-viewer.md) %}

{% include [serverless-containers-roles-invoker](../../_includes/roles-serverless-containers-invoker.md) %}

{% include [serverless-containers-roles-editor](../../_includes/roles-serverless-containers-editor.md) %}

{% include [serverless-containers-roles-admin](../../_includes/roles-serverless-containers-admin.md) %}

### {{ roles-viewer }} {#viewer}

Пользователь с ролью `{{ roles-viewer }}` может просматривать информацию о ресурсах, например, посмотреть список контейнеров или их ревизий.

### {{ roles-editor }} {#editor}

Пользователь с ролью `{{ roles-editor }}` может управлять контейнерами, например, создать контейнер или вызвать его.

Помимо этого роль `{{ roles-editor }}` включает в себя все разрешения роли `{{ roles-viewer }}`.

### {{ roles-admin }} {#admin}

Пользователь с ролью `{{ roles-admin }}` может управлять правами доступа к ресурсам, например, разрешить другим пользователям вызывать контейнер.

Помимо этого роль `{{ roles-admin }}` включает в себя все разрешения роли `{{ roles-editor }}`.