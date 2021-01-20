# Release notes of the upload SDK for C or C++

This topic describes the release notes of different versions of the upload SDK for C or C++.

## 2019-01-15

|**Release date**|**Version**|**Description**|Download link|
|----------------|-----------|---------------|-------------|
|2019-01-15|V1.0.0|-   Various types of media files can be uploaded to ApsaraVideo VOD, including video and audio files, images, and auxiliary media assets such as watermarks and subtitle files.
-   Local media files can be uploaded to ApsaraVideo VOD. The maximum size of a file that can be uploaded is 48.8 TB. Resumable upload is not supported.
-   Online media files can be uploaded to ApsaraVideo VOD. The maximum size of a file that can be uploaded is 48.8 TB. Online media files are downloaded to local temporary directories and then uploaded to ApsaraVideo VOD. Resumable upload is not supported.
-   M3U8 video files can be uploaded. An operation is added for parsing the M3U8 index files to obtain the lists of part URLs. The URLs of part files can also be specified as needed. For more information, see [Upload SDK for C or C++](/intl.en-US/Upload SDK/Server upload/C/C++ Upload SDK.md).

|[Upload SDK for C or C++ and sample code](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/102787/cn_zh/1558078831675/VodSDK-C_1.0.0.tar.gz)|

