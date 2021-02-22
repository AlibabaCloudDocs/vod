# Configure a project

Before you use the upload SDK for Android, you must configure a project. This topic describes how to configure a project.

iOS 7 or a later version is used on your terminal device.

## SDK integration

You can implement SDK integration in pod mode or manual mode.

-   SDK integration in pod mode
    1.  Add the dependencies of the ApsaraVideo VOD upload SDK to the Podfile file.

        pod 'VODUpload'

    2.  Update the pod repository.

        pod repo update

    3.  Install the upload SDK.

        pod install

-   SDK integration in manual mode
    1.  Download the upload SDK for iOS. For more information, see the "Download client SDKs" section of [SDK download](/intl.en-US/SDK Downloads/SDK download.md).
    2.  Download the Object Storage Service \(OSS\) SDK for iOS. For more information, see the "Download the SDK" section of [Preface](/intl.en-US/SDK Reference/iOS/Preface.md).
    3.  In Xcode, drag the VODUpload.framework and AliyunOSSiOS.framework to the Target project. In the dialog box that appears, select **Copy items if needed**.
    4.  Add the following system dependent libraries.
        -   AVFoundation.framework
        -   CoreMedia.framework
        -   SystemConfiguration.framework
        -   MobileCoreServices.framework
        -   libresolv.9.tbd

## Project configuration

After the SDK is integrated, open the project and modify the configuration.

1.  Choose **Build Setting** \> **Linking** \> **Other Linker Flags**.

2.  Add the -ObjC option.


