---
editable: false
sourcePath: en/_api-ref-grpc/iam/v1/api-ref/grpc/UserAccount/get.md
---

# Identity and Access Management API, gRPC: UserAccountService.Get {#Get}

Returns the specified UserAccount resource.

## gRPC request

**rpc Get ([GetUserAccountRequest](#yandex.cloud.iam.v1.GetUserAccountRequest)) returns ([UserAccount](#yandex.cloud.iam.v1.UserAccount))**

## GetUserAccountRequest {#yandex.cloud.iam.v1.GetUserAccountRequest}

```json
{
  "userAccountId": "string"
}
```

#|
||Field | Description ||
|| userAccountId | **string**

Required field. ID of the UserAccount resource to return. ||
|#

## UserAccount {#yandex.cloud.iam.v1.UserAccount}

```json
{
  "id": "string",
  // Includes only one of the fields `yandexPassportUserAccount`, `samlUserAccount`
  "yandexPassportUserAccount": {
    "login": "string",
    "defaultEmail": "string"
  },
  "samlUserAccount": {
    "federationId": "string",
    "nameId": "string",
    "attributes": {
      "value": [
        "string"
      ]
    }
  }
  // end of the list of possible fields
}
```

Currently represents only [Yandex account](/docs/iam/concepts/#passport).

#|
||Field | Description ||
|| id | **string**

ID of the user account. ||
|| yandexPassportUserAccount | **[YandexPassportUserAccount](#yandex.cloud.iam.v1.YandexPassportUserAccount)**

A YandexPassportUserAccount resource.

Includes only one of the fields `yandexPassportUserAccount`, `samlUserAccount`. ||
|| samlUserAccount | **[SamlUserAccount](#yandex.cloud.iam.v1.SamlUserAccount)**

A SAML federated user.

Includes only one of the fields `yandexPassportUserAccount`, `samlUserAccount`. ||
|#

## YandexPassportUserAccount {#yandex.cloud.iam.v1.YandexPassportUserAccount}

A YandexPassportUserAccount resource.
For more information, see [Yandex account](/docs/iam/concepts/#passport).

#|
||Field | Description ||
|| login | **string**

Login of the Yandex user account. ||
|| defaultEmail | **string**

Default email of the Yandex user account. ||
|#

## SamlUserAccount {#yandex.cloud.iam.v1.SamlUserAccount}

A SAML federated user.
For more information, see [federations](/docs/iam/concepts/federations).

#|
||Field | Description ||
|| federationId | **string**

Required field. ID of the federation that the federation belongs to. ||
|| nameId | **string**

Required field. Name Id of the SAML federated user.
The name is unique within the federation. 1-256 characters long. ||
|| attributes | **[Attribute](#yandex.cloud.iam.v1.SamlUserAccount.Attribute)**

Additional attributes of the SAML federated user. ||
|#

## Attribute {#yandex.cloud.iam.v1.SamlUserAccount.Attribute}

#|
||Field | Description ||
|| value[] | **string** ||
|#