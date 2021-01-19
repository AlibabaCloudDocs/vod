DynamicImageComplete 
=========================================

This topic describes the DynamicImageComplete event as well as its notification content and sample callbacks.

Event type 
-------------------------------

DynamicImageComplete

Event description 
--------------------------------------

The DynamicImageComplete event is generated after a dynamic image is complete.
**Note**

* If you have configured a CDN domain name and enabled URL signing, you must generate your own auth_key to access the URL of the dynamic image. Otherwise, the `HTTP 403` error code is returned for your request. For more information about URL signing, see [URL signing](/intl.en-US/Developer Guide/Video security/URL signing.md).

  

* If no CDN domain name is configured, the URL of the OSS origin server is returned. This URL can be accessed only when the ACL of the relevant OSS bucket is set to public read. To ensure data security, we recommend that you configure a CDN domain name. For more information, see [Add a domain name](/intl.en-US/User Guide/Domain management/Add a domain name.md).

  




Event notification content 
-----------------------------------------------



|      Parameter      |          Type           | Required |                                                                                                                                       Description                                                                                                                                       |
|---------------------|-------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| EventTime           | String                  | Yes      | The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.                                                                                                                                                                              |
| EventType           | String                  | Yes      | The event type. The value is **DynamicImageComplete** .                                                                                                                                                                                                                                 |
| VideoId             | String                  | Yes      | The ID of the video.                                                                                                                                                                                                                                                                    |
| Status              | String                  | Yes      | Indicates whether the dynamic image job is complete. Valid values: * **success** : The dynamic image job is complete.   * **fail** : The dynamic image job failed to be complete.    |
| JobId               | String                  | Yes      | The ID of the dynamic image job.                                                                                                                                                                                                                                                        |
| ErrorCode           | String                  | No       | The error code. This parameter is available when an error occurs in the dynamic image job.                                                                                                                                                                                              |
| ErrorMessage        | String                  | No       | The error message. This parameter is available when an error occurs in the dynamic image job.                                                                                                                                                                                           |
| DynamicImageJobInfo | DynamicImageJobInfo\[\] | No       | Details of the dynamic image. The value is a JSON string. This parameter is not available when the dynamic image job fails. For more information, see the following table **DynamicImageJobInfo data** .                                                                                |



**DynamicImageJobInfo data** 


|  Field   |  Type  | Required |                                                                                                                                       Description                                                                                                                                       |
|----------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JobId    | String | Yes      | The ID of the dynamic image job.                                                                                                                                                                                                                                                        |
| Status   | String | Yes      | Indicates whether the dynamic image job is complete. Valid values: * **success** : The dynamic image job is complete.   * **fail** : The dynamic image job failed to be complete.    |
| FileURL  | String | Yes      | The URL of the dynamic image.                                                                                                                                                                                                                                                           |
| FileSize | String | No       | The size of the dynamic image. Unit: bytes.                                                                                                                                                                                                                                             |
| Fps      | String | No       | The frame rate of the video stream, in frames per second.                                                                                                                                                                                                                               |
| Height   | String | No       | The height of the dynamic image. Unit: px.                                                                                                                                                                                                                                              |
| Width    | String | No       | The width of the dynamic image. Unit: px.                                                                                                                                                                                                                                               |



Sample callbacks 
-------------------------------------

Description:

* For an HTTP callback, the following example is the body of the HTTP POST request.

  

* For an MNS callback, the following example is the message body.

  




    {
        "Status":"success",
        "VideoId":"6a45f222e08fhdjdn2d144503213****",
        "EventType":"DynamicImageComplete",
        "EventTime":"2019-11-05T09:12:58Z",
        "DynamicImageJobInfo":"{
             \"FileSize\":\"1834831\",
             \"FileURL\":\"http://vod.aliyun.test/6a45f222e08fhdjdn2d144503213****/image/dynamic/3af1e9705cb243*****21d4c3719f0d4.gif\",
             \"Fps\":\"25\",
             \"Height\":\"200\",
             \"JobId\":\"3af7e9705cb24js83j231d4c3719****\",
             \"Status\":\"success\",
             \"Width\":\"200\"
         }",
        "JobId":"3af7e9705cb24js83j231d4c3719****"
    }


