# DNSPod配置CNAME流程

您在视频点播中添加自己的域名后，会自动生成有效的CNAME地址。如果您想启用视频点播加速服务，您需在自己域名所在的DNS服务商处，为域名添加CNAME记录，访问加速域名的请求才能转发到CDN节点上，达到加速效果。本文以DNSPod为例，为您介绍CNAME的配置流程。

## 操作步骤

1.  获取加速域名的CNAME地址。

    1.  登录[视频点播控制台](https://vod.console.aliyun.com/)。

    2.  单击**配置管理\>分发加速配置\>域名管理**。

    3.  选择您要配置的域名，鼠标悬浮于查看标识上，复制加速域名对应的CNAME值。

        ![复制CNAME](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2767006061/p182210.png)

2.  添加CNAME记录。

    1.  登录DNSPod的[域名解析控制台](https://console.dnspod.cn/)。

    2.  在对应域名的域名解析页，选择添加记录。

    3.  进行相关配置。

        **说明：** 一个加速域名对应一个CNAME地址，主域名的CNAME地址不能被二级域名使用。如果您需要加速二级域名，需将二级域名也添加到CDN上，并解析到对应的CNAME地址，或者在CDN上添加泛域名，泛域名的CNAME可以被二级域名使用。

        -   记录类型：选择`CNAME`。
        -   主机记录：加速域名的前缀。

            |如果您的加速域名为|主机记录为|
            |:--------|:----|
            |`testcdn.aliyun.com`|`testcdn`|
            |`www.aliyun.com`|`www`|
            |`aliyun.com`|`@`|
            |`*.aliyun.com`|`*`|

        -   解析线路：默认值。
        -   记录值：输入加速域名对应的CNAME地址。
        -   TTL：全称Time To Live，表示DNS记录在DNS服务器上缓存时间，使用默认值。
    4.  单击**保存**。

        成功配置CNAME且生效后，加速服务会立即生效。

        **说明：**

        -   新增CNAME记录实时生效，修改CNAME记录在72小时内生效。
        -   成功配置CNAME后状态更新约有10分钟延迟，控制台的域名列表页可能仍提示“未配置CNAME”，请您暂时忽略。
3.  验证CNAME配置是否生效。

    1.  打开Windows的CMD命令行程序。

    2.  在命令行中ping加速域名，如果返回的解析结果和CDN控制台上该加速域名的CNAME值一致，则表示CDN加速已经生效。

        ![CNAME生效验证](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6423839951/p66693.png)


