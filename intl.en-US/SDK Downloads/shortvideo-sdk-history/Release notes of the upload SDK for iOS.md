# Release notes of the upload SDK for iOS

This topic describes the release notes of different versions of the upload SDK for iOS.

## 2020-06-23

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2020-06-23|V1.6.1|The known issues are fixed to improve stability.|[Upload SDK for iOS and sample code](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.6.1/ApsaraVideo_AlivcVideoUpload_v1.6.1_iOS_20200623.zip)|

## 2020-03-13

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2020-03-13|V1.6.0|The issue is fixed where the setting of the UserData parameter does not take effect.|[Upload SDK for iOS and sample code](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.6.0/ApsaraVideo_AlivcVideoUpload_v1.6.0_iOS_20200313.zip)|

## 2019-06-14

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-06-14|V1.5.3|-   The multi-application capability is added by using the Security Token Service \(STS\)-based upload mode.
-   The capability of setting a workflow is added by using the STS-based upload mode.
-   The demo only demonstrates how to use an upload credential to upload videos. The code that is used to implement STS-based upload is stored in the /old folder. We recommend that you use an upload credential to upload videos.
-   The known issues are fixed to improve stability.

|[Upload SDK for iOS and sample code](https://vod-download.cn-shanghai.aliyuncs.com/sdk/vodupload/1.5.3/ApsaraVideo_AlivcVideoUpload_v1.5.3_iOS_20190614.zip)|

## 2018-12-21

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-12-21|V1.5.0|-   A demo is added to demonstrate how to use an upload credential to upload videos to ApsaraVideo VOD.
-   The region parameter is added.
-   The recordUploadProgress parameter is added. You can set the parameter to specify whether to enable progress recording for resumable upload.
-   The upload progress can be reported.
-   The known issues are fixed to improve stability.

|[Upload SDK for iOS and sample code](https://vod-download.cn-shanghai.aliyuncs.com/sdk/vodupload/1.5/ApsaraVideo_Uplpad_v1.5.0_iOS_20181221.zip)|

## 2018-08-07

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-08-07|V1.4.0|-   The issue is fixed where the size of a part is smaller than 100 KB in Object Storage Service \(OSS\).
-   The issue is fixed where the upload credential is recreated for resumable upload when the upload to ApsaraVideo VOD is unexpectedly interrupted. This issue leads to playback failures of uploaded files.

|[Upload SDK for iOS and sample code](https://vod-download.cn-shanghai.aliyuncs.com/vodupload/1.4/ApsaraVideo_Uplpad_v1.4.0_iOS_20180806.zip)|

## 2018-01-24

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-01-24|V1.3.0|-   The STS operations are added.
-   Different upload modes are distinguished in the demo.
-   The part size, network timeout period, and maximum number of retransmission times can be customized.
-   The resumable upload operation of OSS is adopted.
-   A demo is added to demonstrate how to use STS to call operations.
-   The multi-file upload operation is replaced with the resumable upload operation when the OSS API is called to upload short videos.

|[Upload SDK V1.3.0 for iOS](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516712191000/VODUploadSDK-ios-1.3.0.zip?spm=5176.doc51992.2.27.WGPO3F&file=VODUploadSDK-ios-1.3.0.zip)

[Sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516712221266/VODUploadDemo-ios-1.3.0.zip?spm=5176.doc51992.2.28.KsGPXV&file=VODUploadDemo-ios-1.3.0.zip) |

## 2017-11-24

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2017-11-24|V1.1.1|-   The upload operation for short videos is added so that you do not need to call a management list multiple times.
-   The STS mode is added for the operation of short video upload.
-   The maximum number of retransmission times and retransmission events can be customized.
-   The upload demo is modified to separate short video upload from multi-file upload. In addition, documents are provided for you to better understand the differences between the two types of upload.
-   CocoaPods-based upload is supported.

|[Upload SDK V1.1.1 for iOS](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1512714088186/VODUploadSDK-iOS-1.1.1.zip)

[Sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1512714065120/VODUploadDemo.zip) |

