# 凭证方式与STS方式对比

上传凭证、播放凭证和STS方式都能解决上传和播放过程中的授权和安全问题，防止被恶意上传和播放。

-   上传凭证

    上传凭证是点播服务下发的，上传媒体文件到点播存储的授权凭证，具有时效性、限制访问对象和次数等特征。更多详情，请参见[上传地址和凭证](/intl.zh-CN/开发指南/媒体上传/上传地址和凭证.md)。

-   播放凭证

    播放凭证是点播服务下发的，授权播放器获取视频播放地址的授权凭证，也具有时效性、限制访问对象和次数等特征。更多详情，请参见[获取播放地址播放](/intl.zh-CN/开发指南/音视频播放/获取播放地址播放.md)。

-   STS方式

    STS（Security Token Service）是为阿里云账号（或RAM用户）提供短期访问权限管理的云服务。通过STS，可以为第三方访问颁发一个自定义时效和访问权限的访问凭证。第三方用户可以使用STS短期访问凭证直接调用阿里云服务API，或登录阿里云管理控制台操作被授权访问的资源。更多详情，请参见[创建角色并进行STS临时授权](/intl.zh-CN/开发指南/账号和授权/创建角色并进行STS临时授权.md)。


## 凭证的优势

上传凭证、播放凭证是视频点播推荐使用的上传、播放授权方式，相比STS方式优势如下：

|对比项|凭证方式|STS方式|
|---|----|-----|
|易用性|使用简单，准备好账号AccessKey授予点播权限即可。|配置较为复杂，角色和授权策略的配置较为繁琐。|
|安全性|上传凭证、播放凭证的授权粒度为单视频维度，且仅能使用一次。|权限粒度较粗，在点播上是API维度，意味着端上拿到STS授权可无限次上传N个视频或播放该账号下的所有视频。|
|灵活性|上传凭证、播放凭证支持更多配置参数，比如上传时指定消息回调地址、播放时指定域名等。更多信息，请参见[获取视频上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)和[获取视频播放凭证](/intl.zh-CN/服务端API/音视频播放/获取视频播放凭证.md)。|需要等待客户端SDK发布新版迭代，新增功能会有所滞后。|
|访问容量|默认分配较大余量，可弹性伸缩，支撑任意用户的海量个性化授权请求。|作为中心化服务，为所有产品提供授权，有严格的流控，不适合于高并发场景。|

