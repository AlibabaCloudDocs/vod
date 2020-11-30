# URL鉴权

URL鉴权功能旨在保护用户上传到视频点播的内容资源不被非法站点下载盗用，可通过控制台配置。本文为您简要介绍了URL鉴权的原理和鉴权方法。

## 背景

一般情况下，可以通过配置访问Referer黑名单和白名单来实现对访客身份的识别和过滤，保护站点资源。但由于Referer内容可以伪造，采用URL鉴权方式更为安全有效。

## 原理

URL鉴权功能通过阿里云CDN加速节点与客户资源站点配合，形成了更为安全可靠的源站资源防盗方法。

1.  由CDN客户站点提供给用户加密 URL（包含权限验证信息）。
2.  用户使用加密后的 URL 向加速节点发起请求。
3.  加速节点对加密 URL 中的权限信息进行验证以判断请求的合法性，对合法请求给予正常响应，并拒绝非法请求，从而有效保护CDN客户站点资源。

## 配置方法

您可以在控制台的[域名管理](https://vod.console.aliyun.com/#/domain/list)页面配置URL鉴权，具体操作，请参见[URL鉴权](/cn.zh-CN/控制台指南/域名管理/访问控制/URL鉴权.md)。

-   开启URL鉴权后，阿里云VOD的播放器SDK，以及获取播放地址的API/SDK都会自动生成带时效的播放URL。如您需要生成鉴权的动态URL，请使用下述鉴权方法。

    **说明：** 开启URL鉴权后，视频、音频、封面、截图等地址都会进行鉴权

-   主Key和备Key拥有同样的效力，备Key主要用于平滑更换。若主KEY执行更换，所有使用主KEY生成的播放地址会立即失效。备KEY作为主KEY更换时，使用主KEY的播放地址不会马上中断，备KEY可以继续替代主KEY提供服务。
-   设置目标域名下URL地址的全局默认有效时长后，可对单个URL定制有效时长。

    **说明：** 此时CDN会在timestamp后追加设置的默认有效时长


## 鉴权方法

-   鉴权URL构成

    鉴权URL由播放文件地址+验证串构成。示例如下：

    ```
    http://DomainName/Filename?auth_key=timestamp-rand-uid-md5hash
    ```

    验证串是根据鉴权key+过期时间通过md5算法计算得出，且具有时效性。timestamp、rand、uid、md5hash的字段描述参见下文。

-   鉴权字段描述

    |字段|描述|
    |--|--|
    |timestamp|URL失效时间。为Unix时间戳，1970年1月1日以来的秒数。URL地址会在指定的timestamp之后的`默认有效时长`后失效。在超过timestamp字段指定的时间之后的`默认有效时长`后，URL鉴权失效，此时CDN返回HTTP 403。

示例：指定timestamp为1597474800（即2020-08-15 15:00:00），同时在控制台设置的`默认有效时长`为30分钟，则链接真正失效时间是2020-08-15 15:30:00。 |
    |rand|随机数。一般为0，如要确保每次生成的URL不同则可使用UUID等做随机数。|
    |uid|附加参数。一般为0。|
    |md5hash|通过md5算法计算出的验证串。数字和小写英文字母混合0-9、a-z，固定长度32。    -   URI：请求文件的相对地址，不包含参数，如 /Filename。
    -   PrivateKey：控制台配置的主Key或备Key，二者皆可。
    -   md5sum：表示计算MD5值，请使用开发语言对应的函数。
示例：

    ```
sstring = "URI-timestamp-rand-uid-PrivateKey" 
md5hash = md5sum(sstring)
    ``` |

-   示例说明

    假设情况：

    1.  请求文件地址。示例如下：

        ```
        http://192.168.0.0/16/video/standard/1K.html
        ```

    2.  鉴权Key设置为：aliyuncdnexp1234（控制台设置的主Key或备Key）。
    3.  鉴权URL指定失效时间为：2015年10月10日00:00:00。
    4.  rand和uid字段都设置为0。
    则：

    1.  计算出来的鉴权URL指定失效时间的Unix时间戳为1444435200
    2.  用于计算md5hash签名的字符串。示例如下：

        ```
        /video/standard/1K.html-1444435200-0-0-aliyuncdnexp1234"
        ```

    3.  计算`md5hash`值。示例如下：

        ```
        md5hash = md5sum("/video/standard/1K.html-1444435200-0-0-aliyuncdnexp1234") = 80cd3862d699b7118eed99103f2a3a4f
        ```

    4.  请求时URL。示例如下：

        ```
        http://cdn.example.com/video/standard/1K.html?auth_key=1444435200-0-0-80cd3862d699b7118eed99103f2a3a4f
        ```

        **说明：** auth\_key 即为鉴权URL所带的鉴权信息。


