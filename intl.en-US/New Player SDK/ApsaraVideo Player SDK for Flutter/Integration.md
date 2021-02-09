# Integration

This topic describes the development environments and integration methods of ApsaraVideo Player SDK for Flutter to help you integrate the SDK.

## Environment preparation

-   Android Studio: If you use Android Studio as the development tool, you can download the Flutter plug-in on the **Plugin** page. When you use a version earlier than Flutter V1.21, you must also configure Dart SDK.
-   Xcode: If you use Xcode as the development tool, you must install Flutter V1.20.3 or later on an iOS device. For more information about the download URL, see [Flutter SDK releases](https://flutter.dev/docs/development/tools/sdk/releases?tab=macos).
-   We recommend that you use ApsaraVideo Player SDK for Flutter V5.2.2 or later. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

## Procedure

1.  Download the [ApsaraVideo Player SDK](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.2.3/flutter_aliplayer_5.2.3.zip) zip file and decompress the file.

2.  Import the decompressed source code into the development tool.

3.  Use flutter\_aliplayer as the dependency in the pubspec.yaml file.

    ```
    flutter_aliplayer: ^5.2.3
    ```

    If you need to integrate RTS SDK into ApsaraVideo Player SDK for Flutter, add the following dependencies:

    ```
     flutter_aliplayer_artc: ^5.2.3
      flutter_aliplayer_rts: ^1.5.0
    ```

4.  Select another dependency library in the directory of your project.


## Project description

The following figure shows the directory structure of a project.

![Directory structure of ApsaraVideo Player SDK for Flutter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9793582161/p211510.png)

The following table describes the names and features of the files in the directory.

|File|Feature|Required|
|----|-------|--------|
|android|The native code for Android and ApsaraVideo Player SDK for Android.|Yes|
|ios|The native code for iOS and ApsaraVideo Player SDK for iOS.|Yes|
|lib|The code of API operations for Flutter, which is used to communicate with the native code.|Yes|
|extra|The RTS SDK.|No|
|example|The demo of ApsaraVideo Player SDK for Flutter.|No|

