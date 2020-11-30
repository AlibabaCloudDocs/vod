# C/C++上传SDK

通过视频点播上传SDK服务，您可以实现方便、快速的上传媒体文件。本文通过示例为您详细介绍C/C++上传SDK服务。

## 功能介绍

使用上传SDK服务可实现的主要功能如下：

-   上传各种媒体文件到视频点播：音视频、图片、辅助媒资（如水印、字幕文件）。
-   上传本地媒体文件到视频点播：默认使用分片上传，最大支持48.8 TB的单个文件，暂不支持断点续传。
-   上传网络媒体文件到视频点播：最大支持48.8 TB的单个文件，需先下载到本地临时目录再上传，暂不支持断点续传。
-   上传m3u8视频：提供解析m3u8索引文件得到分片地址列表的接口，也可以自行指定分片文件地址。

除了上述主要功能外，上传SDK服务还可实现以下功能：

-   上传进度条，支持默认进度回调和自定义进度回调。
-   可指定上传脚本部署的ECS区域，如果和视频点播存储区域相同，则自动使用内网上传，上传更快且更省公网流量。
-   可指定视频点播中心（默认为上海）和存储区域，便于海外上传。
-   支持上传时设置元数据（如标题），以及StorageLocation、UserData、转码模板等。

上传SDK服务支持的文件格式请参见[媒体上传文件格式](/cn.zh-CN/开发指南/媒体上传/概述.md)。

## 环境要求

视频点播C/C++上传SDK与C/C++服务端SDK统一，具体环境准备、SDK安装及初始化等请参见[C/C++SDK使用指南](/cn.zh-CN/服务端SDK/C/C++ SDK/安装.md)。

## 安装SDK

1.  下载C/C++上传SDK及示例代码VodSDK-C\_1.0.0.gz，请参见[服务端上传SDK](/cn.zh-CN/SDK下载/SDK下载.md)。

    **说明：** 此处以SDK1.0.0版本举例说明。其他版本请根据实际情况操作。

2.  按照C/C++服务端安装方式进行安装。具体操作，请参见[安装](/cn.zh-CN/服务端SDK/C/C++ SDK/安装.md)。


## 更新SDK

若发现新的接口或已有接口新的功能在当前SDK没有，请下载最新的C/C++上传SDK覆盖到本地SDK文件。更多信息，请参见[服务端上传SDK](/cn.zh-CN/SDK下载/SDK下载.md)。

**说明：** 您可以打开aliyun-c-sdk-vod目录下的ChangeLog.txt文件查看当前SDK的版本号和发布日期。

## SDK目录说明

-   /VodSDK-C\_1.0.0.gz解压目录/VodSDK-C\_1.0.0/aliyun-c-sdk-vod/src/upload.h
    -   CreateUploadVideoRequest：上传视频的请求类，字段请参见[获取视频上传地址和凭证](/cn.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)。
    -   CreateUploadImageRequest：上传图片的请求类，字段请参见[获取图片上传地址和凭证](/cn.zh-CN/服务端API/媒体上传/获取图片上传地址和凭证.md)。
    -   CreateUploadAttachedMediaRequest：上传辅助媒资的请求类，字段请参见[获取辅助媒资上传地址和凭证](/cn.zh-CN/服务端API/媒体上传/获取辅助媒资上传地址和凭证.md)。
    -   UploadOptions：上传参数结构体，包含如下参数：
        -   void \(\*uploadProgressCallback\) \(int64\_t, int64\_t\)：用于实现自定义上传进度回调，如果不设置则使用默认，设置为NULL则不进行回调。
        -   ecsRegionId：设置上传脚本部署的ECS区域（如果有），如果与视频点播存储同一区域会自动启用内网上传。
        -   multipartUploadLimit：分片上传阈值，单位字节，默认为10 MB（只对视频上传有效）。
        -   multipartUploadOnceSize：分片大小，单位字节，默认为10 MB（只对视频上传有效）。
        -   tmpDir：本地临时存储地址，只对网络上传方式生效。
    -   uploadLocalVideo：上传本地视频。
    -   uploadWebVideo：上传网络视频。
    -   uploadLocalImage：上传本地图片。
    -   uploadWebImage：上传网络图片。
    -   uploadLocalAttachedMedia：上传本地辅助媒资文件。
    -   uploadWebAttachedMedia：上传网络辅助媒资文件。
    -   uploadLocalM3u8：上传本地m3u8视频。
    -   uploadWebM3u8：上传网络m3u8视频。
