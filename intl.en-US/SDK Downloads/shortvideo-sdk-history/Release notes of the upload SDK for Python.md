# Release notes of the upload SDK for Python

This topic describes the release notes of different versions of the upload SDK for Python.

## 2019-04-12

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-04-12|V1.3.1|-   The application ID can be specified during upload to isolate resources in the multi-application service.
-   The workflow ID can be specified during upload to implement automatic media processing.

|[Upload SDK for Python and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/62952/cn_zh/1555416515158/VodUploadSDK-Python_1.3.1.zip)|

## 2019-02-12

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2019-02-12|V1.3.0|-   The VOD center and storage region can be specified to facilitate upload outside China. The default VOD center is in the China \(Shanghai\) region.
-   Auxiliary media assets, such as watermarks and subtitle files, can be uploaded.
-   Custom settings, such as the UserData parameter, and more metadata can be set during upload.
-   The upload method of online files is changed. Online files are downloaded to local directories and then uploaded to ApsaraVideo VOD. The maximum size of a file that can be uploaded is 48.8 TB.
-   The upload method of M3U8 video files is improved. An operation is added to parse the part information in the M3U8 index files by default. The part list can also be customized.

|[Upload SDK for Python and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1549973452610/VodUploadSDK-Python_1.3.0.zip)|

## 2018-07-05

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2018-07-05|V1.2.1|-   The UploadVideoRequest.setStorageLocation operation is added.
-   The issue is fixed where an upload credential is not updated after expiration during the upload of a large file.

|[Upload SDK for Python and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/53059/cn_zh/1530773238454/VodUploadSDK-Python_1.2.1.zip)|

## 2017-12-21

|Release date|Version|Description|Download link|
|------------|-------|-----------|-------------|
|2017-12-21|V1.1.1|-   A local video, M3U8 video file with TS files, or image can be uploaded to ApsaraVideo VOD at a time.
-   An online video, M3U8 video file with TS files, or image that has an HTTP, HTTPS, or OSS endpoint can be uploaded to ApsaraVideo VOD.
-   Python 2 and Python 3 are supported.

|[Upload SDK for Python and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1519886203800/VodUploadSDK-Python_1.1.1.zip)|

