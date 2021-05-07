# UpdateImageInfos

Modifies the information about one or more images at a time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateImageInfos&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateImageInfos|The operation that you want to perform. Set the value to **UpdateImageInfos**. |
|UpdateContent|String|Yes|\[\{"ImageId":"ff8fe57e3461416c\*\*\*\*\*6a267a4e09","Title":"Title","Description":"Description","Tags":"Tag 1,Tag 2"\}\]|The new information about the one or more images. You can modify the information about up to 20 images at a time. For more information, see the **UpdateContent** section of this topic.

 **Note:** The values of the nested parameters Title, Description, and Tags under the UpdateContent parameter cannot contain emoticons. |

## UpdateContent

**Note:** You must convert the UpdateContent`[]` parameter to a string before you pass it in.

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|ImageId

|String

|Yes

|The ID of the image. |
|Title

|String

|No

|The title of the image. The title can be up to 128 bytes in length. Encode the title in UTF-8. |
|Description

|String

|No

|The description of the image. The description can be up to 1,024 bytes in length. Encode the description in UTF-8. |
|Tags

|String

|No

|The tags of the image. Each tag can be up to 32 bytes in length. You can specify a maximum of 16 tags. Separate multiple tags with commas \(,\). Encode the tags in UTF-8. |
|CateId

|Long

|No

|The ID of the category. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NonExistImageIds|List|f45cf4eba5c8\*\*\*\*\*0233389558c39|The IDs of the images that do not exist. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateImageInfos
&UpdateContent=[{"ImageId":"ff8fe57e3461416c*****6a267a4e09","Title":"Title","Description":"Description","Tags":"Tag 1,Tag 2"}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateImageInfosResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <NonExistImageIds>f45cf4eba5c8*****0233389558c39</NonExistImageIds>
</UpdateImageInfosResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "NonExistImageIds":["f45cf4eba5c8*****0233389558c39"]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

