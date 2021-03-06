# MNS可靠事件通知

阿里云消息服务MNS（Message Service）是一种高效、可靠、安全、便捷、可弹性扩展的分布式消息服务。本文为您介绍MNS可靠事件通知的注意事项、配置流程和消费消息。

-   MNS提供了队列模型，支持多个生产者和消费者并发访问同一个队列，并能确保某条消息在取出之后的特定时间段内，无法被其他消费者获得。消息被消费后一段时间内不可见，需要用户主动删除，否则该消息会被再次消费。具体介绍，请参见[什么是消息服务MNS]()。
-   点播服务支持多个存储区域（中国大陆、新加坡等），每个区域可以单独配置事件通知的回调方式和回调地址。用户可以上传视频到不同区域的存储，视频处理（如上传、转码）完成后，点播服务会根据存储区域配置的回调及时通知用户，并将内容推送到用户MNS服务的队列中。

## 注意事项

-   点播服务发起MNS回调时，若未授权点播服务访问、Endpoint不是公网或队列名称不对导致消息写入失败，点播服务会继续重试回调2次，即总共最多回调3次；超过后会丢弃。
-   消息队列推荐区域：
    -   如果视频保存在中国大陆区域（如华北2、华东2等），建议使用**华东2（上海）**区域的队列，推送消息到非**华东2（上海）**区域的队列存在较短时间的延迟。
    -   如果视频保存在其他区域（如新加坡、印度尼西亚等），建议创建或使用该区域的消息队列。

        如：视频存储区域为印度（孟买），则应创建或使用**印度（孟买）**区域的消息队列。


## 配置MNS可靠事件通知

1.  登录[阿里云控制台](https://home.console.aliyun.com)，访问[点播授权页面](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunVODDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//vod.console.aliyun.com/%22%2C%20%22Service%22%3A%20%22VOD%22%7D)，单击页面下方的**同意授权**。

    ![授权页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0575934061/p178869.png)

2.  登录[消息服务控制台](https://mns.console.aliyun.com/?spm=a2c4g.11186623.2.19.20d83502Ek9Nnu)创建队列或使用已有队列。具体操作，请参见[t1835614.md\#]()。

    **说明：** 建议视频存储在中国大陆的，队列列表选择**华东2（上海）**区域。

3.  调用[设置事件通知配置](/cn.zh-CN/服务端API/全局配置/事件通知/设置事件通知配置.md)接口完成事件通知配置。

    -   `MnsEndpoint`（消息队列公网Endpoint）可以通过单击控制台右上角的**获取Endpoint**按钮获取。

        ![获取Endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6515044061/p178932.png)

    -   `EventTypeList`（回调的事件类型），请参见[事件类型](/cn.zh-CN/开发指南/事件通知/概述.md) 。
4.  完成事件通知配置后，登录[视频点播控制台](https://vod.console.aliyun.com/#/overview)上传视频来触发需要回调的事件。

5.  当满足产生回调事件条件时，点播服务端会将回调内容写入您提供的队列，返回消息服务控制台，单击对应队列的**接收消息**按钮，从接收消息窗口中查看消息内容。


## 消费消息

配置完成后，可以通过如下代码消费消息：

-   如何使用Java代码消费消息，请参见[队列使用手册]()。
-   如何使用Python代码消费消息，请参见[队列使用手册]()。
-   如何使用C\#代码消费消息，请参见[队列使用手册]()。
-   如何使用PHP代码消费消息，请参见[队列使用手册]()。
-   其他语言可以通过调用接口来获取消息内容，首先掌握[调用方式]()后，调用[消费消息]()接口获取消息内容，调用[删除消息]()接口删除消息。

队列支持多个生产者和消费者并发访问同一个队列，并能确保某条消息在取出之后的特定时间段内，无法被其他消费者获得。消息被消费后一段时间内不可见，需要用户主动删除，否则该消息会被再次消费。

