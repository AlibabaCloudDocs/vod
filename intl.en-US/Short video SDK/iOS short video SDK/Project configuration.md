# Project configuration

This topic shows you how to integrate the short video SDK for iOS in pod mode and manually integrate the SDK.

Required environments are prepared. The following table describes the required environments for development.

|Environment|Supported version|
|-----------|-----------------|
|Android|iOS 9.0 and later.|
|macOS High Sierra|macOS High Sierra 10.13 and later.|
|Xcode|Xcode 9.0 and later. To download Xcode, visit [Mac App Store](https://apps.apple.com/cn/app/xcode/id497799835?mt=12).|

## SDK reference

For more information about the documents in Chinese, see [SDK Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/iOS_cn/index.html).

For more information about the documents in English, see [SDK Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/iOS_en/index.html).

## SDK editions

The short video SDK has the following three editions: Basic Edition, Standard Edition, and Professional Edition. The three editions use the same framework name AliyunVideoSDKPro.framework.

-   Basic Edition supports only the recording and cropping features.
-   Professional Edition and Standard Edition support all features. However, advanced features of the Standard Edition must be separately authorized.

## Integrate the SDK in pod mode \(Recommended\)

Procedure

1.  Add dependencies to the Podfile file. The following table describes the dependencies to be added for different editions of SDKs.

    |Edition|Dependency to be added to the Podfile file|
    |-------|------------------------------------------|
    |Professional Edition|    ```
pod 'AliyunVideoSDKPro', '3.20.0'
pod 'QuCore-ThirdParty', '3.15.0'
pod 'AlivcConan', '1.0.3'
pod 'VODUpload'
pod 'AliyunOSSiOS'
    ``` |
    |Standard Edition|    ```
pod 'AliyunVideoSDKStd', '3.20.0'
pod 'QuCore-ThirdParty', '3.15.0'
pod 'AlivcConan', '1.0.3'
pod 'VODUpload'
pod 'AliyunOSSiOS'
    ``` |
    |Basic Edition|    ```
pod 'AliyunVideoSDKBasic', '3.20.0'
pod 'QuCore-ThirdParty', '3.15.0'
pod 'AlivcConan', '1.0.3'
pod 'VODUpload'
pod 'AliyunOSSiOS'
    ``` |

2.  Update the pod repository.

    ```
    pod repo update
    ```

3.  Install the pods.

    ```
    pod install
    ```


**Note:** Make sure that you can access and update the pod repository over the network. After the pods are installed, check whether the framework versions are the latest, as listed on the Alibaba Cloud international site \(alibabacloud.com\).

## Manually integrate the SDK \(Not recommended\)

To manually integrate the SDK, you must download packages of the latest release from GitHub, including six frameworks and one bundle resource package.

|Name|Type|Description|Download link|
|----|----|-----------|-------------|
|AliyunVideoSDKPro|Static framework|Short video SDK|[Professional Edition](https://github.com/aliyunvideo/AliyunVideoSDKPro/releases) [Standard Edition](https://github.com/aliyunvideo/AliyunVideoSDKStd/releases) [Basic Edition](https://github.com/aliyunvideo/AliyunVideoSDKBasic/releases)|
|AliyunVideoCore|Dynamic framework|Short video SDK|[Professional Edition](https://github.com/aliyunvideo/AliyunVideoSDKPro/releases) [Standard Edition](https://github.com/aliyunvideo/AliyunVideoSDKStd/releases) [Basic Edition](https://github.com/aliyunvideo/AliyunVideoSDKBasic/releases)|
|AliyunVideoSDKPro.bundle|Resource package|Short video SDK|[Resource package that is required only by Professional Edition](https://github.com/aliyunvideo/AliyunVideoSDKPro/releases)|
|alivcffmpeg|Dynamic framework|FFmpeg framework|[Download link on GitHub](https://github.com/aliyunvideo/QuCore-ThirdParty/releases)|
|AlivcConan|Dynamic framework|Tool framework|[Download link on GitHub](https://github.com/aliyunvideo/AlivcConanSDK/releases)|
|VODUpload|Static framework|Upload framework of ApsaraVideo VOD|[Download link on GitHub](https://github.com/aliyunvideo/VODUpload/releases)|
|AliyunOSSiOS|Static framework|OSS upload framework|[Download link on GitHub](https://github.com/aliyun/aliyun-oss-ios-sdk/releases)|

In the preceding frameworks, AliyunVideoCore, alivcffmpeg, and AlivcConan are dynamic frameworks. When you manually integrate and release dynamic frameworks, take note of the following points:

1.  To add a dynamic framework, select the target. Then, add the dynamic framework in the **Embedded Binaries** section of the **General** tab.
2.  To submit an application to App Store, you must strip dynamic frameworks of the x86-based simulator architecture. Otherwise, your application will be rejected. You can strip dynamic frameworks of the simulator architecture by using one of the following methods:
    -   Use the lipo command line tool to strip the dynamic frameworks of the simulator architecture.
    -   Integrate dynamic frameworks in pod mode. Then, dynamic frameworks of the simulator architecture are automatically stripped when the pods are packaged.

Procedure

1.  Add dynamic frameworks.

    Click the **General** tab. In the **Frameworks**, **Libraries**, and **Embedded Content** section, click **+**. Select **Add Other...** from the drop-down list and import the AliyunVideoCore.framework, AlivcConan.framework, and alivcffmpeg.framework files. After the frameworks are imported, select Embed &Sign.

2.  Add static frameworks.

    Click the **General** tab. In the **Frameworks**, **Libraries**, and **Embedded Content** section, click **+**. Select **Add Other...** from the drop-down list and import the AliyunVideoSDKPro.framework, AliyunOSSiOS.framework, and VODUpload.framework files.

3.  Add other frameworks.

    Click the **General** tab. In the **Frameworks**, **Libraries**, and **Embedded Content** section, click **+** and import the MobileCoreServices.framework, SystemConfiguration.framework, and libresolv.tbd files.

4.  If you are using the short video SDK Professional Edition,

    import the AliyunVideoSDKPro.bundle resource package to your project.


**Note:**

The process of manually integrating the SDK is complex. In addition, you must strip dynamic frameworks when you submit your application to App Store. We recommend that you integrate the SDK in pod mode.

If an error occurs during compilation, set the **Compile Sources As** parameter to **Objective-C++** in the **Apple Clang - Language** section of the **Build Settings** tab.

## Configure the project

After the SDK is integrated, open the project and modify the configuration.

1.  Choose **Build Setting** \> **Linking** \> **Other Linker Flags** and add -ObjC.

2.  Choose **Build Setting** \> **Build Options** and set the **Enable Bitcde** parameter to NO.

3.  Open the info.Plist file of the project and add the following permissions:

    ```
    Privacy - Camera Usage Description
    Privacy - Microphone Usage Description
    Privacy - Photo Library Usage Description
    ```


