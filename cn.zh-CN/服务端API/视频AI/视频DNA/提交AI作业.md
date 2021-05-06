# 提交AI作业

调用SubmitAIJob提交AI作业。

**说明：**

-   只有开通相关的AI服务后，才能调用此接口。更多详情，请参见[视频AI](~~101148~~)。
-   AI作业内容包含视频DNA作业和智能标签作业。
-   作业在提交成功后会异步执行，不保证接口返回时作业已处理完成。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SubmitAIJob&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SubmitAIJob|系统规定参数。取值：**SubmitAIJob**。 |
|MediaId|String|是|3D3D12340d9\*\*\*\*\*401fab46a0b847|视频ID。 |
|Types|String|否|AIMediaDNA|AI作业类型。多个用英文逗号（,）分隔。取值：

 -   **AIMediaDNA**：视频DNA。
-   **AIVideoTag**：智能标签。 |
|Config|String|否|\{"AIVideoTagConfig": \{"AnalyseTypes": "Face,ASR"\} \}|作业配置，JSON格式。具体结构定义，请参见[AIConfig](~~92878~~)。

 -   视频存储在上海地域的，Face、ASR、OCR、Category、Annotation五种类型都支持。
-   视频存储在北京地域的，暂时只支持Face。
-   视频存储在其他地域的，暂不支持该服务。

 **说明：** 关于存储区域的说明，请参见[点播中心和访问域名\>接入地址和存储区域](~~98194~~)。 |
|UserData|String|否|\{"Extend":\{"localId":"\*\*\*","test":"www"\}\}|自定义设置，为JSON字符串。参数结构详情参考[UserData](~~86952#h2--userdata-div-id-userdata-div-3~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AIJobList|Array of AIJob| |AI作业信息列表。 |
|AIJob| | | |
|JobId|String|9e82640c85114bf5af23edfaf\*\*\*\*|作业ID。 |
|MediaId|String|3D3D12340d92c641401fab46a0b847\*\*\*\*|视频ID。 |
|Type|String|AIVideoTag|作业类型。取值：

 -   **AIMediaDNA**：视频DNA。
-   **AIVideoTag**：智能标签。 |
|RequestId|String|25818875-5F78-4A13-BEF6-D73936\*\*\*\*|请求ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=SubmitAIJob
&MediaId=3D3D12340d9*****401fab46a0b847
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SubmitAIJobResponse>
      <RequestId>25818875-5F78-4A13-BEF6-D73936****</RequestId>
      <AIJobList>
            <AIJob>
                  <Status>1</Status>
                  <Type>AIVideoTag</Type>
                  <Message>1</Message>
                  <MediaId>3D3D12340d92c641401fab46a0b847****</MediaId>
                  <CreationTime>1</CreationTime>
                  <Data>1</Data>
                  <Code>1</Code>
                  <JobId>9e82640c85114bf5af23edfaf****</JobId>
            </AIJob>
      </AIJobList>
</SubmitAIJobResponse>
```

`JSON`格式

```
{
	"RequestId": "25818875-5F78-4A13-BEF6-D73936****",
	"AIJobList": {
		"AIJob": [{
			"Status": "1",
			"Type": "AIVideoTag",
			"Message": "1",
			"MediaId": "3D3D12340d92c641401fab46a0b847****",
			"CreationTime": "1",
			"Data": "1",
			"Code": "1",
			"JobId": "9e82640c85114bf5af23edfaf****"
		}]        
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

