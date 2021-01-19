# Integration

This topic describes the supported systems, development environments, and integration methods of ApsaraVideo Player SDK for iOS. This topic also describes how to integrate the SDK.

## Supported systems

iOS 8.0 and later are supported.

**Note:** This topic describes how to integrate ApsaraVideo Player SDK V4.5.0 or later. If you use an earlier SDK version, update it to ApsaraVideo Player SDK V4.5.0 or later. For more information, see [Update ApsaraVideo Player SDK for iOS from V3.x.x to V4.5.0]().

## Environment preparation

We recommend that you use Xcode as the development tool. This topic is based on the Xcode development environment.

## Integrate the SDK by using on-premises files

-   Download the SDK

    Download the latest version of ApsaraVideo Player SDK for iOS. For more information, see [Release notes of ApsaraVideo Player SDK for iOS](/intl.en-US/SDK Downloads/player-sdk-new-history/Player SDK for iOS.md).

-   SDK structure
    -   ARM folder: The bitcode is enabled, but simulator architectures are not included in the folder.
    -   ARM\_NO\_BITCODE folder: The bitcode is not enabled and simulator architectures are not included in the folder.
    -   ARM\_SIMULATOR folder: The bitcode is enabled and simulator architectures are included in the folder.

        **Note:** To submit an application to Apple App Store, you must strip the simulator architectures from dynamic frameworks. Otherwise, your application fails to be submitted.

    -   The following figure shows frameworks.

        ![Integration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9870401161/p209497.png)

        **Note:** AlivcConan, alivcffmpeg, and AliyunPlayer are required for SDK integration. You can find header files in AliyunPlayer directories. AliyunMediaDownloader directories are optional, which are used to download files for offline playback. dSYM files are used to symbolicate crash reports.

-   Integration procedure

    In this example, ApsaraVideo Player SDK V4.5.0 for iOS is integrated. The integration procedure for later versions is similar, except for the version number.

    1.  Download the latest version of ApsaraVideo Player SDK for iOS and add it to a project in Xcode.
    2.  On the General tab, add frameworks of ApsaraVideo Player SDK for iOS to the Embedded Binaries section.

        ![Integration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0970401161/p209500.png)

    3.  Modify the framework search paths on the Build Settings tab by adding directories of framework files.

        **Note:** If your code or the third-party code that you reference conflicts with the symbol file of the alivcffmpeg or AlivcConan framework, remove alivcffmpeg or AlivcConan from Linked Frameworks and Libraries. The two frameworks are not required for application links.


## Integrate the SDK by using CocoaPods

The following example shows how to integrate ApsaraVideo Player SDK for iOS by using CocoaPods statements:

```
platform:ios, '8.0'
target 'yourProject' do
pod 'AliPlayerSDK_iOS'
end
```

