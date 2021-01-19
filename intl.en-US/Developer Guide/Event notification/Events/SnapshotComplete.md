SnapshotComplete 
=====================================

This topic describes the SnapshotComplete event as well as its notification content and sample callbacks.

Event type 
-------------------------------

SnapshotComplete

Event description 
--------------------------------------

The SnapshotComplete event is generated after snapshots are taken for a video.

* Snapshotting and transcoding are performed concurrently.

  

* If the snapshots are thumbnail snapshots and the CoverUrl parameter is not specified, one of the thumbnail snapshots is selected as the video thumbnail. For more information about thumbnail snapshots, see [Video snapshots](/intl.en-US/Developer Guide/Media processing/Video snapshot.md).

  

* You can call the [GetVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md) operation to obtain the URLs of the video thumbnail and snapshots of the CoverSnapshot type.

  

* You can call the [ListSnapshots](/intl.en-US/API Reference/Media management/Image Management/ListSnapshots.md) operation to obtain the URLs of the latest snapshots taken for a specific video.

  



**Note**

If you have enabled URL signing, you must generate your own auth_key to access the URLs of the snapshots. Otherwise, the HTTP 403 error code is returned for your request. For more information about URL signing, see [URL signing](/intl.en-US/Developer Guide/Video security/URL signing.md).

Event notification content 
-----------------------------------------------



|   Parameter   |       Type       | Required |                                                                                                                                                 Description                                                                                                                                                  |
|---------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| EventTime     | String           | Yes      | The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.                                                                                                                                                                                                   |
| EventType     | String           | Yes      | The event type. The value is **SnapshotComplete** .                                                                                                                                                                                                                                                          |
| VideoId       | String           | Yes      | The ID of the video.                                                                                                                                                                                                                                                                                         |
| Status        | String           | Yes      | Indicates whether snapshots are taken for the video. Valid values: * **success** : Snapshots are taken for the video.   * **fail** : Snapshots failed to be taken for the video.                          |
| SubType       | String           | No       | The subtype of the snapshot. The value is **SpecifiedTime** . **Note** The value of SpecifiedTime indicates that the snapshot is taken through calls to the [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitSnapshotJob.md) operation. |
| ErrorCode     | String           | No       | The error code. This parameter is available when snapshots fail to be taken for the video.                                                                                                                                                                                                                   |
| ErrorMessage  | String           | No       | The error message. This parameter is available when snapshots fail to be taken for the video.                                                                                                                                                                                                                |
| CoverUrl      | String           | No       | The URL of the thumbnail. This parameter is not available if snapshots fail to be taken.                                                                                                                                                                                                                     |
| SnapshotInfos | SnapshotInfo\[\] | No       | Details about the snapshots. This parameter is unavailable if snapshots fail to be taken. For more information, see the following table **SnapshotInfos** .                                                                                                                                                  |
| Extend        | String           | No       | The user-defined parameter that is returned in the pass-through mode in callbacks. For more information, see the "UserData" section in [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md).                                                                       |



**SnapshotInfos** 


|      Field      |  Type  | Required |                                                                                                                                                                                                                                                             Description                                                                                                                                                                                                                                                              |
|-----------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Status          | String | Yes      | Indicates whether snapshots are taken for the video. Valid values: * **success** : Snapshots are taken for the video.   * **fail** : Snapshots failed to be taken for the video.                                                                                                                                                                                                                                                  |
| SnapshotType    | String | Yes      | The type of the snapshot. Valid values: * **CoverSnapshot** : thumbnail snapshot   * **NormalSnapshot** : normal snapshot   * **SpriteSnapshot** : sprite snapshot    For more information, see [Video snapshots](/intl.en-US/Developer Guide/Media processing/Video snapshot.md).                                                                                               |
| SnapshotCount   | Long   | Yes      | The total number of snapshots.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| SnapshotFormat  | String | Yes      | The format of the snapshot name. This parameter can be used together with the OSS storage URL or CDN domain name to generate a snapshot URL. **Note** If you have a domain name that may change frequently, you can have the snapshot URLs generated based on this parameter.                                                                                                                                                                                                                                        |
| SnapshotRegular | String | Yes      | The rule used to generate snapshot URLs. Snapshot URLs can be generated based on rules. **We recommend that you have snapshot URLs generated based on the SnapshotRegular value.** For more information about how to generate snapshot URLs, see the following section. **Note** If you have a domain name, the rule to generate CDN URLs is returned. If you do not have a domain name, the rule used to generate OSS storage URLs is returned. This parameter does not return the rule to generate **HTTPS** URLs. |
| JobId           | String | Yes      | The ID of the snapshotting job.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |


**Note**

A newly uploaded video and its snapshots have the same OSS storage URL. For more information, see [Manage VOD resources](/intl.en-US/User Guide/Global settings/Manage VOD resources.md).

**Generation of snapshot URLs** 

Snapshot URLs can be generated based on one of the following methods:

* Generate a snapshot URL based on the SnapshotFormat value

  * Rule: http(s)://{CDN domain name or OSS storage URL}/SnapshotFormat.

    
  
  * Description: The {SnapshotCount} value is the serial number of each snapshot. Add leading zeros to ensure that the value consists of five digits.

    
  
  * Examples:

    * If the serial number of the first snapshot is 00001, the snapshot URL is:

      `http://sample.com/2327a6ec24b44844b3a5``e2c1b691****/``covers/990f3820db2948b5b4a13d65d9a4****-00001.jpg`.
      
    
    * If the serial number of the second snapshot is 00002, the snapshot URL is:

      `http://sample.com/2327a6ec24b44844b3a5e2c1b691****/covers/990f3820db2948b5b4a13d65d9a4****-00002.jpg`.

      The URLs for other snapshots can be generated in the same manner.
      
    

    
  

  

* Generate a snapshot URL based on the SnapshotRegular value

  * Rule: The SnapshotRegular value indicates a complete rule to generate snapshot URLs.

    
  
  * Description: Snapshot URLs can be generated based on the SnapshotRegular value in the same manner as that based on the SnapshotFormat value.

    
  

  




Sample callbacks 
-------------------------------------

Description:

* For an HTTP callback, the following example is the body of the HTTP POST request.

  

* For an MNS callback, the following example is the message body.

  




    {
      "EventType": "SnapshotComplete",
      "EventTime": "2018-07-31T10:07:31Z",
      "CoverUrl": "http://sample/covers/990f3820db2948b5b4a13d65d9a4****-00002.jpg",
      "Extend":"test data",
      "SnapshotInfos": [
        {
          "Status": "success",
          "SnapshotType": "CoverSnapshot",
          "SnapshotCount": 2,
          "SnapshotFormat": "2327a6ec24b44844b3a5e2c1b691****/covers/990f3820db2948b5b4a13d65d9a4****-{SnapshotCount}.jpg",
          "SnapshotRegular": "http://sample/covers/990f3820db2948b5b4a13d65d9a4****-{SnapshotCount}.jpg",
          "JobId": "ee16d4bbf3f7*****e094bcb8cf8ddde"
        },
        {
          "Status": "success",
          "SnapshotType": "SpriteSnapshot",
          "SnapshotCount": 1,
          "SnapshotFormat": "2327a6ec24b44844b3a5e2c1b691****/covers/sprite/990f3820db2948b5b4a13d65d9a4****-{SnapshotCount}.jpg",
          "SnapshotRegular": "http://sample/covers/sprite/990f3820db2948b5b4a13d65d9a4****-{SnapshotCount}.jpg",
          "JobId": "b3187205eed*****b72adf4eb3840713"
        }
      ]
    }



