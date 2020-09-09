# HLS标准加密

-   [简介](#section_q3j_3um_nu5)
-   [整体架构](#section_pzk_bn2_5xr)
-   [相关概念](#section_3rz_klm_f4c)
-   [准备工作](#section_kvp_5vq_5au)
-   [接入流程](#section_buv_lpp_9uw)
    -   [1.创建转码模板](#section_q1z_9qt_4m3)
        -   [加密模板](#section_zsx_ysa_v3m)
        -   [不转码模板](#section_2pl_qpg_5b4)
    -   [2.RAM授权](#section_pv1_oxq_9h7)
    -   [3.创建Service Key](#section_a6m_ln6_0tz)
        -   [问题: 如何查看Service Key？](#section_vd0_3pc_k8q)
        -   [问题: 如何使用Service Key生成秘钥？](#section_16o_6i6_tn6)
        -   [问题: 如何使用生成的秘钥？](#section_roo_01w_a8v)
    -   [4.上传视频](#section_5b8_wd2_zc4)
    -   [5.接收上传完成回调消息](#section_u3d_29t_vdb)
        -   [问题: 如何设置接收上传完成回调消息？](#section_qw8_m9v_o09)
    -   [6.发起标准加密转码](#section_t2m_0ak_eo6)
        -   [问题：如何验证加密转码是否成功？](#section_u02_d3g_fz7)
    -   [7.标准加密视频播放](#section_gee_l8n_137)
        -   [问题：生成的令牌如何传递到解密接口？](#section_riz_suf_61y)
        -   [问题：播放器如何解密播放？](#section_noq_dxf_b9s)
        -   [问题：如何快速验证加密播放？](#section_ki9_2pq_der)
        -   [解密播放最佳实践](#section_o44_cbz_nn5)
-   [其它常见问题](#section_q4e_9qk_z6u)

## 简介

视频加密是对视频内容保护的一种手段。对视频中的内容进行加密，可有效防止视频泄露和盗链问题。目前，视频加密广泛用于在线教育及财经等领域。

**说明：** 阿里视频云点播目前支持加密方式: 私有加密，HLS标准加密。此文档主要介绍HLS标准加密。

## 整体架构

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/68612/cn_zh/1544414908310/%E6%A0%87%E5%87%86%E5%8A%A0%E5%AF%86%E6%9E%B6%E6%9E%84%E5%9B%BE.png)

## 相关概念

-   密钥管理服务

    [密钥管理服务](https://common-buy.aliyun.com/?spm=a2c4g.11186623.2.3.bhZoMo&commodityCode=kms#/open)（Key Management Service，简称KMS，是一种安全管理服务，主要负责数据密钥的生产、加密、解密等工作。

-   数据密钥

    数据密钥（Data Key，简称DK）也称明文密钥。DK为加密数据使用的明文数据密钥。

-   信封数据密钥

    信封数据密钥（Enveloped Data Key，简称EDK）也称密文密钥。EDK为通过信封加密技术保密后的密文数据密钥。

-   访问控制

    [访问控制](https://www.aliyun.com/product/ram?spm=a2c4g.11186623.2.4.QY4xuc)（Resource Access Management 简称RAM）是阿里云为客户提供的用户身份管理与资源访问控制服务。


## 准备工作

-   搭建密钥管理服务，封装阿里云秘钥管理服务\(KMS\)，生成AES\_128密钥，详细参 [GenerateDataKey](https://help.aliyun.com/document_detail/28948.html?spm=a2c4g.11186623.6.570.Xo2XY0)。
-   搭建令牌颁发服务，生成MtsHlsUriToken。
-   解密密钥：EDK\(密文密钥\)，调用KMS服务的解密接口进行解密，详细参见 [Decrypt](https://help.aliyun.com/document_detail/28950.html?spm=a2c4g.11186623.2.7.Vla9Fq)。
-   解密拿到DK即明文密钥，需要**base64decode**后再返回给播放器。

## 接入流程

标准加密必须按照以下流程接入。

## 1.创建转码模板

HLS标准加密转码需要创建两个转码模板。

## 加密模板

在视频点播控制台[配置管理--\>媒体处理配置--\>转码模板组](https://vod.console.aliyun.com/?spm=5176.2020520001.aliyun_sidebar.aliyun_sidebar_vod.5eb84bd3S6WzrN&accounttraceid=3c95d5a5-cfbb-4f25-97d6-a1ee0cd4d8e3#/settings/transcode/list)，创建HLS模板并勾选HLS加密选项\(**必须勾选，否则不加密**\)，详细设置请参考[转码设置](/cn.zh-CN/控制台指南/全局设置/转码设置.md)，该模板在调用[提交媒体转码作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口时通过TemplateGroupId参数传递，如此视频点播将按照设置的模板和传递的秘钥信息进行标准加密转码。 如下图所示：

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0617097951/p140111.png)

## 不转码模板

不转码即分发模板，用户可在点播控制台 [配置管理--\>媒体处理配置--\>转码设置](https://vod.console.aliyun.com/?spm=5176.2020520001.aliyun_sidebar.aliyun_sidebar_vod.5eb84bd3S6WzrN&accounttraceid=3c95d5a5-cfbb-4f25-97d6-a1ee0cd4d8e3#/settings/transcode/list) 激活，该模板是用来上传视频用。

**说明：** 目前点播上传视频默认都会自动触发转码\(自动触发暂不支持HLS标准加密\)，因此对于标准加密为防止自动触发转码，需要先使用不转码模板上传视频\(该类模板不会自动触发转码\)，然后再调用[提交媒体处理作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口发起标准加密转码。

如下图所示： ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/68612/cn_zh/1544415043992/%E6%BF%80%E6%B4%BB%E4%B8%8D%E8%BD%AC%E7%A0%81.png)

**说明：** 如果不转码模板已经存在则无须再次激活。

## 2.RAM授权

使用RAM服务给视频点播授权访问业务方秘钥管理服务\(KMS\)的权限，请点击 [RAM授权](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunVODDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//vod.console.aliyun.com/%22%2C%20%22Service%22%3A%20%22VOD%22%7D) 给视频点播授权，如下图所示： ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/68612/cn_zh/1544415123472/%E6%A0%87%E5%87%86%E5%8A%A0%E5%AF%86RAM%E6%8E%88%E6%9D%83.png)

## 3.创建Service Key

Service Key为秘钥管理服务的一种加密主Key，接入标准加密的秘钥**必须**要使用该Service Key生成，由于视频点播控制台暂不支持用户自主创建Service Key，请提工单申请创建Service Key。

**说明：**

-   申请Service Key之前，需要先[开通KMS服务](https://common-buy.aliyun.com/?spm=a2c4g.11186623.2.3.bhZoMo&commodityCode=kms#/open)。
-   Service Key与视频存储的源站区域必须一致，例如：视频存储在华东2，则Service Key必须是华东2

## 问题: 如何查看Service Key？

Service Key 可在业务方自己的秘钥管理服务控制台可看到描述为 **vod** 的加密主Key。如下图所示：

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0617097951/p140115.png)

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0617097951/p140116.png)

## 问题: 如何使用Service Key生成秘钥？

调用秘钥管理服务\(KMS\)的[GenerateDataKey](https://help.aliyun.com/document_detail/28948.html) 接口，通过Service Key生成**AES\_128**密钥，代码示例详细请参考[提交媒体处理作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)标准加密Demo。

**说明：** GenerateDataKey接口只需要传：KeyId\(上述中的**Service Key**\)和KeySpec\(固定为：**AES\_128**\)即可，其他参数不用传，否则可能加密失败。

## 问题: 如何使用生成的秘钥？

GenerateDataKey接口会返回两种秘钥：一种是密文秘钥\(CipherText\)，另一种是明文秘钥\(PlainText\)。用户只需要将密文秘钥传递给视频点播服务即可，具体参数传递详细请参考[提交媒体处理作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)中的 [EncryptConfig](https://help.aliyun.com/document_detail/86952.html?spm=a2c4g.11186623.2.18.719e133fzpKwh2#EncryptConfig) 参数，代码示例详细请参考 [提交媒体处理作业](/cn.zh-CN/服务端SDK/Java SDK/媒体处理.md)标准加密Demo。

**说明：**

-   **强烈推荐**业务方对生成的密文秘钥和明文秘钥进行缓存。
-   创建的Service Key不可删除、不可更新，只用于生成加密密钥。
-   关于密钥相关费用，参见 [密钥管理服务-计费方式-API调用费用](https://help.aliyun.com/document_detail/52608.html?spm=a2c4g.11186623.6.547.1jyvOK)。

## 4.上传视频

使用上述Step1中激活的**不转码即分发**模板用于创建视频上传凭证和地址，视频点播控制台上传详细请参考[控制台上传](/cn.zh-CN/控制台指南/媒资库/媒资上传.md)，服务端接口上传详细请参考[服务端上传](/cn.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)。

## 5.接收上传完成回调消息

接收到上传完成回调消息表明文件已经上传到视频点播。

## 问题: 如何设置接收上传完成回调消息？

视频点播控制台设置上传消息回调，接收到上传完成回调消息后可通过[提交媒体处理作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口发起标准加密转码，上传完成回调接收设置详细请参考[回调设置](/cn.zh-CN/控制台指南/全局设置/回调设置.md)。

## 6.发起标准加密转码

调用媒体处理作业接口传递Step1中创建的加密模板ID和标准加密参数发起标准加密转码，参数详情请参考[提交媒体处理作业](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md) 文档。

## 问题：如何验证加密转码是否成功？

可通过以下三种方式来逐步判断标准加密是否成功。

-   如果视频只有m3u8格式输出，那么视频状态为**审核中**或者**正常**状态，则一般表明视频标准加密成功，否则视频状态会为**转码失败**。
-   如果视频不只有m3u8格式输出，那么需要到视频点播控制台视频管理详情查看是否存在加密标志的m3u8文件地址输出，如果有一般表明标准加密成功。
-   如果前面两种方式都不能判断，那么可以将带有加密标志的m3u8文件的地址拷贝出来，使用curl -v "m3u8文件地址",查看获取到的m3u8内容是否存在URI="<业务方在发起标准加密时传递的解密地址，即EncryptConfig中的DecryptKeyUri参数值\>"关键信息，有则表明为标准加密且加密成功，参数详细请参考[EncryptConfig](/cn.zh-CN/服务端API/附录/请求参数说明.md),例如URI="http://decrypt.demo.com?CipherText=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMt"

## 7.标准加密视频播放

标准加密视频的播放需要业务方先依据秘钥管理服务解密接口搭建解密服务，详细请参考[Decrypt](https://help.aliyun.com/document_detail/28950.html?spm=a2c4g.11186623.6.573.7a647a0fDiJNgg)。如果业务方需要对解密接口进行安全验证，则需要提供令牌生成服务，生成的令牌能够在解密服务中被解析验证。

**说明：** 解密接口返回的数据为[GenerateDataKey](https://help.aliyun.com/document_detail/28948.html) 生成的两种秘钥中的明文秘钥\(PlainText\)经过base64decode之后的数据。

## 问题：生成的令牌如何传递到解密接口？

要将令牌重写到解密接口上，业务方必须使用域名进行加速播放，在请求m3u8地址时需要将生成的令牌通过MtsHlsUriToken参数传递，CDN域名会自动将该参数重写到解密接口上并请求解密接口。

## 问题：域名MtsHlsUriToken参数重写怎么开通？

目前用户可以在**点播控制台--\>配置管理--\>分发加速配置--\>域名管理--\>视频相关--\>加密播放** 实现域名MtsHlsUriToken参数重写功能的自助开通。

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6930469951/p164111.png)

## 问题：播放器如何解密播放？

标准加密视频对于支持HLS协议播放的播放器都可以解密播放，播放器解密标准加密的大致步骤如下：

-   通过[获取视频播放地址](/cn.zh-CN/服务端API/音视频播放/获取视频播放地址.md)和[获取视频播放凭证](/cn.zh-CN/服务端API/音视频播放/获取视频播放凭证.md)接口获取视频的播放地址和凭证。
-   获取m3u8文件地址后，播放器会解析m3u8文件中的EXT-X-KEY标签中的URI并访问，从而获取到带密文秘钥的解密接口URI，此URI为您发起标准加密时传递的 [EncryptConfig](https://help.aliyun.com/document_detail/86952.html?spm=a2c4g.11186623.2.18.743f133fhowUI8#EncryptConfig)中的**DecryptKeyUri**参数值。若只允许合法用户才可以访问，那么需要播放器在获取解密秘钥时携带您承认的认证信息，认证信息可以通过MtsHlsUriToken参数传入。

    **说明：** 例如：

    -   视频的播放地址为：https://vod.demo.com/encrypt-stream-hd.m3u8 ，则请求时需要携带MtsHlsUriToken参数传入。
    -   最终请求地址为：https://vod.demo.com/encrypt-stream-hd.m3u8?MtsHlsUriToken=令牌 ，播放时播放器会向阿里CDN请求该地址，当解析到m3u8中的解密URI时，阿里CDN会自动将解密URI拼接MtsHlsUriToken参数。
    -   解密地址为：https://vod.decrypt.com?Ciphertext=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMtOTYyOT
    -   最终解密请求地址为：https://vod.decrypt.com?Ciphertext=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMtOTYyOT&MtsHlsUriToken=颁发的令牌 。
-   播放器在解析到解密地址URI时会自动请求解密接口获取解密秘钥。
-   拿到解密秘钥去解密加密过的ts文件进行播放。

## 问题：如何快速验证加密播放？

可以通过阿里云播放器诊断平台播放对标准加密的m3u8地址快速验证播放是否正常，拷贝m3u8文件地址\(如有MtsHlsUriToken参数一并拷贝\)到 [阿里云播放器诊断平台](http://player.alicdn.com/detection.html) 尝试标准加密的解密播放。

**说明：** 由于播放需要请求解密接口，所以请先确保解密服务是否正常。

## 解密播放最佳实践

标准加密视频解密播放最佳实践详细请参考 [标准加密安全播放](https://help.aliyun.com/document_detail/124805.html)。

## 其它常见问题

-   接口提示:

    [SubmitTranscodeJobs](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)调用提示KeyNotFound相关信息，请先联系点播后台在相应的区域\(例如：华北2、华东2\)创建Service Key 并用于生成加密密钥。

-   非加密文件:

    生成的文件未加密，请确认转码模板是否勾选了HLS加密\(标准加密、私有加密必须勾选\),导致输出文件都是未加密。

-   自定义密钥:

    加密的明文密钥必须使用 [GenerateDataKey](https://help.aliyun.com/document_detail/28948.html) 生成，不能使用自定义字符串生成加密密钥，否则加密转码失败。

-   加密失败:

    标准加密转码失败或没有任何加密文件生成，请确认 [GenerateDataKey](https://help.aliyun.com/document_detail/28948.html) 生成的密钥类型是否为AES\_128密钥，否则加密转码会失败导致不会生成任何加密文件。

-   解密失败:

    标准加密文件解密播放失败，请确认是解密接口应该将KMS生成的明文密钥再次base64decode之后给播放器解密播放，不然解密播放会失败。

-   重复生成:

    标准加密转码触发都是由用户主动触发，如果重复生成加密文件，请确认是否重复调用[SubmitTranscodeJobs](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)接口。


