# 查询AI图片任务列表

调用GetAIImageJobs查询AI图片任务列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetAIImageJobs&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetAIImageJobs|操作接口名，系统规定参数。取值：**GetAIImageJobs**。 |
|JobIds|String|是|cf08a2c6e11e\*\*\*\*\*de1711b738b9067|任务ID。多个ID使用英文逗号（,）分隔，最大支持10个。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AIImageJobList|Array of AIImageJob| |AI图片任务列表。 |
|AIImageResult|String|\[\{"Score":5.035636554444242,"Url":"http://outin-\*\*\*\*\*.oss-cn-shanghai.aliyuncs.com/357a8748c577\*\*\*\*\*789d2726e6436aa/image/ai/b0a7612554d\*\*\*\*\*5cbe3-00001.gif"\}\]|AI图片的OSS地址。

 **说明：** 为任务结果，因此该地址不提供完整的鉴权信息，需要鉴权信息需用户生成或者调用[ListAIImage](~~186924~~)接口获取媒资结果。\| |
|Code|String|Success|错误码。 |
|CreationTime|String|2020-10-15T03:30:03Z|AI图片任务创建时间。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|JobId|String|cf08a2c6e11e\*\*\*\*\*de1711b738b9067|AI图片处理的任务ID。 |
|Message|String|success|错误信息。 |
|Status|String|success|任务状态：

 -   **success**：成功。
-   **fail**：失败。 |
|TemplateConfig|String|\{"Format":"gif","SetDefaultCover":"true"\}|提交任务时，对指定模板的配置信息的快照。 |
|TemplateId|String|5a86a00f15194\*\*\*\*\*d7fe7de1b4a173|AI模板ID。 |
|UserData|String|\{"Extend":\{"localId":"\*\*\*\*","test":"www"\}\}|自定义设置。

 -   必须是JSON字符串。
-   需要包含MessageCallback或者Extend参数。
-   最大长度为512个字节。

 参数构造详情，请参见[UserData](~~86952~~)。 |
|VideoId|String|357a8748c577\*\*\*\*\*789d2726e6436aa|视频ID。 |
|RequestId|String|7721B494-1F78-4E\*\*\*\*\*E8-A7CEE7315BFA|请求ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=GetAIImageJobs
&JobIds=cf08a2c6e11e*****de1711b738b9067
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetAIImageJobsResponse>
      <AIImageJobList>
            <Status>success</Status>
            <VideoId>357a8748c577*****789d2726e6436aa</VideoId>
            <Message>success</Message>
            <UserData>{"Extend":{"localId":"****","test":"www"}}</UserData>
            <AIImageResult>[{"Score":5.035636554444242,"Url":"http://outin-*****.oss-cn-shanghai.aliyuncs.com/357a8748c577*****789d2726e6436aa/image/ai/b0a7612554d*****5cbe3-00001.gif"}]</AIImageResult>
            <CreationTime>2020-10-15T03:30:03Z</CreationTime>
            <TemplateConfig>{"Format":"gif","SetDefaultCover":"true"}</TemplateConfig>
            <Code>Success</Code>
            <TemplateId>5a86a00f15194*****d7fe7de1b4a173</TemplateId>
            <JobId>cf08a2c6e11e*****de1711b738b9067</JobId>
      </AIImageJobList>
      <RequestId>7721B494-1F78-4E*****E8-A7CEE7315BFA</RequestId>
</GetAIImageJobsResponse>
```

`JSON`格式

```
{
	"AIImageJobList": [{
		"Status": "success",
		"VideoId": "357a8748c577*****789d2726e6436aa",
		"Message": "success",
		"UserData": "{\"Extend\":{\"localId\":\"****\",\"test\":\"www\"}}",
		"AIImageResult": "[{\"Score\":5.035636554444242,\"Url\":\"http://outin-*****.oss-cn-shanghai.aliyuncs.com/357a8748c577*****789d2726e6436aa/image/ai/b0a7612554d*****5cbe3-00001.gif\"}]",
		"CreationTime": "2020-10-15T03:30:03Z",
		"TemplateConfig": "{\"Format\":\"gif\",\"SetDefaultCover\":\"true\"}",
		"Code": "Success",
		"TemplateId": "5a86a00f15194*****d7fe7de1b4a173",
		"JobId": "cf08a2c6e11e*****de1711b738b9067"
	}],
	"RequestId": "7721B494-1F78-4E*****E8-A7CEE7315BFA"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## SDK示例

建议使用[服务端SDK](~~101789~~)来调用API，此API各语言调用的示例代码，请参见：

-   [Java](~~100692~~)
-   [Python](~~101181~~)
-   [PHP](~~101159~~)
-   [.NET](~~100844~~)
-   [Node.js](~~101564~~)
-   [Go](~~101575~~)
-   [C/C++](~~102987~~)

