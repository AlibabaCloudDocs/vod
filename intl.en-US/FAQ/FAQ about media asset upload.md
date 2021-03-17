# FAQ about media asset upload

This topic provides answers to some frequently asked questions on page stretching and compatibility issues when you upload media files.

## What can I do if a compatibility issue occurs when I use the SDK for JavaScript to upload a media file in WeChat?

This issue occurs because the WeChat browser is not compatible with the HTML5 player. To resolve this issue, delete the `multiple=""` parameter from `<input type="file" name="file" id="files" multiple="">`.

## What can I do if the preview page is stretched when the resolution is set to 480p in the stream ingest SDK?

When the resolution of an ingested stream is set to 480p in the stream ingest SDK, the video image of the stream is properly displayed. However, the preview page may be stretched. This issue occurs because the resolution of a 480p video is 480 × 640 pixels, which is not supported by most mobile phone screens.

To resolve this issue, modify the settings of the SurfaceView parameter for the preview page in the activity\_push.xml file, as shown in the following figure.

![TFpnKZEWmJXIKEqkNHdU.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9758495161/p179081.png)

![poYUFCTzncXdWoUOyJKp.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9758495161/p179082.png)

## How can I view and import an AAR package in Android Studio?

To view files in an AAR package, change the file name extension of the package from `.aar` to `.zip` and decompress the package. Then, you can view the `.class` files, `.xml` files, `.jar` files, images, and text files in the package.

To import an AAR package, perform the following steps:

1.  Copy the `.aar` package to your project and reload the project. Generally, copy the package to the Project name/libs/ directory.

    ![dvMgYjWarBrxAKHObAjW.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9758495161/p179083.png)

2.  In the build.gradle file, add the path of an on-premises repository to the root tag and add the compilation dependencies to the dependencies part.

    Replace libs in the sample code with the name of the directory to which the AAR package is imported. In the **compile** parameter, set the **name** field to the name of the AAR package and the **ext** field to the file name extension.

    ![IdybZmRLnUQfWAveqGGK.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0858495161/p179084.png)

3.  Choose **Build** \> **Rebuild** to rebuild the project.

    When the project is rebuilt, the imported AAR package is displayed in the **External Libraries** directory of the project.

    ![jwqQxvgFgbACgUTpklPK.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0858495161/p179085.png)


