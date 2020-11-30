# iOS端集成

您可以阅读本文，了解趣视频Demo的iOS端集成操作。

开发前的环境要求如下表所示。

|类别|说明|
|--|--|
|系统版本|iOS 9.0 及以上。|
|iPhone设备|支持iPhone5及以上。|
|CPU架构支持|真机支持ARM64、ARMV7 、ARMV7s。暂不支持模拟器。|
|Xcode版本|支持Xcode9.0及以上，下载[Xcode](https://apps.apple.com/cn/app/xcode/id497799835?mt=12)。|

您需要先集成并启动服务端，具体操作，请参见[服务端集成](/cn.zh-CN/趣视频解决方案/服务端集成.md)。

## 操作步骤

1.  下载趣视频Demo并解压。趣视频iOS端下载，请参见[SDK下载](/cn.zh-CN/SDK下载/SDK下载.md)。

    目录结构说明

    ```
    - demo  
          - |- AlivcCommon      #公用组件
          - |- AlivcCore        #短视频公用组件
          - |- AlivcCrop        #短视频裁剪组件
          - |- AlivcEdit        #短视频编辑组件
          - |- AlivcRecord      #短视频录制组件
          - |- AlivcSmartVideo  #趣视频组件
          - |- AliyunVideoClient_Entrance    #短视频主工程
    - doc  #文档相关
    - sdk  #项目使用的SDK，也可以根据需要手动导入
    - xxxReleaseNote.md  #说明
    ```

2.  工程导入与配置。

    1.  打开**Xcode**，单击**Open a project or file**，双击打开demo目录下的AliyunVideoClient\_Entrance.xcworkspace文件。

        ![打开](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7818266061/p186080.png)

    2.  配置服务端地址。

        文件路径：demo/AlivcCommon/AlivcCommon/Classes/Macro/AlivcDefine.m。

        修改文件中的`kAlivcQuUrlString`变量，设置为完成趣视频服务端集成的云服务器（ECS）公网IP地址，并添加端口号8080。

        示例：http://<云服务器（ECS）公网IP地址\> :8080。

        ![Ip地址](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8818266061/p186081.png)

3.  修改Bundle Identifier和开发者证书。

    **说明：**

    Bundle Identifier改成为`com.<公司名>.<项目名>`，避免由于Bundle已被注册从而运行失败。

    Bundle Identifier需定义在服务端配置文件的package\_name中。若没有在服务端配置Bundle Identifier，会导致iOS端App运行时被服务端包名拦截器拦截，导致请求出现403错误报错（Request failed:forbidden） 。服务端配置Bundle Identifier，具体操作，请参见[服务端集成](/cn.zh-CN/趣视频解决方案/服务端集成.md)。

    **General**选项卡中修改。

    ![修改General](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8818266061/p186082.png)

    **Sign & Capabilities**选项卡中修改。

    ![Sign](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8818266061/p186083.png)

4.  在**Sign & Capabilities**选项卡，勾选**Automatically manage signing**，在下方选择自己的**Team**。

    1.  选择**Team**。

        ![选择Team](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2457036061/p184852.png)

    2.  若以前没添加过账号，单击**Add an Account**添加。

        ![添加](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2457036061/p184855.png)

    3.  完成账号添加。

        ![添加Team](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3457036061/p184858.png)

    4.  在Team里选择新创建的账号即可，并且在完成签名后确保下方没有报错提示。

5.  工程编译运行。

    1.  选择运行Target为AlivcVoiceCallSoloClient，将一台IOS真机设备使用数据线与电脑链接，在**Xcode**中选择相应的真机设备，真机在设置中打开开发者模式。

    2.  单击**build and run**按钮编译。

    ![编译](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9818266061/p186084.png)


