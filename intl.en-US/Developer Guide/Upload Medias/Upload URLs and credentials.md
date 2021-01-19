Upload URLs and credentials 
================================================

You must obtain upload URLs and credentials before you can upload media files. You can use SDKs to call operations or send HTTP or HTTPS requests to obtain the upload URLs and credentials. This topic describes the limits, usage notes, obtainment methods, and API operations of upload URLs and credentials, as well as how to parse upload URLs and credentials.

Introduction 
---------------------------------

Upload URLs and credentials are issued by ApsaraVideo VOD to authorize users to upload media files to OSS buckets allocated by ApsaraVideo VOD.

* Upload credentials

  Upload credentials are used to handle authorization and security issues during uploads and prevent malicious users from uploading media files. In addition, ApsaraVideo VOD automatically creates media IDs (MediaId) when it issues upload URLs and credentials.
  




<!-- -->

* Media IDs

  Media IDs are also called video IDs (VideoId) or image IDs (ImageId). They are used to track and manage the lifecycle of a media file. Typically, the initial state of a media file is **Uploading** . The media file automatically enters different states (such as Uploaded, Transcoding, and Normal) after the corresponding processing is complete. You can also use media IDs to initiate operations on videos such as transcoding, snapshotting, AI processing, and editing.
  




Limits 
---------------------------

* An upload URL and credential can be used only for a single media file, such as a single audio file, a single video, or a single image.

  

* If you send repeated requests to obtain the upload URL and credential for the same video, different upload URLs and credentials are issued.

  

* Upload URLs are allocated by ApsaraVideo VOD. You cannot specify upload URLs.

  

* All upload credentials have the same validity period of **3,000** **seconds** (50 minutes).

  

* If you are uploading a large video file, it may take an extended period of time to complete the upload. In this case, you must refresh the upload credential after it expires. The new upload credential has the same validity period of 3,000 seconds and the upload URL remains unchanged.

  

* For images and attached media resources such as watermarks or subtitle files, you must obtain a new upload credential when the original one expires.

  




Usage notes 
--------------------------------

The process of obtaining upload URLs and credentials is a core process in ApsaraVideo VOD and is required for each upload operation. Take note of the following points for different upload methods:

* Use client SDKs

  You must obtain upload URLs and credentials on your own and provide them to the client.
  

* Call API operations

  You must obtain upload URLs and credentials on your own and then parse and use them to complete the upload.
  

* Use OSS SDKs

  You must obtain upload URLs and credentials on your own and then parse and use them to complete the upload.
  

* Use server SDKs

  Server upload SDKs provide upload URLs and credentials. You do not need to obtain them on your own. Server upload SDKs for the following programming languages are supported: Java, Python, PHP, .NET, Node.js, Go, and C/C++.
  




Obtainment methods 
---------------------------------------

You can use one of the following methods to obtain upload URLs and credentials:

* We recommend that you use [Server SDKs](/intl.en-US/Server SDK Reference/Instructions.md) to call API operations to obtain upload credentials. This method is simple and efficient. For more information, see the SDK examples in API documentation.

  

* You can send HTTP or HTTPS requests to obtain upload URLs and credentials. For more information, see [Common parameters](/intl.en-US/API Reference/Calling methods/Common parameters.md) and [Request examples](/intl.en-US/API Reference/Calling methods/Call Examples.md).

  




Common API operations 
------------------------------------------

Upload credentials include credentials for uploading videos, images, and attached media resources. The following API operations are used to obtain these upload credentials:

* [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md)

  

* [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md)

  

* [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md)

  

* [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md)

  




Parse upload URLs and credentials 
------------------------------------------------------

By default, you do not need to parse upload URLs and credentials or care about how they are parsed. However, if you want to upload media files by using OSS SDKs or by calling API operations, you must parse upload URLs and credentials.

To obtain the URLs and credentials for uploading media files to OSS, decode the upload URLs (UploadAddress) and upload credentials (UploadAuth) in Base64.

* After UploadAddress is decoded in Base64, a JSON string is obtained. The string contains the following fields:

  

  |  Field   |              Description              |
  |----------|---------------------------------------|
  | Bucket   | The name of the specified OSS bucket. |
  | Endpoint | The OSS endpoint.                     |
  | FileName | The name of the media file.           |

  

* After UploadAuth is decoded in Base64, a JSON string is obtained. The string contains the following fields:

  

  |      Field      |                                                                                        Description                                                                                        |
  |-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | AccessKeyId     | The AccessKey ID of the upload credential.                                                                                                                                                |
  | AccessKeySecret | The AccessKey secret of the upload credential.                                                                                                                                            |
  | SecurityToken   | The security token of the upload credential.                                                                                                                                              |
  | Expiration      | The validity period of the upload credential. The validity period of upload credentials for uploading videos is 3,000 seconds. You must refresh the upload credentials after they expire. |

  

  For more information, see [Upload videos by using OSS SDKs](/intl.en-US/Best Practice/Upload videos by using the OSS native SDK.md).
  




