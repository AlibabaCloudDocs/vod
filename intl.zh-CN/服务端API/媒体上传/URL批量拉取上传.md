# URL批量拉取上传

调用UploadMediaByURL基于源文件URL，批量拉取媒体文件进行上传。

上传完成后会收到[URL上传视频完成](~~86326~~)事件通知，您可以通过[获取URL上传信息](~~106830~~)查询上传状态。

**说明：**

-   提交成功后，会在云端生成异步执行的任务，进行排队执行；上传完成后可根据事件通知（消息回调）返回的URL和视频ID等信息进行关联。
-   URL拉取上传的时效性较低，主要针对离线搬站场景，一般提交后会在数小时、甚至数天内完成迁移上传。如果想要更实时，建议您使用[服务端上传SDK](~~51992~~)，其会在本地实时下载和上传。
-   URL上传目前仅支持**上海**地域。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UploadMediaByURL&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UploadMediaByURL|系统规定参数。取值：**UploadMediaByURL**。 |
|UploadURLs|String|是|https://\*\*\*\*.mp4|视频源文件URL。

 -   URL中需要包括扩展名, 比如`https://****.mp4`中mp4为扩展名。
    -   如果URL中不包含扩展名，可以在UploadMetadatas中传入FileExtension来指定。
    -   如果URL中有扩展名且同时传入FileExtension，以传入的FileExtension为准。
    -   指定支持的扩展名，请参见[上传概述](~~55396~~)。
-   URL编码，多个地址以英文逗号（,）分隔，最多支持20个。
-   避免存在特殊字符导致无法上传视频，需要URL编码后再做逗号拼接。 |
|TemplateGroupId|String|否|ca3a8f6e49\*\*\*\*\*57b65806709586|转码模板组ID。

 -   登录[点播控制台](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.16.6948257eaZ4m54#/settings/transcode/list)，选择**配置管理** \> **媒体处理配置** \> **转码模板组**查看模版组ID。
-   不为空时，会使用指定的模板组进行转码。
-   可以在UploadMetadatas中进行设置。 |
|StorageLocation|String|否|outin-bfefbb90a47c\*\*\*\*\*\*163e1c7426.oss-cn-shanghai.aliyuncs.com|视频存储地址。

 登录[点播控制台](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored)，选择**配置管理** \> **媒资管理配置** \> **存储管理**查看存储地址。不指定时会使用默认存储。 |
|UploadMetadatas|String|否|\{"SourceURL":"http://test.com/a.mp4","Title":"urlUploadTest"\}|上传视频元数据信息，为JSON字符串。

 -   与UploadURLs里的URL匹配才能生效。
-   JSON格式：`[UploadMetadata, UploadMetadata,…]`，需转为JSON字符串 。
-   更多信息，请参见下表**UploadMetadata**。 |
|UserData|String|否|\{"MessageCallback":\{"CallbackURL":"http://test.test.com"\},"Extend":\{"localId":"xxx","test":"www"\}\}|自定义设置。为JSON字符串，支持消息回调、上传加速等设置。使用上传加速前，需要您提交工单给后台帮您开通后再使用。更多信息，请参见[UserData](~~86952#UserData~~)。

 **说明：** 此参数中消息回调的使用前提是需要在控制台配置HTTP回调地址和勾选对应的回调事件类型才能使用，否则回调设置不生效。 |
|AppId|String|否|app-\*\*\*\*|应用ID。默认取值：**app-1000000**。 更多详情，请参见[多应用](~~113600~~)。 |
|WorkflowId|String|否|e1e243b4254\*\*\*\*\*8248197d6f74f9|工作流ID。

 **说明：** 如果同时传递了WorkflowId和TemplateGroupId，以WorkflowId为准。更多信息，请参见[工作流](~~115347~~)。 |

## UploadMetadata

|名称

|类型

|是否必需

|描述 |
|----|----|------|----|
|SourceURL

|String

|是

|需要上传的视频源文件URL。 |
|Title

|String

|是

|视频标题。长度不超过128个字节。UTF-8编码。 |
|FileSize

|String

|否

|文件大小。 |
|Description

|String

|否

|视频描述。长度不超过1024个字节。UTF-8编码。 |
|CoverURL

|String

|否

|自定义视频封面URL地址。 |
|CateId

|String

|否

|视频分类ID。登录[点播控制台](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored)，选择**配置管理** \> **媒资管理配置** \> **分类管理**编辑或查看分类的ID。 |
|Tags

|String

|否

|视频标签。单个标签不超过32字节，最多不超过16个标签。多个标签，请使用英文逗号（,）分隔。UTF8编码。 |
|TemplateGroupId

|String

|否

|转码模板组ID。登录[点播控制台](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.16.6948257eaZ4m54#/settings/transcode/list)，选择**配置管理** \> **媒体处理配置** \> **转码模板组**查看模版组ID。不为空时，会使用指定的模板组进行转码。会覆盖外层传入的TemplateGroupId。 |
|WorkflowId

|String

|否

|工作流ID。注意：如果同时传递了WorkflowId和TemplateGroupId，以WorkflowId为准。更多信息，请参见[工作流](~~115347~~)。 |
|FileExtension

|String

|否

|视频扩展名，支持的扩展名，请参见[上传概述](~~55396~~)。 |

**说明：**

-   UploadMetadata 中的参数（如Title、Description、Tags等）不能包含表情符。
-   为确保正常播放，**不转码即分发**模板组仅支持MP4、FLV、M3U8和MP3格式的视频。若使用阿里云播放器，版本须为3.1.0或以上。
-   指定不转码的模板组，视频上传后仅有[上传完成](~~55630~~)事件通知，没有[转码完成](~~55636~~)事件通知。
-   上传完成后，除了上传和转码通知，还有[URL上传视频完成](~~86326~~)事件通知。
-   批量提交时，每一个SourceURL有独立的通知。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|请求ID。 |
|UploadJobs|Array of UploadJob| |多个Job信息。 |
|JobId|String|ad90a501b1b94\*\*\*\*\*fb72374ad005046|上传Job ID。 |
|SourceURL|String|http://\*\*\*\*.mp4|上传Job对应的URL。 |

**说明：**

-   该接口为异步上传视频接口，任务将提交到上传队列排队，完成时间受已有任务数量影响。

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=UploadMediaByURL
&UploadURLs=https://****.mp4
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UploadMediaByURLResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <UploadJobs>
		    <JobId>ad90a501b1b94*****fb72374ad005046</JobId>
		    <SourceURL>http://****.mp4</SourceURL>
	  </UploadJobs>
</UploadMediaByURLResponse>
```

`JSON` 格式

```
{
    "RequestId":"25818875-5F78-4A*****F6-D7393642CA58",
    "UploadJobs":[
        {
            "SourceURL":"http://****.mp4",
            "JobId":"ad90a501b1b94*****fb72374ad005046"
        }]
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/vod)查看更多错误码。

## 接口错误码

下表列举了本接口特有的错误码。

|错误代码

|错误信息

|HTTP 状态码

|说明 |
|------|------|----------|----|
|InvalidParameter.UploadURLs

|The specified parameter UploadURLs is not valid.

|400

|参数UploadURLs无效。 |

## SDK示例

建议使用[服务端SDK](~~101789~~)来调用API，此API各语言调用的示例代码，请参见：

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

