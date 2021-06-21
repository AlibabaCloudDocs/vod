# DRM加密

本文为您介绍在控制台使用DRM（Digital Rights Management）加密功能的操作步骤，包括证书上传、控制台配置以及播放器配置。

## 使用限制

目前点播DRM加密功能只支持在控制台开启，暂不支持API调用。

## 上传证书

**说明：** 面向iOS平台用户，需要进行Fairplay证书上传操作。

1.  申请Fairplay证书。

    由于Apple公司要求，使用Fairplay加密需要向其申请相关证书，详情请参见[申请Fairplay证书](/intl.zh-CN/控制台指南/DRM管理/申请Fairplay证书.md)。

2.  登录[视频点播控制台](https://vod.console.aliyun.com/)。

3.  在点播控制台左侧导航栏选择**配置管理**。

4.  单击**媒体处理配置** \> **DRM证书管理**，进入DRM证书管理页面。

5.  单击**上传证书**开始上传。

    ![上传](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6317736061/p177092.png)


## 控制台配置

1.  登录[视频点播控制台](https://vod.console.aliyun.com/)。

2.  在点播控制台左侧导航栏选择**配置管理**。

3.  单击**媒体处理配置** \> **转码模板组**。

4.  单击**添加转码模板组**。

    ![转码](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796683061/p177096.png)

5.  在**添加转码模板组**页面，单击**添加模板**。

6.  在**基本参数\>封装格式**中，选择**hls**。

7.  在**高级参数\>加密方式**中，选择**DRM加密**。

    ![添加DRM模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796683061/p177122.png)

8.  进行转码。

    通过控制台、API或上传SDK上传视频时，指定配置了DRM的模板进行转码。转码成功后，在**控制台\>媒资库\>音/视频**中，选择进行转码后的视频，单击**管理**进入该视频管理页面，选择**视频地址**页签进行查看。进行DRM转码后的视频，在格式列表下会有**DRM**相关标识。

    ![标识](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796683061/p177131.png)


## 播放器配置

目前点播DRM功能需要结合阿里云播放器一起使用，降低开发门槛。播放器在播放DRM的视频时，需要有以下设置：

-   支持播放DRM视频的播放器版本：5.2.1及以上。目前iOS平台支持Fairplay，Android平台支持WideVine。
-   Android平台，为了保证高安全等级的视频能正常播放，建议使用surfaceView进行播放。
-   iOS平台需要全局调用一次AliPlayerGlobalSettings中的setFairPlayCertID方法来设置证书ID。证书ID可在**控制台\>配置管理\>DRM证书管理**中的证书ID列表获取。

**说明：** 目前仅支持移动端，Web端将在近期支持。播放高安全等级视频时无法支持旋转、镜像、截图等操作。

