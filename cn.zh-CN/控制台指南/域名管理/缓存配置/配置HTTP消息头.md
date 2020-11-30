# 配置HTTP消息头

您可以通过配置HTTP消息头，定义HTTP事务中的具体操作参数。通过阅读本文，您可以了解设置HTTP头响应的操作方法。

HTTP消息头是指，在超文本传输协议HTTP（Hypertext Transfer Protocol）的请求和响应消息中，协议头部的组件。HTTP消息头准确描述了正在获取的资源、服务器或客户端的行为。

**说明：**

-   HTTP消息头的设置会影响该加速域名下所有资源，当您通过客户端（例如浏览器）访问资源时，会影响请求响应，但不会影响缓存服务器。
-   目前不支持泛域名设置。

1.  登录[视频点播控制台](https://vod.console.aliyun.com/)。

2.  在点播控制台左侧导航栏选择**配置管理**。

3.  单击**分发加速配置** \> **域名管理**，进入域名管理页面。

4.  选择您要配置的域名，单击**配置**。

    ![配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1277415061/p180549.png)

5.  单击**缓存配置**。

6.  单击**HTTP头**页签，单击**添加**。

    ![添加HTTP头](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7928415061/p181565.png)

7.  选择**参数**，输入**取值**，单击**确定**完成配置。

    ![添加](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7928415061/p181590.png)

    参数和描述请参见下表。

    |参数|描述|示例|
    |:-|:-|--|
    |Content-Type|指定客户端程序响应对象的内容类型。|image|
    |Cache-Control|指定客户端程序请求和响应遵循的缓存机制。|no-cache|
    |Content-Disposition|指定客户端程序把请求所得的内容存为一个文件时提供的默认的文件名。|123.txt|
    |Content-Language|指定客户端程序响应对象的语言。|zh-CN|
    |Expires|指定客户端程序响应对象的过期时间。|Wed, 21 Oct 2015 07:28:00 GMT|
    |Access-Control-Allow-Origin|指定允许的跨域请求的来源。|\* **说明：** 您可以填写`*`表示全部域名；也可以填写完整域名，例如`www.aliyun.com`。 |
    |Access-Control-Allow-Headers|指定允许的跨域请求的字段。|X-Custom-Header|
    |Access-Control-Allow-Methods|指定允许的跨域请求方法。|POST、GET**说明：** 如果您需要同时添加POST和GET，请使用英文逗号（,）隔开。 |
    |Access-Control-Max-Age|指定客户端程序对特定资源的预取请求返回结果的缓存时间。单位：秒。|600|
    |Access-Control-Expose-Headers|指定允许访问的自定义头信息。|Content-Length|


