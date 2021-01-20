# Release notes of the upload SDK for Android

This topic describes the release notes of different versions of the upload SDK for Android

## 2020-06-23

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2020-06-23|V1.6.1|The known issues are fixed to improve stability.|[Upload SDK for Android and sample code](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.6.1/ApsaraVideo_Upload_v1.6.1_Android_20200623.zip)|

## 2020-03-12

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2020-03-12|V1.6.0|The issue is fixed where the setting of the UserData parameter does not take effect.|[Upload SDK for Android and sample code](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.6.0/ApsaraVideo_Upload_v1.6.0_Android_20200311.zip?spm=a2c4g.11186623.2.13.5d68689de8CAmR&file=ApsaraVideo_Upload_v1.6.0_Android_20200311.zip)|

## 2019-12-02

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-12-02|V1.5.5|-   The SDK is adapted to Android Q.
-   The issue is fixed where multiple video files fail to be uploaded at the same time by using STS.

|[Upload SDK for Android and sample code](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.5.5/ApsaraVideo_Upload_v1.5.5_Android_20191202.zip)|

## 2019-11-21

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-11-21|V1.5.4|-   Risky code is deleted and the issue is fixed where Google code fails the scanning.
-   The issue is fixed where an unexpected quit occurs when a video file whose file name contains a space is uploaded by using STS.

|[Upload SDK for Android and sample code](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.5.4/ApsaraVideo_Upload_v1.5.4_Android_20191122.zip)|

## 2019-06-14

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-06-14|V1.5.3|-   The multi-application capability is added by using the STS-based upload mode.
-   The capability of setting a workflow is added by using the STS-based upload mode.
-   The demo only demonstrates how to use an upload credential to upload videos. The code that is used to implement STS-based upload is stored in the /old folder. We recommend that you use an upload credential to upload videos.
-   The issue is fixed where the value of local resumable upload is deleted when a video ID does not exist on the cloud.
-   The known issues are fixed to improve stability.

|[Upload SDK for Android and sample code](https://vod-download.cn-shanghai.aliyuncs.com/sdk/vodupload/1.5.3/ApsaraVideo_Upload_v1.5.3_Android_20190614.zip)|

## 2018-12-21

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-12-21|V1.5.0|-   A demo is added to demonstrate how to use an upload credential to upload videos to ApsaraVideo VOD.
-   The region parameter is added.
-   The recordUploadProgress parameter is added. You can set the parameter to specify whether to enable progress recording for resumable upload.
-   The upload progress can be reported.
-   The known issues are fixed to improve stability.

|[Upload SDK for Android and sample code](https://vod-download.cn-shanghai.aliyuncs.com/sdk/vodupload/1.5/ApsaraVideo_Upload_v1.5.0_Android_20181221.zip)|

## 2018-08-07

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-08-07|V1.4.0|-   The issue is fixed where the size of a part is smaller than 100 KB in OSS.
-   The issue is fixed where the upload credential is recreated for resumable upload when the upload to ApsaraVideo VOD is unexpectedly interrupted. This issue leads to playback failures of uploaded files.

|[Upload SDK for Android and sample code](https://vod-download.cn-shanghai.aliyuncs.com/vodupload/1.4/ApsaraVideo_Uplpad_v1.4.0_Android_20180806.zip)|

## 2018-01-22

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-01-22|V1.3.0|-   The STS operations are added.
-   Different upload modes are distinguished in the demo.
-   The part size, network timeout period, and maximum number of retransmission times can be customized.
-   The resumable upload operation of OSS is adopted.
-   A demo is added to demonstrate how to use STS to call operations.
-   The multi-file upload operation is replaced with the resumable upload operation when the OSS API is called to upload short videos.

|[Upload SDK V1.3.0 for Android](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516604091547/VodUploadSDK_1.3.0.zip?spm=5176.doc51992.2.31.JXmtz7&file=VodUploadSDK_1.3.0.zip)

[Upload SDK demo for Android 1.3.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516604049881/VODUploadDemo-android-1.3.0.zip?spm=5176.doc51992.2.32.JXmtz7&file=VODUploadDemo-android-1.3.0.zip) |

## 2017-11-24

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2017-11-24|V1.1.1|-   The upload operation for short videos is added so that you do not need to call a management list multiple times.
-   The STS mode is added for the operation of short video upload.
-   The maximum number of retransmission times and retransmission events can be customized.
-   The upload demo is modified to separate short video upload from multi-file upload. In addition, documents are provided for you to better understand the differences between the two types of upload.

|[Upload SDK V1.1.1 for Android](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1511938777522/VodUploadSDK1.1.1.zip)

[Upload SDK demo V1.1.1 for Android](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/53059/cn_zh/1511525715563/VODUploadDemo-android-1.1.1.zip) |

