# 获取URL上传信息

调用GetURLUploadInfos获取URL上传信息。

**说明：** 通过URL上传时返回的JobId或者上传时使用的URL获取URL上传信息，包括URL上传状态、UserData、创建时间、完成时间。如果上传失败可以查看错误码和错误信息，上传成功可以查到对应的视频ID。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetURLUploadInfos&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetURLUploadInfos|系统规定参数。取值：**GetURLUploadInfos**。 |
|JobIds|String|否|86c192\*\*\*\*\*5fba0,7afb\*\*\*\*\*201e7fa,2cc49\*\*\*\*\*97378|JobId列表。JobId可以通过[GetPlayInfo](~~56124~~)接口中返回的PlayInfo结构体中获取。

 **说明：** 多个ID使用英文逗号（,）分隔，最多支持10个。 |
|UploadURLs|String|否|http://\*\*\*\*.mp4|上传源视频URL列表。需URLencode，多个使用英文逗号（,）分隔，最多支持10个。如果同一URL视频多次上传，建议传入单个URL进行查询。 |

**说明：** JobIds和UploadURLs必须指定一个，二者同时传入时只处理JobIds。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExists|List|\["\*\*\*\*1", "\*\*\*\*2"\]|不存在的ID或URL列表。 |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|请求ID。 |
|URLUploadInfoList|Array of UrlUploadJobInfoDTO| |URL上传信息列表。具体上传名称及描述，请参见[URL上传信息](~~52839~~)。 |
|CompleteTime|String|2019-01-01T01:11:01Z|完成时间。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|CreationTime|String|2019-01-01T01:01:01Z|创建时间。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|ErrorCode|String|200|错误码。 |
|ErrorMessage|String|error\_message|错误信息。 |
|FileSize|String|24|文件大小。单位：字节。 |
|JobId|String|86c192\*\*\*\*\*5fba0|Job ID。 |
|MediaId|String|93ab850b4f6f\*\*\*\*\*54b6e91d24d81d4|上传视频ID。 |
|Status|String|SUCCESS|URL拉取任务状态。具体的拉取状态取值及说明，请参见[URL上传任务状态](~~52839~~)。 |
|UploadURL|String|http://\*\*\*\*.mp4|上传URL地址。

 **说明：** 最多可以返回100条记录。 |
|UserData|String|\{"MessageCallback":"\{"CallbackURL":"http://test.test.com"\}", "Extend":"\{"localId":"\*\*\*", "test":"www"\}"\}|自定义设置。为JSON字符串。更多信息，请参见[UserData](~~86952~~)。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=GetURLUploadInfos
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetURLUploadInfosResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <URLUploadInfoList>
        <Status>SUCCESS</Status>
        <UploadURL>http://****.mp4</UploadURL>
        <MediaId>93ab850b4f6f*****54b6e91d24d81d4</MediaId>
        <UserData>{"MessageCallback":"{"CallbackURL":"http://test.test.com"}", "Extend":"{"localId":"***", "test":"www"}"}</UserData>
        <CreationTime>2019-01-01T01:01:01Z</CreationTime>
        <ErrorCode>200</ErrorCode>
        <ErrorMessage>error_message</ErrorMessage>
        <CompleteTime>2019-01-01T01:11:01Z</CompleteTime>
        <JobId>86c192*****5fba0</JobId>
        <FileSize>24</FileSize>
  </URLUploadInfoList>
  <NonExists>["****1", "****2"]</NonExists>
</GetURLUploadInfosResponse>
```

`JSON` 格式

```
{
	"RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
	"URLUploadInfoList": [{
		"Status": "SUCCESS",
		"UploadURL": "http://****.mp4",
		"MediaId": "93ab850b4f6f*****54b6e91d24d81d4",
		"UserData": "{\"MessageCallback\":\"{\"CallbackURL\":\"http://test.test.com\"}\", \"Extend\":\"{\"localId\":\"***\", \"test\":\"www\"}\"}",
		"CreationTime": "2019-01-01T01:01:01Z",
		"ErrorCode": "200",
		"ErrorMessage": "error_message",
		"CompleteTime": "2019-01-01T01:11:01Z",
		"JobId": "86c192*****5fba0",
		"FileSize": "24"
	}],
	"NonExists": "[\"****1\", \"****2\"]"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

