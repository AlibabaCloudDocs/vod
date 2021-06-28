# Java上传SDK

通过视频点播（VOD）上传SDK服务，您可以实现方便、快速地上传媒体文件。本文通过示例为您详细介绍Java上传SDK服务。

## 功能介绍

使用上传SDK服务可实现的主要功能如下：

-   上传本地音视频到视频点播：默认使用分片上传，最大支持48.8 TB的单个文件并且支持断点续传。
-   上传网络音视频到视频点播：自动从URL地址下载并上传到视频点播，最大支持48.8 TB的单个文件。
-   上传本地图片到视频点播：自动从本地文件路径上传到视频点播。
-   上传网络图片到视频点播：自动从URL地址下载并上传到视频点播。
-   上传本地M3U8音视频（包括所有分片文件）到视频点播：需指定本地M3U8索引文件和分片文件目录。
-   上传网络M3U8音视频（包括所有分片文件）到视频点播：需指定网络M3U8索引文件和分片文件的URL地址。
-   上传本地辅助媒资文件到视频点播：自动从本地文件路径上传到视频点播。
-   上传网络辅助媒资文件到视频点播：自动从URL地址下载并上传到视频点播。

**说明：** 上传的URL，需要将URL编码后再传入使用，避免存在特殊字符导致无法上传视频的情况。

除了上述主要功能外，上传SDK服务还可实现以下功能：

-   上传进度条，支持SDK默认进度回调和自定义进度回调，M3U8文件上传暂不支持。
-   可指定上传脚本部署的ECS区域，如果与视频点播存储（OSS）区域相同，则自动使用内网上传文件至存储，上传更快且更省公网流量（由于视频点播API只提供外网域名访问，因此部署上传脚本的ECS服务器必须具有访问外网的权限）。
-   可指定视频点播中心（默认为上海）和存储区域，便于海外上传。
-   支持上传时设置元数据（标题）、StorageLocation、UserData、转码模板、视频点播工作流等。
-   支持STS方式接入，需实现传递和刷新STS的接口。当文件上传时间超过STS过期时间时，SDK内部定期获取新的STS信息，进行后续上传操作。

上传SDK服务支持的文件格式请参见[媒体上传文件格式](/cn.zh-CN/开发指南/媒体上传/概述.md)。

## 前提条件

-   您已经完成注册阿里云账号，并完成实名认证。
-   服务端环境需要Java 1.8版本。

## 安装SDK

**说明：** 本文以Java 1.8版本、Java 上传SDK1.4.14版本举例说明。其他版本请根据实际情况操作。

1.  下载Java上传SDK及示例代码。下载信息，请参见[服务端上传SDK](/cn.zh-CN/SDK下载/SDK下载.md)。

2.  解压Java上传SDK及示例代码文件（VODUploadDemo-java-1.4.14.zip）。

    文件介绍：

    -   lib：存放Java上传SDK所需要的jar包。
    -   sample：存放Java上传SDK的示例代码。
3.  引入jar包。

    以Eclipse和IntelliJ IDEA为例介绍引入操作。

    -   在Eclipse中右击您的工程，选择**Properties** \> **Java Build Path** \> **Add JARs**。
    -   在IntelliJ IDEA中打开您的工程，选择**File** \> **Project Structure** \> **Modules**，单击右侧**Dependencies**，然后单击**+**，再单击**JARs or directories**。
    找到解压后的VODUploadDemo-java-1.4.14文件，并将lib目录下的所有jar文件添加到您的项目中。

4.  配置依赖。

    **说明：** 请确保部分jar包符合以下要求：

    -   使用上传SDK aliyun-java-vod-upload-1.4.14.jar时，需保证aliyun-sdk-oss的版本号不小于3.9.0。
    -   目前视频点播已在国内发布的区域有上海、深圳、北京，使用上传SDK上传到深圳、北京区域，需保证aliyun-java-sdk-vod版本号不低于2.15.11、aliyun-java-sdk-core版本号不小于4.4.5。
    您需要添加以下Maven依赖。

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


