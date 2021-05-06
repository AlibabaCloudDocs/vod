# Integration

This topic describes the supported systems, development environments, and integration methods of ApsaraVideo Player SDK for iOS. This topic also describes how to integrate the SDK.

|Item|Description|
|----|-----------|
|iOS version|iOS 8.0 and later are supported.|
|Development tool|We recommend that you use Xcode. The operations in this topic are based on Xcode. You can click [here](https://apps.apple.com/cn/app/xcode/id497799835?spm=a2c4g.11186623.2.16.5bea69f9T6AnTj&mt=12) to download Xcode.|
|SDK version|ApsaraVideo Player SDK V5.3.0 and later are supported.|

## Preparations

Download the SDK

Download the latest version of ApsaraVideo Player SDK for iOS. For more information, see [Release notes of ApsaraVideo Player SDK for iOS](/intl.en-US/SDK Downloads/player-sdk-new-history/Release notes of ApsaraVideo Player SDK for iOS.md).

The files in the SDK package need to be decompress. To download these files, open the terminal and run the following commands:

```
cd $(SDK_PATH)   // The SDK_PATH variable specifies the path of the SDK package.
sh createMoreKindsOfArch.sh
```

After you download the files in the SDK package, you can view the structure of the SDK package, as shown in the following figure.

![SDK structure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2335620261/p254185.png)

The SDK package contains the following folders:

-   ARM folder: The bitcode is enabled and simulator architectures are not included in the folder.
-   ARM\_NO\_BITCODE folder: The bitcode is disabled and simulator architectures are not included in the folder.
-   ARM\_SIMULATOR\_NO\_BITCODE: The bitcode is disabled and the i386 x86\_64 armv7 arm64 architecture is included.
-   ARM\_SIMULATOR folder: The bitcode is enabled and simulator architectures are included in the folder.

**Note:** To submit an application to Apple App Store, you must strip the simulator architectures from dynamic frameworks. Otherwise, your application fails to be submitted.

The SDK package contains the following frameworks:

-   AliyunMediaDownloader: optional. This framework is used to download files for offline playback.
-   artcSource.framework: optional. This framework is used to support the Alibaba Real-Time Communication \(ARTC\) protocol.
-   artpSource.framework: optional. This framework is used to support the Alibaba Real-Time Transport Protocol \(ARTP\) protocol.
-   RtsSDK.framework: optional. This framework is used to provide the Real-Time Streaming \(RTS\) feature.
-   AlivcConan: The dependency on this framework has been removed in ApsaraVideo Player SDK V5.3.0.

**Note:**

When you package your application files, dSYM files are used to symbolicate crash reports.

AliyunPlayer and alivcffmpeg are required for SDK integration. You can find header files in the directory of the AliyunPlayer framework.

## SDK integration

You can integrate the SDK by using on-premises files or CocoaPods.

Download the latest version of ApsaraVideo Player SDK for iOS and add it to a project in Xcode.

-   **Using on-premises files**
    1.  Click the **General** tab.
    2.  Add the frameworks of ApsaraVideo Player SDK for iOS to the **Frameworks, Libraries, and Embedded Content** section. Select **Embed & Sign** in the **Embed** column for these frameworks.

        ![Integrate the SDK by using on-premises files](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2335620261/p254192.png)

    3.  Click the **Build Settings** tab.
    4.  In the **Search Paths** section, set the **Framework Search Paths** parameter to the on-premises path of the frameworks.

        **Note:** If your code or the third-party code that you reference conflicts with the symbol file of the alivcffmpeg or AlivcConan framework, remove alivcffmpeg or AlivcConan from Linked Frameworks and Libraries. The two frameworks are not required for application links. The dependency on AlivcConan has been removed in ApsaraVideo Player SDK V5.3.0.

-   **Using CocoaPods**

    The following example shows how to integrate ApsaraVideo Player SDK for iOS by using CocoaPods statements:

    ```
    ruby
      platform:ios, '8.0'
      target 'yourProject' do
        pod 'AliPlayerSDK_iOS'
       end
    ```

    The following code provides an example on how to integrate ApsaraVideo Player SDK for iOS to support ARTC, ARTP, and RTS:

    ```
    ruby
      platform:ios, '8.0'
      target 'yourProject' do
        pod 'AliPlayerSDK_iOS', '5.3.0'
        pod 'AliPlayerSDK_iOS_ARTP', '5.3.0'
        pod 'AliPlayerSDK_iOS_ARTC', '5.3.0'
        pod 'RtsSDK', '1.5.0'
       end
    ```

    **Note:** If you want to integrate ApsaraVideo Player SDK for iOS and the short video SDK for iOS at the same time, replace AliPlayerSDK\_iOS with AliPlayerPartSDK\_iOS. This is because AliPlayerPartSDK\_iOS contains no FFmpeg frameworks, which avoids conflicts with the FFmpeg framework of the short video SDK for iOS.


