# Integration

This topic describes the supported systems, development environments, and integration methods of ApsaraVideo Player SDK for Android. This topic also describes how to integrate the SDK.

|Item|Requirement|
|----|-----------|
|System version|Android 4.3 or later is used.|
|Mobile phone processor|One of the following processor architectures is used:-   ARMv7
-   ARM64 |
|Development tool|A development tool is available. We recommend that you use Android Studio as the development tool. This topic is based on the Android Studio development environment. To download Android Studio, visit the [Android Studio](https://developer.android.google.cn/studio/) page.|
|Version of ApsaraVideo Player SDK for Android|ApsaraVideo Player SDK V5.3.0 for Android or later is used. For more information, see [Update ApsaraVideo Player SDK for Android from V3.x.x to V4.5.0]().|

## Integrate the SDK

You can integrate the SDK by using on-premises files or the Gradle package.

1.  **Integrate the SDK by using on-premises files**
    -   Download the SDK

        Download the latest version of ApsaraVideo Player SDK for Android. For more information, see [Release notes of ApsaraVideo Player SDK for Android](/intl.en-US/SDK Downloads/player-sdk-new-history/Release notes of ApsaraVideo Player SDK for Android.md).

    -   SDK structure

        ![Structure](../images/p182917.png)

        The SDK package contains the following .aar files:

        -   AliyunPlayer-x.x.x-full.aar: a complete AAR package that contains FFmpeg dynamic frameworks.
        -   AliyunPlayer-x.x.x-part.aar: an AAR package that does not contain FFmpeg dynamic frameworks.
        -   AlivcArtp-x.x.x.aar: an AAR package that supports the Alibaba Real-time Transport Protocol \(ARTP\) protocol. This package is optional.
        -   AlivcArtc-x.x.x.aar: an AAR package that supports the Alibaba Real-Time Communication \(ARTC\) protocol. This package is optional.
        **Note:**

        -   To integrate a player SDK without the feature of short video playback, use the AliyunPlayer-x.xx.x-full.aar package as the dependency.
        -   To integrate a player SDK that supports short video playback, you must use the AliyunPlayer-x.x.x-part.aar package as the dependency. In addition, you must add the com.aliyun.video.android:AlivcFFmpeg:x.x.x package, the version of which is compatible for both the player SDK and the short video SDK.
        -   An FFmpeg error may occur if you choose an invalid dependency for SDK integration.
    -   Integration procedure
        1.  Copy the required AAR package to the libs directory of your project. Create a libs directory if it does not exist.

            ![Image](../images/p182953.png)

        2.  In the build.gradle file of the project, add the flatDir setting in the repositories part of the allprojects block. Sample code:

            ```
            flatDir {
               dirs 'libs'
            }
            ```

        3.  Add the reference to the AAR package and the Gradle package com.alivc.conan:AlivcConan:x.x.x to the dependencies part in the build.gradle file of your application. Sample code:

            ```
            dependencies {
                  implementation fileTree(dir: 'libs', include: ['*.aar'])
                  // You need only to add the Gradle package com.alivc.conan:AlivcConan:x.x.x to the dependencies part for ApsaraVideo Player whose version is earlier than V5.3.0.
                  implementation 'com.alivc.conan:AlivcConan:x.x.x'
            }
            ```

    -   Obfuscation configuration

        Add the following obfuscation configuration to the proguard-rules.pro file of your application. Sample code:

        ```
        -keep class com.alivc.**{*;}
        -keep class com.aliyun.**{*;}
        -keep class com.cicada.**{*;}
        -dontwarn com.alivc.**
        -dontwarn com.aliyun.**
        -dontwarn com.cicada.**
        ```

2.  **Integrate the SDK by using the Gradle package**
    1.  Add the URL of Alibaba Cloud Maven repository to the buildscript block and the allprojects block in the build.gradle file. Sample code:

        ```
        maven {
            url 'https://maven.aliyun.com/repository/releases'
        }
        ```

        The following figure shows the result of the preceding operations.

        ![Result](../images/p182983.png)

    2.  Add the reference to the AAR package to the dependencies part in the build.gradle file of your application. Sample code:

        ```
        implementation 'com.aliyun.sdk.android:AliyunPlayer:x.x.x-full'
        // You need only to add the Gradle package com.alivc.conan:AlivcConan:x.x.x to the dependencies part for ApsaraVideo Player whose version is earlier than V5.3.0.
        implementation 'com.alivc.conan:AlivcConan:x.x.x'
        ```

        The following figure shows the result of the preceding operations.

        ![Result](../images/p182991.png)


## Integrate a demo of ApsaraVideo Player

-   Download the demo

    Download the latest version of ApsaraVideo Player SDK for Android. For more information, see [Release notes of ApsaraVideo Player SDK for Android](/intl.en-US/SDK Downloads/player-sdk-new-history/Release notes of ApsaraVideo Player SDK for Android.md).

    ![image-20210128161414045](../images/p243024.png)

    The following table describes the SDK structure.

    |Fold or file|Description|
    |------------|-----------|
    |demo|The demo of ApsaraVideo Player.|
    |JavaDoc|The API reference of ApsaraVideo Player.|
    |sdk|The .aar library of ApsaraVideo Player SDK for Android.|
    |X.X.XReleaseNote|The release notes.|

-   Run the demo

    In the navigation bar of Android Studio, choose **File** \> **New** \> **Import Project...**. Import the demo of ApsaraVideo Player, as shown in the following figure.

    ![mage-20210128162213155.png](../images/p243028.png)

    In the demo, Gradle dependency is used to import ApsaraVideo Player SDK for Android. In addition, some API operations are encapsulated in the SDK, and custom user interfaces \(UIs\) are provided. You can integrate required modules in the demo or directly use ApsaraVideo Player SDK as needed.

-   Integrate modules in the demo

    |Module|Description|
    |------|-----------|
    |AliyunListPlayer|The list playback module, which contains the sample code of the list player.|
    |AliyunLiveShiftPlayer|The time shifting module, which contains the sample code of the time shifting feature.|
    |AliyunPlayer|The ApsaraVideo Player module, which contains the sample code of ApsaraVideo Player.|
    |AliyunPlayerBase|The base module of the ApsaraVideo Player demo, in which ApsaraVideo Player SDK for Android is integrated by using the Gradle package.|
    |AliyunVideoCommon|The common module for Alibaba Cloud projects. The module contains some utility classes.|
    |zxing|The QR code scanning module.|
    |thirdparty-lib|The module that contains all dependencies required by the demo.|

    **Note:**

    -   You must import the AliyunPlayerBase and AliyunVideoCommon modules no matter which player-related module in the demo you want to import.
    -   You must also import the thirdparty-lib module. The thirdparty-lib module is not a built-in module in Android Studio. You must manually copy the module to the directory that stores the AliyunPlayerBase and AliyunVideoCommon modules in the project.
    In the following example, the AliyunPlayer module is used to show you how to integrate modules in the demo:

    1.  In the navigation bar of Android Studio, choose **File** \> **New** \> **Import Module...**. Select the module to be imported, as shown in the following figure.

        ![image-20210128173551010](../images/p243052.png)

    2.  Click **Finish**. Other required modules are automatically selected in Android Studio, as shown in the following figure.

        ![image-20210128173905107](../images/p243056.png)

    3.  After you import the modules, manually import the thirdparty-lib module by copying the module to the project. Add the reference to the module and the URL of Alibaba Cloud Maven repository to the build.gradle file. The following figure shows the imported thirdparty-lib module.

        ![image-20210201100541465](../images/p243059.png)

        ```
        buildscript {
            apply from: 'thirdparty-lib/config.gradle'
        
            repositories {
                google()
                jcenter()
                maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
                // The Maven repository that is required for the project.
                maven { url 'http://4thline.org/m2' }
            }
        }
        
        allprojects {
            repositories {
                google()
                jcenter()
                maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
                // The Maven repository that is required for the project.
                maven { url 'http://4thline.org/m2' }
            }
        }
        ```

    4.  Import the player\_demo module to the build.gradle file of your application. Other required modules are automatically imported based on the player\_demo module.

        ```
        implementation project(':Aliyunplayer:player_demo')
        ```

-   Integrate the demo of ApsaraVideo Player without using custom UIs

    The demo of ApsaraVideo Player contains many custom UIs. If you do not need custom UIs, the modules in the demo to be imported can be greatly reduced.

    -   Integrate ApsaraVideo Player SDK for Android by using on-premises files or the Gradle package. In the following example, ApsaraVideo Player SDK for Android is integrated by using the Gradle package. Add the URL of Alibaba Cloud Maven repository to the buildscript block and the allprojects block in the build.gradle file.

        ```
        buildscript {
              repositories {
                  google()
                  jcenter()
                  maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
              }
          }
        
          allprojects {
              repositories {
                  google()
                  jcenter()
                  maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
              }
          }
        ```

    -   Add dependencies of ApsaraVideo Player to the build.gradle file of your application, as shown in the following code:

        ```
        implementation 'com.aliyun.sdk.android:AliyunPlayer:x.x.x-full'
        // You need only to add the Gradle package com.alivc.conan:AlivcConan:x.x.x to the dependencies part for ApsaraVideo Player whose version is earlier than V5.3.0.
        implementation 'com.alivc.conan:AlivcConan:x.x.x'
        ```

    -   Copy specific code in the demo.

        Copy the AliyunRenderView, IRenderView, TextureRenderView, and SurfaceRenderView files in the Aliyunplayer/AlivcPlayerTools/src/main/java/com/aliyun/player/alivecpalyerexpand/widget directory.

        **Note:**

        -   The SurfaceRenerView file is used to render video images based on the SurfaceView class. The TextureRenderView file is used to render video images based on the TextureView class.
        -   The AliyunRenderView file is used to encapsulate the player and bind the player with the render view.
        -   You do not need to copy the AliyunVodPlayerView file because this file contains the sample code of the AliyunRenderView class.
        ![image-20210202094604436](../images/p243070.png)

    -   Use the AliyunRenderView class.

        You can reference the sample code in the AliyunVodPlayerView file.

        Create an AliyunRenderView object.

        ```
          <?xml version="1.0" encoding="utf-8"?>
          <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              xmlns:app="http://schemas.android.com/apk/res-auto"
              xmlns:tools="http://schemas.android.com/tools"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              tools:context=".AliPlayerActivity">
        
              <com.aliyun.playertest.playerDemo.AliyunRenderView
                  android:id="@+id/aliyunRenderView"
                  android:layout_width="match_parent"
                  android:layout_height="200dp" />
        
          </LinearLayout>
        ```

        Use the methods of the AliyunRenderView class.

        ```
        java
          // Set the type of the render view. Valid values: SurfaceType.TEXTURE_VIEW and SurfaceType.SURFACE_VIEW.
          aliyunRenderView.setSurfaceType(AliyunRenderView.SurfaceType.SURFACE_VIEW);
        
          // Set listeners.
          aliyunRenderView.setXXXListener;
        
          // Set the playback source. The setDataSource method is an overload method. You can also use this method to set data sources such as sts and playAuth.
          aliyunRenderView.setDataSource(urlSource);
        
          // The methods related to the playback.
          aliyunRenderView.prepare();
          aliyunRenderView.start()
          aliyunRenderView.pause()
          aliyunRenderView.stop()
          aliyunRenderView.release()
        ```

        **Note:** The preceding code shows specific methods of the AliyunRenderView class. To use the other methods of the AliyunRenderView class, you can reference the AliyunVodPlayerView class. Alternatively, you can use the other methods of the AliyunRenderView class based on the API reference of ApsaraVideo Player SDK for Android.


