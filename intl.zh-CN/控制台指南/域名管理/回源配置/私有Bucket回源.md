# 私有Bucket回源

您可以阅读本文，快速了解私有Bucket授权与配置操作。

当加速域名要回源至该账号下标记为私有的Bucket时，需要先进行授权，授权成功并开启回源配置后才能访问私有Bucket。您可以配合使用视频点播服务提供的refer防盗链、鉴权等功能，有效保护您的资源安全。

**说明：**

-   授权成功并开启对应域名的私有Bucket功能后，该加速域名便可访问您私有Bucket内的资源内容。请谨慎决策。若您授权的私有Bucket内容不适合作为CDN加速的回源内容，请勿授权或开启该功能。
-   如果您的加速域名正在使用私有Bucket作为源站进行回源，请勿关闭私有Bucket回源。
-   若您的网站有攻击风险，请购买高防服务，请勿授权或开启私有Bucket功能。

## 操作步骤

1.  登录[视频点播控制台](https://vod.console.aliyun.com/)。

2.  在点播控制台左侧导航栏选择**配置管理**。

3.  单击**分发加速配置** \> **域名管理**，进入域名管理页面。

4.  选择您要配置的域名，单击**配置**。

    ![配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1277415061/p180549.png)

5.  进行授权，如已授权，请忽略此步骤。

    1.  单击**回源配置**，选择**私有Bucket回源**，单击**立即授权**。

        ![立即授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0338415061/p180601.png)

    2.  单击**同意授权**。

        ![同意授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0338415061/p180603.png)

6.  单击**回源配置**，开启**私有Bucket回源**，完成配置。

    ![开启私有Bucket回源](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0825276061/p180606.png)


