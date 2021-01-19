# Integration

This topic describes the supported systems, development environments, and integration methods of ApsaraVideo Player SDK for Android. This topic also describes how to integrate the SDK.

## Supported systems

Android 4.0 and later are supported. The following processor architectures of mobile phones are supported:

-   ARMv7
-   ARM64

**Note:** This topic describes how to integrate ApsaraVideo Player SDK V4.5.0 or later. If you use an earlier SDK version, update it to ApsaraVideo Player SDK V4.5.0 or later. For more information, see [Update ApsaraVideo Player SDK for Android from V3.x.x to V4.5.0](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/Upgrade from V3.x.x to V4.5.0.md).

## Environment preparation

We recommend that you use Android Studio as the development tool. This topic is based on the Android Studio development environment.

## Integration methods

-   Integrate the SDK by using on-premises files
    -   Download the SDK

        Download the latest version of ApsaraVideo Player SDK for Android. For more information, see [Release notes of ApsaraVideo Player SDK for Android](/intl.en-US/SDK Downloads/player-sdk-new-history/Player SDK for Android.md).

    -   SDK structure

        ![Structure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3080401161/p209520.png)

        The SDK package contains the following .aar files:

        -   AliyunPlayer-4.5.0-full.aar: a complete AAR package that contains FFmpeg dynamic frameworks.
        -   AliyunPlayer-4.5.0-part.aar: an AAR package that does not contain FFmpeg dynamic frameworks.
        You can select an AAR package as needed.

        -   To integrate a player SDK without the feature of short video playback, use AliyunPlayer-4.5.0-full.aar as the dependency.
        -   To integrate a player SDK that supports short video playback, you must use AliyunPlayer-4.5.0-part.aar as the dependency. In addition, you must add the com.aliyun.video.android:AlivcFFmpeg:1.0.0 package, the version of which is compatible for both the player SDK and the short video SDK.

            **Note:** An FFmpeg error may occur if you choose an invalid dependency for SDK integration.

    -   Integration procedure
        1.  Copy the required AAR package to the libs directory of your project. Create a libs directory if it does not exist.

            ![image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3080401161/p209525.png)

        2.  In the build.gradle file, declare the position of the libs directory in the repositories part of the allprojects block, and add Alibaba Cloud Maven repository URL to the build.gradle file. Example:

            ```
            maven {
                url 'https://maven.aliyun.com/repository/releases'
            }
            flatDir {
                dirs 'libs'
            }
            ```

            The following figure shows the result of the preceding operations.

            ![Result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3080401161/p209527.png)

        3.  Add the reference to the AAR package and the Gradle package com.alivc.conan:AlivcConan:0.9.5 to the dependencies part in the build.gradle file. Example:

            ```
            dependencies {
                implementation fileTree(dir: 'libs', include: ['*.jar'])
                // Other dependencies.
                // Two dependencies of ApsaraVideo Player.
                implementation (name:'AliyunPlayer-4.5.0-full',ext:'aar')
                implementation 'com.alivc.conan:AlivcConan:0.9.5'
            }
            ```

            The following figure shows the result of the preceding operations.

            ![Result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3080401161/p209529.png)

            Click **build.gradle** to complete the integration. After ApsaraVideo Player SDK for Android is integrated, the APK file size increases by about 7.5 MB.

    -   Obfuscation configuration

        The following code shows the obfuscation configuration:

        ```
        -keep class com.alivc.**{*;}
        -keep class com.aliyun.**{*;}
        -keep class com.cicada.**{*;}
        -dontwarn com.alivc.**
        -dontwarn com.aliyun.**
        -dontwarn com.cicada. **
        ```

-   Integrate the SDK by using the Gradle package
    1.  Add Alibaba Cloud Maven repository URL to the buildscript block and the allprojects block in the build.gradle file. Example:

        ```
        maven(){
            url 'https://maven.aliyun.com/repository/releases'
        }
        ```

        The following figure shows the result of the preceding operations.

        ![Result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3080401161/p209530.png)

    2.  Add the reference to the AAR package to the dependencies part in the build.gradle file. Example:

        ```
        implementation 'com.aliyun.sdk.android:AliyunPlayer:4.5.0-full'
        implementation 'com.alivc.conan:AlivcConan:0.9.5'
        ```

        The following figure shows the result of the preceding operations.

        ![Result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3080401161/p209532.png)

    3.  Click **build.gradle** to complete the integration. After ApsaraVideo Player SDK for Android is integrated, the APK file size increases by about 7.5 MB.

