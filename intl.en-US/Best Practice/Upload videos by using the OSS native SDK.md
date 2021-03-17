# Upload videos by using the OSS native SDK

## Scenario

ApsaraVideo VOD supports multiple [upload methods](https://help.aliyun.com/document_detail/55396.html?spm=a2c4g.11186623.2.64.47154eaf9iu1C0#h2-u4E0Au4F20u65B9u5F0F2), including the [client upload](https://help.aliyun.com/document_detail/55398.html) and [server upload](https://help.aliyun.com/document_detail/55399.html). However, ApsaraVideo VOD may not provide the upload SDK in your required language such as Go. In this case, you can upload videos by using the OSS native SDK.

## Prerequisites

Before you read this topic, check whether the upload SDK is provided in your required language. ApsaraVideo VOD provides the following SDKs:

-   Upload SDK for clients:
    -   [Upload SDK for Android](https://help.aliyun.com/document_detail/62955.html)
    -   [Upload SDK for iOS](https://help.aliyun.com/document_detail/62954.html)
    -   [Upload SDK for web](https://help.aliyun.com/document_detail/52204.html)
-   Upload SDK for servers:
    -   [Upload SDK for Java](https://help.aliyun.com/document_detail/53406.html)
    -   [Upload SDK for Python](https://help.aliyun.com/document_detail/64148.html)
    -   [Upload SDK for PHP](https://help.aliyun.com/document_detail/100976.html)
    -   [Upload SDK for C or C++](https://help.aliyun.com/document_detail/102770.html)

**Note:** You can also go to the [SDK download](https://help.aliyun.com/document_detail/51992.html) page to download SDKs and demos. If no upload SDK is provided in your required language, you can continue with this topic for development.

## Preparations

-   Activate and configure ApsaraVideo VOD.
-   Obtain the AccessKey of your Alibaba Cloud account and the upload permission. For more information, see [Overview](https://help.aliyun.com/document_detail/57055.html).

## Upload procedure

![Upload procedure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9668495161/p180094.png)

1.  Obtain the upload URL and credential. For more information, see [Upload URL and credential](https://help.aliyun.com/document_detail/55397.html?spm=a2c4g.11186623.2.60.627e4eafSZjXWo).

    **Note:** A media asset record is created and a video ID is returned in this step. Keep the video ID for subsequent operations. For example, you can play a video, manage a video, and use AI to process a video based on the video ID.

2.  Parse the values of the returned UploadAddress and UploadAuth parameters to obtain the Object Storage Service \(OSS\) upload URL and authorization information. For more information, see [Upload URL and credential](https://help.aliyun.com/document_detail/55397.html?spm=a2c4g.11186623.2.61.627e4eafSZjXWo#UploadAuthDecode).
3.  Call OSS SDK to upload video files to the specified bucket by using Security Token Service \(STS\)-based authentication. Use the decoded upload URL and authentication information rather than your AccessKey for initialization.

## Code implementation

-   To implement the core code, perform the following four steps:
    1.  Use the AccessKey to initialize the ApsaraVideo VOD client.
    2.  Obtain the upload URL and credential for a video.
    3.  Use the upload URL and credential to initialize the OSS client.
    4.  Upload an on-premises file.
-   You can call the operation in the SDK that is provided by ApsaraVideo VOD to obtain the upload URL and credential. For more information, see [Upload URL and credential](https://help.aliyun.com/document_detail/55397.html?spm=a2c4g.11186623.2.62.627e4eafSZjXWo#h2-u83B7u53D6u65B9u5F0F4).
-   OSS provides SDKs in the following languages for you to upload videos on a server:
    -   OSS SDK for .NET
    -   OSS SDK for C
    -   OSS SDK for Go
    -   OSS SDK for Ruby
    -   OSS SDK for Java

## Upload demo for PHP

**Environment preparation**

-   Install PHP 5.3 or later. You can run the php -v command to view the current PHP version.
-   Install the cURL extension. You can run the php -m command to check whether the cURL extension is installed.

**Installation**

1.  Create an empty folder that is named aliyun-php-sdk in your PHP project.
2.  Download the entire source code from [aliyun-openapi-php-sdk](https://github.com/aliyun/aliyun-openapi-php-sdk?spm=a2c4g.11186623.2.68.627e4eafSZjXWo). Decompress the downloaded package and copy the aliyun-php-sdk-core and aliyun-php-sdk-vod folders to the aliyun-php-sdk directory.
3.  Download the latest source code of OSS SDK for PHP from [aliyun-oss-php-sdk](https://github.com/aliyun/aliyun-oss-php-sdk/releases?spm=a2c4g.11186623.2.69.627e4eafSZjXWo). Decompress the downloaded package. Then, add the decompressed folder to the aliyun-php-sdk directory. For example, if [aliyun-oss-php-sdk-2.2.4.zip](https://github.com/aliyun/aliyun-oss-php-sdk/archive/v2.2.4.zip?spm=a2c4g.11186623.2.70.627e4eafSZjXWo&file=v2.2.4.zip) is downloaded and decompressed, the decompressed folder is aliyun-oss-php-sdk-2.2.4.
4.  Open the aliyun-php-sdk/aliyun-php-sdk-core/Config.php file, find "//config sdk auto load path.", and then add the following code below this line:

    ```
    Autoloader::addAutoloadPath("aliyun-php-sdk-vod");
    ```

5.  Reference the files of ApsaraVideo VOD and OSS in the code.

    The following code provides an example:

    ```
    require_once './aliyun-php-sdk/aliyun-php-sdk-core/Config.php';   // Assume that your source code file is in the aliyun-php-sdk directory.
    require_once './aliyun-php-sdk/aliyun-oss-php-sdk-2.2.4/autoload.php';
    use vod\Request\V20170321 as vod;
    use OSS\OssClient;
    use OSS\Core\OssException;
    ```

    **Note:** For more information, see the topics about the installation of ApsaraVideo VOD SDK for PHP and OSS SDK for PHP.


**Reference code**

-   Define the functions of the core steps:
    1.  Use the AccessKey to initialize the ApsaraVideo VOD client.

        The following code provides an example:

        ```
        function init_vod_client($accessKeyId, $accessKeySecret) {
            $regionId = 'cn-shanghai';     // Specify the access region of ApsaraVideo VOD, for example, cn-shanghai.
            $profile = DefaultProfile::getProfile($regionId, $accessKeyId, $accessKeySecret);
            return new DefaultAcsClient($profile);
        }
        ```

    2.  Obtain the upload URL and credential for a video.

        The following code provides an example:

        ```
        function create_upload_video($vodClient) {
            $request = new vod\CreateUploadVideoRequest();
            $request->setTitle("Video title"); // Required. The title of the video.
            $request->setFileName("File Name. mov"); // Required. The name of the source video file, which must contain a file name extension.
            $request->setDescription("video description"); // Optional. The description of the source video file.
            $request->setCoverURL("http://img.alicdn.com/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png "); // Optional. The customized thumbnail.
            $request->setTags("Tag 1,Tag 2"); // Optional. The tags of the video. Separate multiple video tags with commas (,).
            return $vodClient->getAcsResponse($request);
        }
        ```

    3.  Use the upload URL and credential to initialize the OSS client. Before you pass the parameters of the upload URL and credential, decode them in the Base64 format and then in the JSON format.

        The following code provides an example:

        ```
        function init_oss_client($uploadAuth, $uploadAddress) {
            $ossClient = new OssClient($uploadAuth['AccessKeyId'], $uploadAuth['AccessKeySecret'], $uploadAddress['Endpoint'], 
                false, $uploadAuth['SecurityToken']);
            $ossClient->setTimeout(86400*7);   // Set the request timeout period, in seconds. The default value is 5,184,000. We recommend that you set the parameter to a large value because the upload of large files takes a long time.
            $ossClient->setConnectTimeout(10);  // Specify the connection timeout period, in seconds. The default value is 10.
            return $ossClient;
        }
        ```

        **Note:** If an error occurs due to improper Secure Sockets Layer \(SSL\) configuration, replace https with http before you initialize the OSS Client. For example, "cURL error: SSL certificate problem" appears.

        ```
        $uploadAddress['Endpoint'] = str_replace("https:", "http:", $uploadAddress['Endpoint']);
        ```

    4.  Upload an on-premises file.

        The following code provides an example:

        ```
        function upload_local_file($ossClient, $uploadAddress, $localFile) {
            return $ossClient->uploadFile($uploadAddress['Bucket'], $uploadAddress['FileName'], $localFile);
        }
        ```

    5.  Update the upload credential.

        The following code provides an example:

        ```
        function refresh_upload_video($vodClient, $videoId) {
            $request = new vod\RefreshUploadVideoRequest();
            $request->setVideoId($videoId);
            return $vodClient->getAcsResponse($request);
        }
        ```

-   Execute the entire process. Capture exceptions during the execution.

    The following code provides an example:

    ```
    $accessKeyId = '<AccessKeyId>';                    // Your AccessKey ID.
    $accessKeySecret = '<AccessKeySecret>';            // Your AccessKey secret.
    $localFile = '/Users/yours/Video/testVideo.flv';   // The full path of the on-premises file that you want to upload to ApsaraVideo VOD.
    try {
        // Initialize the ApsaraVideo VOD client and obtain the upload URL and credential.
        $vodClient = init_vod_client($accessKeyId, $accessKeySecret);
        $createRes = create_upload_video($vodClient);
        // If the execution is successful, VideoId, UploadAddress, and UploadAuth are returned.
        $videoId = $createRes->VideoId;
        $uploadAddress = json_decode(base64_decode($createRes->UploadAddress), true);
        $uploadAuth = json_decode(base64_decode($createRes->UploadAuth), true);
        // Use UploadAuth and UploadAddress to initialize the OSS client.
        $ossClient = init_oss_client($uploadAuth, $uploadAddress);
        // Upload the file. Take note that multiple parts are uploaded in parallel. The system starts to upload the next file only when all parts of the current file have been uploaded. The consumed time depends on the file size and upstream bandwidth.
        //$result = upload_local_file($ossClient, $uploadAddress, $localFile);
        $result = multipart_upload_file($ossClient, $uploadAddress, $localFile);
        printf("Succeed, VideoId: %s", $videoId);
    } catch (Exception $e) {
        // var_dump($e);
        printf("Failed, ErrorMessage: %s", $e->getMessage());
    }
    ```


## Upload demo for Go

**Environment preparation**

Install Go 1.7 or later. You can visit the official website of Go to download an appropriate version.

**Installation**

-   Run the go get command to install the upload SDK for Go.

    ```
    go get -u github.com/aliyun/alibaba-cloud-sdk-go/sdk
    ```

    **Note:**

    -   No messages are displayed during the installation. Please wait. If the installation times out, run the command again.
    -   If the src/github.com/aliyun/alibaba-cloud-sdk-go/services/vod subdirectory appears in the directory that is specified by GOPATH, the SDK is installed.
-   Run the glide command to install the upload SDK for Go.

    ```
    glide get github.com/aliyun/alibaba-cloud-sdk-go
    ```

-   Define the functions of the core steps:
    1.  Use the AccessKey to initialize the ApsaraVideo VOD client.

        The following code provides an example:

        ```
        func InitVodClient(accessKeyId string, accessKeySecret string) (client *vod.Client, err error) {
            // Specify the access region of ApsaraVideo VOD.
            regionId := "cn-shanghai"
            // Create an authorization object.
            credential := &credentials.AccessKeyCredential{
                accessKeyId,
                accessKeySecret,
            }
            // Customize configuration.
            config := sdk.NewConfig()
            config.AutoRetry = true      // Specify whether the connection is automatically retried upon a connection failure.
            config.MaxRetryTime = 3 // The maximum number of retries allowed.
            config.Timeout = 3000000000  // The connection timeout period, in nanoseconds. The default value is 3 seconds.
            // Create a vodClient instance.
            return vod.NewClientWithOptions(regionId, config, credential)
        }
        ```

    2.  Obtain the upload URL and credential for a video.

        The following code provides an example:

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

    3.  Use the upload URL and credential to initialize the OSS client. Before you pass the parameters of the upload URL and credential, decode them in the Base64 format and then in the JSON format.

        The following code provides an example:

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

    4.  Upload an on-premises file.

        The following code provides an example:

        ```
        func UploadLocalFile(client *oss.Client, uploadAddressDTO UploadAddressDTO, localFile string) {
            // Obtain the bucket.
            bucket, err := client.Bucket(uploadAddressDTO.Bucket)
            if err ! = nil {
                fmt.Println("Error:", err)
                os.Exit(-1)
            }
            // Upload an on-premises file.
            err = bucket.PutObjectFromFile(uploadAddressDTO.FileName, localFile)
            if err ! = nil {
                fmt.Println("Error:", err)
                os.Exit(-1)
            }
        }
        ```

    5.  Update the upload credential.

        The following code provides an example:

        ```
        func MyRefreshUploadVideo(client *vod.Client) (response *vod.RefreshUploadVideoResponse, err error) {
            request := vod.CreateRefreshUploadVideoRequest()
            request.VideoId = ""
            request.AcceptFormat = "JSON"
            return client.RefreshUploadVideo(request)
        }
        ```

-   Execute the entire process. Capture exceptions during the execution.

    The following code provides an example:

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
        var accessKeyId string = "<AccessKeyId>";                    // Your AccessKey ID.
        var accessKeySecret string = "<AccessKeySecret>";            // Your AccessKey secret.
        var localFile string = "/Users/yours/Video/testVideo.flv";   // The full path of the on-premises file that you want to upload to ApsaraVideo VOD.
        // Initialize the ApsaraVideo VOD client and obtain the upload URL and credential.
        var vodClient, initVodClientErr = InitVodClient(accessKeyId, accessKeySecret)
        if initVodClientErr ! = nil {
            fmt.Println("Error:", initVodClientErr)
            return
        }
        // Obtain the upload URL and credential.
        var response, createUploadVideoErr = MyCreateUploadVideo(vodClient)
        if createUploadVideoErr ! = nil {
            fmt.Println("Error:", createUploadVideoErr)
            return
        }
        // If the execution is successful, VideoId, UploadAddress, and UploadAuth are returned.
        var videoId = response.VideoId
        var uploadAuthDTO UploadAuthDTO
        var uploadAddressDTO UploadAddressDTO
        var uploadAuthDecode, _ = base64.StdEncoding.DecodeString(response.UploadAuth)
        var uploadAddressDecode, _ = base64.StdEncoding.DecodeString(response.UploadAddress)
        json.Unmarshal(uploadAuthDecode, &uploadAuthDTO)
        json.Unmarshal(uploadAddressDecode, &uploadAddressDTO)
        // Use UploadAuth and UploadAddress to initialize the OSS client.
        var ossClient, _ = InitOssClient(uploadAuthDTO, uploadAddressDTO)
        // Upload the file. Take note that multiple parts are uploaded in parallel. The system starts to upload the next file only when all parts of the current file have been uploaded. The consumed time depends on the file size and upstream bandwidth.
        UploadLocalFile(ossClient, uploadAddressDTO, localFile)
        //MultipartUploadFile(ossClient, uploadAddressDTO, localFile)
        fmt.Println("Succeed, VideoId:", videoId)
    }
    ```


## Upload demo for .NET

**Environment preparation**

-   Install .NET Framework 4.6.1 or later.
-   Install .NET Standard 2.0 or later.

**Note:** For more information, see environment requirements.

**Installation**

-   Install the SDK by using NuGet. In Solution Explorer, right-click your project and select Manage NuGet Packages. In NuGet Package Manager, click the Browse tab, enter aliyun-net-sdk-core, and then install the latest version of the module. Repeat the preceding steps to install the aliyun-net-sdk-vod module.
-   Install the SDK by using .NET Core command-line interface \(CLI\).

    The following code provides an example:

    ```
    dotnet add package aliyun-net-sdk-core
    dotnet add package aliyun-net-sdk-vod
    ```

    **Note:** For more information, see the topics about the installation of ApsaraVideo VOD SDK for .NET and OSS SDK for .NET.


**Reference code**

-   Define the functions of the core steps:
    1.  Use the AccessKey to initialize the ApsaraVideo VOD client.

        The following code provides an example:

        ```
        public static DefaultAcsClient InitVodClient(string accessKeyId, string accessKeySecret)
        {
            // Specify the access region of ApsaraVideo VOD, for example, cn-shanghai.
            string regionId = "cn-shanghai";
            IClientProfile profile = DefaultProfile.GetProfile(regionId, accessKeyId, accessKeySecret);
            return new DefaultAcsClient(profile);
        }
        ```

    2.  Obtain the upload URL and credential for a video.

        The following code provides an example:

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
            // Specify the request timeout period.
            request.SetReadTimeoutInMilliSeconds(1000);
            request.SetConnectTimeoutInMilliSeconds(1000);
            return vodClient.GetAcsResponse(request);
        }
        ```

    3.  Use the upload URL and credential to initialize the OSS client. Before you pass the parameters of the upload URL and credential, decode them in the Base64 format and then in the JSON format.

        The following code provides an example:

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

    4.  Upload an on-premises file.

        The following code provides an example:

        ```
        public static void UploadLocalFile(OssClient ossClient, JObject uploadAddress, string localFile) 
        {
            string bucketName = uploadAddress.GetValue("Bucket").ToString();
            string objectName = uploadAddress.GetValue("FileName").ToString();
            ossClient.PutObject(bucketName, objectName, localFile);
        }
        ```

    5.  Update the upload credential.

        The following code provides an example:

        ```
        public static RefreshUploadVideoResponse RefreshUploadVideo(DefaultAcsClient vodClient)
        {
            RefreshUploadVideoRequest request = new RefreshUploadVideoRequest();
            request.AcceptFormat = Aliyun.Acs.Core.Http.FormatType.JSON;
            request.VideoId = "VideoId";
            // Specify the request timeout period.
            request.SetReadTimeoutInMilliSeconds(1000);
            request.SetConnectTimeoutInMilliSeconds(1000);
            return vodClient.GetAcsResponse(request);
        }
        ```

-   Execute the entire process. Capture exceptions during the execution.

    The following code provides an example:

    ```
    // Your AccessKey ID.
    string accessKeyId = "<Your AccessKeyId>"; 
    // Your AccessKey secret.
    string accessKeySecret = "<Your AccessKeySecret>";
    // The full path of the on-premises file that you want to upload to ApsaraVideo VOD. The file name extension must be included in the path.
    string localFile = "/Users/yours/Video/testVideo.flv";
    try {
        // Initialize the ApsaraVideo VOD client and obtain the upload URL and credential.
        DefaultAcsClient vodClient = InitVodClient(accessKeyId, accessKeySecret);
        CreateUploadVideoResponse createUploadVideoResponse = CreateUploadVideo(vodClient);
        // If the execution is successful, VideoId, UploadAddress, and UploadAuth are returned.
        String videoId = createUploadVideoResponse.VideoId;
        JObject uploadAuth = JObject.Parse(Base64Decode(createUploadVideoResponse.UploadAuth));
        JObject uploadAddress = JObject.Parse(Base64Decode(createUploadVideoResponse.UploadAddress));
        // Use UploadAuth and UploadAddress to initialize the OSS client.
        OssClient ossClient = InitOssClient(uploadAuth, uploadAddress);
        // Upload the file. Take note that multiple parts are uploaded in parallel. The system starts to upload the next file only when all parts of the current file have been uploaded. The consumed time depends on the file size and upstream bandwidth.
        UploadLocalFile(ossClient, uploadAddress, localFile);
        Console.WriteLine("Put local file succeed, VideoId : " + videoId);
    } 
    catch (Exception e) 
    {
        Console.WriteLine("Put local file fail, ErrorMessage : " + e.Message);
    }
    ```


## Upload demo for Java

**Environment preparation**

-   Install Java 1.8 or later.
-   You can run the java -version command to check the Java version.

**Installation**

Add dependencies to a Maven project. To use OSS SDK for Java in a Maven project, you only need to add specific dependencies to the pom.xml file. For example, if you use OSS SDK V2.8.3, add the following content to the pom.xml file:

```
<dependency>
    <groupId>com.aliyun.oss</groupId>
    <artifactId>aliyun-sdk-oss</artifactId>
    <version>2.8.3</version>
</dependency>
```

**Note:** For more information, see the topics about the installation of ApsaraVideo VOD SDK for Java and OSS SDK for Java.

**Reference code**

-   Define the functions of the core steps:
    1.  Use the AccessKey to initialize the ApsaraVideo VOD client.

        The following code provides an example:

        ```
        public static DefaultAcsClient initVodClient(String accessKeyId, String accessKeySecret) throws ClientException {
            // Specify the access region of ApsaraVideo VOD, for example, cn-shanghai. For more information about other access regions, see [VOD centers and access domains] (~~98194~~).
            String regionId = "cn-shanghai";
            DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
            DefaultAcsClient client = new DefaultAcsClient(profile);
            return client;
        }
        ```

    2.  Obtain the upload URL and credential for a video.

        The following code provides an example:

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
            // Specify the request timeout period.
            request.setSysReadTimeout(1000);
            request.setSysConnectTimeout(1000);
            return vodClient.getAcsResponse(request);
        }
        ```

    3.  Use the upload URL and credential to initialize the OSS client. Before you pass the parameters of the upload URL and credential, decode them in the Base64 format and then in the JSON format.

        The following code provides an example:

        ```
        public static OSSClient initOssClient(JSONObject uploadAuth, JSONObject uploadAddress) {
            String endpoint = uploadAddress.getString("Endpoint");
            String accessKeyId = uploadAuth.getString("AccessKeyId");
            String accessKeySecret = uploadAuth.getString("AccessKeySecret");
            String securityToken = uploadAuth.getString("SecurityToken");
            return new OSSClient(endpoint, accessKeyId, accessKeySecret, securityToken);
        }
        ```

    4.  Upload an on-premises file.

        The following code provides an example:

        ```
        public static void uploadLocalFile(OSSClient ossClient, JSONObject uploadAddress, String localFile){
            String bucketName = uploadAddress.getString("Bucket");
            String objectName = uploadAddress.getString("FileName");
            File file = new File(localFile);
            ossClient.putObject(bucketName, objectName, file);
        }
        ```

    5.  Update the upload credential.

        The following code provides an example:

        ```
        public static RefreshUploadVideoResponse refreshUploadVideo(DefaultAcsClient vodClient) throws ClientException {
            RefreshUploadVideoRequest request = new RefreshUploadVideoRequest();
            request.setAcceptFormat(FormatType.JSON);
            request.setVideoId("VideoId");
            // Specify the request timeout period.
            request.setSysReadTimeout(1000);
            request.setSysConnectTimeout(1000);
            return vodClient.getAcsResponse(request);
        }
        ```

-   Execute the entire process. Capture exceptions during the execution.

    The following code provides an example:

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
            // Your AccessKey ID.
            String accessKeyId = "<Your AccessKeyId>";
            // Your AccessKey secret.
            String accessKeySecret = "<Your AccessKeySecret>";
            // The full path of the on-premises file that you want to upload to ApsaraVideo VOD. The file name extension must be included in the path.
            String localFile = "/Users/yours/Video/testVideo.flv";
            try {
                // Initialize the ApsaraVideo VOD client and obtain the upload URL and credential.
                DefaultAcsClient vodClient = initVodClient(accessKeyId, accessKeySecret);
                CreateUploadVideoResponse createUploadVideoResponse = createUploadVideo(vodClient);
                // If the execution is successful, VideoId, UploadAddress, and UploadAuth are returned.
                String videoId = createUploadVideoResponse.getVideoId();
                JSONObject uploadAuth = JSONObject.parseObject(decodeBase64(createUploadVideoResponse.getUploadAuth()));
                JSONObject uploadAddress = JSONObject.parseObject(decodeBase64(createUploadVideoResponse.getUploadAddress()));
                // Use UploadAuth and UploadAddress to initialize the OSS client.
                OSSClient ossClient = initOssClient(uploadAuth, uploadAddress);
                // Upload the file. Take note that multiple parts are uploaded in parallel. The system starts to upload the next file only when all parts of the current file have been uploaded. The consumed time depends on the file size and upstream bandwidth.
                uploadLocalFile(ossClient, uploadAddress, localFile);
                System.out.println("Put local file succeed, VideoId : " + videoId);
            } catch (Exception e) {
                System.out.println("Put local file fail, ErrorMessage : " + e.getLocalizedMessage());
            }
        }
    }
    ```


## Demo download

|Language|Source code|References|
|--------|-----------|----------|
|Upload demo for PHP|[Source code of the upload demo for PHP](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1510043384229/vod-php-upload-demo-1.0.1.zip?spm=a2c4g.11186623.2.79.627e4eafSZjXWo&file=vod-php-upload-demo-1.0.1.zip)|[OSS SDK for PHP](https://help.aliyun.com/document_detail/32103.html?spm=a2c4g.11186623.2.80.627e4eafSZjXWo)|
|Upload demo for Go|[Source code of the upload demo for Go](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1550544147777/SimpleUpload.go?spm=a2c4g.11186623.2.81.627e4eafSZjXWo&file=SimpleUpload.go)|[OSS SDK for Go](https://help.aliyun.com/document_detail/32147.html?spm=a2c4g.11186623.2.82.627e4eafSZjXWo)|
|Upload demo for .NET|[Source code of the upload demo for .NET](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1556179514218/VodUploadOssDemo.cs?spm=a2c4g.11186623.2.87.2c134eaf9gJJ3q&file=VodUploadOssDemo.cs)|[OSS SDK for .NET](https://help.aliyun.com/document_detail/32090.html?spm=a2c4g.11186623.2.88.2c134eaf9gJJ3q)|
|Upload demo for Java|[Source code of the upload demo for Java](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/61388/cn_zh/1562322405607/UploadDemo.java?spm=a2c4g.11186623.2.85.627e4eafSZjXWo&file=UploadDemo.java)|[OSS SDK for Java](https://help.aliyun.com/document_detail/32008.html?spm=a2c4g.11186623.2.86.627e4eafSZjXWo)|

**Note:** For more information about the upload SDKs in other languages and demo download links, see [SDK download](https://help.aliyun.com/document_detail/51992.html?spm=a2c4g.11186623.2.87.627e4eafSZjXWo).

