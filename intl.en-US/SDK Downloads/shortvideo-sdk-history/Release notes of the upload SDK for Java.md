# Release notes of the upload SDK for Java

This topic describes the release notes of different versions of the upload SDK for Java.

## 2020-09-23

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2020-09-23|V1.4.13|-   The issue is fixed where error messages are returned by the uploadWebM3u8 operation and the uploadURLStream operation when you use Security Token Service \(STS\) to upload videos.
-   The Object Storage Service \(OSS\) dependency is updated.

**Note:** The OSS SDK must be V3.9.0 or later.

|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1600848199952/VODUploadDemo-java-1.4.13.zip)|

## 2020-03-16

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2020-03-16|V1.4.12|Automatic resolution to the addresses of TS files is supported for the upload of M3U8 files. The addresses can be relative paths or absolute paths.|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1584350505412/VODUploadDemo-java-1.4.12.zip)|

## 2019-07-22

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-07-22|V1.4.11|Custom local directories are supported for the upload of M3U8 files. The custom local directories are used to temporarily store the downloaded files.|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1563778063998/VODUploadDemo-java-1.4.11.zip)|

## 2019-07-12

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-07-12|V1.4.10|The issue is fixed where an M3U8 file fails to be uploaded based on the URL that contains authentication information.|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1562903947499/VODUploadDemo-java-1.4.10.zip)|

## 2019-06-25

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-06-25|V1.4.9|The upload of ultra-large audio and video streams is supported.|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1561708141494/VODUploadDemo-java-1.4.9.zip)|

## 2019-06-06

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-06-06|V1.4.8|STS-based upload is supported.|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1559795565842/VODUploadDemo-java-1.4.8.zip)|

## 2019-04-12

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-04-12|V1.4.7|-   The application ID can be specified when you upload audio and video files, images, and auxiliary media assets.
-   The type and description can be set when you upload images.

|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1555048043943/VODUploadDemo-java-1.4.7.zip)|

## 2019-03-10

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-03-10|V1.4.6|-   Local auxiliary media assets can be uploaded to ApsaraVideo VOD. After you specify the local directory of an auxiliary media asset, the upload SDK automatically uploads the auxiliary media asset to ApsaraVideo VOD.
-   Online auxiliary media assets can be uploaded to ApsaraVideo VOD. After you specify the URL of an online auxiliary media asset, the upload SDK automatically downloads the auxiliary media asset from the URL and uploads it to ApsaraVideo VOD.

|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1552227669169/VODUploadDemo-java-1.4.6.zip)|

## 2019-02-19

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-02-19|V1.4.5|-   The workflow ID can be specified during the upload of audio or video files.
-   The incompatibility issues of SDK are fixed.
    -   aliyun-java-sdk-core is updated to V4.3.3.
    -   aliyun-java-sdk-vod is updated to V2.15.0.
    -   V2.8.2 and later versions of the com.google.code.gson dependency are added.

|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1550571710324/VODUploadDemo-java-1.4.5.zip)|

## 2019-01-30

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-01-30|V1.4.4|-   Local M3U8 audio and video files including all part files can be uploaded to ApsaraVideo VOD. To upload the files, you must specify the local directories of M3U8 index files and part files.
-   Online M3U8 audio and video files including all part files can be uploaded to ApsaraVideo VOD. To upload the files, you must specify the URLs of M3U8 index files and part files.
-   The region of the ECS instance where you want to deploy an upload script can be specified. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the specified file is automatically uploaded by using an internal network, which can accelerate the upload speed and save the public network traffic.
-   The VOD center and storage region can be specified to facilitate upload outside China. The default VOD center is in the China \(Shanghai\) region.
-   The issue is fixed where the specified part size does not take effect in multipart upload.

|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1548820581839/VODUploadDemo-java-1.4.4.zip)|

## 2018-12-21

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-12-21|V1.4.3|The UserData parameter can be set when you upload audio and video files.|[Upload SDK for Java and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1545382153255/VODUploadDemo-java-1.4.3.zip)|

