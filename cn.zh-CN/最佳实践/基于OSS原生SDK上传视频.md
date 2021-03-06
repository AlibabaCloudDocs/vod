# 基于OSS原生SDK上传视频

通过阅读本文，让您了解基于OSS原生SDK上传视频的实现方式。

## 场景

视频点播提供了丰富的[上传方式](/cn.zh-CN/开发指南/媒体上传/概述.md)包括[客户端上传](/cn.zh-CN/开发指南/媒体上传/客户端上传.md)、[服务端上传](/cn.zh-CN/开发指南/媒体上传/服务端上传.md)等，但可能缺乏需要的语言版本（如Go等），此时可以直接基于OSS原生SDK进行上传。

## SDK说明

点播服务已为您提供客户端上传SDK和服务端上传SDK，如下所示：

-   客户端上传SDK。
    -   [Android上传SDK](/cn.zh-CN/上传SDK/客户端上传/Android上传SDK/文件上传.md)。
    -   [iOS上传SDK](iOS上传SDKt1959822.dita#task_1995648)。
    -   [Web端上传SDK](Web端上传SDKt1959815.dita#task_1995648)。
-   服务端上传SDK。
    -   [Java上传SDK](Java上传SDKt1959828.dita#task_1995280)。
    -   [t1959829.dita\#task\_1995280](/cn.zh-CN/上传SDK/服务端上传/Python上传SDK.md)。
    -   [t1959830.dita\#task\_1995280](/cn.zh-CN/上传SDK/服务端上传/PHP上传SDK.md)。
    -   [t1959831.dita\#task\_1995280](/cn.zh-CN/上传SDK/服务端上传/C/C++上传SDK.md)。

**说明：** 也可以直接访问[SDK下载](SDK下载t1959787.xdita#topic-1959787)页面下载SDK和Demo，如确实没有您需要的版本，可以继续阅读本文再行开发。

## 准备工作

-   确认已开通点播服务并完成了相关配置。
-   确认已准备了[阿里云账号AccessKey](/cn.zh-CN/开发指南/账号和授权/概述.md)，并授予了上传权限。

## 上传步骤

![上传步骤](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6361984061/p180094.png)

1.  访问点播服务获取，请参见[上传地址和凭证](/cn.zh-CN/开发指南/媒体上传/上传地址和凭证.md)。

    **说明：** 这一步还会创建视频媒资记录，返回视频ID，请妥善保存，后续可根据视频ID进行视频播放、管理和AI处理等。

2.  解析上传地址（UploadAddress）和上传凭证（UploadAuth），得到OSS的上传地址和授权信息。解析方式请参见[上传地址和凭证](/cn.zh-CN/开发指南/媒体上传/上传地址和凭证.md)。
3.  调用OSS SDK将视频文件上传至指定的bucket中，注意使用STS Auth方式，且使用解析后的上传地址和授权信息进行初始化，不要使用自己的AccessKey等信息。

## 代码实现

-   核心代码实现共分4步：
    1.  使用AK初始化VOD客户端。
    2.  获取视频上传地址和凭证。
    3.  使用上传凭证和地址初始化OSS客户端。
    4.  上传本地文件。
-   可以使用点播服务的接口，例如[获取视频上传地址和凭证](/cn.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)。
-   使用OSS SDK在服务端上传，可参考如下版本：
    -   OSS-.NET-SDK。
    -   OSS-C-SDK。
    -   OSS-Go-SDK。
    -   OSS-Ruby-SDK。
    -   OSS-Java-SDK。

## PHP上传示例

**环境准备**

-   PHP 5.3+，可在终端执行`php -v`命令查看当前的PHP版本。
-   cURL扩展，可在终端执行`php -m`命令查看curl扩展是否已经安装好。

**安装**

1.  在您的PHP项目中添加空文件夹aliyun-php-sdk。
2.  从[aliyun-openapi-php-sdk](https://github.com/aliyun/aliyun-openapi-php-sdk?spm=a2c4g.11186623.2.68.627e4eafSZjXWo)下载整个源码，解压后拷贝aliyun-php-sdk-core和aliyun-php-sdk-vod两个文件夹到aliyun-php-sdk目录下。
3.  从[aliyun-oss-php-sdk](https://github.com/aliyun/aliyun-oss-php-sdk/releases?spm=a2c4g.11186623.2.69.627e4eafSZjXWo)下载最新的OSS PHP SDK的源码，解压ZIP文件后添加文件夹到aliyun-php-sdk目录下。以下载[v.2.2.4 Source code \(zip\)](https://github.com/aliyun/aliyun-oss-php-sdk/archive/v2.2.4.zip?spm=a2c4g.11186623.2.70.627e4eafSZjXWo&file=v2.2.4.zip)为例，解压后文件夹为aliyun-oss-php-sdk-2.2.4。
4.  打开aliyun-php-sdk/aliyun-php-sdk-core/Config.php文件，找到"//config sdk auto load path."在这行下面添加：

    ```
    Autoloader::addAutoloadPath("aliyun-php-sdk-vod");
    ```

5.  在代码中引用VOD和OSS的文件。

    示例代码如下所示：

    ```
    require_once './aliyun-php-sdk/aliyun-php-sdk-core/Config.php';   // 假定您的源码文件和aliyun-php-sdk处于同一目录。
    require_once './aliyun-php-sdk/aliyun-oss-php-sdk-2.2.4/autoload.php';
    use vod\Request\V20170321 as vod;
    use OSS\OssClient;
    use OSS\Core\OssException;
    ```

    **说明：** 更多信息，请参见[VOD PHP SDK安装](VOD PHP SDK安装t1959700.dita#task_1989494)和[OSS PHP SDK安装](OSS PHP SDK安装t22352.dita#concept_85580_zh)。


**参考代码**

-   定义核心步骤的函数：
    1.  使用AK初始化VOD客户端。

        示例代码如下所示：

        ```
        function init_vod_client($accessKeyId, $accessKeySecret) {
            $regionId = 'cn-shanghai';     // 根据点播接入服务所在的Region填写，例如：接入服务在上海，则填cn-shanghai
            $profile = DefaultProfile::getProfile($regionId, $accessKeyId, $accessKeySecret);
            return new DefaultAcsClient($profile);
        }
        ```

    2.  获取视频上传地址和凭证。

        示例代码如下所示：

        ```
        function create_upload_video($vodClient) {
            $request = new vod\CreateUploadVideoRequest();
            $request->setTitle("视频标题");        // 视频标题(必填参数)
            $request->setFileName("文件名称.mov"); // 视频源文件名称，必须包含扩展名(必填参数)
            $request->setDescription("视频描述");  // 视频源文件描述(可选)
            $request->setCoverURL("http://img.alicdn.com/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png"); // 自定义视频封面(可选)
            $request->setTags("标签1,标签2"); // 视频标签，多个用逗号分隔(可选)
            return $vodClient->getAcsResponse($request);
        }
        ```

    3.  使用上传凭证和地址初始化OSS客户端（注意需要先Base64解码并Json Decode再传入）。

        示例代码如下所示：

        ```
        function init_oss_client($uploadAuth, $uploadAddress) {
            $ossClient = new OssClient($uploadAuth['AccessKeyId'], $uploadAuth['AccessKeySecret'], $uploadAddress['Endpoint'], 
                false, $uploadAuth['SecurityToken']);
            $ossClient->setTimeout(86400*7);    // 设置请求超时时间，单位秒，默认是5184000秒, 建议不要设置太小，如果上传文件很大，消耗的时间会比较长
            $ossClient->setConnectTimeout(10);  // 设置连接超时时间，单位秒，默认是10秒
            return $ossClient;
        }
        ```

        **说明：** 如果由于SSL配置异常导致错误\(如出现cURL error: SSL certificate problem\), 可将https替换为http后再初始化OssClient。

        ```
        $uploadAddress['Endpoint'] = str_replace("https:", "http:", $uploadAddress['Endpoint']);
        ```

    4.  上传本地文件。

        示例代码如下所示：

        ```
        function upload_local_file($ossClient, $uploadAddress, $localFile) {
            return $ossClient->uploadFile($uploadAddress['Bucket'], $uploadAddress['FileName'], $localFile);
        }
        ```

    5.  刷新上传凭证。

        示例代码如下所示：

        ```
        function refresh_upload_video($vodClient, $videoId) {
            $request = new vod\RefreshUploadVideoRequest();
            $request->setVideoId($videoId);
            return $vodClient->getAcsResponse($request);
        }
        ```

-   执行完整流程（注意捕获异常）。

    示例代码如下所示：

    ```
    $accessKeyId = '<AccessKeyId>';                    // 您的AccessKeyId
    $accessKeySecret = '<AccessKeySecret>';            // 您的AccessKeySecret
    $localFile = '/Users/yours/Video/testVideo.flv';   // 需要上传到VOD的本地视频文件的完整路径
    try {
        // 初始化VOD客户端并获取上传地址和凭证
        $vodClient = init_vod_client($accessKeyId, $accessKeySecret);
        $createRes = create_upload_video($vodClient);
        // 执行成功会返回VideoId、UploadAddress和UploadAuth
        $videoId = $createRes->VideoId;
        $uploadAddress = json_decode(base64_decode($createRes->UploadAddress), true);
        $uploadAuth = json_decode(base64_decode($createRes->UploadAuth), true);
        // 使用UploadAuth和UploadAddress初始化OSS客户端
        $ossClient = init_oss_client($uploadAuth, $uploadAddress);
        // 上传文件，注意是同步上传会阻塞等待，耗时与文件大小和网络上行带宽有关
        //$result = upload_local_file($ossClient, $uploadAddress, $localFile);
        $result = multipart_upload_file($ossClient, $uploadAddress, $localFile);
        printf("Succeed, VideoId: %s", $videoId);
    } catch (Exception $e) {
        // var_dump($e);
        printf("Failed, ErrorMessage: %s", $e->getMessage());
    }
    ```


## GO上传示例

**环境准备**

支持Go 1.7及以上版本，可到Go官网下载合适的版本安装。

**安装**

-   安装SDK。
    -   使用go get安装SDK。

        ```
        go get -u github.com/aliyun/alibaba-cloud-sdk-go/sdk
        ```

        **说明：**

        -   安装过程中，界面不会打印提示，请耐心等待。如发生超时，请再次执行命令。
        -   当GOPATH对应的目录下出现了子目录src/github.com/aliyun/alibaba-cloud-sdk-go/services/vod即表示SDK安装成功。
    -   使用glide安装SDK。

        ```
        glide get github.com/aliyun/alibaba-cloud-sdk-go
        ```

-   定义核心步骤的函数。
    1.  使用AK初始化VOD客户端。

        示例代码如下所示：

        ```
        func InitVodClient(accessKeyId string, accessKeySecret string) (client *vod.Client, err error) {
            // 点播服务接入区域
            regionId := "cn-shanghai"
            // 创建授权对象
            credential := &credentials.AccessKeyCredential{
                accessKeyId,
                accessKeySecret,
            }
            // 自定义config
            config := sdk.NewConfig()
            config.AutoRetry = true      // 失败是否自动重试
            config.MaxRetryTime = 3      // 最大重试次数
            config.Timeout = 3000000000  // 连接超时，单位：纳秒；默认为3秒
            // 创建vodClient实例
            return vod.NewClientWithOptions(regionId, config, credential)
        }
        ```

    2.  获取视频上传地址和凭证。

        示例代码如下所示：

        ```
        func MyCreateUploadVideo(client *vod.Client) (response *vod.CreateUploadVideoResponse, err error) {
            request := vod.CreateCreateUploadVideoRequest()
            request.Title = "Sample Video Title"
            request.Description = "Sample Description"
            request.FileName = "/opt/video/sample/video_file.mp4"
            //request.CateId = "-1"
            request.CoverURL = "http://img.alicdn.com/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png"
            request.Tags = "tag1,tag2"
            request.AcceptFormat = "JSON"
            return client.CreateUploadVideo(request)
        }
        ```

    3.  使用上传凭证和地址初始化OSS客户端（注意需要先Base64解码并Json Decode再传入）。

        示例代码如下所示：

        ```
        func InitOssClient(uploadAuthDTO UploadAuthDTO, uploadAddressDTO UploadAddressDTO) (*oss.Client, error) {
            client, err := oss.New(uploadAddressDTO.Endpoint,
                uploadAuthDTO.AccessKeyId,
                uploadAuthDTO.AccessKeySecret,
                oss.SecurityToken(uploadAuthDTO.SecurityToken),
                oss.Timeout(86400*7, 86400*7))
            return client, err
        }
        ```

    4.  上传本地文件。

        示例代码如下所示：

        ```
        func UploadLocalFile(client *oss.Client, uploadAddressDTO UploadAddressDTO, localFile string) {
            // 获取存储空间。
            bucket, err := client.Bucket(uploadAddressDTO.Bucket)
            if err != nil {
                fmt.Println("Error:", err)
                os.Exit(-1)
            }
            // 上传本地文件。
            err = bucket.PutObjectFromFile(uploadAddressDTO.FileName, localFile)
            if err != nil {
                fmt.Println("Error:", err)
                os.Exit(-1)
            }
        }
        ```

    5.  刷新上传凭证。

        示例代码如下所示：

        ```
        func MyRefreshUploadVideo(client *vod.Client) (response *vod.RefreshUploadVideoResponse, err error) {
            request := vod.CreateRefreshUploadVideoRequest()
            request.VideoId = ""
            request.AcceptFormat = "JSON"
            return client.RefreshUploadVideo(request)
        }
        ```

-   执行完整流程（注意捕获异常）。

    示例代码如下所示：

    ```
    type UploadAuthDTO struct {
        AccessKeyId string
        AccessKeySecret string
        SecurityToken string
    }
    type UploadAddressDTO struct {
        Endpoint string
        Bucket string
        FileName string
    }
    func main() {
        var accessKeyId string = "<AccessKeyId>";                    // 您的AccessKeyId
        var accessKeySecret string = "<AccessKeySecret>";            // 您的AccessKeySecret
        var localFile string = "/Users/yours/Video/testVideo.flv";   // 需要上传到VOD的本地视频文件的完整路径
        // 初始化VOD客户端并获取上传地址和凭证
        var vodClient, initVodClientErr = InitVodClient(accessKeyId, accessKeySecret)
        if initVodClientErr != nil {
            fmt.Println("Error:", initVodClientErr)
            return
        }
        // 获取上传地址和凭证
        var response, createUploadVideoErr = MyCreateUploadVideo(vodClient)
        if createUploadVideoErr != nil {
            fmt.Println("Error:", createUploadVideoErr)
            return
        }
        // 执行成功会返回VideoId、UploadAddress和UploadAuth
        var videoId = response.VideoId
        var uploadAuthDTO UploadAuthDTO
        var uploadAddressDTO UploadAddressDTO
        var uploadAuthDecode, _ = base64.StdEncoding.DecodeString(response.UploadAuth)
        var uploadAddressDecode, _ = base64.StdEncoding.DecodeString(response.UploadAddress)
        json.Unmarshal(uploadAuthDecode, &uploadAuthDTO)
        json.Unmarshal(uploadAddressDecode, &uploadAddressDTO)
        // 使用UploadAuth和UploadAddress初始化OSS客户端
        var ossClient, _ = InitOssClient(uploadAuthDTO, uploadAddressDTO)
        // 上传文件，注意是同步上传会阻塞等待，耗时与文件大小和网络上行带宽有关
        UploadLocalFile(ossClient, uploadAddressDTO, localFile)
        //MultipartUploadFile(ossClient, uploadAddressDTO, localFile)
        fmt.Println("Succeed, VideoId:", videoId)
    }
    ```


## .NET上传示例

**环境准备**

-   .NET Framework 4.6.1及其以上版本。
-   .NET Standard 2.0及其以上版本。

**说明：** 更多信息，请参见[环境要求](/cn.zh-CN/服务端SDK/.NET SDK/安装.md)。

**安装**

-   NuGet安装方式，在**解决方案资源管理器面板**中右击您的项目单击**管理Nuget程序包**，在打开的NuGet管理面板中单击**浏览**。在选项卡中分别输入`aliyun-net-sdk-core`和`aliyun-net-sdk-vod`，选择对应模块最新版本单击**安装**。
-   .NET CLI工具安装。

    示例代码如下所示：

    ```
    dotnet add package aliyun-net-sdk-core
    dotnet add package aliyun-net-sdk-vod
    ```

    **说明：** 说明 更多信息，请参见[VOD .NET SDK安装](/cn.zh-CN/服务端SDK/.NET SDK/安装.md)和[OSS .NET SDK安装](OSS .NET SDK安装t22471.dita#concept_32086_zh)。


**参考代码**

-   定义核心步骤的函数：
    1.  使用AK初始化VOD客户端。

        示例代码如下所示：

        ```
        public static DefaultAcsClient InitVodClient(string accessKeyId, string accessKeySecret)
        {
            // 根据点播接入服务所在的Region填写，例如：接入服务在上海，则填cn-shanghai
            string regionId = "cn-shanghai";
            IClientProfile profile = DefaultProfile.GetProfile(regionId, accessKeyId, accessKeySecret);
            return new DefaultAcsClient(profile);
        }
        ```

    2.  获取视频上传地址和凭证。

        示例代码如下所示：

        ```
        public static CreateUploadVideoResponse CreateUploadVideo(DefaultAcsClient vodClient)
        {
            CreateUploadVideoRequest request = new CreateUploadVideoRequest();
            request.AcceptFormat = Aliyun.Acs.Core.Http.FormatType.JSON;
            request.FileName = "vod_test.mp4";
            request.Title = "this is title";
            //request.Description = "this is desc";
            //request.Tags = "tag1,tag2";
            //request.CoverURL = "http://vod.aliyun.com/test_cover_url.jpg";
            //request.CateId = -1;
            //request.TemplateGroupId = "";
            //request.WorkflowId = "";
            //request.StorageLocation = "";
            //request.AppId = "app-1000000";
            //设置请求超时时间
            request.SetReadTimeoutInMilliSeconds(1000);
            request.SetConnectTimeoutInMilliSeconds(1000);
            return vodClient.GetAcsResponse(request);
        }
        ```

    3.  使用上传凭证和地址初始化OSS客户端（注意需要先Base64解码并Json Decode再传入）。

        示例代码如下所示：

        ```
        public static OssClient InitOssClient(JObject uploadAuth, JObject uploadAddress) 
        {
            string endpoint = uploadAddress.GetValue("Endpoint").ToString();
            string accessKeyId = uploadAuth.GetValue("AccessKeyId").ToString();
            string accessKeySecret = uploadAuth.GetValue("AccessKeySecret").ToString();
            string securityToken = uploadAuth.GetValue("SecurityToken").ToString();
            return new OssClient(endpoint, accessKeyId, accessKeySecret, securityToken);
        }
        ```

    4.  上传本地文件。

        示例代码如下所示：

        ```
        public static void UploadLocalFile(OssClient ossClient, JObject uploadAddress, string localFile) 
        {
            string bucketName = uploadAddress.GetValue("Bucket").ToString();
            string objectName = uploadAddress.GetValue("FileName").ToString();
            ossClient.PutObject(bucketName, objectName, localFile);
        }
        ```

    5.  刷新上传凭证。

        示例代码如下所示：

        ```
        public static RefreshUploadVideoResponse RefreshUploadVideo(DefaultAcsClient vodClient)
        {
            RefreshUploadVideoRequest request = new RefreshUploadVideoRequest();
            request.AcceptFormat = Aliyun.Acs.Core.Http.FormatType.JSON;
            request.VideoId = "VideoId";
            //设置请求超时时间
            request.SetReadTimeoutInMilliSeconds(1000);
            request.SetConnectTimeoutInMilliSeconds(1000);
            return vodClient.GetAcsResponse(request);
        }
        ```

-   执行完整流程（注意捕获异常）。

    示例代码如下所示：

    ```
    //您的AccessKeyId
    string accessKeyId = "<Your AccessKeyId>"; 
    //您的AccessKeySecret
    string accessKeySecret = "<Your AccessKeySecret>";
    //需要上传到VOD的本地视频文件的完整路径，需要包含文件扩展名
    string localFile = "/Users/yours/Video/testVideo.flv";
    try {
        // 初始化VOD客户端并获取上传地址和凭证
        DefaultAcsClient vodClient = InitVodClient(accessKeyId, accessKeySecret);
        CreateUploadVideoResponse createUploadVideoResponse = CreateUploadVideo(vodClient);
        // 执行成功会返回VideoId、UploadAddress和UploadAuth
        String videoId = createUploadVideoResponse.VideoId;
        JObject uploadAuth = JObject.Parse(Base64Decode(createUploadVideoResponse.UploadAuth));
        JObject uploadAddress = JObject.Parse(Base64Decode(createUploadVideoResponse.UploadAddress));
        // 使用UploadAuth和UploadAddress初始化OSS客户端
        OssClient ossClient = InitOssClient(uploadAuth, uploadAddress);
        // 上传文件，注意是同步上传会阻塞等待，耗时与文件大小和网络上行带宽有关
        UploadLocalFile(ossClient, uploadAddress, localFile);
        Console.WriteLine("Put local file succeed, VideoId : " + videoId);
    } 
    catch (Exception e) 
    {
        Console.WriteLine("Put local file fail, ErrorMessage : " + e.Message);
    }
    ```


## Java上传示例

**环境准备**

-   环境要求使用Java 1.8及以上版本。
-   可在终端执行`java -version`命令查看Java版本。

**安装**

在Maven项目中加入依赖项在Maven工程中使用OSS Java SDK，只需在pom.xml中加入相应依赖即可。以2.8.3版本为例，在内加入如下内容：

```
<dependency>
    <groupId>com.aliyun.oss</groupId>
    <artifactId>aliyun-sdk-oss</artifactId>
    <version>2.8.3</version>
</dependency>
```

**说明：** 更多信息，请参见[VOD Java SDK安装](VOD Java SDK安装t1959664.dita#task_1988430)和[OSS Java SDK安装](OSS Java SDK安装t22261.dita#OSS_SDK_0002)。

**参考代码**

-   定义核心步骤的函数：
    1.  使用AK初始化VOD客户端。

        示例代码如下所示：

        ```
        public static DefaultAcsClient initVodClient(String accessKeyId, String accessKeySecret) throws ClientException {
            // 根据点播接入服务所在的Region填写，例如：接入服务在上海，则填cn-shanghai；其他区域请参见[点播中心和访问域名](/cn.zh-CN/开发指南/点播中心和访问域名.md)。
            String regionId = "cn-shanghai";
            DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
            DefaultAcsClient client = new DefaultAcsClient(profile);
            return client;
        }
        ```

    2.  获取视频上传地址和凭证。

        示例代码如下所示：

        ```
        public static CreateUploadVideoResponse createUploadVideo(DefaultAcsClient vodClient) {
            CreateUploadVideoRequest request = new CreateUploadVideoRequest();
            request.setFileName("vod_test.mp4");
            request.setTitle("this is title");
            //request.setDescription("this is desc");
            //request.setTags("tag1,tag2");
            //request.setCoverURL("http://vod.aliyun.com/test_cover_url.jpg");
            //request.setCateId(-1L);
            //request.setTemplateGroupId("");
            //request.setWorkflowId("");
            //request.setStorageLocation("");
            //request.setAppId("app-1000000");
            //设置请求超时时间
            request.setSysReadTimeout(1000);
            request.setSysConnectTimeout(1000);
            return vodClient.getAcsResponse(request);
        }
        ```

    3.  使用上传凭证和地址初始化OSS客户端（注意需要先Base64解码并Json Decode再传入）。

        示例代码如下所示：

        ```
        public static OSSClient initOssClient(JSONObject uploadAuth, JSONObject uploadAddress) {
            String endpoint = uploadAddress.getString("Endpoint");
            String accessKeyId = uploadAuth.getString("AccessKeyId");
            String accessKeySecret = uploadAuth.getString("AccessKeySecret");
            String securityToken = uploadAuth.getString("SecurityToken");
            return new OSSClient(endpoint, accessKeyId, accessKeySecret, securityToken);
        }
        ```

    4.  上传本地文件。

        示例代码如下所示：

        ```
        public static void uploadLocalFile(OSSClient ossClient, JSONObject uploadAddress, String localFile){
            String bucketName = uploadAddress.getString("Bucket");
            String objectName = uploadAddress.getString("FileName");
            File file = new File(localFile);
            ossClient.putObject(bucketName, objectName, file);
        }
        ```

    5.  刷新上传凭证。

        示例代码如下所示：

        ```
        public static RefreshUploadVideoResponse refreshUploadVideo(DefaultAcsClient vodClient) throws ClientException {
            RefreshUploadVideoRequest request = new RefreshUploadVideoRequest();
            request.setAcceptFormat(FormatType.JSON);
            request.setVideoId("VideoId");
            //设置请求超时时间
            request.setSysReadTimeout(1000);
            request.setSysConnectTimeout(1000);
            return vodClient.getAcsResponse(request);
        }
        ```

-   执行完整流程（注意捕获异常）。

    示例代码如下所示：

    ```
    import com.alibaba.fastjson.JSONObject;
    import com.aliyun.oss.OSSClient;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.http.FormatType;
    import com.aliyuncs.profile.DefaultProfile;
    import com.aliyuncs.vod.model.v20170321.CreateUploadVideoRequest;
    import com.aliyuncs.vod.model.v20170321.CreateUploadVideoResponse;
    import com.aliyuncs.vod.model.v20170321.RefreshUploadVideoRequest;
    import com.aliyuncs.vod.model.v20170321.RefreshUploadVideoResponse;
    import org.apache.commons.codec.binary.Base64;
    import java.io.File;
    public class UploadDemo {
        public static void main(String[] argv) {
            //您的AccessKeyId
            String accessKeyId = "<Your AccessKeyId>";
            //您的AccessKeySecret
            String accessKeySecret = "<Your AccessKeySecret>";
            //需要上传到VOD的本地视频文件的完整路径，需要包含文件扩展名
            String localFile = "/Users/yours/Video/testVideo.flv";
            try {
                // 初始化VOD客户端并获取上传地址和凭证
                DefaultAcsClient vodClient = initVodClient(accessKeyId, accessKeySecret);
                CreateUploadVideoResponse createUploadVideoResponse = createUploadVideo(vodClient);
                // 执行成功会返回VideoId、UploadAddress和UploadAuth
                String videoId = createUploadVideoResponse.getVideoId();
                JSONObject uploadAuth = JSONObject.parseObject(decodeBase64(createUploadVideoResponse.getUploadAuth()));
                JSONObject uploadAddress = JSONObject.parseObject(decodeBase64(createUploadVideoResponse.getUploadAddress()));
                // 使用UploadAuth和UploadAddress初始化OSS客户端
                OSSClient ossClient = initOssClient(uploadAuth, uploadAddress);
                // 上传文件，注意是同步上传会阻塞等待，耗时与文件大小和网络上行带宽有关
                uploadLocalFile(ossClient, uploadAddress, localFile);
                System.out.println("Put local file succeed, VideoId : " + videoId);
            } catch (Exception e) {
                System.out.println("Put local file fail, ErrorMessage : " + e.getLocalizedMessage());
            }
        }
    }
    ```


## Demo下载

|形式|源码|更多参考信息|
|--|--|------|
|PHP上传Demo|[PHP版上传Demo源码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1510043384229/vod-php-upload-demo-1.0.1.zip?spm=a2c4g.11186623.2.79.627e4eafSZjXWo&file=vod-php-upload-demo-1.0.1.zip)|[OSS-PHP-SDK上传文件](OSS-PHP-SDK上传文件t22358.dita#concept_32103_zh)|
|GO上传Demo|[GO版上传Demo源码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1550544147777/SimpleUpload.go?spm=a2c4g.11186623.2.81.627e4eafSZjXWo&file=SimpleUpload.go)|[OSS-Go-SDK上传文件](OSS-Go-SDK上传文件t22397.dita#concept_32147_zh)|
|.NET上传Demo|[.NET版上传Demo源码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1556179514218/VodUploadOssDemo.cs?spm=a2c4g.11186623.2.87.2c134eaf9gJJ3q&file=VodUploadOssDemo.cs)|[OSS-.NET-SDK上传文件](OSS-.NET-SDK上传文件t22478.dita#concept_32090_zh)|
|Java上传Demo|[Java版上传Demo源码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1562322405607/UploadDemo.java?spm=a2c4g.11186623.2.85.627e4eafSZjXWo&file=UploadDemo.java)|[OSS-Java-SDK上传文件](OSS-Java-SDK上传文件t22268.dita#concept_32013_zh)|

**说明：** 其它语言上传SDK及Demo下载请参见[上传SDK下载](/cn.zh-CN/SDK下载/SDK下载.md)。