-   /VodSDK-C\_1.0.0.gz解压目录/VodSDK-C\_1.0.0/aliyun-c-sdk-vod/samples目录
    -   uploadVideo.cpp：上传视频的示例代码。
    -   uploadImage.cpp：上传图片的示例代码。
    -   uploadAttachedMedia.cpp：上传辅助媒资的示例代码。

## 使用示例

以上传本地视频和网络视频为例，如下所示：

```
void testCallback(int64_t consumed_bytes, int64_t total_bytes)
{
    printf("total :%ld, %ld\n", consumed_bytes, total_bytes);
}
//测试上传本地视频
VodApiResponse testUploadLocalVideo(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testLocal.mp4";
    request.title = "testUploadLocalVideo";
    request.cateId = "1";
    request.coverURL = "http://xxxx.jpg";
    request.tags = "test1,test2";
    request.templateGroupId = "6ae347b0140181ad371d197ebe28****";
    requests.torageLocation. = "outin-xx.oss-cn-beijing.aliyuncs.com";
    Json::Value userData;
    Json::Value callbackUrl;
    callbackUrl["CallbackURL"] = "https://demo.sample.com/ProcessMessageCallback";
    userData["MessageCallback"] = callbackUrl;
    Json::Value extend;
    extend["localId"] = "xxx";
    extend["test"] = "www";
    userData["Extend"] = extend;
    request.userData = userData.toStyledString();
    UploadOptions uploadOptions;
    //设置上传脚本部署的ECS区域（如果有），如与视频点播存储同一区域会自动启用内网上传
    //uploadOptions.ecsRegionId = "cn-shanghai";
    //设置自定义回调函数，否则设置为默认，设置为NULL不回调
    //uploadOptions.uploadProgressCallback = testCallback;
    //uploadOptions.multipartUploadLimit = 20*1024*1024;//设置分片上传阈值
    //uploadOptions.multipartUploadOnceSize = 10*1024*1024;//设置分片上传分片大小
    VodApiResponse result = uploadLocalVideo(authInfo, request, "./test.mp4", uploadOptions);
    return result;
}
//测试上传网络视频
VodApiResponse testUploadWebVideo(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testWeb.mp4";
    request.title = "testUploadWebVideo";
    UploadOptions uploadOptions;
    //设置上传脚本部署的ECS区域（如果有），如与视频点播存储同一区域会自动启用内网上传
    //uploadOptions.ecsRegionId = "cn-shanghai";
    //设置自定义回调函数，否则设置为默认，设置为NULL不回调
    //uploadOptions.uploadProgressCallback = testCallback;
    //uploadOptions.multipartUploadLimit = 20*1024*1024;//设置分片上传阈值
    //uploadOptions.multipartUploadOnceSize = 10*1024*1024;//设置分片上传分片大小
    //设置下载临时目录，默认为/tmp/
    //uploadOptions.tmpDir = "/tmp/";
    VodApiResponse result = uploadWebVideo(authInfo, request, "<Your Download Url>", uploadOptions);
    return result;
}
//测试上传本地m3u8视频
VodApiResponse testUploadLocalM3u8(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testLocal.m3u8";
    request.title = "testUploadLocalM3u8";
    list<string> tsList;
    //注意：如果不添加则会自动解析
    //tsList.push_back("/tmp/1.ts");
    UploadOptions uploadOptions;
    VodApiResponse result = uploadLocalM3u8(authInfo, request, "./test.m3u8", tsList, uploadOptions);
    return result;
}
//测试上传网络m3u8视频
VodApiResponse testUploadWebM3u8(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testWeb.m3u8";
    request.title = "testUploadWebM3u8";
    list<string> tsList;
    //注意：如果不添加则会自动解析
    //tsList.push_back("<Ts1 Download Url>");
    //tsList.push_back("<Ts2 Download Url>");
    UploadOptions uploadOptions;
    VodApiResponse result = uploadWebM3u8(authInfo, request, "<Your M3u8 Download Url>", tsList, uploadOptions);
    return result;
}
####  调用测试代码   ####
VodCredential initVodClient(std::string accessKeyId, std::string accessKeySecret) {
    VodCredential authInfo;
    authInfo.accessKeyId = accessKeyId;
    authInfo.accessKeySecret = accessKeySecret;
    authInfo.regionId = "cn-shanghai";
    return authInfo;
}
int main(int argc, char * argv[]) {
    VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    VodApiResponse response;
    response = testUploadLocalVideo(authInfo);
    //response = testUploadWebVideo(authInfo);
    //response = testUploadLocalM3u8(authInfo);
    //response = testUploadWebM3u8(authInfo);
    printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
}
```

更多示例代码请参见samples目录中其它示例文件。

