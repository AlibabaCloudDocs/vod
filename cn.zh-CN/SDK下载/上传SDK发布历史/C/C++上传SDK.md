# C/C++上传SDK

本文为您介绍了阿里云C/C++上传SDK在不同更新时间对应的更新功能。

## 2019-01-15

|**日期**|**版本**|**修改内容**|下载地址|
|------|------|--------|----|
|2019-01-15|V1.0.0|-   可上传各种媒体文件到点播。如视频（含音频）、图片、辅助媒资（如水印与字幕文件）。
-   支持上传本地媒体文件到点播，最大支持48.8 TB的单个文件（暂不支持断点续传）。
-   支持上传网络媒体文件到点播，最大支持48.8 TB的单个文件，会先下载到本地临时目录再上传（暂不支持断点续传）。
-   支持上传M3U8视频，同时提供解析M3U8索引文件得到分片地址列表的接口，也可自行指定分片文件地址。具体内容，请参见[上传说明](/cn.zh-CN/上传SDK/服务端上传/C/C++上传SDK.md)。

|[C/C++上传SDK及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/102787/cn_zh/1558078831675/VodSDK-C_1.0.0.tar.gz)|

