---
editable: false
sourcePath: en/_api-ref-grpc/mdb/mysql/v1/api-ref/grpc/Database/create.md
---

# Managed Service for MySQL API, gRPC: DatabaseService.Create {#Create}

Creates a new database in a cluster.

## gRPC request

**rpc Create ([CreateDatabaseRequest](#yandex.cloud.mdb.mysql.v1.CreateDatabaseRequest)) returns ([operation.Operation](#yandex.cloud.operation.Operation))**

## CreateDatabaseRequest {#yandex.cloud.mdb.mysql.v1.CreateDatabaseRequest}

```json
{
  "clusterId": "string",
  "databaseSpec": {
    "name": "string"
  }
}
```

#|
||Field | Description ||
|| clusterId | **string**

Required field. ID of the cluster to create the database in.

To get this ID, make a [ClusterService.List](/docs/managed-mysql/api-ref/grpc/Cluster/list#List) request. ||
|| databaseSpec | **[DatabaseSpec](#yandex.cloud.mdb.mysql.v1.DatabaseSpec)**

Required field. Configuration of the database. ||
|#

## DatabaseSpec {#yandex.cloud.mdb.mysql.v1.DatabaseSpec}

#|
||Field | Description ||
|| name | **string**

Required field. Name of the database. ||
|#

## operation.Operation {#yandex.cloud.operation.Operation}

```json
{
  "id": "string",
  "description": "string",
  "createdAt": "google.protobuf.Timestamp",
  "createdBy": "string",
  "modifiedAt": "google.protobuf.Timestamp",
  "done": "bool",
  "metadata": {
    "clusterId": "string",
    "databaseName": "string"
  },
  // Includes only one of the fields `error`, `response`
  "error": "google.rpc.Status",
  "response": {
    "name": "string",
    "clusterId": "string"
  }
  // end of the list of possible fields
}
```

An Operation resource. For more information, see [Operation](/docs/api-design-guide/concepts/operation).

#|
||Field | Description ||
|| id | **string**

ID of the operation. ||
|| description | **string**

Description of the operation. 0-256 characters long. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Creation timestamp. ||
|| createdBy | **string**

ID of the user or service account who initiated the operation. ||
|| modifiedAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

The time when the Operation resource was last modified. ||
|| done | **bool**

If the value is `false`, it means the operation is still in progress.
If `true`, the operation is completed, and either `error` or `response` is available. ||
|| metadata | **[CreateDatabaseMetadata](#yandex.cloud.mdb.mysql.v1.CreateDatabaseMetadata)**

Service-specific metadata associated with the operation.
It typically contains the ID of the target resource that the operation is performed on.
Any method that returns a long-running operation should document the metadata type, if any. ||
|| error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**

The error result of the operation in case of failure or cancellation.

Includes only one of the fields `error`, `response`.

The operation result.
If `done == false` and there was no failure detected, neither `error` nor `response` is set.
If `done == false` and there was a failure detected, `error` is set.
If `done == true`, exactly one of `error` or `response` is set. ||
|| response | **[Database](#yandex.cloud.mdb.mysql.v1.Database)**

The normal response of the operation in case of success.
If the original method returns no data on success, such as Delete,
the response is [google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty).
If the original method is the standard Create/Update,
the response should be the target resource of the operation.
Any method that returns a long-running operation should document the response type, if any.

Includes only one of the fields `error`, `response`.

The operation result.
If `done == false` and there was no failure detected, neither `error` nor `response` is set.
If `done == false` and there was a failure detected, `error` is set.
If `done == true`, exactly one of `error` or `response` is set. ||
|#

## CreateDatabaseMetadata {#yandex.cloud.mdb.mysql.v1.CreateDatabaseMetadata}

#|
||Field | Description ||
|| clusterId | **string**

ID of the cluster the database is being created in. ||
|| databaseName | **string**

Name of the database that is being created. ||
|#

## Database {#yandex.cloud.mdb.mysql.v1.Database}

An object that represents MySQL database.

See [the documentation](/docs/managed-mysql/operations/databases) for details.

#|
||Field | Description ||
|| name | **string**

Name of the database. ||
|| clusterId | **string**

ID of the cluster that the database belongs to. ||
|#