# Configure a project

Before you use the upload SDK for Android, you must configure a project. This topic describes how to configure a project.

Android 2.3 or later is used.

## Import the upload SDK

You can import the upload SDK by adding Maven dependencies or importing on-premises JAR dependencies.

-   Maven dependencies
    1.  Add the following dependencies to a Maven project:

        ```
        dependencies {
            compile 'com.aliyun.video.android:upload:1.6.2'
        }
        ```

    2.  Add the URL of a Maven repository to the build.gradle file in the root directory.

        ```
        allprojects {
            repositories {
                maven { url "https://maven.aliyun.com/nexus/content/repositories/releases" }
            }
        }
        ```

    3.  Install Object Storage Service \(OSS\) SDK for Android. For more information, see [Installation](/intl.en-US/SDK Reference/Android/Installation.md).
-   On-premises JAR dependencies
    1.  Download the upload SDK for Android provided by ApsaraVideo VOD. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md). Decompress the SDK and import the following JAR packages in the libs directory to the libs directory of the project: aliyun-vod-upload-android-sdk-xxx.jar, gson-xxx.jar, and jsr305-xxx.jar.
    2.  Install OSS SDK for Android. For more information, see [Installation](/intl.en-US/SDK Reference/Android/Installation.md).

