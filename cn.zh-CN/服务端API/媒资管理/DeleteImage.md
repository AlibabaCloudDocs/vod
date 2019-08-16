# DeleteImage {#doc_api_vod_DeleteImage .reference}

调用DeleteImage删除用户上传的图片及视频自动截图。

**说明：** **真正删除源文件，且不可逆，一旦删除，图片无法找回。某些情况存在CDN缓存，图片URL不会立即失效。**

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteImage&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteImage|系统规定参数。取值：**DeleteImage**。

 |
|DeleteImageType|String|是|VideoId|图片删除操作类型。取值：

 -   **ImageURL**：根据图片URL删除指定图片。
-   **ImageId**：根据图片ID删除指定图片。
-   **VideoId**：根据视频ID删除其关联图片。

 |
|AccessKeyId|String|否|your\_id|您的AccessKey ID。

 |
|ImageIds|String|否|ImageId1,ImageId2|图片ID。

 -   支持批量，多个英文逗号分隔。
-   DeleteImageType=ImageId时必传。

 |
|ImageType|String|否|All|图片类型。DeleteImageType=VideoId时必传。

 取值：

 -   **CoverSnapshot**：封面截图。
-   **NormalSnapshot**：SubmitSnapshotJob接口发起的普通截图 。
-   **SpriteSnapshot**：SubmitSnapshotJob接口发起的雪碧截图。
-   **SpriteOriginSnapshot**：组成雪碧图的原始小图。
-   **All（以上多种类型的图片）**：非All时支持多个类型英文逗号分隔传入。

 |
|ImageURLs|String|否|http://xxxx,http://xxxxx|图片URL。

 -   DeleteImageType=ImageURL时必传。
-   URL编码，多个以英文逗号分隔。
-   避免存在特殊字符导致图片无法删除成功，需要URL编码后再做逗号拼接。

 |
|VideoId|String|否|fdbsngsn4363mnf|视频ID。DeleteImageType=VideoId时必传。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DeleteImage
&DeleteImageType=VideoId
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteImageResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</DeleteImageResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

