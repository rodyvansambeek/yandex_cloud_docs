---
editable: false
sourcePath: en/_api-ref-grpc/compute/v1/api-ref/grpc/Disk/list.md
---

# Compute Cloud API, gRPC: DiskService.List {#List}

Retrieves the list of Disk resources in the specified folder.

## gRPC request

**rpc List ([ListDisksRequest](#yandex.cloud.compute.v1.ListDisksRequest)) returns ([ListDisksResponse](#yandex.cloud.compute.v1.ListDisksResponse))**

## ListDisksRequest {#yandex.cloud.compute.v1.ListDisksRequest}

```json
{
  "folderId": "string",
  "pageSize": "int64",
  "pageToken": "string",
  "filter": "string",
  "orderBy": "string"
}
```

#|
||Field | Description ||
|| folderId | **string**

Required field. ID of the folder to list disks in.
To get the folder ID use a [yandex.cloud.resourcemanager.v1.FolderService.List](/docs/resource-manager/api-ref/grpc/Folder/list#List) request. ||
|| pageSize | **int64**

The maximum number of results per page to return. If the number of available
results is larger than `pageSize`,
the service returns a [ListDisksResponse.nextPageToken](#yandex.cloud.compute.v1.ListDisksResponse)
that can be used to get the next page of results in subsequent list requests. ||
|| pageToken | **string**

Page token. To get the next page of results, set `pageToken` to the
[ListDisksResponse.nextPageToken](#yandex.cloud.compute.v1.ListDisksResponse) returned by a previous list request. ||
|| filter | **string**

A filter expression that filters resources listed in the response.
The expression consists of one or more conditions united by `AND` operator: `<condition1> [AND <condition2> [<...> AND <conditionN>]]`.

Each condition has the form `<field> <operator> <value>`, where:
1. `<field>` is the field name. Currently you can use filtering only on the limited number of fields.
2. `<operator>` is a logical operator, one of `=`, `!=`, `IN`, `NOT IN`.
3. `<value>` represents a value.
String values should be written in double (`"`) or single (`'`) quotes. C-style escape sequences are supported (`\"` turns to `"`, `\'` to `'`, `\\` to backslash). ||
|| orderBy | **string**

By which column the listing should be ordered and in which direction,
format is "createdAt desc". "id asc" if omitted.
The default sorting order is ascending ||
|#

## ListDisksResponse {#yandex.cloud.compute.v1.ListDisksResponse}

```json
{
  "disks": [
    {
      "id": "string",
      "folderId": "string",
      "createdAt": "google.protobuf.Timestamp",
      "name": "string",
      "description": "string",
      "labels": "string",
      "typeId": "string",
      "zoneId": "string",
      "size": "int64",
      "blockSize": "int64",
      "productIds": [
        "string"
      ],
      "status": "Status",
      // Includes only one of the fields `sourceImageId`, `sourceSnapshotId`
      "sourceImageId": "string",
      "sourceSnapshotId": "string",
      // end of the list of possible fields
      "instanceIds": [
        "string"
      ],
      "diskPlacementPolicy": {
        "placementGroupId": "string",
        "placementGroupPartition": "int64"
      },
      "hardwareGeneration": {
        // Includes only one of the fields `legacyFeatures`, `generation2Features`
        "legacyFeatures": {
          "pciTopology": "PCITopology"
        },
        "generation2Features": "Generation2HardwareFeatures"
        // end of the list of possible fields
      },
      "kmsKey": {
        "keyId": "string",
        "versionId": "string"
      }
    }
  ],
  "nextPageToken": "string"
}
```

#|
||Field | Description ||
|| disks[] | **[Disk](#yandex.cloud.compute.v1.Disk)**

List of Disk resources. ||
|| nextPageToken | **string**

This token allows you to get the next page of results for list requests. If the number of results
is larger than [ListDisksRequest.pageSize](#yandex.cloud.compute.v1.ListDisksRequest), use
the `nextPageToken` as the value
for the [ListDisksRequest.pageToken](#yandex.cloud.compute.v1.ListDisksRequest) query parameter
in the next list request. Each subsequent list request will have its own
`nextPageToken` to continue paging through the results. ||
|#

## Disk {#yandex.cloud.compute.v1.Disk}

A Disk resource. For more information, see [Disks](/docs/compute/concepts/disk).

#|
||Field | Description ||
|| id | **string**

ID of the disk. ||
|| folderId | **string**

ID of the folder that the disk belongs to. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)** ||
|| name | **string**

Name of the disk. 1-63 characters long. ||
|| description | **string**

Description of the disk. 0-256 characters long. ||
|| labels | **string**

Resource labels as `key:value` pairs. Maximum of 64 per resource. ||
|| typeId | **string**

ID of the disk type. ||
|| zoneId | **string**

ID of the availability zone where the disk resides. ||
|| size | **int64**

Size of the disk, specified in bytes. ||
|| blockSize | **int64**

Block size of the disk, specified in bytes. ||
|| productIds[] | **string**

License IDs that indicate which licenses are attached to this resource.
License IDs are used to calculate additional charges for the use of the virtual machine.

The correct license ID is generated by the platform. IDs are inherited by new resources created from this resource.

If you know the license IDs, specify them when you create the image.
For example, if you create a disk image using a third-party utility and load it into Object Storage, the license IDs will be lost.
You can specify them in the [yandex.cloud.compute.v1.ImageService.Create](/docs/compute/api-ref/grpc/Image/create#Create) request. ||
|| status | enum **Status**

Current status of the disk.

- `STATUS_UNSPECIFIED`
- `CREATING`: Disk is being created.
- `READY`: Disk is ready to use.
- `ERROR`: Disk encountered a problem and cannot operate.
- `DELETING`: Disk is being deleted. ||
|| sourceImageId | **string**

ID of the image that was used for disk creation.

Includes only one of the fields `sourceImageId`, `sourceSnapshotId`. ||
|| sourceSnapshotId | **string**

ID of the snapshot that was used for disk creation.

Includes only one of the fields `sourceImageId`, `sourceSnapshotId`. ||
|| instanceIds[] | **string**

Array of instances to which the disk is attached. ||
|| diskPlacementPolicy | **[DiskPlacementPolicy](#yandex.cloud.compute.v1.DiskPlacementPolicy)**

Placement policy configuration. ||
|| hardwareGeneration | **[HardwareGeneration](#yandex.cloud.compute.v1.HardwareGeneration)**

If specified, forces the same HardwareGeneration features to be applied to the instance
created using this disk as a boot one. Otherwise the current default will be used. ||
|| kmsKey | **[KMSKey](#yandex.cloud.compute.v1.KMSKey)**

Key encryption key info. ||
|#

## DiskPlacementPolicy {#yandex.cloud.compute.v1.DiskPlacementPolicy}

#|
||Field | Description ||
|| placementGroupId | **string**

Placement group ID. ||
|| placementGroupPartition | **int64** ||
|#

## HardwareGeneration {#yandex.cloud.compute.v1.HardwareGeneration}

A set of features, specific to a particular Compute hardware generation.
They are not necessary supported by every host OS or distro, thus they are fixed to an image
and are applied to all instances created with it as their boot disk image.
These features significantly determine how the instance is created, thus cannot be changed after the fact.

#|
||Field | Description ||
|| legacyFeatures | **[LegacyHardwareFeatures](#yandex.cloud.compute.v1.LegacyHardwareFeatures)**

Includes only one of the fields `legacyFeatures`, `generation2Features`. ||
|| generation2Features | **[Generation2HardwareFeatures](#yandex.cloud.compute.v1.Generation2HardwareFeatures)**

Includes only one of the fields `legacyFeatures`, `generation2Features`. ||
|#

## LegacyHardwareFeatures {#yandex.cloud.compute.v1.LegacyHardwareFeatures}

A first hardware generation, by default compatible with all legacy images.
Allows switching to PCI_TOPOLOGY_V2 and back.

#|
||Field | Description ||
|| pciTopology | enum **PCITopology**

- `PCI_TOPOLOGY_UNSPECIFIED`
- `PCI_TOPOLOGY_V1`
- `PCI_TOPOLOGY_V2` ||
|#

## Generation2HardwareFeatures {#yandex.cloud.compute.v1.Generation2HardwareFeatures}

A second hardware generation, which by default assumes PCI_TOPOLOGY_V2
and UEFI boot (with UEFI related features).

#|
||Field | Description ||
|| Empty | > ||
|#

## KMSKey {#yandex.cloud.compute.v1.KMSKey}

#|
||Field | Description ||
|| keyId | **string**

ID of KMS symmetric key ||
|| versionId | **string**

Version of KMS symmetric key ||
|#