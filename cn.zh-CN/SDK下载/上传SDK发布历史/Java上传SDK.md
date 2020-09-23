# Java上传SDK

|**日期**|**版本**|**修改内容**|下载地址|
|------|------|--------|----|
|2020-09-23|1.4.13|-   修复使用STS方式上传，uploadWebM3u8、uploadURLStream接口报错问题。
-   升级OSS依赖版本。

 注意：使用本版本，需保证aliyun-sdk-oss\>=3.9.0|[Java上传SDK 1.4.13及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1600848199952/VODUploadDemo-java-1.4.13.zip)|
|2020-03-16|1.4.12|m3u8文件上传：支持自动解析m3u8文件中的ts地址，包括相对和绝对路径|[Java上传SDK 1.4.12及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1584350505412/VODUploadDemo-java-1.4.12.zip)|
|2019-07-22|1.4.11|网络m3u8文件上传：支持自定义本地目录，用于存放内部下载的临时文件|[Java上传SDK 1.4.11及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1563778063998/VODUploadDemo-java-1.4.11.zip)|
|2019-07-12|1.4.10|网络m3u8文件上传：修复带鉴权信息的m3u8地址上传失败的问题|[Java上传SDK 1.4.10及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1562903947499/VODUploadDemo-java-1.4.10.zip)|
|2019-06-25|1.4.9|支持超大音视频网络流上传|[Java上传SDK 1.4.9及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1561708141494/VODUploadDemo-java-1.4.9.zip)|
|2019-06-06|1.4.8|支持STS方式上传|[Java上传SDK 1.4.8及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1559795565842/VODUploadDemo-java-1.4.8.zip)|
|2019-04-12|1.4.7|-   上传音视频、图片和辅助媒资时，支持设置应用ID
-   图片上传支持设置分类和描述

|[Java上传SDK 1.4.7及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1555048043943/VODUploadDemo-java-1.4.7.zip)|
|2019-03-10|1.4.6|-   上传本地辅助媒资文件到点播，指定本地文件路径，即可自动上传到点播
-   上传网络辅助媒资文件到点播，指定URL地址，即可自动下载并上传到点播

|[Java上传SDK 1.4.6及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1552227669169/VODUploadDemo-java-1.4.6.zip)|
|2019-02-19|1.4.5|-   支持上传音视频文件时设置点播工作流WorkflowId参数
-   修复SDK兼容问题：
    -   升级aliyun-java-sdk-core版本号至4.3.3
    -   升级aliyun-java-sdk-vod版本号至2.15.0
    -   增加依赖包com.google.code.gson 版本号\>=2.8.2

|[Java上传SDK 1.4.5及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/106648/cn_zh/1550571710324/VODUploadDemo-java-1.4.5.zip)|
|2019-01-30|1.4.4|-   上传本地m3u8音视频（包括所有分片文件）到点播，指定本地m3u8索引文件和分片文件目录
-   上传网络m3u8音视频（包括所有分片文件）到点播，需指定m3u8索引文件和分片文件的URL地址
-   可指定上传脚本部署的ECS区域，如果和点播存储区域相同，则自动使用内网上传，上传更快且更省公网流量
-   可指定点播中心（默认为上海）和存储区域，便于海外上传
-   修复分片上传设置分片大小不生效的问题

|[Java上传SDK 1.4.4及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1548820581839/VODUploadDemo-java-1.4.4.zip)|
|2018-12-21|1.4.3|支持上传音视频文件时设置UserData参数|[Java上传SDK 1.4.3及示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1545382153255/VODUploadDemo-java-1.4.3.zip)|