## 示例代码

**说明：** 在使用示例代码时，需要手动引入对应的类。

-   上传SDK示例

    sample目录下的`UploadVideoDemo.java`文件，为上传示例代码。

    部分示例代码展示，如下所示。详细示例代码，请参见`UploadVideoDemo.java`文件。

    ```
    public class UploadVideoDemo {
    
        //账号AK信息请填写(必选)
        private static final String accessKeyId = "<your accessKeyId>";
        //账号AK信息请填写(必选)
        private static final String accessKeySecret = "<your accessKeySecret>";
    
        public static void main(String[] args) {
            // 一、视频文件上传
            // 视频标题(必选)
            String title = "测试标题";
            // 1.本地文件上传和文件流上传时，文件名称为上传文件绝对路径，如:/User/sample/文件名称.mp4 (必选)
            // 2.网络流上传时，文件名称为源文件名，如文件名称.mp4(必选)。
            // 任何上传方式文件名必须包含扩展名
            String fileName = "/path/文件名.mp4";
            // 本地文件上传
            //testUploadVideo(accessKeyId, accessKeySecret, title, fileName);
    
            // 待上传视频的网络流地址
            String url = "http://xxxx.xxxx.com/xxxx.mp4";
    
            // 2.网络流上传
            // 文件扩展名，当url中不包含扩展名时，需要设置该参数
            String fileExtension = "mp4";
            //testUploadURLStream(accessKeyId, accessKeySecret, title, url, fileExtension);
    
            // 二、图片上传
            //testUploadImageLocalFile(accessKeyId, accessKeySecret);
    
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
            /* 可指定分片上传时每个分片的大小，默认为2M字节 */
            request.setPartSize(2 * 1024 * 1024L);
            /* 可指定分片上传时的并发线程数，默认为1，(注：该配置会占用服务器CPU资源，需根据服务器情况指定）*/
            request.setTaskNum(1);
            /* 是否开启断点续传, 默认断点续传功能关闭。当网络不稳定或者程序崩溃时，再次发起相同上传请求，可以继续未完成的上传任务，适用于超时3000秒仍不能上传完成的大文件。
            注意: 断点续传开启后，会在上传过程中将上传位置写入本地磁盘文件，影响文件上传速度，请您根据实际情况选择是否开启*/
            //request.setEnableCheckpoint(false);
            /* OSS慢请求日志打印超时时间，是指每个分片上传时间超过该阈值时会打印debug日志，如果想屏蔽此日志，请调整该阈值。单位: 毫秒，默认为300000毫秒*/
            //request.setSlowRequestsThreshold(300000L);
            /* 可指定每个分片慢请求时打印日志的时间阈值，默认为300s*/
            //request.setSlowRequestsThreshold(300000L);
            /* 是否显示水印(可选)，指定模板组ID时，根据模板组配置确定是否显示水印*/
            //request.setIsShowWaterMark(true);
            /* 自定义消息回调设置(可选)，参数说明请参见[请求参数说明](/cn.zh-CN/服务端API/附录/请求参数说明.md)。*/
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
            //request.setTemplateGroupId("8c4792cbc8694e7084fd5330e56a33d");
            /* 工作流ID(可选) */
            //request.setWorkflowId("d4430d07361f0*be1339577859b0177b");
            /* 存储区域(可选) */
            //request.setStorageLocation("in-201703232118266-5sejdln9o.oss-cn-shanghai.aliyuncs.com");
            /* 开启默认上传进度回调 */
            //request.setPrintProgress(false);
            /* 设置自定义上传进度回调 (必须继承 VoDProgressListener) */
            //request.setProgressListener(new PutObjectProgressListener());
            /* 设置您实现的生成STS信息的接口实现类*/
            // request.setVoDRefreshSTSTokenListener(new RefreshSTSTokenImpl());
            /* 设置应用ID*/
            //request.setAppId("app-1000000");
            /* 点播服务接入点 */
            //request.setApiRegionId("cn-shanghai");
            /* ECS部署区域*/
            // request.setEcsRegionId("cn-shanghai");
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
         * URL网络流上传。支持断点续传，最大支持48.8TB的单个文件。
         * 该上传方式需要先将网络文件下载到本地磁盘，再进行上传，所以要保证本地磁盘有充足的空间。
         * 当您设置的URL中不包括文件扩展名时，需要单独设置fileExtension，表示文件扩展名。
         * @param accessKeyId
         * @param accessKeySecret
         * @param title
         * @param fileName
         * @param url
         */
        private static void testUploadURLStream(String accessKeyId, String accessKeySecret, String title, String url, String fileExtension) {
            UploadURLStreamRequest request = new UploadURLStreamRequest(accessKeyId, accessKeySecret, title, url);
    
            /* 文件扩展名*/
            request.setFileExtension(fileExtension);
            /* 网络文件下载连接超时，单位毫秒，0-表示不限制*/
            request.setDownloadConnectTimeout(1000);
            /* 网络文件下载读取超时，单位毫秒，0-表示不限制*/
            request.setDownloadReadTimeout(0);
            /* 网络文件下载后保存的本地目录*/
            request.setLocalDownloadFilePath("/Users/download");
            /* 是否显示水印(可选)，指定模板组ID时，根据模板组配置确定是否显示水印*/
            //request.setShowWaterMark(true);
            /* 自定义消息回调设置(可选)，参数说明请参见[请求参数说明](/cn.zh-CN/服务端API/附录/请求参数说明.md) */
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
            //request.setTemplateGroupId("8c4792cbc8694e7084fd5330e56a33d");
            /* 工作流ID(可选) */
            //request.setWorkflowId("d4430d07361f0*be1339577859b0177b");
            /* 存储区域(可选) */
            //request.setStorageLocation("xxxxxx.oss-cn-shanghai.aliyuncs.com");
            /* 开启默认上传进度回调 */
            //request.setPrintProgress(true);
            /* 设置自定义上传进度回调 (必须继承 VoDProgressListener) */
            //request.setProgressListener(new PutObjectProgressListener());
            /* 设置应用ID*/
            //request.setAppId("app-1000000");
            /* 点播服务接入点 */
            //request.setApiRegionId("cn-shanghai");
            /* ECS部署区域*/
            // request.setEcsRegionId("cn-shanghai");
            UploadVideoImpl uploader = new UploadVideoImpl();
            UploadURLStreamResponse response = uploader.uploadURLStream(request);
            System.out.print("RequestId=" + response.getRequestId() + "\n"); //请求视频点播服务的请求ID
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
         * 参数请参见[t1235495.dita\#doc\_api\_vod\_CreateUploadImage](/cn.zh-CN/服务端API/媒体上传/获取图片上传地址和凭证.md)
         *
         * @param accessKeyId
         * @param accessKeySecret
         */
        private static void testUploadImageLocalFile(String accessKeyId, String accessKeySecret) {
            /* 图片类型（必选）取值范围：default（默认)，cover（封面），watermark（水印）*/
            String imageType = "default";
            UploadImageRequest request = new UploadImageRequest(accessKeyId, accessKeySecret, imageType);
            request.setImageType("default");
            /* 图片文件扩展名（可选）取值范围：png，jpg，jpeg */
            //request.setImageExt("png");
            /* 图片标题（可选）长度不超过128个字节，UTF8编码 */
            //request.setTitle("图片标题");
            /* 图片标签（可选）单个标签不超过32字节，最多不超过16个标签，多个用逗号分隔，UTF8编码 */
            //request.setTags("标签1,标签2");
            /* 存储区域（可选）*/
            //request.setStorageLocation("out-4f3952f78c0211e8b3020013e7.oss-cn-shanghai.aliyuncs.com");
            /* fileName为源文件名称，如:文件名称.png*/
            String fileName = "/User/sample/文件名称.png";
            request.setFileName(fileName);
            /* 开启默认上传进度回调 */
            //request.setPrintProgress(false);
            /* 设置自定义上传进度回调 (必须继承 VoDProgressListener) */
            // request.setProgressListener(new PutObjectProgressListener());
            /* 设置应用ID*/
            //request.setAppId("app-1000000");
            /* 点播服务接入点 */
            //request.setApiRegionId("cn-shanghai");
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

    AccessKey获取，操作步骤如下所示。

    1.  进入[AccessKey管理](https://ram.console.aliyun.com/manage/ak)页面。
    2.  选择需要用到的AccessKey ID，单击**查看Secret**，通过手机验证后，即可获取AccessKey Secret。
-   上传进度条示例

    sample目录下的`PutObjectProgressListener.java`文件，为上传进度回调函数示例代码。

    该类必须继承VoDProgressListener类，ProgressEvent是通过OSS上传文件时产生的进度回调通知，您可以自定义各个事件通知的业务处理逻辑

    示例代码如下所示。

    ```
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
                //开始上传事件
                case TRANSFER_STARTED_EVENT:
                    if (videoId != null) {
                        System.out.println("Start to upload videoId "+videoId+"......");
                    }
                    if (imageId != null) {
                        System.out.println("Start to upload imageId "+imageId+"......");
                    }
                    break;
                //计算待上传文件总大小事件通知，只有调用本地文件方式上传时支持该事件
                case REQUEST_CONTENT_LENGTH_EVENT:
                    this.totalBytes = bytes;
                    System.out.println(this.totalBytes + "bytes in total will be uploaded to OSS.");
                    break;
                //已经上传成功文件大小事件通知
                case REQUEST_BYTE_TRANSFER_EVENT:
                    this.bytesWritten += bytes;
                    if (this.totalBytes != -1) {
                        int percent = (int) (this.bytesWritten * 100.0 / this.totalBytes);
                        System.out.println(bytes+" bytes have been written at this time, upload progress: "+
                                percent +"%(" +  this.bytesWritten +  "/"  + this.totalBytes  + ")");
                    } else {
                        System.out.println(bytes + " bytes have been written at this time, upload sub total : " +
                                "(" + this.bytesWritten + ")");
                    }
                    break;
                //文件全部上传成功事件通知
                case TRANSFER_COMPLETED_EVENT:
                    this.succeed = true;
                    if (videoId != null) {
                        System.out.println("Succeed to upload videoId "  + videoId  + " , " + this.bytesWritten + " bytes have been transferred in total.");
                    }
                    if (imageId != null) {
                        System.out.println("Succeed to upload imageId " + imageId + " , " + this.bytesWritten + " bytes have been transferred in total.");
                    }
                    break;
                //文件上传失败事件通知
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

