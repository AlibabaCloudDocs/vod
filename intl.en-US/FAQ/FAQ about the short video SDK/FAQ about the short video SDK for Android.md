# FAQ about the short video SDK for Android

This topic provides answers to some frequently asked questions when you use the short video SDK for Android.

## I have added effects to a video during editing. However, the video that is produced by using the AliyunICompose.compose method does not contain the effects. Why does this happen?

In the short video SDK V3.5.0 for Android or earlier, you must call the AliyunIEditor.onPause method to persist the added effects to an on-premises configuration file. If you do not call this method, the effects are not persisted to the on-premises configuration file. As a result, the Project field generated by deserializing the response of the AliyunICompose.compose method does not contain the effects. In this case, the produced video does not contain the effects.

## When I edit a video, I call the applyMusic operation to add a music stream to the video. Then, I set the startTime parameter to specify the point in time when the music starts to play. However, the music always starts from the beginning. Why does this happen?

In the EffectBean class, the startTime parameter specifies a point in time in the main stream instead of the effect material stream, which is when the specified effect starts working. In the short video SDK V3.6.0 for Android and later, the streamStartTime parameter is added to specify a point in time in the effect material stream, which is when the specified effect starts working. If you use the short video SDK V3.6.0 for Android and later, you can set the streamStartTime parameter to meet your business needs. If you use an earlier version, you must crop the effect material stream to add background music \(BGM\) to a video.

![](../images/p179087.png)

As shown in the preceding figure, when the main stream reaches the 10-second mark, the BGM starts from the 3-second mark of the effect material stream. When the BGM reaches the 10-second mark of the effect material stream, the BGM starts again from the 3-second mark. When the BGM reaches the 6-second mark of the effect material stream, the main stream reaches the 20-second mark. At this point in time, the BGM ends.

## What can I do if the following error is returned when I use the short video SDK Basic Edition for Android: java.lang.NoSuchFieldError: No field height of type I in class Lcom/aliyun/snap/snap\_core/R$id; or its superclasses \(declaration of 'com.aliyun.snap.snap\_core.R$id' appears in /data/app/com.rablive.jwrablive-2/base.apk:classes2.dex\)?

This error occurs because the name of an XML file in your project is the same as that of an XML file in the AAR package of the SDK. This error is a result of a duplicate name conflict.

To resolve this issue, add a prefix to the XML file in the project or AAR package. The following XML files may cause duplicate name conflicts: `activity_setting.xml` and `activity_video_play.xml`.

## What can I do if the following error is returned when I use the short video SDK Basic Edition for Android: java.lang.NoSuchFieldError: No static field notification\_template\_lines of type I in class Lcom/aliyun/snap/snap\_core/R$layout; or its superclasses \(declaration of 'com.aliyun.snap.snap\_core.R$layout' appears/data/app/com.Aliyun.AliyunVideoSDK.VodSaaSDemo\_android-1/base.apk\)?

This error occurs because the user interface \(UI\) of the short video SDK Basic Edition is not open source. The short video SDK uses the support library package of Android. However, the support library package is not included in the compiled AAR package. This causes a version mismatch in the support library package. To resolve this issue, import the support library package of the same version, as shown in the following code:

```
// Important. If the third-party library package you import to your project uses the support library package, make sure that the version of the support library package is correct. We recommend that you import the source code of the third-party library package to your project.
compile 'com.android.support:appcompat-v7:24.2.1'
compile 'com.android.support:design:24.2.1'
```

If the third-party library package is imported without the use of source code, it is difficult to change the version of the support library package used in the third-party library package. In this case, we recommend that you change the version of the support library package in the .gradle file of your application, as shown in the following code:

```
configurations.all {
resolutionStrategy {
force 'com.android.support:appcompat-v7:24.2.1'
force 'com.android.support:design:24.2.1'
}
}
```

## Does the short video SDK provide an operation to obtain the thumbnail of a video?

