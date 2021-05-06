# Project configuration

This topic provides links to the documents for the short video SDK for Android and shows you how to integrate the SDK.

Required environments are prepared. The following table describes the required environments for development.

|Environment|Supported version|
|-----------|-----------------|
|Android|Android 4.3 and later.|
|Java|Java 1.7 and later.|
|API LEVEL|Android API level 18 and later.|
|Android Studio|Android Studio 2.3 and later. To download Android Studio, visit [Android Studio](https://developer.android.google.cn/studio/).|

## SDK reference

-   V3.17.0 and later

    For more information about the documents in Chinese, see [SDK Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_new_cn/index.html).

    For more information about the documents in English, see [SDK Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_new_en/index.html).

    To upgrade the existing SDK to the latest version, download the [upgrade tool](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/shortVideo/tool/interface_upgrade.py).

-   Earlier than V3.17.0

    For more information about the documents in Chinese, see [SDK Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_cn/index.html).

    For more information about the documents in English, see [SDK Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_en/index.html).


## Integrate the SDK by using Maven

Integrate the SDK by using Maven \(Recommended\)

Add the Alibaba Cloud Maven repository

Add the URL of the Maven repository to the build.gradle file.

```
allprojects {
    repositories {
        maven {
            url 'http://maven.aliyun.com/nexus/content/repositories/releases/'
       }
    }
}
```

Add dependencies to a Maven project.

```
dependencies{
    implementation 'com.aliyun.video.android:svideopro:3.20.0' // Required. The short video SDK in Professional Edition.
    implementation 'com.aliyun.video.android:core:1.2.2' // Required. A core library.
    implementation  'com.alivc.conan:AlivcConan:1.0.3' // Required. A core library.
    implementation  'com.aliyun.video.android:AlivcFFmpeg:2.0.0' // Required.
    implementation  'com.aliyun.video.android:upload:1.6.0' // Optional. The upload library.
    implementation 'com.google.code.gson:gson:2.8.0' // A third-party library.
    implementation 'com.squareup.okhttp3:okhttp:3.2.0' // A third-party library.
}
```

**Note:** The short video SDK supports only armeabi-v7a and arm64-v8a instruction sets. To ensure the compatibility with armeabi, we recommend that you copy the .so files in the armeabi-v7a folder to the armeabi folder. The compatibility with ARMv5 and ARMv6 devices is insignificant because Android rapidly develops but the short video SDK is applicable only to Android 4.3 and later.

## Manually integrate the SDK

Import AAR packages

1.  Create a module.

    In **Android Studio**, choose **File** \> **New** \> **New Module** and create an Android library as a module. In this example, the AliyunSvideoLibrary module is created.

    ![SDK_1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0924540161/p179175.png)

2.  Copy AliyunSdk-RCE.aar, AlivcConan-x.x.x.aar, and AlivcCore.jar from the decompressed SDK package to the new module to add them to your project.

    ![SDK_2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0924540161/p179184.png)

3.  Add the dependencies on the AAR and JAR packages by using Gradle.

    ```
    dependencies {
     implementation fileTree(include: ['*.jar','*.aar'], dir: 'libs')
    }
    ```

4.  Add the dependency on the AliyunSvideoLibrary module to the app module.

    ```
     dependencies {
        implementation project(":AliyunSvideoLibrary")
    }
    ```


Import .so files

1.  Copy the jniLibs folder from the decompressed SDK package to the main folder of the app module. Then, declare the path of jniLibs in the build.gradle file of the app module.

    The following sample code can be used:

    ```
    android {
     sourceSets.main {
         jni.srcDirs = []
         jniLibs.srcDir "src/main/jniLibs" 
     }
    }
    ```

2.  Load the dynamic-link libraries that are required by the SDK.

    These dynamic-link libraries are contained in the latest version of the SDK and do not need to be manually loaded.

    The following libraries are used:

    ```
    libalivcffmpeg.so-------------Required. The third-party library on which the SDK depends.
    libaliresample.so-------------------Optional. The library that is required for audio resampling.
    ```

3.  Add the dependencies that are required by the upload feature.

    The upload of short videos depends on the upload SDK and Object Storage Service \(OSS\). If the upload feature is not required, skip this step.

    ```
    implementation 'com.aliyun.video.android:upload:1.6.0'
    implementation 'com.google.code.gson:gson:2.8.0'
    implementation 'com.squareup.okhttp3:okhttp:3.2.0'
    implementation 'com.aliyun.dpa:oss-android-sdk:+'
    ```

4.  Initialize the configuration.

    Call the following method in the onCreate method of the Application class in the app module:

    ```
    com.aliyun.vod.common.httpfinal.QupaiHttpFinal.getInstance().initOkHttpFinal();
    ```


## Required permissions

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.FLASHLIGHT" />
<uses-permission android:name="android.permission.RECORD_VIDEO" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

**Note:** Permissions need to be dynamically requested in Android 6.0 and later.

## Obfuscation configuration

You can set the obfuscation configuration in the proguard-rules.pro file. The following sample code can be used:

```
######################Obfuscation configuration of the short video SDK#########################
-keep class com.aliyun.**{*;}
-keep class com.duanqu.**{*;}
-keep class com.qu.**{*;}
-keep class com.alibaba.**{*;}
-keep class component.alivc.**{*;}
-keep class com.alivc.**{*;}
```

