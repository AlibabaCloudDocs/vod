# 使用STS方式上传

通过阅读本文，您可以了解使用STS方式进行上传的基本流程。

## 简介

阿里云临时安全令牌STS（Security Token Service）是阿里云通用的鉴权方式。通过STS方式上传，上传SDK内部会封装所有上传的细节，您只需要关注STS的获取、过期刷新以及文件上传完成的回调即可。更多信息，请参见[什么是STS](/cn.zh-CN/API参考/API 参考（STS）/什么是STS.md)。

## 基本流程

1.  在控制台配置STS点播权限并向业务服务发送请求STS，更多信息，请参见[创建角色并进行STS临时授权](/cn.zh-CN/开发指南/账号和授权/创建角色并进行STS临时授权.md)。
2.  业务服务APPServer向阿里云服务请求STS。
3.  业务服务APPServer从STS服务获取STS。相关示例代码请参见[创建角色并进行STS临时授权](/cn.zh-CN/开发指南/账号和授权/创建角色并进行STS临时授权.md)。
4.  业务服务APPServer返回STS凭证给客户端。
5.  客户端添加本地文件并设置STS，开始上传。

![sts_upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7475775061/p183822.png)

**说明：** 业务服务APPServer向阿里云服务发送请求，从阿里云RAM或STS服务获取STS，为了提高获取效率和避免RAM或STS服务对请求的流控限制，需要在业务服务APPServer中对STS进行缓存。

## 设置STS

STS在初始化上传实例的时候进行设置，具体的初始化代码如下所示：

-   iOS示例代码

    ```
    [self.uploader
         init:`STS Key Id`
         accessKeySecret:`STS Key Secret`
         secretToken:STS Secret Token`
         expireTime:`STS Expire Time`
         listener:listener
    ];                 
    ```

-   Android示例代码

    ```
    VODUploadClient uploader = new VODUploadClientImpl(getApplicationContext());
    uploader.init(accessKeyId,
                  accessKeySecret,
                  secretToken,
                  expireTime,
                  callback);
    ```

-   H5 JS示例代码

    ```
    var uploader = new AliyunUpload.Vod({
        partSize: 1048576,//分片大小默认1 MB，不能小于100 KB
           parallel: 5,//并行上传分片个数，默认5
        retryCount: 3,//网络原因失败时，重新上传次数，默认为3
        retryDuration: 2,//网络原因失败时，重新上传间隔时间，默认为2秒
        'onUploadstarted': function (uploadInfo) {
              uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret,secretToken);
        }
        …… //其他回调
    });
    ```


## 相关参考

如果您想了解上传文件列表管理、上传成功回调处理，凭证过期回调处理等，可以阅读相关平台的上传SDK文档。

-   [Android端文件上传](/cn.zh-CN/上传SDK/客户端上传/Android上传SDK/文件上传.md)
-   [iOS端文件上传](/cn.zh-CN/上传SDK/客户端上传/iOS上传SDK/文件上传.md)
-   [使用JavaScript上传SDK](/cn.zh-CN/上传SDK/客户端上传/使用JavaScript上传SDK.md)

