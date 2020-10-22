# 获取URL上传信息

调用GetURLUploadInfos获取URL上传信息。

**说明：** 通过URL上传时返回的JobId或者上传时使用的URL获取URL上传信息，包括URL上传状态、UserData、创建时间、完成时间，如果上传失败可以查看错误码和错误信息，上传成功可以查到对应的视频ID。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetURLUploadInfos&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetURLUploadInfos|系统规定参数。取值：**GetURLUploadInfos**。 |
|JobIds|String|否|86c192\*\*\*\*\*5fba0,7afb\*\*\*\*\*201e7fa,2cc49\*\*\*\*\*97378|JobId列表。多个用逗号分隔，最多支持10个。 |
|UploadURLs|String|否|http://xxx.mp4|上传源视频URL列表。需URLencode，多个用逗号分隔，最多支持10个。如果同一URL视频多次上传，建议传入单个URL进行查询，最多返回100条记录。 |

**说明：** JobIds和UploadURLs必须指定一个，二者同时传入时只处理JobIds。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExists|List|\["XXXX1", "XXX2"\]|不存在的ID或URL列表。 |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|请求ID。 |
|URLUploadInfoList|Array of UrlUploadJobInfoDTO| |[URL上传信息列表](~~52839#title-cpc-fw5-xwn~~)。 |
|CompleteTime|String|2019-01-01T01:01:01Z|完成时间。 |
|CreationTime|String|2019-01-01T01:01:01Z|创建时间。 |
|ErrorCode|String|200|错误码。 |
|ErrorMessage|String|error\_message|错误信息。 |
|FileSize|String|24|文件大小（字节）。 |
|JobId|String|xxxxxxx|Job ID。 |
|MediaId|String|xxxxx|上传视频ID。 |
|Status|String|SUCCESS|[视频状态](~~52839#title-vqg-8cz-7p8~~)。 |
|UploadURL|String|http://xxx|上传URL地址。 |
|UserData|String|xxxx|用户自定义字段。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetURLUploadInfos
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetURLUploadInfosResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <URLUploadInfoList>
            <JobId>86c192*****5fba0</JobId>
            <UploadURL>http://xxx.mp4</UploadURL>
            <MediaId>xxxxx</MediaId>
            <Status>SUCCESS</Status>
            <CreationTime>2019-01-01T01:01:01Z</CreationTime>
            <CompleteTime>2019-01-01T01:05:01Z</CompleteTime>
            <UserData>xxxx</UserData>
      </URLUploadInfoList>
      <URLUploadInfoList>
            <JobId>7afb*****201e7fa</JobId>
            <UploadURL>http://xxxx.flv</UploadURL>
            <Status>PENDING</Status>
            <CreationTime>2019-01-01T01:01:01Z</CreationTime>
            <CompleteTime>2019-01-01T01:05:01Z</CompleteTime>
            <UserData>xxxx</UserData>
      </URLUploadInfoList>
      <URLUploadInfoList>
            <JobId>2cc49*****97378</JobId>
            <UploadURL>http://xxxx.m3u8</UploadURL>
            <Status>UPLOAD_FAIL</Status>
            <CreationTime>2019-01-01T01:01:01Z</CreationTime>
            <CompleteTime>2019-01-01T01:05:01Z</CompleteTime>
            <UserData>xxxx</UserData>
            <ErrorCode></ErrorCode>
            <ErrorMessage></ErrorMessage>
      </URLUploadInfoList>
      <NonExists>XXXX1</NonExists>
      <NonExists>XXX2</NonExists>
</GetURLUploadInfosResponse>
```

`JSON` 格式

```
{
     "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
      "URLUploadInfoList" :[{
                "JobId":"86c192*****5fba0",
                 "UploadURL" : "http://xxx.mp4",
                 "MediaId" : "xxxxx",
                 "Status": "SUCCESS",
                 "CreationTime" : "2019-01-01T01:01:01Z",
                 "CompleteTime": "2019-01-01T01:05:01Z",
                 "UserData": "xxxx"
             }, 
             {
                "JobId":"7afb*****201e7fa",
                 "UploadURL" : "http://xxxx.flv",
                 "Status": "PENDING",
                 "CreationTime" : "2019-01-01T01:01:01Z",
                 "CompleteTime": "2019-01-01T01:05:01Z",
               "UserData": "xxxx"
             }, 
             {
                "JobId":"2cc49*****97378",
                 "UploadURL" : "http://xxxx.m3u8",
                 "Status": "UPLOAD_FAIL",
                 "CreationTime" : "2019-01-01T01:01:01Z",
                 "CompleteTime": "2019-01-01T01:05:01Z",
                 "UserData": "xxxx",
                 "ErrorCode":"",
                 "ErrorMessage":""
             }],
     "NonExists": ["XXXX1", "XXX2"]
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

