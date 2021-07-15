# 删除视频DNA作业

调用SubmitMediaDNADeleteJob删除视频DNA作业。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SubmitMediaDNADeleteJob&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|SubmitMediaDNADeleteJob|系统规定参数。取值：**SubmitMediaDNADeleteJob**。 |
|MediaId|String|是|656eaaa8c43a4597\*\*\*\*\*\*1f09a36|视频ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|e5b1a2e7bee\*\*\*\*\*\*b632c2710b9423f|请求ID。 |
|JobId|String|6805B2EC-CE87-\*\*\*\*-8FF6-9C0E97719A26|任务ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=SubmitMediaDNADeleteJob
&MediaId=656eaaa8c43a4597******1f09a36
&<公共参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<SubmitMediaDNADeleteJobResponse>
<JobId>e5b1a2e7bee******b632c2710b9423f</JobId>
<RequestId>6805B2EC-CE87-****-8FF6-9C0E97719A26</RequestId>
</SubmitMediaDNADeleteJobResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "JobId" : "e5b1a2e7bee******b632c2710b9423f",
  "RequestId" : "6805B2EC-CE87-****-8FF6-9C0E97719A26"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

