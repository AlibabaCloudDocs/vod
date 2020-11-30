HLS标准加密参数透传 
================================

当您需要将视频加密播放时，可以开启HLS标准加密参数透传功能。本文为您介绍HLS标准加密参数透传功能以及操作流程。

功能介绍 
-------------------------

**HLS标准加密参数透传** 功能支持开启HLS（M3U8）标准加密改写，开启加密后可自定义追加参数名称，以配合您的客户端使用个性化的加密参数名。如果不设置自定义参数名，则默认的参数名为`MtsHlsUriToken`。

HLS（HTTP Live Streaming）标准加密改写是改写HLS中M3U8文件的`#EXT-X-KEY`标签，改写成功后会在`#EXT-X-KEY`标签中的URI末尾追加一个参数，该参数的值由客户端请求携带。

操作步骤 
---------------------------

1. 登录[点播控制台](https://vod.console.aliyun.com/)。

   

2. 在点播控制台左侧导航栏选择 **配置管理** 。

   

3. 单击 **分发加速配置 \> 域名管理** ，进入域名管理页面。

   

4. 选择您要配置的域名，单击 **配置** 。

   ![选择域名](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0198425061/p181835.png)
   

5. 单击 **视频相关** ，开启 **HLS标准加密参数透传** **。** 

   ![HLS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0198425061/p181836.png)
   **说明**

   开启后，HLS标准加密参数透传时，将通过改写Token鉴权信息参数帮您鉴权，改写的参数名称为`MtsHlsUriToken` **。**

   




示例 
-----------------------

在VOD控制台开启 **HLS标准加密参数透传** ，默认的参数名为`MtsHlsUriToken`。

客户端请求中携带`MtsHlsUriToken`参数，参数的值为`test`，当CDN解密播放时，会将`MtsHlsUriToken=test`追加到M3U8文件中`#EXT-X-KEY`标签的URI末尾。
**注意**

政务云暂不支持该功能。
