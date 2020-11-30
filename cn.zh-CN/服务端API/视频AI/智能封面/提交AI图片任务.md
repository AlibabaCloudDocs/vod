# 提交AI图片任务

调用SubmitAIImageJob接口提交AI图片处理任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SubmitAIImageJob&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SubmitAIImageJob|系统规定参数。取值：**SubmitAIImageJob**。 |
|AITemplateId|String|是|ef1a8842cb9f\*\*\*\*\*cea80cad902e416|AI图片模板ID。 |
|VideoId|String|是|357a8748c5774\*\*\*\*\*89d2726e6436aa|视频ID。 |
|UserData|String|否|\{"Extend":\{"localId":"\*\*\*\*","test":"www"\}\}|自定义设置。

 -   必须是JSON字符串。
-   需要包含MessageCallback或者Extend参数。
-   最大长度为512个字节。

 参数构造详情，请参见[UserData](~~86952~~)。 |
|AIPipelineId|String|否|6492025b8f\*\*\*\*\*6ba5bb755a33438|AI任务管道ID。

 **说明：** 有默认ID，可不填写。如果需要批量导入，需要使用单独的任务管道，请提交工单联系阿里云售后团队进行配置。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|JobId|String|cf08a2c6e11e\*\*\*\*\*de1711b738b9067|AI图片任务ID。 |
|RequestId|String|218A6807-A21E-43\*\*\*\*\*54-C0512880B0B0|请求ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=SubmitAIImageJob
&AITemplateId=ef1a8842cb9f*****cea80cad902e416
&VideoId=357a8748c5774*****89d2726e6436aa
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SubmitAIImageJobResponse>
      <RequestId>218A6807-A21E-43*****54-C0512880B0B0</RequestId>
      <JobId>cf08a2c6e11e*****de1711b738b9067</JobId>
</SubmitAIImageJobResponse>
```

`JSON` 格式

```
{
	"RequestId": "218A6807-A21E-43*****54-C0512880B0B0",
	"JobId": "cf08a2c6e11e*****de1711b738b9067"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