-   刷新临时Token示例

    sample目录下的`RefreshSTSTokenImpl.java`文件，为刷新临时Token的示例代码。

    示例如下所示。

    ```
    /**
     * @author vod
     * 生成STS信息实现类
     * @date 2019/6/5
     */
    public class RefreshSTSTokenImpl implements VoDRefreshSTSTokenListener {
    
        public STSTokenDTO onRefreshSTSToken() {
            STSTokenDTO stsTokenDTO = new STSTokenDTO();
            stsTokenDTO.setAccessKeyId("<your sts AccessKeyId>");
            stsTokenDTO.setAccessKeySecret("<your sts AccessKeySecret>");
            stsTokenDTO.setSecurityToken("<your sts SecurityToken>");
            return stsTokenDTO;
        }
    
    }
    ```


## 常见问题

由于开发环境的不同，您可能会遇到找不到类等问题。

此类问题通常是IDEA环境编译问题导致，如果确定已经导入所需的资源包，您可以尝试下面两种办法解决：

-   在Maven项目中，单击右侧**Maven**，单击**m**图标，输入`mvn idea:module`重新加载资源。

    ![module](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2527293261/p284429.png)

-   在上方菜单栏，选择**Build** \> **Rebuild Project**重新编辑您的工程。

    ![Rebuild](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2527293261/p284430.png)


