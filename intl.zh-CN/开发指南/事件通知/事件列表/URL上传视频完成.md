# URL上传视频完成

本文为您介绍URL上传视频完成事件、事件通知的内容和回调示例。

## 事件类型

UploadByURLComplete

## 事件说明

提交[URL批量拉取上传](/intl.zh-CN/服务端API/媒体上传/URL批量拉取上传.md)任务后，云端拉取视频上传完成会产生UploadByURLComplete事件。

## 事件内容

|参数名称|类型|必备项|描述|
|----|--|---|--|
|EventTime|String|是|事件产生时间，为UTC时间：yyyy-MM-ddTHH:mm:ssZ。|
|EventType|String|是|事件类型，系统规定参数。固定为：**UploadByURLComplete**。|
|VideoId|String|是|视频ID。当视频拉取成功后会有该字段。|
|JobId|String|是|上传任务ID。|
|SourceURL|String|否|源文件URL地址。|
|Status|String|否|上传结果。-   **success**：成功。
-   **fail**：失败。 |
|ErrorCode|String|否|作业错误码，上传出错时，会有该字段。|
|ErrorMessage|String|否|作业错误信息，上传出错时，会有该字段。|

## 回调示例

回调示例说明：

-   对于HTTP回调，以下内容为HTTP Post Body。
-   对于MNS回调，以下内容为消息体。

-   上传成功

    ```
    { 
      "Status": "success",
      "EventTime": "2017-03-20T07:49:17Z",
      "EventType": "UploadByURLComplete", 
      "VideoId": "43q9fjdun3f****", 
      "JobId": "4c815bjs83j1****", 
      "SourceURL ": "http://sample-bucket.oss-cn-shanghai.aliyuncs.com/27ffc438-164d55217ef-0005-6884-51a-1****.mp4",
      "Size":"123456"
    }
    ```

-   上传失败

    ```
    { 
      "Status": "fail",
      "EventTime": "2017-03-20T07:49:17Z",
      "EventType": "UploadByURLComplete", 
      "ErrorCode ": "URLInvalidError ", 
      "ErrorMessage ": "download video failed by the url, please check it", 
      "JobId": "4c815bjsued19c8e" ,
      "SourceURL ": "http://sample-bucket.oss-cn-shanghai.aliyuncs.com/27ffc438-164d55217ef-0005-6884-51a-1****.mp4"
    }
    ```


