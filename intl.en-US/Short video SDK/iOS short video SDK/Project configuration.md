# Project configuration

## System version

The short video SDK for iOS is applicable to iOS 8.0 and later.

## Development environment

We recommend that you use macOS High Sierra 10.13 and Xcode 9.0 or later.

## API reference

Documents in Chinese: [API Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/iOS_cn/index.html).

Documents in English: [API Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/iOS_en/index.html).

## SDK editions

The short video SDK has three editions: Basic Edition, Standard Edition, and Professional Edition. The three editions use the same framework name AliyunVideoSDKPro.framework.

-   The Basic Edition supports only the recording and cropping features.
-   The Professional Edition and Standard Edition support all features. However, advanced features of the Standard Edition must be authorized separately.

## SDK integration

**SDK integration in pod mode \(recommended\)**

1.  Add dependencies to the Podfile file.

    |Edition|Dependency to be added to the Podfile file|
    |-------|------------------------------------------|
    |Professional Edition|    ```
pod 'AliyunVideoSDKPro', '3.17.1'
pod 'QuCore-ThirdParty', '3.15.0'
pod 'AlivcConan', '1.0.3'
pod 'VODUpload'
pod 'AliyunOSSiOS'
    ``` |
    |Standard Edition|    ```
pod 'AliyunVideoSDKStd', '3.17.1'
pod 'QuCore-ThirdParty', '3.15.0'
pod 'AlivcConan', '1.0.3'
pod 'VODUpload'
pod 'AliyunOSSiOS'
    ``` |
    |Basic Edition|    ```
pod 'AliyunVideoSDKBasic', '3.17.1'
pod 'QuCore-ThirdParty', '3.15.0'
pod 'AlivcConan', '1.0.3'
pod 'VODUpload'pod '
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


**Note:** Make sure that you can access and update the pod repository over the network. After the pods are installed, check whether the framework versions are the latest, as listed on the Alibaba Cloud website.

## SDK integration in manual mode \(not recommended\)

To manually integrate the SDK, you must download packages of the latest release from GitHub, including six frameworks and a bundle resource package.

|Name|Type|Description|Download URL|
|----|----|-----------|------------|
|AliyunVideoSDKPro|Static framework|Short video SDK|[Professional Edition](https://github.com/aliyunvideo/AliyunVideoSDKPro/releases)[Standard Edition](https://github.com/aliyunvideo/AliyunVideoSDKStd/releases)[Basic Edition](https://github.com/aliyunvideo/AliyunVideoSDKBasic/releases)|
|AliyunVideoCore|Dynamic framework|Short video SDK|[Professional Edition](https://github.com/aliyunvideo/AliyunVideoSDKPro/releases)[Standard Edition](https://github.com/aliyunvideo/AliyunVideoSDKStd/releases)[Basic Edition](https://github.com/aliyunvideo/AliyunVideoSDKBasic/releases)|
|AliyunVideoSDKPro.bundle|Resource package|Short video SDK|[Resource package that is required only by the Professional Edition](https://github.com/aliyunvideo/AliyunVideoSDKPro/releases)|
|alivcffmpeg|Dynamic framework|FFmpeg framework|[Download URL on GitHub](https://github.com/aliyunvideo/QuCore-ThirdParty/releases)|
|AlivcConan|Dynamic framework|Tool framework|[Download URL on GitHub](https://github.com/aliyunvideo/AlivcConanSDK/releases)|
|VODUpload|Static framework|Upload framework of ApsaraVideo VOD|[Download URL on GitHub](https://github.com/aliyunvideo/VODUpload/releases)|
|AliyunOSSiOS|Static framework|OSS upload framework|[Download URL on GitHub](https://github.com/aliyun/aliyun-oss-ios-sdk/releases)|

In the preceding frameworks, AliyunVideoCore, alivcffmpeg, and AlivcConan are dynamic frameworks. When you manually integrate and release dynamic frameworks, take note of the following information:

1.  To add a dynamic framework, select the target and choose General \> Embedded Binaries.
2.  To submit an application to App Store, you must strip dynamic frameworks of the x86-based simulator architecture. Otherwise, your application will be rejected. You can strip dynamic frameworks of the simulator architecture by using one of the following methods:
    -   Use the lipo command-line tool to strip the dynamic frameworks of the simulator architecture.
    -   Integrate dynamic frameworks in pod mode. Then, dynamic frameworks of the simulator architecture are automatically stripped when the pods are packaged.

**To manually integrate the SDK, perform the following steps:**

1.  Open the project and select the target. Choose General \> Embedded Binaries. Click the plus sign \(+\), click Add Other, and then import the AliyunVideoCore.framework, AlivcConan.framework, and alivcffmpeg.framework files.

2.  Open the project and select the target. Choose General \> Linked Frameworks And Libraries. Click the plus sign \(+\), click Add Other, and then import the AliyunVideoSDKPro.framework, AliyunOSSiOS.framework, and VODUpload.framework files.

3.  Open the project and select the target. Choose General \> Linked Frameworks And Libraries. Click the plus sign \(+\) and import the libz.tbd, ImageIO.framework, CoreMedia.framework, CoreVideo.framework, VideoToolBox.framework, MediaPlayer.framework, OpenAL.framework, libc++.tbd, libsqlite3.tbd, and libiconv.tbd files.

4.  If you are using the short video SDK Professional Edition, you must also import the AliyunVideoSDKPro.bundle resource package to your project.


**Note:** The process of manually integrating the SDK is complicated. You must also strip dynamic frameworks when you submit your application to App Store. We recommend that you integrate the SDK in pod mode.

## Project configuration

After the SDK is integrated, open the project and modify the configuration.

1.  Choose Build Setting \> Linking \> Other Linker Flags and add -ObjC.

2.  Choose Build Setting \> Build Options and set the Enable Bitcode parameter to NO.

3.  Open the info.Plist file of the project and add the following permissions:

    ```
    Privacy - Camera Usage Description
    Privacy - Microphone Usage Description
    Privacy - Photo Library Usage Description
    ```


