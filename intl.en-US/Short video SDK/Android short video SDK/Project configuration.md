# Project configuration

## System version

The short video SDK is applicable to Android 4.3 and later.

## Development environment

Java 1.7, Android API level 18, and their later versions are supported.

## API reference

-   V3.17.0 and later

    Documents in Chinese: [API Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_new_cn/index.html).

    Documents in English: [API Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_new_en/index.html).

    To upgrade the existing API to the latest version, download the [upgrade tool](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/shortVideo/tool/interface_upgrade.py).

-   Earlier than V3.17.0

    Documents in Chinese: [API Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_cn/index.html).

    Documents in English: [API Reference](https://alivc-demo-cms.alicdn.com/versionProduct/doc/shortVideo/android_en/index.html).


## SDK editions

The short video SDK has three editions: Basic Edition, Standard Edition, and Professional Edition. For more information about the differences among the editions, see [Introduction](https://www.alibabacloud.com/help/doc-detail/53407.htm).

## SDK integration

**Integrate the SDK by using Maven \(Recommended\)**

**Add the Alibaba Cloud Maven repository**

Add the URL of the Maven repository to build.gradle.

```
allprojects {
    repositories {
        maven {
            url 'http://maven.aliyun.com/nexus/content/repositories/releases/'
       }
    }
}
```

**Add dependencies to a Maven project**

|Edition|Dependencies added to the Maven project|
|-------|---------------------------------------|
|Professional Edition|```
dependencies{
    implementation 'com.aliyun.video.android:svideopro:3.17.1'// Required. The short video SDK in Professional Edition.
    implementation 'com.aliyun.video.android:core:1.2.2' // Required. The core library.
    implementation 'com.alivc.conan:AlivcConan:1.0.3' // Required. The core library.
    implementation 'com.aliyun.video.android:AlivcFFmpeg:2.0.0' // Required.
    implementation 'com.aliyun.video.android:upload:1.6.0' // Optional. The upload library.
}
``` |
|Standard Edition|```
dependencies {
    implementation 'com.aliyun.video.android:svideostandard:3.17.1' // Required. The short video SDK in Standard Edition.
    implementation 'com.aliyun.video.android:core:1.2.2' // Required. The core library.
    implementation 'com.alivc.conan:AlivcConan:1.0.3' // Required. The core library.
    implementation 'com.aliyun.video.android:AlivcFFmpeg:2.0.0' // Required.
    implementation 'com.aliyun.video.android:upload:1.6.0' // Optional. The upload library.
}
``` |
|Basic Edition|```
dependencies {
    implementation 'com.aliyun.video.android:svideosnap:3.17.1' // Required. The short video SDK in Basic Edition.
    implementation 'com.aliyun.video.android:core:1.2.2' // Required. The core library.
    implementation 'com.alivc.conan:AlivcConan:1.0.3' // Required. The core library.
    implementation 'com.aliyun.video.android:AlivcFFmpeg:2.0.0' // Required.
    implementation 'com.aliyun.video.android:upload:1.6.0' // Optional. The upload library.
}
``` |

**Note:** The short video SDK supports only armeabi-v7a and arm64-v8a instruction sets. To ensure the compatibility with armeabi, we recommend that you copy .so files in the armeabi-v7a folder to the armeabi folder. The compatibility with ARMv5 and ARMv6 devices is of little significance because Android develops rapidly and the short video SDK is applicable only to Android 4.3 and later.

## Integrate the SDK manually

**Import AAR packages**

1.  Choose File \> New \> New Module and create an Android library as the module, as shown in the following figure. In this example, the AliyunSvideoLibrary module is created.

    ![SDK_1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0924540161/p179175.png)

2.  Copy AliyunSdk-RCE.aar, AlivcConan-x.x.x.aar, and AlivcCore.jar from the decompressed SDK package to the new module to add them to your project.

    ![SDK_2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0924540161/p179184.png)

3.  Add the dependencies on the AAR and JAR packages by using Gradle.

    ```
    dependencies {
     implementation fileTree(include: ['*.jar','*.aar'], dir: 'libs')
    }
    ```

4.  Add the dependency on the AliyunSvideoLibrary module to the app module, as shown in the following code:

    ```
     dependencies {
        implementation project(":AliyunSvideoLibrary")
    }
    ```


**Import .so files**

1.  Copy the jniLibs folder from the decompressed SDK package to the main folder of the app module. Then, declare the path of jniLibs in the build.gradle file of the app module, as shown in the following code:

    ```
    android {
     sourceSets.main {
         jni.srcDirs = []
         jniLibs.srcDir "src/main/jniLibs" 
     }
    }
    ```

2.  Load the following dynamic-link libraries that are required by the SDK. These dynamic-link libraries are contained in the latest version of the SDK and do not need to be manually loaded.

    ```
    libalivcffmpeg.so-------------Required. The third-party library on which the SDK depends.
    libaliresample.so-------------------Optional. The library that is required for audio resampling.
    ```

3.  Add the dependencies that are required by the upload feature. The upload of short videos depends on the upload SDK and Object Storage Service \(OSS\). If the upload feature is not required, skip this step.

    ```
    implementation 'com.aliyun.video.android:upload:1.6.0'
    implementation 'com.google.code.gson:gson:2.8.0'
    implementation 'com.squareup.okhttp3:okhttp:3.2.0'
    implementation 'com.aliyun.dpa:oss-android-sdk:+'
    ```

4.  Initialize the configuration. Call the following method in the onCreate method of the Application class in the app module:

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

```
######################Obfuscation configuration of the short video SDK#########################
-keep class com.aliyun.**{*;}
-keep class com.duanqu.**{*;}
-keep class com.qu.**{*;}
-keep class com.alibaba.**{*;}
-keep class component.alivc.**{*;}
-keep class com.alivc. **{*;}
```