In the short video SDK for iOS, you can call the system operation to obtain the thumbnail of a video. The short video SDK Professional Edition for Android provides the AliyunIThumbnailFetcher operation that allows you to obtain non-keyframe thumbnails. If you use the short video SDK Basic Edition for Android, we recommend that you use a system function to obtain the thumbnail of a video.

## How do I record a video in landscape mode?

-   To set the landscape mode for recording, you can rotate UI elements to landscape to guide users to rotate their devices during recording. To do this, set the application view to portrait.

    ```
    android:screenOrientation="portrait"
    ```

-   The application view is used as the benchmark to determine the rotation angle of a recorded video. If a recorded video contains multiple clips, the rotation angle follows that of the first clip in the recorded video.
-   If you use the short video SDK Professional Edition, your application uses the video production operation to produce recorded videos. The videos are rotated to the portrait mode to adapt to the application view. Assume that the width of a recorded video is 640, the height is 360, and the rotation angle is 270°. The width of the produced video is 360, the height is 640, and the rotation angle is 0°. If you use the short video SDK Basic Edition or Standard Edition, your application produces recorded videos without rotating them to the portrait mode. If a recorded video contains multiple clips, the rotation angle follows that of the first clip in the recorded video. The recording process of the short video SDK Professional Edition is similar to that of the short video SDK Basic Edition or Standard Edition.

The key operation is setRotation:

```
/**
* Set the rotation angle of the video.
* @param rotation
*/
void setRotation(int rotation);
```

To call the setRotation operation, follow this rule:

Call the setRotation operation only after a recording instance is initialized and before the first video clip is recorded.

To call the setRotation operation, perform the following steps:

Set your application view to the portrait mode and set the rotation angle for recording.

1.  Set the application view to the portrait mode and rotate UI elements to guide users to rotate their devices during recording.
2.  Initialize a recording instance, which is similar to normal recording.
3.  Call the setRotation operation to set the rotation angle. You can call the OrientationDetector operation to obtain the rotation angle. For more information, see the corresponding demo.

    ```
    mRecorder.setRotation(int rotation);
    ```

4.  Proceed with recording. Note that you must set the rotation angle for recording before you call the startRecording operation each time.

## What Android instruction sets does the short video SDK support?

The short video SDK supports the armeabi-v7a and arm64-v8 instruction sets.

We recommend that you use armeabi-v7a and arm64-v8 for third-party libraries. If third-party libraries do not contain armeabi-v7a or arm64-v8, copy the .so files in the armeabi-v7a or arm64-v8 folder of the short video SDK to the armeabi folder of third-party libraries. Then, add the following code to the .gradle file:

```
defaultConfig {
　　　　...　　　　
            ndk {　　　　
            abiFilters "armeabi"// To use armeabi-v7a, replace armeabi with armeabi-v7a.　　　　
}
```

Change the file name extension of the .apk file to .zip, decompress the .zip file, and then check whether the .so files are contained in the libs directory.

## Why does the recorded video not contain the BGM added during recording after I call the finishRecordingForEdit operation?

The finishRecordingForEdit operation does not generate recorded videos with BGM. If you call this operation after you record videos, you cannot obtain recorded videos with BGM for editing. To obtain recorded videos with BGM, call the finishRecording operation.

The finishRecording operation and finishRecordingForEdit operation have the following differences: The finishRecording operation merges multiple recorded clips to an MP4 file. After you add one or more pieces of BGM, you can also call the finishRecording operation to synthesize the BGM into the output MP4 file. In contrast, the finishRecordingForEdit operation only adds configurations of a recorded video clip in the specified format to the project.json file after the application calls the startRecording and stopRecording operations to record the video clip. The finishRecordingForEdit operation neither merges multiple clips nor adds BGM to the recorded video. To use the short video SDK to edit the video clip, specify the URL of the project.json file when you create an editor instance.

To edit multiple recorded video clips with BGM, call the finishRecording operation to merge the video clips to an MP4 file and call the AliyunIImport operation to import the MP4 file for editing.

## What can I do if the debug version of an application integrated based on the short video SDK properly runs, but the release version fails when it starts?

