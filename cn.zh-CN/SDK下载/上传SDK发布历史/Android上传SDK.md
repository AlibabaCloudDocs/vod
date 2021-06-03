# Android上传SDK

本文为您介绍了阿里云Android上传SDK在不同更新时间对应的更新功能。

## 2021-06-03

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2021-06-03|V1.6.2|修复SDK稳定性问题。|[Android上传SDK及示例代码](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.6.2/ApsaraVideo_Upload_v1.6.2_Android_20210602.zip)|

## 2020-06-23

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2020-06-23|V1.6.1|修复已知问题，提高稳定性。|[Android上传SDK及示例代码](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.6.1/ApsaraVideo_Upload_v1.6.1_Android_20200623.zip)|

## 2020-03-12

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2020-03-12|V1.6.0|修复设置userdata不生效问题。|[Android上传SDK及示例代码](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.6.0/ApsaraVideo_Upload_v1.6.0_Android_20200311.zip?spm=a2c4g.11186623.2.13.5d68689de8CAmR&file=ApsaraVideo_Upload_v1.6.0_Android_20200311.zip)|

## 2019-12-02

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2019-12-02|V1.5.5|-   适配Android Q版本。
-   解决采用STS方式进行多文件上传失败问题。

|[Android上传SDK及示例代码](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.5.5/ApsaraVideo_Upload_v1.5.5_Android_20191202.zip)|

## 2019-11-21

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2019-11-21|V1.5.4|-   删除风险代码，解决Google代码扫描不通过问题。
-   修复STS上传方式下，上传带空格文件名时的解析崩溃问题。

|[Android上传SDK及示例代码](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/upload/1.5.4/ApsaraVideo_Upload_v1.5.4_Android_20191122.zip)|

## 2019-06-14

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2019-06-14|V1.5.3|-   以STS方式上传添加多应用能力。
-   以STS方式上传添加设置工作流能力。
-   Demo界面仅展示凭证上传的演示，将STS形式的相关代码放入/old文件夹中，推荐使用上传凭证的方式上传。
-   Android修改出现videoID云端不存在时删除本地断点续传的值。
-   修复已知问题，提高稳定性。

|[Android上传SDK及示例代码](https://vod-download.cn-shanghai.aliyuncs.com/sdk/vodupload/1.5.3/ApsaraVideo_Upload_v1.5.3_Android_20190614.zip)|

## 2018-12-21

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2018-12-21|V1.5.0|-   增加点播凭证上传Demo。
-   新增region字段。
-   新增断点续传开关recordUploadProgress。
-   上传进度上报。
-   修复已知问题，提高稳定性。

|[Android上传SDK及示例代码](https://vod-download.cn-shanghai.aliyuncs.com/sdk/vodupload/1.5/ApsaraVideo_Upload_v1.5.0_Android_20181221.zip)|

## 2018-08-07

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2018-08-07|V1.4.0|-   解决OSS最小分片小于100KB的问题。
-   解决上传中异常终止断点续传重复创建点播凭证导致上传文件播放不了的问题。

|[Android上传SDK及示例代码](https://vod-download.cn-shanghai.aliyuncs.com/vodupload/1.4/ApsaraVideo_Uplpad_v1.4.0_Android_20180806.zip)|

## 2018-01-22

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2018-01-22|V1.3.0|-   添加STS接口支持。
-   Demo模式区分。
-   分片大小、网络超时、重传次数可自定义。
-   使用OSS断点续传接口。
-   STS调用Open API Demo实现。
-   短视频内部调用OSS接口不在调用多文件上传接口，且替换为断点续传方式。

|[Android上传SDK 1.3.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516604091547/VodUploadSDK_1.3.0.zip?spm=5176.doc51992.2.31.JXmtz7&file=VodUploadSDK_1.3.0.zip)

[Android上传Demo 1.3.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516604049881/VODUploadDemo-android-1.3.0.zip?spm=5176.doc51992.2.32.JXmtz7&file=VODUploadDemo-android-1.3.0.zip) |

## 2017-11-24

|日期|版本|修改内容|下载地址|
|--|--|----|----|
|2017-11-24|V1.1.1|-   增加短视频上传接口，开发者不用多次调用管理列表。
-   短视频上传接口增加STS模式。
-   支持重试次数和重试事件的自定义。
-   修改上传Demo，将短视频上传和多文件上传分离且提供单独文档，让开发者更加能够理解其中的区别。

|[Android上传SDK 1.1.1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1511938777522/VodUploadSDK1.1.1.zip)

[Android上传Demo 1.1.1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/53059/cn_zh/1511525715563/VODUploadDemo-android-1.1.1.zip) |

