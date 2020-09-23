# Java上传SDK

-   [1. SDK简介](#section_nnb_iol_bep)
    -   [概述](#section_kww_73q_hzv)
    -   [功能介绍](#section_51l_oew_ody)
        -   [主要功能](#section_v7e_21l_2kt)
        -   [其他功能](#section_p1q_rm7_cyp)
-   [2. SDK安装](#section_so7_gx4_pyf)
    -   [环境要求](#section_lru_alb_d7o)
    -   [安装SDK](#section_iad_073_j2w)
-   [3. 示例代码](#section_t8e_ycg_rq9)
    -   [上传SDK示例](#section_y2u_znr_hv2)
    -   [上传进度条示例](#section_zmk_tgn_97k)

## 1. SDK简介

## 概述

点播服务\(VoD\)基于对象存储\(OSS\)构建，开通VoD时会自动分配独立的系统Bucket，以存储各种媒体文件，包括上传的视频、音频、图片等源文件，以及转码后的输出文件、截图和封面等等，并作为点播加速域名的源站。使用VoD上传SDK能方便、快速实现媒体文件的上传。支持的文件格式参考 [媒体上传文件支持](/cn.zh-CN/开发指南/媒体上传/概述.md)。

## 功能介绍

使用此上传SDK可实现以下功能：

## 主要功能

-   上传本地音视频到点播，默认使用分片上传，最大支持48.8TB的单个文件；支持断点续传。
-   上传网络音视频到点播，指定URL地址，即可自动下载并上传到点播，最大支持48.8TB的单个文件。
-   上传本地图片到点播，指定本地文件路径，即可自动上传到点播。
-   上传网络图片到点播，指定URL地址，即可自动下载并上传到点播。
-   上传本地m3u8音视频（包括所有分片文件）到点播，需指定本地m3u8索引文件和分片文件目录。
-   上传网络m3u8音视频（包括所有分片文件）到点播，需指定网络m3u8索引文件和分片文件的URL地址。
-   上传本地辅助媒资文件到点播，指定本地文件路径，即可自动上传到点播。
-   上传网络辅助媒资文件到点播，指定URL地址，即可自动下载并上传到点播。

## 其他功能

-   上传进度条功能，支持SDK默认进度回调和自定义进度回调，m3u8文件上传暂不支持。
-   可指定上传脚本部署的ECS区域，如果与点播存储（OSS）区域相同，则自动使用内网上传文件至存储，上传更快且更省公网流量（由于点播API只提供外网域名访问，因此部署上传脚本的ECS服务器必须具有访问外网的权限）。
-   可指定点播中心（默认为上海）和存储区域，便于海外上传。
-   支持上传时设置元数据\(标题等\)，以及StorageLocation、UserData、转码模板、点播工作流等。
-   支持STS方式接入，需实现传递和刷新STS的接口，当文件上传时间超过STS过期时间时，SDK内部定期获取新的STS信息，进行后续上传操作。

## 2. SDK安装

## 环境要求

Java版本1.8.0

## 安装SDK

以 1.4.12 版本为例，步骤如下:

1.下载Java示例代码VODUploadDemo-java-1.4.13.zip开发包\(包含示例代码和所需jar包）, 见[服务端上传SDK](/cn.zh-CN/SDK下载/SDK下载.md) ;

2.将解压后lib目录下的所有jar文件拷贝至您的项目中;

3.SDK依赖的jar包版本说明

注意：以下列举出部分依赖jar包的版本，您可直接在您的项目中添加maven依赖，也可以将VODUploadDemo-java-1.4.13.zip包中的所有jar包引入您的项目中使用。其中，aliyun-java-vod-upload-1.4.13.jar 还未正式开源，请您直接引入jar包至您的项目中使用。

```
   <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>4.5.1</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun.oss</groupId>
        <artifactId>aliyun-sdk-oss</artifactId>
        <version>3.10.2</version>
    </dependency>
     <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-vod</artifactId>
        <version>2.15.11</version>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.28</version>
    </dependency>
    <dependency>
        <groupId>org.json</groupId>
        <artifactId>json</artifactId>
        <version>20170516</version>
    </dependency>
    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.8.2</version>
    </dependency>
			
```

4.使用IDE开发时引用jar包的方法，以Eclipse和IntelliJ IDEA为例说明如下：

> 4.1 在Eclipse中选择您的工程，右击 -\> Properties -\> Java Build Path -\> Add JARs;

> 4.2 在IntelliJ IDEA中打开您的工程，File -\> Project Structure -\> Modules -\> 右侧Dependencies -\> + -\> JARs or directories

5.选中您在第一步拷贝的所有jar文件;

经过以上几步，您就可以在Eclipse或IntelliJ IDEA项目中使用VODUpload Java SDK。

**说明：**

1、使用上传SDK aliyun-java-vod-upload-1.4.13.jar时，需保证aliyun-sdk-oss的版本\>=3.9.0。

2、目前点播国内区域已发布上海、深圳、北京三个服务区域，使用上传SDK上传到深圳、北京区域，需保证aliyun-java-sdk-vod版本为2.15.11、aliyun-java-sdk-core\>=4.4.5。

## 3. 示例代码

## 上传SDK示例

将VODUploadDemo-java-1.4.13.zip开发包解压后, 在sample目录下的UploadVideoDemo.java为文件上传示例程序, 如下：

```
public class UploadVideoDemo {
    //账号AK信息请填写(必选)
    private static final String accessKeyId = "";
    //账号AK信息请填写(必选)
    private static final String accessKeySecret = "";

    public static void main(String[] args) {
        //1.音视频上传-本地文件上传
        //视频标题(必选)
        String title = "测试标题";
        //本地文件上传和文件流上传时，文件名称为上传文件绝对路径，如:/User/sample/文件名称.mp4 (必选)
        //文件名必须包含扩展名
        String fileName = "测试文件名称.mp4";
        //本地文件上传
        testUploadVideo(accessKeyId, accessKeySecret, title, fileName);

        //2.图片上传-本地文件上传
        testUploadImageLocalFile(accessKeyId, accessKeySecret);
    }

    /**
     * 本地文件上传接口
     *
     * @param accessKeyId
     * @param accessKeySecret
     * @param title
     * @param fileName
     */
    private static void testUploadVideo(String accessKeyId, String accessKeySecret, String title, String fileName) {
        UploadVideoRequest request = new UploadVideoRequest(accessKeyId, accessKeySecret, title, fileName);
        /* 可指定分片上传时每个分片的大小，默认为1M字节 */
        request.setPartSize(1 * 1024 * 1024L);
        /* 可指定分片上传时的并发线程数，默认为1，(注：该配置会占用服务器CPU资源，需根据服务器情况指定）*/
        request.setTaskNum(1);
        /* 是否开启断点续传, 默认断点续传功能关闭。当网络不稳定或者程序崩溃时，再次发起相同上传请求，可以继续未完成的上传任务，适用于超时3000秒仍不能上传完成的大文件。
        注意: 断点续传开启后，会在上传过程中将上传位置写入本地磁盘文件，影响文件上传速度，请您根据实际情况选择是否开启*/
        request.setEnableCheckpoint(false);
        /* OSS慢请求日志打印超时时间，是指每个分片上传时间超过该阈值时会打印debug日志，如果想屏蔽此日志，请调整该阈值。单位: 毫秒，默认为300000毫秒*/
        //request.setSlowRequestsThreshold(300000L);
        /* 可指定每个分片慢请求时打印日志的时间阈值，默认为300s*/
        //request.setSlowRequestsThreshold(300000L);
        /* 是否使用默认水印(可选)，指定模板组ID时，根据模板组配置确定是否使用默认水印*/
        //request.setIsShowWaterMark(true);
        /* 自定义消息回调设置(可选)，参数说明参考文档 https://help.aliyun.com/document_detail/86952.html#UserData */
        // request.setUserData("{\"Extend\":{\"test\":\"www\",\"localId\":\"xxxx\"},\"MessageCallback\":{\"CallbackURL\":\"http://test.test.com\"}}");

        /* 视频分类ID(可选) */
        //request.setCateId(0);
        /* 视频标签,多个用逗号分隔(可选) */
        //request.setTags("标签1,标签2");
        /* 视频描述(可选) */
        //request.setDescription("视频描述");
        /* 封面图片(可选) */
        //request.setCoverURL("http://cover.sample.com/sample.jpg");
        /* 模板组ID(可选) */
        //request.setTemplateGroupId("8c4792cbc8694*****d5330e56a33d");
        /* 点播服务接入点 */
        //request.setApiRegionId("cn-shanghai");
        /* ECS部署区域，如果与点播存储（OSS）区域相同，则自动使用内网上传文件至存储*/
        // request.setEcsRegionId("cn-shanghai");
        /* 存储区域(可选) */
        //request.setStorageLocation("in-2017032*****18266-5sejdln9o.oss-cn-shanghai.aliyuncs.com");
        /* 开启默认上传进度回调 */
        // request.setPrintProgress(true);
        /* 设置自定义上传进度回调 (必须继承 ProgressListener) */
        // request.setProgressListener(new PutObjectProgressListener());
        UploadVideoImpl uploader = new UploadVideoImpl();
        UploadVideoResponse response = uploader.uploadVideo(request);
        System.out.print("RequestId=" + response.getRequestId() + "\n");  //请求视频点播服务的请求ID
        if (response.isSuccess()) {
            System.out.print("VideoId=" + response.getVideoId() + "\n");
        } else {
            /* 如果设置回调URL无效，不影响视频上传，可以返回VideoId同时会返回错误码。其他情况上传失败时，VideoId为空，此时需要根据返回错误码分析具体错误原因 */
            System.out.print("VideoId=" + response.getVideoId() + "\n");
            System.out.print("ErrorCode=" + response.getCode() + "\n");
            System.out.print("ErrorMessage=" + response.getMessage() + "\n");
        }
    }

    /**
     * 图片上传接口，本地文件上传示例
     * 参数参考文档 https://help.aliyun.com/document_detail/55619.html
     *
     * @param accessKeyId
     * @param accessKeySecret
     */
    private static void testUploadImageLocalFile(String accessKeyId, String accessKeySecret) {
        // 图片类型（必选）取值范围：default（默认)，cover（封面），watermark(水印)
        String imageType = "cover";
        UploadImageRequest request = new UploadImageRequest(accessKeyId, accessKeySecret, imageType);
        /* 图片文件扩展名（可选）取值范围：png，jpg，jpeg */
        //request.setImageExt("png");
        /* 图片标题（可选）长度不超过128个字节，UTF8编码 */
        //request.setTitle("图片标题");
        /* 图片标签（可选）单个标签不超过32字节，最多不超过16个标签，多个用逗号分隔，UTF8编码 */
        //request.setTags("标签1,标签2");
        /* 存储区域（可选）*/
        //request.setStorageLocation("out-4f3952f78c021*****013e7.oss-cn-shanghai.aliyuncs.com");
        /* 流式上传时，InputStream为必选，fileName为源文件名称，如:文件名称.png(可选)*/
        //request.setFileName("测试文件名称.png");
        /* 开启默认上传进度回调 */
        // request.setPrintProgress(true);
        /* 设置自定义上传进度回调 (必须继承 ProgressListener) */
        // request.setProgressListener(new PutObjectProgressListener());
        /* 点播服务接入点 */
        //request.setApiRegionId("cn-shanghai");
        /* ECS部署区域，如果与点播存储（OSS）区域相同，则自动使用内网上传文件至存储*/
        // request.setEcsRegionId("cn-shanghai");

        UploadImageImpl uploadImage = new UploadImageImpl();
        UploadImageResponse response = uploadImage.upload(request);
        System.out.print("RequestId=" + response.getRequestId() + "\n");
        if (response.isSuccess()) {
            System.out.print("ImageId=" + response.getImageId() + "\n");
            System.out.print("ImageURL=" + response.getImageURL() + "\n");
        } else {
            System.out.print("ErrorCode=" + response.getCode() + "\n");
            System.out.print("ErrorMessage=" + response.getMessage() + "\n");
        }


    }
}
			
```

## 上传进度条示例

将VODUploadDemo-java-1.4.13.zip开发包解压后, 在sample目录下的PutObjectProgressListener.java为上传进度回调函数示例程序，该类必须继承VoDProgressListener类。其中，ProgressEvent是通过OSS上传文件时产生的进度回调通知，您可自定义各个事件通知的业务处理逻辑，示例代码如下：

```
import com.aliyun.oss.event.ProgressEvent;
import com.aliyun.oss.event.ProgressEventType;

/**
 * 上传进度回调方法类
 * 当您开启上传进度回调时该事件回调才会生效。
 * OSS分片上传成功或失败均触发相应的回调事件，您可根据业务逻辑处理相应的事件回调。
 * 当创建音视频信息成功后，此上传进度回调中的videoId为本次上传生成的视频ID，您可以根据视频ID进行音视频管理。
 * 当创建图片信息成功后，此上传进度回调中的ImageId为本次上传生成的图片ID，您可以根据视频ID进行图片管理。
 */

public class PutObjectProgressListener implements VoDProgressListener {
    /**
     * 已成功上传至OSS的字节数
     */
    private long bytesWritten = 0;
    /**
     * 原始文件的总字节数
     */
    private long totalBytes = -1;
    /**
     * 本次上传成功标记
     */
    private boolean succeed = false;
    /**
     * 视频ID
     */
    private String videoId;
    /**
     * 图片ID
     */
    private String imageId;

    public void progressChanged(ProgressEvent progressEvent) {
        long bytes = progressEvent.getBytes();
        ProgressEventType eventType = progressEvent.getEventType();
        switch (eventType) {
            // 开始上传事件
            case TRANSFER_STARTED_EVENT:
                if (videoId != null) {
                    System.out.println("Start to upload videoId " + videoId + "......");
                }
                if (imageId != null) {
                    System.out.println("Start to upload imageId " + imageId + "......");
                }
                break;
            // 计算待上传文件总大小事件通知，只有调用本地文件方式上传时支持该事件
            case REQUEST_CONTENT_LENGTH_EVENT:
                this.totalBytes = bytes;
                System.out.println(this.totalBytes + "bytes in total will be uploaded to OSS.");
                break;
            // 已经上传成功文件大小事件通知
            case REQUEST_BYTE_TRANSFER_EVENT:
                this.bytesWritten += bytes;
                if (this.totalBytes != -1) {
                    int percent = (int) (this.bytesWritten * 100.0 / this.totalBytes);
                    System.out.println(bytes + " bytes have been written at this time, upload progress: " +
                            percent + "%(" + this.bytesWritten + "/" + this.totalBytes + ")");
                } else {
                    System.out.println(bytes + " bytes have been written at this time, upload sub total : " +
                            "(" + this.bytesWritten + ")");
                }
                break;
            // 文件全部上传成功事件通知
            case TRANSFER_COMPLETED_EVENT:
                this.succeed = true;
                if (videoId != null) {
                    System.out.println("Succeed to upload videoId " + videoId + " , " + this.bytesWritten + " bytes have been transferred in total.");
                }
                if (imageId != null) {
                    System.out.println("Succeed to upload imageId " + imageId + " , " + this.bytesWritten + " bytes have been transferred in total.");
                }
                break;
            // 文件上传失败事件通知
            case TRANSFER_FAILED_EVENT:
                if (videoId != null) {
                    System.out.println("Failed to upload videoId " + videoId + " , " + this.bytesWritten + " bytes have been transferred.");
                }
                if (imageId != null) {
                    System.out.println("Failed to upload imageId " + imageId + " , " + this.bytesWritten + " bytes have been transferred.");
                }
                break;

            default:
                break;
        }
    }

    public boolean isSucceed() {
        return succeed;
    }

    public void onVidReady(String videoId) {
        setVideoId(videoId);
    }

    public void onImageIdReady(String imageId) {
        setImageId(imageId);
    }

    public String getVideoId() {
        return videoId;
    }

    public void setVideoId(String videoId) {
        this.videoId = videoId;
    }

    public String getImageId() {
        return imageId;
    }

    public void setImageId(String imageId) {
        this.imageId = imageId;
    }
}

			
```

