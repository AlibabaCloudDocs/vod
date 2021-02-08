# GetAttachedMediaInfo

Queries the basic information about one or more auxiliary media assets. The basic information includes the title, type, tags, and creation time of an auxiliary media asset.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetAttachedMediaInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetAttachedMediaInfo|The operation that you want to perform. Set the value to **GetAttachedMediaInfo**. |
|MediaIds|String|Yes|eb1861d2c9a8\*\*\*\*\*42340e989dd56,0222e203cf80\*\*\*\*\*f9c22870a4d2c|The ID of the auxiliary media asset. Separate multiple IDs with commas \(,\). A maximum of 20 IDs can be specified. |
|AuthTimeout|Long|No|3600|The validity period of the URL of the auxiliary media asset. Unit: seconds.

 **Note:**

-   If the OutputType parameter is set to **cdn**:
    -   The URL of the auxiliary media asset has a validity period only if URL signing is enabled. Otherwise, the URL of the auxiliary media asset is permanently valid.
    -   Minimum value: **1**.
    -   Maximum value: unlimited.
    -   Default value: If you do not set this parameter, the default validity period that is specified in URL signing is used.
-   If the OutputType parameter is set to **oss**:
    -   The URL of the auxiliary media asset has a validity period only if the permissions on the Object Storage Service \(OSS\) bucket are private. Otherwise, the URL of the auxiliary media asset is permanently valid.
    -   Minimum value: **1**.
    -   Maximum value: **2592000** \(30 days\). The maximum value is limited to reduce security risks of the origin.
    -   Default value: If you do not set this parameter, the default value is **3600**. |
|OutputType|String|No|oss|The type of the URL of the auxiliary media asset. Valid values:

 -   **oss**: OSS URL
-   **cdn** \(default\): Content Delivery Network \(CDN\) URL |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AttachedMediaList|Array of AttachedMedia| |The information about the media asset. |
|AppId|String|app-\*\*\*\*\*|The ID of the application. |
|Categories|Array of Category| |The list of categories. |
|CateId|Long|198673|The ID of the video category. |
|CateName|String|Test|The name of the category.

 -   The value can be up to 64 bytes in length.
-   The string must be encoded in the UTF-8 format. |
|Level|Long|0|The level of the category. A value of 0 indicates a level 1 category. |
|ParentId|Long|-1|The ID of the parent category. The parent category ID of a level 1 category is -1. |
|CreationTime|String|2019-01-01T10:00:00Z|The time when the auxiliary media asset was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Description test|The description of the auxiliary media asset. |
|MediaId|String|0222e203cf80\*\*\*\*\*f9c22870a4d2c|The ID of the auxiliary media asset. |
|ModificationTime|String|2020-05-31T11:42:20Z|The time when the auxiliary media asset was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Status|String|Normal|The status of the auxiliary media asset. Valid values:

 -   **Uploading**: The auxiliary media asset is being uploaded. This is the initial status.
-   **Normal**: The auxiliary media asset is uploaded.
-   **UploadFail**: The auxiliary media asset fails to be uploaded. |
|StorageLocation|String|outin-bfefbb9\*\*\*\*\*c7426.oss-cn-shanghai.aliyuncs.com|The OSS bucket where the auxiliary media asset is stored. |
|Tags|String|tag1,tag2|The tags of the auxiliary media asset. |
|Title|String|Subtitle test|The title of the auxiliary media asset. |
|Type|String|subtitle|The type of the auxiliary media asset. Valid values:

 -   **watermark**
-   **subtitle**
-   **material** |
|URL|String|https://al\*\*\*\*\*.cn/subtitle/9843C2\*\*\*\*\*4E186F19B6.vtt?auth\_key=159099\*\*\*\*\*f60e0b7fd59|The URL of the auxiliary media asset.

 **Note:** If a CDN domain name is specified, a CDN URL is returned. Otherwise, an OSS URL is returned. |
|NonExistMediaIds|List|eb1861d2c9a8\*\*\*\*\*42340e989dd56|The IDs of the auxiliary media assets that do not exist. |
|RequestId|String|221BCB57-B217-42\*\*\*\*\*BF-619BD13378F9|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetAttachedMediaInfo
&MediaIds=eb1861d2c9a8*****42340e989dd56,0222e203cf80*****f9c22870a4d2c
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetAttachedMediaInfoResponse>
  <NonExistMediaIds>eb1861d2c9a8*****42340e989dd56</NonExistMediaIds>
  <RequestId>221BCB57-B217-42*****BF-619BD13378F9</RequestId>
  <AttachedMediaList>
        <Status>Normal</Status>
        <Type>subtitle</Type>
        <Description>Description test</Description>
        <AppId>app-*****</AppId>
        <MediaId>0222e203cf80*****f9c22870a4d2c</MediaId>
        <CreationTime>2019-01-01T10:00:00Z</CreationTime>
        <Title>Subtitle test</Title>
        <ModificationTime>2020-05-31T11:42:20Z</ModificationTime>
        <StorageLocation>outin-bfefbb9*****c7426.oss-cn-shanghai.aliyuncs.com</StorageLocation>
        <URL>https://al*****.cn/subtitle/9843C2*****4E186F19B6.vtt?auth_key=159099*****f60e0b7fd59</URL>
        <Tags>tag1,tag2</Tags>
  </AttachedMediaList>
  <AttachedMediaList>
        <Categories>
              <ParentId>-1</ParentId>
              <Level>0</Level>
              <CateName>Test</CateName>
              <CateId>198673</CateId>
        </Categories>
  </AttachedMediaList>
</GetAttachedMediaInfoResponse>
```

`JSON` format

```
{
    "NonExistMediaIds": "eb1861d2c9a8*****42340e989dd56",
    "RequestId": "221BCB57-B217-42*****BF-619BD13378F9",
    "AttachedMediaList": [{
        "Status": "Normal",
        "Type": "subtitle",
        "Description": "Description test",
        "AppId": "app-*****",
        "MediaId": "0222e203cf80*****f9c22870a4d2c",
        "CreationTime": "2019-01-01T10:00:00Z",
        "Title": "Subtitle test",
        "ModificationTime": "2020-05-31T11:42:20Z",
        "StorageLocation": "outin-bfefbb9*****c7426.oss-cn-shanghai.aliyuncs.com",
        "URL": "https://al*****.cn/subtitle/9843C2*****4E186F19B6.vtt?auth_key=159099*****f60e0b7fd59",
        "Tags": "tag1,tag2"
    }, {
        "Categories": [{
            "ParentId": "-1",
            "Level": "0",
            "CateName": "Test",
            "CateId": "198673"
        }]
    }]
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
|ExceededMax

|The input parameter 'MediaIds' Exceed the limit.

|400

|The error message returned because the number of auxiliary media asset IDs exceeds the upper limit of 20. |

