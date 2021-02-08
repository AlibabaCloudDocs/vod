# DeleteImage

Deletes uploaded images and automatic snapshots of videos.

**Note:** This operation irreversibly deletes image mezzanine files. Deleted images cannot be recovered. If some images are cached in Content Delivery Network \(CDN\), the image URLs do not immediately become invalid.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteImage&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteImage|The operation that you want to perform. Set the value to **DeleteImage**. |
|DeleteImageType|String|Yes|VideoId|The method that is used to delete images. Valid values:

 -   **ImageURL**: Delete the specified image based on the image URL.
-   **ImageId**: Delete the specified image based on the image ID.
-   **VideoId**: Delete the image that is associated with a video ID. |
|ImageURLs|String|No|https://al\*\*\*\*\*.cn/image/default/41AE7ADABBE\*\*\*\*\*.png|The URL of the image.

 -   This parameter only takes effect when the **DeleteImageType** parameter is set to **ImageURL**. In this case, you must set this parameter.
-   Encode multiple image URLs and separate them with commas \(,\).
-   The use of special characters in image URLs may lead to the failure to delete the images. To prevent such failure, you must encode the image URLs before you concatenate them into a string with commas \(,\). |
|ImageIds|String|No|bbc65bba53f\*\*\*\*\*ed90de118a7849,594228cdd14b4d\*\*\*\*\*069fc17a8c4a|The ID of the image.

 -   This parameter only takes effect when the **DeleteImageType** parameter is set to **ImageId**. In this case, you must set this parameter.
-   Separate multiple IDs with commas \(,\). |
|VideoId|String|No|eb1861d2c9a8\*\*\*\*\*842340e989dd56|The ID of the video. This parameter only takes effect when the **DeleteImageType** parameter is set to **VideoId**. In this case, you must set this parameter. |
|ImageType|String|No|All|The type of the image. This parameter only takes effect when the **DeleteImageType** parameter is set to **VideoId**. In this case, you must set this parameter. Valid values:

 -   **CoverSnapshot**: thumbnail snapshot.
-   **NormalSnapshot**: normal snapshot.
-   **SpriteSnapshot**: sprite snapshot.
-   **SpriteOriginSnapshot**: sprite source snapshot.
-   **All**: images of all the preceding types. If this parameter is not set to All, you can specify multiple types and separate them with commas \(,\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteImage
&DeleteImageType=VideoId
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteImageResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</DeleteImageResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## Common errors

The following table describes the common errors that this operation can return.

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|NoSuchResource

|The specified resource does not exist.

|404

|The error message returned because the specified image does not exist. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

