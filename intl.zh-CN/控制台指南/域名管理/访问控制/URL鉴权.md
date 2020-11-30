# URL鉴权

因Referer防盗链方式无法彻底保护站点资源，建议您配置URL鉴权来保护站点的资源不被非法站点下载盗用。

## 实现原理

URL鉴权功能通过阿里云CDN加速节点与客户资源站点配合，形成了更为安全可靠的源站资源防盗方法。

1.  CDN客户站点提供加密URL，URL中包含权限验证信息。
2.  用户使用加密后的URL向加速节点发起请求。
3.  加速节点对加密URL中的权限信息进行验证，判断请求的合法性。正常响应合法请求，拒绝非法请求。

**说明：** 您的请求URL经过CDN鉴权后，URL中的特殊字符，例如：`=`、``等会被转义。

1.  登录[视频点播控制台](https://vod.console.aliyun.com/)。

2.  在点播控制台左侧导航栏选择**配置管理**。

3.  单击**分发加速配置** \> **域名管理**，进入域名管理页面。

4.  选择您要配置的域名，单击**配置**。

    ![配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1277415061/p180549.png)

5.  单击**访问控制**。

6.  单击**URL鉴权**页签，单击**修改配置**。

    ![修改配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3961325061/p181688.png)

7.  开启**URL鉴权**，配置URL鉴权信息，单击**确定**完成。

    ![修改配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3961325061/p181693.png)

    配置项和说明如下表所示。

    |配项置|说明|
    |---|--|
    |**鉴权类型**|视频点播分发加速仅支持鉴权A，来实现对源站资源的有效保护。

**说明：** URL鉴权错误，都会返回403报错，请重新计算。

    -   MD5计算类错误

例如：`X-Tengine-Error:denied by req auth: invalid md5hash=de7bfdc915ced05e17380a149bd760be`

    -   时间类报错

例如：`X-Tengine-Error:denied by req auth: expired timestamp=1439469547` |
    |**主KEY**|输入自定义的鉴权方式对应的主用密码。|
    |**备KEY**|输入自定义的鉴权方式对应的备用密码。|
    |**默认有效时长**|输入鉴权方式的默认有效时长，单位：分钟。|
    |**支持试看**|试看指用户在观看视频或者音频等内容时，只能观看指定时间（如前五分钟）的内容，通常用于会员等付费业务场景。详情请参见[t1959346.md\#](/intl.zh-CN/最佳实践/点播试看.md)。|

8.  生成鉴权URL。

    在**生成鉴权URL**区域，配置**原始URL**和鉴权信息。

    ![生成鉴权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3961325061/p181697.png)

    配置项和说明如下表所示。

    |参数|说明|
    |--|--|
    |**原始URL**|您可以输入完整的原始URL地址，例如：`https://www.aliyun.com`。|
    |**鉴权类型**|默认为鉴权A方式。|
    |**鉴权KEY**|您可以根据所需，设置鉴权密码。**鉴权KEY**是**鉴权URL设置**中配置的**主KEY**或**备KEY**。|
    |**有效时间**|您可以根据所需，设置URL鉴权的有效时长。单位为：秒，例如：1800。**说明：** CDN鉴权的有效时间默认为30分钟，如果您想使链接生成的有效时间小于30分钟，需要将**有效时间**设置为负数。例如，您想设置链接有效时间为10s，则需要设置**有效时间**为-1790s。 |

9.  单击**开始生成**。

    ![生成](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3961325061/p181708.png)