You can view error logs to check whether your application fails to use Java native interface \(JNI\) to find the necessary Java classes. JNI calls Java Reflection API to find Java classes. If ProGuard obfuscates SDK classes and JNI classes, JNI cannot find the necessary Java classes, which may cause JNI loading failures. To resolve this issue, copy the ProGuard configuration in the demo project to your project.

## How do I add a blacklist for hardware encoding and a whitelist for hardware decoding?

Run the following code to add a blacklist for hardware encoding:

```
```
/**
* Add a blacklist for hardware encoding. The models and versions must correspond to each other in sequence.
* If a blacklist for hardware encoding is enabled, models in the blacklist use software encoding, whereas other models use hardware encoding.
* @param models List of models {@link Build#MODEL}
* @param versions List of system versions {@link Build.VERSION#SDK_INT} // If you do not need to specify versions, set the value to 0.
*/NativeAdaptiveUtil.encoderAdaptiveList(String[] models,int[] versions);
```
```

Run the following code to add a whitelist for hardware decoding:

```
/**
* Add a whitelist for hardware decoding. The models and versions must correspond to each other in sequence.
* If a whitelist for hardware decoding is enabled, models in the whitelist use hardware decoding, whereas other models use software decoding.
* @param models List of models {@link Build#MODEL}
* @param versions List of system versions {@link Build.VERSION#SDK_INT} // If you do not need to specify versions, set the value to 0.
* @see #setHWDecoderEnable(boolean)
*/
NativeAdaptiveUtil.decoderAdaptiveList(String[] models, int[] versions);
```

## How do I add a common animated sticker when I record a video?

You can use the AliyunIRecorder\#addPaster\(EffectPaster effectPaster,float sx,float sy,float sw,float sh,float rotation,boolean flip\) operation and set the EffectPaster parameter to add a common animated sticker. Note that you must set the isTrack parameter to false. Otherwise, the sticker is added as a face sticker, which follows human faces. The sticker is hidden if no human face is detected. Call this operation after the RecordCallback\#OnInitReady\(\) callback is fired. Otherwise, the added sticker is hidden.

## How do I add GIF files to main streams?

The short video SDK of a version earlier than V3.7.0 enables you to add GIF files to main streams only as images. In contrast, V3.7.0 and later enable you to add GIF files to main streams as videos or images. When a GIF file is added as a video, all frames of the GIF file are played. However, when a GIF file is added as an image, only the first frame of the GIF file is played.

## How do I set the rotation angle for recording?

You can call the setRotation or setRecordRotation operation to set the rotation angle for recording. The setRotation operation is an adaptive operation. After the rotation angle detected by the angle sensor of a mobile phone is passed to this operation, the recording angle and face angle are returned. You can also call the setRecordRotation operation to set a recording angle.

## Why does the size of a group of pictures \(GOP\) not work when I set it by using the short video SDK for Android?

If you use an improper encoder for hardware encoding, the actual GOP size may be different from the settings. If you require accurate GOP sizes, we recommend that you use software encoding.

## What can I do if a video is stuck after a transition effect is configured or the applySourceChange operation is called for the video?

After you configure a transition effect or call the applySourceChange operation for a video, call the AliyunIEditor.play\(\) operation to play the video.

## What can I do if the recording UI displays only a part of a common animated sticker?

Call the following operation to obtain the width and height of the material of the common animated sticker:

```
AliyunIRecorder#addPaster(EffectPaster effectPaster,float sx,float sy,float sw,float sh,float rotation,boolean flip) 
```

Set the sw parameter to the ratio of the sticker width to the screen width. Set the sh parameter to the ratio of the sticker height to the screen height.

Assume that the sticker width is 200, the sticker height is 300, the screen width is 540, and the screen height is 720. Then, set the sw parameter to \(float\)200/540, and the sh parameter to \(float\)300/720.`` The sx and sy parameters are normalized values of the width and height of the sticker, with the center point of the sticker as the anchor.

## What can I do if the "Please invoke the FileDownloader\#init in Application\#onCreate first" message appears when I use the demo?

Call the `DownloaderManager.getInstance().init(Context context);` operation in the OnCreate\(\) method of the application.
