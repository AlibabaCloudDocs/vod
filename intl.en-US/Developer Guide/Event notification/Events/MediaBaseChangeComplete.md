MediaBaseChangeComplete 
============================================

This topic describes the MediaBaseChangeComplete event as well as its notification content and sample callbacks.

Event type 
-------------------------------

MediaBaseChangeComplete

Event description 
--------------------------------------

The MediaBaseChangeComplete event is generated when the [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md), [UpdateVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfo.md), [UpdateVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfos.md), or [DeleteVideo](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteVideo.md) operation is called.

Event notification content 
-----------------------------------------------



|  Parameter   |  Type  | Required |                                                                                                                                                                      Description                                                                                                                                                                       |
|--------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| EventType    | String | Yes      | The event type. The value is MediaBaseChangeComplete.                                                                                                                                                                                                                                                                                                  |
| EventTime    | String | Yes      | The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.                                                                                                                                                                                                                                             |
| Status       | String | Yes      | Indicates whether the basic information of the media resource is changed. Valid values: * **success** : The basic information of the media resource is changed.   * **fail** : The basic information of the media resource failed to be changed.    |
| MediaType    | String | Yes      | The type of the media resource. Valid values: * **video** : audio and video   * **image** : image   * **attached** : attached media resource                                                                       |
| MediaId      | String | Yes      | The ID of the media resource.                                                                                                                                                                                                                                                                                                                          |
| OperateMode  | String | Yes      | The mode of operation. Valid values: * **create** : creates new information.   * **update** : updates information.   * **delete** : deletes information.                                                           |
| MediaContent | String | Yes      | The changed content. The value is a JSON string. Basic audio and video information can be changed. For more information, see the following **Basic audio and video information** section.                                                                                                                                                              |



**Basic audio and video information** 


|    Field    |  Type  | Required |                                                 Description                                                  |
|-------------|--------|----------|--------------------------------------------------------------------------------------------------------------|
| Title       | String | No       | The title. The value is a JSON string. Example: `{"OldValue":"OldTitle", "NewValue":"NewTitle"}`.            |
| Description | String | No       | The description. The value is a JSON string. Example: `{"OldValue":"OldDesc", "NewValue":"NewDesc"}`.        |
| CoverURL    | String | No       | The thumbnail. The value is a JSON string. Example: `{"OldValue":"OldCoverURL", "NewValue": "NewCoverURL"}`. |
| CateId      | String | No       | The category ID. The value is a JSON string. Example: `{"OldValue":123, "NewValue":456}`.                    |
| Tags        | String | No       | The tag. The value is a JSON string. Example: `{"OldValue":"OldTag", "NewValue" :"NewTag"}`.                 |


**Note**

* OldValue: specifies the value before the change.

  

* NewValue: specifies the new value after the change.

  

* When you add new information, the OldValue field is empty. When you delete information, the NewValue field is empty.

  




Sample callbacks 
-------------------------------------

Description:

* For an HTTP callback, the following example is the body of the HTTP POST request.

  

* For an MNS callback, the following example is the message body.

  




    {
      "EventType":"MediaBaseChangeComplete",
      "EventTime":"2019-06-20T02:18:58Z",
      "Status":"success",
      "MediaId":"3b46b391419aj294m83b459f7435****",
      "MediaType":"video",
      "OperateMode":"update",
      "MediaContent":
      {
         "Description":"{\"OldValue\":\"OldDesc\", \"NewValue\":\"NewDesc\"}",
         "CoverURL":"{\"NewValue\":\"http://test.aliyun.com/image/cover/8C46D968F6954348AFC7A88****-6-2.png\"}",
         "CateId":"{\"NewValue\":100002****}"
       }
    }


