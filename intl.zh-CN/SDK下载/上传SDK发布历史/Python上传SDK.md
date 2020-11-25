# Python上传SDK

本文为您介绍了阿里云Python上传SDK在不同更新时间对应的更新功能。

## 2019-04-12

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2019-04-12|V1.3.1|-   上传时可指定应用ID，实现多应用体系的资源隔离。
-   上传时可指定工作流ID，实现自动化媒体处理。

|[Python上传SDK及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/62952/cn_zh/1555416515158/VodUploadSDK-Python_1.3.1.zip)|

## 2019-02-12

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2019-02-12|V1.3.0|-   支持指定点播中心（默认为上海）和存储区域，便于海外上传。
-   支持辅助媒资（水印、字幕文件）的上传。
-   支持上传时设置UserData等个性化配置和更多元数据。
-   上传网络文件调整为先下载到本地，再上传到点播，支持大文件上传，最大支持48.8 TB的单个文件。
-   改进M3U8视频的上传，提供默认解析M3U8分片信息的接口，也可自定义分片列表。

|[Python上传SDK及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1549973452610/VodUploadSDK-Python_1.3.0.zip)|

## 2018-07-05

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2018-07-05|V1.2.1|-   支持设置视频存储区域UploadVideoRequest.setStorageLocation。
-   修复上传大文件时上传凭证过期未刷新的问题。

|[Python上传SDK及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/53059/cn_zh/1530773238454/VodUploadSDK-Python_1.2.1.zip)|

## 2017-12-21

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2017-12-21|V1.1.1|-   支持上传本地单个视频、M3U8视频（含ts分片）、图片文件到点播。
-   支持上传网络上的（HTTP/HTTPS链接，含OSS链接）单个视频、M3U8视频（含ts分片）、图片文件到点播。
-   支持Python2、Python3版本。

|[Python上传SDK及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1519886203800/VodUploadSDK-Python_1.1.1.zip)|

