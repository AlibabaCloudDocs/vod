# 视频DNA完成

本文为您介绍视频DNA完成事件、事件通知的内容和回调示例。

## 事件类型

AIMediaDNAComplete

## 事件说明

当视频DNA作业完成时，会产生AIMediaDNAComplete事件。

## 事件内容

|参数名称|类型|必备项|描述|
|----|--|---|--|
|EventTime|String|是|事件产生时间，为UTC时间：yyyy-MM-ddTHH:mm:ssZ。|
|EventType|String|是|事件类型，系统规定参数。固定为：**AIMediaDNAComplete**。|
|JobId|String|是|作业ID，与提交DNA作业接口返回的JobId一致。|
|MediaId|String|是|视频ID。|
|Status|String|是|作业状态。-   **success**：成功。
-   **fail**：失败。 |
|Code|String|否|作业错误码，当作业失败时，会有该字段。|
|Message|String|否|作业错误信息，当作业失败时，会有该字段。|
|Data|String|是|DNA处理结果数据，JSON对象。具体结构，请参见[视频DNA结果](/intl.zh-CN/服务端API/附录/视频AI参数说明.md)。|

## 回调示例

回调示例说明：

-   对于HTTP回调，以下内容为HTTP Post Body。
-   对于MNS回调，以下内容为消息体。

```
{
    "EventTime": "2017-03-20T07:49:17Z",
    "EventType": "AIMediaDNAComplete",
    "JobId": "88c6ca184c0edj384a5b665e2a12****",
    "MediaId": "3D12340d92cjsw83k1fab46a0b847fd****",
    "Status": "success",
    "Code": "0",
    "Message": "OK",
    "Data": "{\"VideoDNA\":[{\"Similarity\":\"0.99\",\"PrimaryKey\":\"7a1d275cc8da4jw93mkde0e182e80****\",\"Detail\":[{\"Input\":{\"Start\":\"0.0\",\"Duration\":\"14.0\"},\"Duplication\":{\"Start\":\"0.5\",\"Duration\":\"14.4\"}}]}]}"
}
```

