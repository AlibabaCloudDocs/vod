# 查询AI作业

调用ListAIJob查询AI作业。在提交AI作业后，会进行异步处理，通过此接口可以实时查询作业信息。

**说明：** 该接口可查询的AI作业包含视频DNA作业和智能标签作业。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAIJob&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAIJob|操作接口名，系统规定参数。取值：**ListAIJob**。 |
|JobIds|String|是|a718a3a1e8\*\*\*\*\*bb42ee3bc88921e9|作业ID列表。JobId可以通过[GetPlayInfo](~~56124~~)接口中返回的PlayInfo结构体中获取。

 **说明：** 多个ID之间用英文逗号（,）隔开，一次最多可以查10个。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AIJobList|Array of AIJob| |作业信息列表。 |
|AIJob| | | |
|Code|String|0|作业错误码。当Status为失败时，可关注该字段。 |
|CompleteTime|String|2020-06-28T02:04:47Z|作业结束时间。日期格式按照ISO8601表示法，并使用UTC时间，格式为：*yyyy-MM-dd*T*HH:mm:ss*Z。 |
|CreationTime|String|2020-06-28T02:04:32Z|作业开始时间。日期格式按照ISO8601表示法，并使用UTC时间，格式为：*yyyy-MM-dd*T*HH:mm:ss*Z。 |
|Data|String|\{"OrigASRData":\{"AsrTextList":\[\{"EndTime":700,"StartTime":0,"Text":"嗯。","ChannelId":0,"SpeechRate":85\},\{"EndTime":3750,"StartTime":1630,"Text":"的。","ChannelId":0,"SpeechRate":28\},\{"EndTime":5910,"StartTime":4020,"Text":"听不厌。","ChannelId":0,"SpeechRate":95\},\{"EndTime":12750,"StartTime":10090,"Text":"留言。","ChannelId":0,"SpeechRate":45\},\{"EndTime":25230,"StartTime":13590,"Text":"hello，中午好。","ChannelId":0,"SpeechRate":20\},\{"EndTime":30000,"StartTime":28220,"Text":"嗯。","ChannelId":0,"SpeechRate":33\}\],"Duration":"30016"\}\}|作业结果数据，JSON数据格式。Type取值：

 -   **AIMediaDNA**。
-   **AIVideoTagResult**。

 具体数据结构请参见[AITemplateConfig](~~89863~~)。 |
|JobId|String|53d4a9c7b00c\*\*\*\*\*cdcb4b0c2c854c7|作业ID。 |
|MediaId|String|a718a3a1e8\*\*\*\*\*bb42ee3bc88921e9|视频ID。 |
|Message|String|OK|作业错误信息。当Status为失败时，可关注该字段。 |
|Status|String|success|作业状态。取值：

 -   **success**：成功。
-   **fail**：失败。
-   **init**：初始化。
-   **processing**：处理中。 |
|Type|String|AIVideoTag|作业类型。多个类型使用英文逗号（,）分隔。取值：

 -   **AIMediaDNA**：视频DNA。
-   **AIVideoTag**：智能标签。 |
|NonExistAIJobIds|List|\["aasdcsfg\*\*\*\*\*782740asd", "k2l3ibask\*\*\*\*\*od98wrns9"\]|不存在的作业ID列表。 |
|RequestId|String|8233A0E4-E112-44\*\*\*\*\*58-2BCED1B88173|请求ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=ListAIJob
&JobIds=1236ca184c0e47098a5b665e2xxxxxx
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListAIJobResponse>
  <RequestId>8233A0E4-E112-44*****58-2BCED1B88173</RequestId>
  <NonExistAIJobIds>
        <String>["aasdcsfg*****782740asd", "k2l3ibask*****od98wrns9"]</String>
  </NonExistAIJobIds>
  <AIJobList>
        <AIJob>
              <Status>success</Status>
              <Type>AIVideoTag</Type>
              <Message>OK</Message>
              <MediaId>a718a3a1e8*****bb42ee3bc88921e9</MediaId>
              <CreationTime>2020-06-28T02:04:32Z</CreationTime>
              <Data>{"OrigASRData":{"AsrTextList":[{"EndTime":700,"StartTime":0,"Text":"嗯。","ChannelId":0,"SpeechRate":85},{"EndTime":3750,"StartTime":1630,"Text":"的。","ChannelId":0,"SpeechRate":28},{"EndTime":5910,"StartTime":4020,"Text":"听不厌。","ChannelId":0,"SpeechRate":95},{"EndTime":12750,"StartTime":10090,"Text":"留言。","ChannelId":0,"SpeechRate":45},{"EndTime":25230,"StartTime":13590,"Text":"hello，中午好。","ChannelId":0,"SpeechRate":20},{"EndTime":30000,"StartTime":28220,"Text":"嗯。","ChannelId":0,"SpeechRate":33}],"Duration":"30016"}}</Data>
              <CompleteTime>2020-06-28T02:04:47Z</CompleteTime>
              <Code>0</Code>
              <JobId>53d4a9c7b00c*****cdcb4b0c2c854c7</JobId>
        </AIJob>
  </AIJobList>
</ListAIJobResponse>
```

`JSON`格式

```
{
	"RequestId": "8233A0E4-E112-44*****58-2BCED1B88173",
	"NonExistAIJobIds": {
		"String": "[\"aasdcsfg*****782740asd\", \"k2l3ibask*****od98wrns9\"]"
	},
	"AIJobList": {
		"AIJob": [
			{
				"Status": "success",
				"Type": "AIVideoTag",
				"Message": "OK",
				"MediaId": "a718a3a1e8*****bb42ee3bc88921e9",
				"CreationTime": "2020-06-28T02:04:32Z",
				"Data": "{\"OrigASRData\":{\"AsrTextList\":[{\"EndTime\":700,\"StartTime\":0,\"Text\":\"嗯。\",\"ChannelId\":0,\"SpeechRate\":85},{\"EndTime\":3750,\"StartTime\":1630,\"Text\":\"的。\",\"ChannelId\":0,\"SpeechRate\":28},{\"EndTime\":5910,\"StartTime\":4020,\"Text\":\"听不厌。\",\"ChannelId\":0,\"SpeechRate\":95},{\"EndTime\":12750,\"StartTime\":10090,\"Text\":\"留言。\",\"ChannelId\":0,\"SpeechRate\":45},{\"EndTime\":25230,\"StartTime\":13590,\"Text\":\"hello，中午好。\",\"ChannelId\":0,\"SpeechRate\":20},{\"EndTime\":30000,\"StartTime\":28220,\"Text\":\"嗯。\",\"ChannelId\":0,\"SpeechRate\":33}],\"Duration\":\"30016\"}}",
				"CompleteTime": "2020-06-28T02:04:47Z",
				"Code": "0",
				"JobId": "53d4a9c7b00c*****cdcb4b0c2c854c7"
			}
		]
	}
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

