# HLS标准加密

HLS标准加密需要配合密钥管理服务和令牌服务使用，本文为您介绍HLS标准加密的相关概念、准备工作、接入流程和常见问题。

## 整体架构

![HLS整体架构](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9479475061/p178336.png)

## 相关概念

-   密钥管理服务

    [密钥管理服务](https://common-buy.aliyun.com/?spm=a2c4g.11186623.2.3.bhZoMo&commodityCode=kms#/open)（Key Management Service，简称KMS），是一种安全管理服务，主要负责数据密钥的生产、加密、解密等工作。

-   访问控制

    [访问控制](https://www.aliyun.com/product/ram?spm=a2c4g.11186623.2.4.QY4xuc)（Resource Access Management 简称RAM）是阿里云为客户提供的用户身份管理与资源访问控制服务。

-   数据密钥

    数据密钥（Data Key，简称DK）也称明文密钥。DK为加密数据使用的明文数据密钥。

-   信封数据密钥

    信封数据密钥（Enveloped Data Key，简称EDK）也称密文密钥。EDK为通过信封加密技术保密后的密文数据密钥。


## 准备工作

1.  [开通KMS服务](https://common-buy.aliyun.com/?spm=a2c4g.11186623.2.3.bhZoMo&commodityCode=kms#/open)。
2.  提交[工单](https://workorder.console.aliyun.com/console.htm#/ticket/add?productCode=vod&commonQuestionId=561&isSmart=true&iatraceid=1606446020666-2b842b67ddd84da10488b6&channel=selfservice)申请创建Service Key。Service Key与视频存储的源站区域必须一致，例如：视频存储在华东2，则Service Key必须是华东2。

    **说明：** Service Key是秘钥管理服务的一种加密主Key，接入标准加密的秘钥必须要使用该Service Key生成。视频点播控制台暂不支持用户自主创建Service Key。

3.  搭建密钥管理服务，封装阿里云秘钥管理服务（KMS），调用[GenerateDataKey](/cn.zh-CN/API参考/密钥/GenerateDataKey.md)接口生成一个AES\_128密钥。

    **说明：** GenerateDataKey接口只需要传KeyId（上述中的Service Key）和KeySpec（固定为：AES\_128）即可，其他参数不用传，否则可能加密失败。

4.  搭建令牌颁发服务，生成MtsHlsUriToken。
5.  解密密钥EDK（密文密钥），调用[Decrypt](/cn.zh-CN/API参考/密钥/Decrypt.md)接口进行解密。如果业务方需要对解密接口进行安全验证，则需要提供令牌生成服务，生成的令牌能够在解密服务中被解析验证。

    **说明：** 解密接口返回的数据，是[GenerateDataKey](/cn.zh-CN/API参考/密钥/GenerateDataKey.md)生成的两种秘钥中的明文秘钥（PlainText）经过base64decode之后的数据。


## 接入流程

标准加密必须按照以下流程接入。

1.  创建转码模板

    HLS标准加密转码需要创建两个转码模板。

    -   加密模板：在控制台的[添加转码模板组](https://vod.console.aliyun.com/?#/settings/transcode/add)页面，创建HLS模板，开启**视频加密**，并勾选**私有加密**选项（必须勾选，否则不加密）。具体操作，请参见[转码设置](/cn.zh-CN/控制台指南/配置管理/转码设置.md)。

        ![加密模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6231389061/p183774.png)

        **说明：** 该模板在调用[提交媒体转码作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口时，通过TemplateGroupId参数传递，如此视频点播将按照设置的模板和传递的秘钥信息进行标准加密转码。

    -   不转码模板

        您可在控制台的[转码设置](https://vod.console.aliyun.com/#/settings/transcode/list)页面激活不转码模板，如果不转码模板已经存在则无须再次激活。

        **说明：** 目前点播上传视频默认都会自动触发转码（自动触发暂不支持HLS标准加密）\)，因此对于标准加密为防止自动触发转码，需要先使用不转码模板上传视频（该类模板不会自动触发转码），然后再调用[提交媒体转码作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口发起标准加密转码。

2.  RAM授权

    使用RAM服务给视频点播授权访问业务方秘钥管理服务\(KMS\)的权限，请参见[RAM授权](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunVODDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//vod.console.aliyun.com/%22%2C%20%22Service%22%3A%20%22VOD%22%7D)给视频点播授权。

    ![授权页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0579475061/p183776.png)

3.  上传视频

    使用步骤1中激活的不转码模板用于创建视频上传凭证和地址。控制台具体操作，请参见[媒资上传](/cn.zh-CN/控制台指南/媒资库/媒资上传.md)；服务端接口上传，请参见[获取视频上传地址和凭证](/cn.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)。

4.  接收上传完成回调消息

    接收到[视频上传完成](/cn.zh-CN/开发指南/事件通知/事件列表/视频上传完成.md)回调消息表明文件已经上传到视频点播。

5.  发起标准加密转码

    调用[提交媒体转码作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口传递创建的**加密模板ID**和**标准加密参数**发起标准加密转码。

6.  验证加密转码是否成功

    可通过以下三种方式来逐步判断标准加密是否成功。

    -   如果视频只有m3u8格式输出，那么视频状态为转码失败。
    -   如果视频不只有m3u8格式输出，那么需要到视频点播控制台视频管理详情查看是否存在加密标志的m3u8文件地址输出，如果有一般表明标准加密成功。
    -   如果前面两种方式都不能判断，那么可以将带有加密标志的m3u8文件的地址拷贝出来，使用`curl -v "m3u8文件地址"`，查看获取到的m3u8内容是否存在`URI="<业务方在发起标准加密时传递的解密地址，即[加密配置 EncryptConfig](/cn.zh-CN/服务端API/附录/请求参数说明.md)中的DecryptKeyUri参数值>"`关键信息，有则表明为标准加密且加密成功。
7.  获取视频的播放地址和凭证

    调用[获取视频播放地址](/cn.zh-CN/服务端API/音视频播放/获取视频播放地址.md)和[获取视频播放凭证](/cn.zh-CN/服务端API/音视频播放/获取视频播放凭证.md)接口获取视频的播放地址和凭证。

8.  传入认证信息

    获取m3u8文件地址后，播放器会解析m3u8文件中的EXT-X-KEY标签中的URI并访问，从而获取到带密文秘钥的解密接口URI，此URI为您发起标准加密时传递的[加密配置 EncryptConfig](/cn.zh-CN/服务端API/附录/请求参数说明.md)中的`DecryptKeyUri`参数值。

    若只允许合法用户才可以访问，那么需要播放器在获取解密秘钥时携带您承认的认证信息，认证信息可以通过MtsHlsUriToken参数传入。

    示例：

    -   视频的播放地址为：`https://vod.demo.com/encrypt-stream-hd.m3u8`，则请求时需要携带`MtsHlsUriToken`参数传入。
    -   最终请求地址为：`https://vod.demo.com/encrypt-stream-hd.m3u8?MtsHlsUriToken=<令牌>`
    -   解密地址为：`https://vod.decrypt.com?Ciphertext=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMtOTYyOT`
    -   最终解密请求地址为：`https://vod.decrypt.com?Ciphertext=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMtOTYyOT&MtsHlsUriToken=<颁发的令牌>` 。
9.  播放器在解析到解密地址URI时会自动请求解密接口获取解密秘钥，拿到解密秘钥去解密加密过的ts文件进行播放。


## 解密播放最佳实践

标准加密视频解密播放最佳实践，请参见[HLS标准加密安全播放](/cn.zh-CN/最佳实践/HLS标准加密安全播放.md)。

## 常见问题

-   如何查看Service Key？

    Service Key 可在业务方自己的秘钥管理服务控制台可看到描述为vod的加密主Key。如下图所示：

    ![查看Service Key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9930326061/p178340.png)![查看Service Key详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9930326061/p178341.png)

-   如何使用Service Key生成秘钥？

    调用秘钥管理服务\(KMS\)的[GenerateDataKey](/cn.zh-CN/API参考/密钥/GenerateDataKey.md) 接口，通过Service Key生成AES\_128密钥。

    **说明：** GenerateDataKey接口只需要传KeyId（上述中的Service Key）和KeySpec（固定为：AES\_128）即可，其他参数不用传，否则可能加密失败。

-   如何使用生成的秘钥？

    GenerateDataKey接口会返回两种秘钥：一种是密文秘钥（CipherText），另一种是明文秘钥（PlainText）。用户只需要将密文秘钥传递给视频点播服务即可，具体参数传递请参见[提交媒体转码作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)中的[加密配置 EncryptConfig](/cn.zh-CN/服务端API/附录/请求参数说明.md)参数。

    **说明：**

    -   强烈推荐业务方对生成的密文秘钥和明文秘钥进行缓存。
    -   创建的Service Key不可删除、不可更新，只用于生成加密密钥。
    -   关于密钥相关费用，参见 [密钥管理服务-计费方式-API调用费用](https://help.aliyun.com/document_detail/52608.html?spm=a2c4g.11186623.6.547.1jyvOK)。
-   生成的令牌如何传递到解密接口？

    要将令牌重写到解密接口上，业务方必须使用域名进行加速播放，在请求m3u8地址时需要将生成的令牌通过MtsHlsUriToken参数传递，CDN域名会自动将该参数重写到解密接口上并请求解密接口。

-   域名MtsHlsUriToken参数重写怎么开通？

    目前用户可以在**点播控制台** \> **配置管理** \> **分发加速配置** \> **域名管理** \> **视频相关** \> **加密播放** 实现域名MtsHlsUriToken参数重写功能的自助开通。

    ![开通MtsHlsUriToken](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9930326061/p178342.png)

-   播放器如何解密播放？

    标准加密视频对于支持HLS协议播放的播放器都可以解密播放，播放器解密标准加密的大致步骤如下：

    1.  通过[获取视频播放地址](/cn.zh-CN/服务端API/音视频播放/获取视频播放地址.md)和[获取视频播放凭证](/cn.zh-CN/服务端API/音视频播放/获取视频播放凭证.md)接口获取视频的播放地址和凭证。
    2.  获取m3u8文件地址后，播放器会解析m3u8文件中的EXT-X-KEY标签中的URI并访问，从而获取到带密文秘钥的解密接口URI，此URI为您发起标准加密时传递的[加密配置 EncryptConfig](/cn.zh-CN/服务端API/附录/请求参数说明.md)中的DecryptKeyUri参数值。若只允许合法用户才可以访问，那么需要播放器在获取解密秘钥时携带您承认的认证信息，认证信息可以通过MtsHlsUriToken参数传入。

        例如：

        -   视频的播放地址为：`https://vod.demo.com/encrypt-stream-hd.m3u8` ，则请求时需要携带`MtsHlsUriToken`参数传入。
        -   最终请求地址为：`https://vod.demo.com/encrypt-stream-hd.m3u8?MtsHlsUriToken=令牌` ，播放时播放器会向阿里CDN请求该地址，当解析到m3u8中的解密URI时，阿里CDN会自动将解密URI拼接`MtsHlsUriToken`参数。
        -   解密地址为：`https://vod.decrypt.com?Ciphertext=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMtOTYyOT`。
        -   最终解密请求地址为：`https://vod.decrypt.com?Ciphertext=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMtOTYyOT&MtsHlsUriToken=颁发的令牌`。
    3.  播放器在解析到解密地址URI时会自动请求解密接口获取解密秘钥。
    4.  拿到解密秘钥去解密加密过的ts文件进行播放。
-   如何快速验证加密播放？

    可以通过阿里云播放器诊断平台播放对标准加密的m3u8地址快速验证播放是否正常，拷贝m3u8文件地址（如有MtsHlsUriToken参数一并拷贝）到[阿里云播放器诊断平台](http://player.alicdn.com/detection.html)尝试标准加密的解密播放。

    **说明：** 由于播放需要请求解密接口，所以请先确保解密服务是否正常。

-   其它常见问题
    -   接口提示：

        调用[提交媒体转码作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)提示KeyNotFound相关信息，请先联系点播后台在相应的区域（例如：华北2、华东2）创建Service Key 并用于生成加密密钥。

    -   非加密文件：

        生成的文件未加密，请确认转码模板是否开启**视频加密**并勾选了**私有加密**。

    -   自定义密钥：

        加密的明文密钥必须使用[GenerateDataKey](/cn.zh-CN/API参考/密钥/GenerateDataKey.md)生成，不能使用自定义字符串生成加密密钥，否则加密转码失败。

    -   加密失败：

        标准加密转码失败或没有任何加密文件生成，请确认[GenerateDataKey](/cn.zh-CN/API参考/密钥/GenerateDataKey.md)生成的密钥类型是否为AES\_128密钥，否则加密转码会失败导致不会生成任何加密文件。

    -   解密失败：

        标准加密文件解密播放失败，请确认是解密接口应该将KMS生成的明文密钥再次base64decode之后给播放器解密播放，不然解密播放会失败。

    -   重复生成：

        标准加密转码触发都是由用户主动触发，如果重复生成加密文件，请确认是否重复调用[提交媒体转码作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口。


