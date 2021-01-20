# Release notes of the upload SDK for PHP

This topic describes the release notes of different versions of the upload SDK for PHP.

## 2019-04-12

|**Release date**|**Version**|**Description**|Download link|
|----------------|-----------|---------------|-------------|
|2019-04-12|V1.0.2|-   The application ID can be specified during upload to isolate resources in the multi-application service.
-   The workflow ID can be specified during upload to implement automatic media processing.

|[Upload SDK for PHP and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/62952/cn_zh/1555416464043/VodUploadSDK-PHP_1.0.2.zip)|

## 2019-02-28

|**Release date**|**Version**|**Description**|Download link|
|----------------|-----------|---------------|-------------|
|2019-02-28|V1.0.1|-   The UserData parameter can be set during the upload of images and auxiliary media assets.
-   Upload exceptions outside China are fixed.

|[Upload SDK for PHP and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1551433743776/VodUploadSDK-PHP_1.0.1.zip)|

## 2018-12-21

|**Release date**|**Version**|**Description**|Download link|
|----------------|-----------|---------------|-------------|
|2018-12-21|V1.0.0|-   Various types of media files can be uploaded to ApsaraVideo VOD, including video and audio files, images, and auxiliary media assets such as watermarks and subtitle files.
-   Local media files can be uploaded to ApsaraVideo VOD. The maximum size of a file that can be uploaded is 48.8 TB. Resumable upload is not supported.
-   Online media files can be uploaded to ApsaraVideo VOD. The maximum size of a file that can be uploaded is 48.8 TB. Online media files are downloaded to local temporary directories and then uploaded to ApsaraVideo VOD. Resumable upload is not supported.
-   M3U8 video files can be uploaded. An operation is added for parsing the M3U8 index files to obtain the lists of part URLs. The URLs of part files can also be specified as needed. For more information, see [Upload SDK for PHP](/intl.en-US/Upload SDK/Server upload/PHP upload SDK.md).

|[Upload SDK for PHP and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1545717905651/VodUploadSDK-PHP_1.0.0.zip?file=VodUploadSDK-PHP_1.0.0.zip)|

