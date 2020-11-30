# Android端集成

您可以阅读本文，了解趣视频Demo的Android端集成操作。

开发前的环境要求如下表所示。

|类别|说明|
|--|--|
|系统版本|支持Android 4.3及以上。|
|API版本|不低于18。|
|CPU架构|真机支持ARM64、ARMV7。暂不支持模拟器。|
|Android Studio版本支持|支持Android Studio3.1及以上。下载[Android Studio](https://developer.android.google.cn/studio/)。|

您需要先集成并启动服务端，具体操作，请参见[服务端集成](/intl.zh-CN/趣视频解决方案/服务端集成.md)。

## 操作步骤

1.  下载趣视频Demo并解压。趣视频Android端下载，请参见[SDK下载](/intl.zh-CN/SDK下载/SDK下载.md)。

    目录结构说明

    ```
    - demo  
      - ApsaraVideoQuVideo
          - |- AlivcLittleVideo     #主要包含趣视频业务相关代码
          - |- AliyunCrop           #裁剪相关模块，主要包含裁剪界面的实现代码
          - |- AliyunEditor         #编辑相关模块，主要包含编辑界面的实现代码
          - |- AliyunFileDownLoader #资源下载、数据库相关模块
          - |- AliyunRecorder       #录制界面相关代码
          - |- AliyunSVideoBase     #主要为一些自定义view 、工具类等
          - |- AliyunSvideoMusic    #音乐界面相关模块
          - |- AliyunVideoCommon    #公共模块，主要是一些工具类     
          - |- thirdparty-lib       #主要包含Demo中所需要的第三方依赖
    - SDK  #项目使用的SDK，也可以根据需要手动导入
    - xxxReleaseNote.md  #说明
    ```

2.  工程导入与配置。

    1.  打开**Android Studio**，单击**Open an existing Android Studio project**，并选择Android端源码根目录下的./demo/ApsaraVideoQuVideo文件夹。

        ![文件目录](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7239166061/p186077.png)

    2.  配置服务端地址。

        文件路径：AlivcLittleVideo/src/mian/java/com/aliyun/apsara/alivclittlevideo/constantsAlivcLittleServerApiConstants.java。

        修改文件中的`BASE_URL`变量，设置为完成趣视频服务端集成的云服务器（ECS）公网IP地址，并添加端口号8080。

        示例：http://<云服务器（ECS）公网IP地址\> :8080。

        ![修改文件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7239166061/p186078.png)

3.  工程编译运行。

    1.  将一台Android真机设备（需在系统设置中开启开发者模式和USB调试功能）使用数据线与电脑连接，在手机端同意调试后在Android Studio中选择接入的真机设备。

    2.  单击**build and run**按钮编译，Android真机会安装并启动趣视频App。

    ![编译](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7239166061/p186079.png)


