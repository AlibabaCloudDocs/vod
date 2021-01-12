# Production and upload

## Features

The short video SDK provides the AliyunIVodCompose class that is designed for video production and upload. This core class encapsulates video production and upload features to facilitate the operations on clients. You can use this core class to produce and upload edited videos on a dedicated user interface \(UI\).

**Note:**

-   The production and upload methods have the requirement for the calling order. The production method must be called before the upload method.
-   The production method can be called multiple times. The upload method uploads only the latest video file that is produced.
-   If a video is edited, you must save the effects added to the video to the on-premises profile before you create an AliyunIVodCompose instance. Otherwise, the produced video does not contain these effects. To save added effects to the on-premises profile, call the following method:

```
AliyunIEditor#saveEffectToLocal();
```

## Edition difference

|Edition|Description|
|-------|-----------|
|Professional Edition|All features are supported.|
|Standard Edition|All features are supported.|
|Basic Edition|The production and upload features are not supported. You can use the upload SDK of ApsaraVideo VOD to upload videos and images to ApsaraVideo VOD.|

## Production and upload

|Action|Sample code|
|------|-----------|
|Initialize an AliyunIVodCompose instance for production.|```
AliyunComposeFactory#createAliyunVodCompose();
AliyunIVodCompose#init(Context context);
``` |
|Start the production.|```
AliyunIVodCompose#compose(String config, String output, AliyunIComposeCallBack callback);
``` |
|Pause the production.|```
AliyunIVodCompose#pauseCompose();
``` |
|Resume the production.|```
AliyunIVodCompose#resumeCompose();
``` |
|Cancel the production.|```
AliyunIVodCompose#cancelCompose();
``` |
|Upload a video.|```
/**
* Uploads a video by using the upload URL and credential.
* videoPath: the path of the video file.
* uploadAddress: the upload URL.
* uploadAuth: the upload credential.
* aliyunVodUploadCallBack: the upload callback.
*/
AliyunIVodCompose#uploadVideoWithVod(String videoPath, String uploadAddress, String uploadAuth, AliyunIVodUploadCallBack aliyunVodUploadCallBack);
``` |
|Upload an image.|```
/**
* Uploads an image by using the upload URL and credential.
* imagePath: the path of the image file.
* uploadAddress: the upload URL.
* uploadAuth: the upload credential.
* aliyunVodUploadCallBack: the upload callback.
*/
AliyunIVodCompose#uploadImuploadImageWithVodageWithVod(String imagePath, String uploadAddress, String uploadAuth, AliyunIVodUploadCallBack aliyunVodUploadCallBack);
``` |
|Update the upload credential.|```
/**
* uploadAuth: the upload credential.
*/
AliyunIVodCompose#refreshWithUploadAuth(String uploadAuth);
``` |
|Cancel the upload.|```
AliyunIVodCompose#cancelUpload();
``` |
|Resume the upload.|```
AliyunIVodCompose#resumeUpload();
``` |
|Pause the upload.|```
AliyunIVodCompose#pauseUpload();
``` |
|Release resources.|```
AliyunIVodCompose#release();
``` |

**Note:**

-   The AliyunIVodCompose class uploads a video or an image by using the upload URL and credential. For more information, see [CreateUploadVideo](https://help.aliyun.com/document_detail/55407.html).
-   The upload credential has a validity period. If the upload credential expires, you must obtain a new credential by using the onUploadTokenExpired method. For more information, see [RefreshUploadVideo](https://help.aliyun.com/document_detail/55408.html).

