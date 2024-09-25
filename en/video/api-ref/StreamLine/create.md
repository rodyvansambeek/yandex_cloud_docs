---
editable: false
sourcePath: en/_api-ref/video/v1/api-ref/StreamLine/create.md
---

# Video API, REST: StreamLine.create
Create stream line.
 

 
## HTTP request {#https-request}
```
POST https://video.{{ api-host }}/video/v1/streamLines
```
 
## Body parameters {#body_params}
 
```json 
{
  "channelId": "string",
  "title": "string",
  "thumbnailId": "string",
  "labels": "object",

  //  includes only one of the fields `manualLine`, `autoLine`
  "rtmpPush": {},
  "srtPush": {},
  "rtmpPull": {
    "url": "string"
  },
  "srtPull": {
    "url": "string"
  },
  "tcpPull": {
    "url": "string"
  },
  "rtspPull": {
    "url": "string"
  },
  // end of the list of possible fields

  "manualLine": {},
  "autoLine": {}
}
```

 
Field | Description
--- | ---
channelId | **string**<br><p>ID of the channel.</p> 
title | **string**<br><p>Line title.</p> 
thumbnailId | **string**<br><p>ID of the thumbnail.</p> 
labels | **object**<br><p>Custom labels as ``key:value`` pairs. Maximum 64 per resource.</p> 
rtmpPush | **object**<br>RTMP push input type. <br> includes only one of the fields `rtmpPush`, `srtPush`, `rtmpPull`, `srtPull`, `tcpPull`, `rtspPull`<br>
srtPush | **object**<br>SRT push input type. <br> includes only one of the fields `rtmpPush`, `srtPush`, `rtmpPull`, `srtPull`, `tcpPull`, `rtspPull`<br>
rtmpPull | **object**<br>RTMP pull input type. <br> includes only one of the fields `rtmpPush`, `srtPush`, `rtmpPull`, `srtPull`, `tcpPull`, `rtspPull`<br>
rtmpPull.<br>url | **string**<br><p>URL of a RTMP streaming server.</p> 
srtPull | **object**<br>SRT pull input type. <br> includes only one of the fields `rtmpPush`, `srtPush`, `rtmpPull`, `srtPull`, `tcpPull`, `rtspPull`<br>
srtPull.<br>url | **string**<br><p>URL of a SRT streaming server.</p> 
tcpPull | **object**<br>TCP pull input type. <br> includes only one of the fields `rtmpPush`, `srtPush`, `rtmpPull`, `srtPull`, `tcpPull`, `rtspPull`<br>
tcpPull.<br>url | **string**<br><p>URL of a TCP streaming server.</p> 
rtspPull | **object**<br>RTSP pull input type. <br> includes only one of the fields `rtmpPush`, `srtPush`, `rtmpPull`, `srtPull`, `tcpPull`, `rtspPull`<br>
rtspPull.<br>url | **string**<br><p>URL of a RTSP streaming server.</p> 
manualLine | **object**<br>Manual control of stream. <br> includes only one of the fields `manualLine`, `autoLine`<br>
autoLine | **object**<br>Automatic control of stream. <br> includes only one of the fields `manualLine`, `autoLine`<br>
 
## Response {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "id": "string",
  "description": "string",
  "createdAt": "string",
  "createdBy": "string",
  "modifiedAt": "string",
  "done": true,
  "metadata": "object",

  //  includes only one of the fields `error`, `response`
  "error": {
    "code": "integer",
    "message": "string",
    "details": [
      "object"
    ]
  },
  "response": "object",
  // end of the list of possible fields

}
```
An Operation resource. For more information, see [Operation](/docs/api-design-guide/concepts/operation).
 
Field | Description
--- | ---
id | **string**<br><p>ID of the operation.</p> 
description | **string**<br><p>Description of the operation. 0-256 characters long.</p> 
createdAt | **string** (date-time)<br><p>Creation timestamp.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format. The range of possible values is from ``0001-01-01T00:00:00Z`` to ``9999-12-31T23:59:59.999999999Z``, i.e. from 0 to 9 digits for fractions of a second.</p> <p>To work with values in this field, use the APIs described in the <a href="https://developers.google.com/protocol-buffers/docs/reference/overview">Protocol Buffers reference</a>. In some languages, built-in datetime utilities do not support nanosecond precision (9 digits).</p> 
createdBy | **string**<br><p>ID of the user or service account who initiated the operation.</p> 
modifiedAt | **string** (date-time)<br><p>The time when the Operation resource was last modified.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format. The range of possible values is from ``0001-01-01T00:00:00Z`` to ``9999-12-31T23:59:59.999999999Z``, i.e. from 0 to 9 digits for fractions of a second.</p> <p>To work with values in this field, use the APIs described in the <a href="https://developers.google.com/protocol-buffers/docs/reference/overview">Protocol Buffers reference</a>. In some languages, built-in datetime utilities do not support nanosecond precision (9 digits).</p> 
done | **boolean** (boolean)<br><p>If the value is ``false``, it means the operation is still in progress. If ``true``, the operation is completed, and either ``error`` or ``response`` is available.</p> 
metadata | **object**<br><p>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any.</p> 
error | **object**<br>The error result of the operation in case of failure or cancellation. <br> includes only one of the fields `error`, `response`<br>
error.<br>code | **integer** (int32)<br><p>Error code. An enum value of <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">google.rpc.Code</a>.</p> 
error.<br>message | **string**<br><p>An error message.</p> 
error.<br>details[] | **object**<br><p>A list of messages that carry the error details.</p> 
response | **object** <br> includes only one of the fields `error`, `response`<br><br><p>The normal response of the operation in case of success. If the original method returns no data on success, such as Delete, the response is <a href="https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#empty">google.protobuf.Empty</a>. If the original method is the standard Create/Update, the response should be the target resource of the operation. Any method that returns a long-running operation should document the response type, if any.</p> 