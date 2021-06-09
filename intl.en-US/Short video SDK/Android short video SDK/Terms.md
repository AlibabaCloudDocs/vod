# Terms

The short video SDK for Android is an open source player component that is developed by Alibaba Cloud. The short video SDK for Android provides powerful features for video playback, including video recording, duet recording, and video merging.

## Version information

The short video SDK provides the Version class to obtain the SDK version information. You can use the variables that are defined in this class to obtain the SDK version information. Such information can help locate your issues.

```
public class Version {
    public static final String VERSION = "";
    public static final String BUILD_ID = "";
    public static final String SRC_COMMIT_ID = "";
    public static final String ALIVC_COMMIT_ID = "";
    public static final String ANDROID_COMMIT_ID = "";
}
```

## License

You must activate the license of the short video SDK before you use the short video SDK. For more information, see [t1959865.dita\#multiTask7429](/intl.en-US/Short video SDK/Introduction.md).

**Note:** When you activate the license, make sure that the package name that you submit is the same as that configured in Android Studio.

## Video resolution

The resolution of a video indicates the effective horizontal and vertical pixels of the video. Generally, a higher resolution indicates a clearer video. However, a higher resolution indicates a larger file, which requires a longer processing time. Considering that the performance varies among different mobile devices, we recommend that you use 720P or a lower resolution. The following table describes the common video resolutions.

|Resolution|1:1|3:4|9:16|
|----------|---|---|----|
|480P|480\*480|480\*640|480\*848|
|540P|540\*540|540\*720|540\*960|
|720P|720\*720|720\*960|720\*1280|
|1080P|1080\*1080|1080\*1440|1080\*1920|

-   **Recording module**

    You can use the setMediaInfo\(MediaInfo mediaInfo\) method of AliyunIRecorder to set a resolution for the recorded video by setting the videoWidth and videoHeight attributes of a MediaInfo object.

-   **Cropping module**

    You can use the setCropParam\(CropParam param\) method of AliyunICrop to set a resolution for the output video by setting the outputWidth and outputHeight attributes of a CropParam object.

-   **Editing module**

    You can use the setVideoParam\(AliyunVideoParam param\) method of AliyunIImport to set a resolution for the output video by setting the mOutputWidth and mOutputHeight attributes of an AliyunVideoParam object.


**Note:** Do not directly use the screen resolution of a mobile device as the video resolution. The aspect ratio that is specified by GLSurfaceView must be the same as that of the resolution that is configured for the recorded video. If the aspect ratios are different, the height of the recorded video is videoWidth multiplied by the aspect ratio specified by GLSurfaceView. Then, videoWidth and the calculated height are used as the final resolution of the recorded video.

## Video rotation angle

A video file may contain the rotation angle information. The short video SDK allows you to set a rotation angle for the recorded video. When you record a video in landscape mode, you can use the setRotation\(int rotation\) method of AliyunIRecorder to set the rotation angle of the camera. Then, the recorded video contains the rotation angle information.

## Bitrate

The bitrate of a video indicates the number of bits that are transmitted per second. The unit is bit per second \(bit/s\). After you set a bitrate for a video, the video encoder compresses the video to the desired size. Within a specific range, a higher bitrate indicates a clearer video with a larger file size. The following table describes the recommended bitrates of different resolutions.

|Resolution|Recommended bitrate|
|----------|-------------------|
|480P|1000000~2000000|
|540P|2000000~3000000|
|720P|2000000~4000000|
|1080P|2000000~6000000|

-   **Recording module**

    You can use the setVideoBitrate\(int bitrate\) method of AliyunIRecorder to set a bitrate for the recorded video.

-   **Cropping module**

    You can use the setCropParam\(CropParam param\) method of AliyunICrop to set a bitrate for the output video by setting the mVideoBitrate attribute of a CropParam object.

-   **Editing module**

    You can use the setVideoParam\(AliyunVideoParam param\) method of AliyunIImport to set a bitrate for the output video by setting the mBitrate attribute of an AliyunVideoParam object.


## Frame rate

The frame rate of a video indicates the number of image frames that are displayed per second. The unit is frame per second \(FPS\). A higher frame rate indicates a smoother video with a larger file size. The recommended video frame rate is 25 FPS to 30 FPS.

-   **Recording module**

    You can use the setMediaInfo\(MediaInfo mediaInfo\) method of AliyunIRecorder to set a frame rate for the recorded video by setting the mEncoderFps attribute of a MediaInfo object.

-   **Cropping module**

    You can use the setCropParam\(CropParam param\) method of AliyunICrop to set a frame rate for the output video by setting the frameRate attribute of a CropParam object.

-   **Editing module**

    You can use the setVideoParam\(AliyunVideoParam param\) method of AliyunIImport to set a frame rate for the output video by setting the mFrameRate attribute of an AliyunVideoParam object.


## Keyframe

Frame is the basic unit of video images. A video file is composed of multiple consecutive frames. A keyframe is also called an I-frame. The key frame is important for interframe compression and encoding. During decoding, a complete image can be reconstructed with only a keyframe. Keyframes can be generated without referencing other images. A keyframe can be used as an image and a reference point for seeking.

## GOP

A group of pictures \(GOP\) is a collection of successive frames. A GOP starts with a keyframe, followed by a group of B-frames and P-frames. If the GOP size is too small, the number of keyframes increases in a video and the compression ratio decreases. If the GOP size is too large, seeking takes more time. In addition, reverse playback freezes because a GOP must be decoded for reversely playing the frames. In the short video SDK, the default GOP size is 5. We recommend that you set the GOP size to a value within 5 to 30.

-   **Recording module**

    You can use the setGop\(int gop\) method of AliyunIRecorder to set a GOP size for the recorded video.

-   **Cropping module**

    You can use the setCropParam\(CropParam param\) method of AliyunICrop to set a GOP size for the output video by setting the gop attribute of a CropParam object.

-   **Editing module**

    You can use the setVideoParam\(AliyunVideoParam param\) method of AliyunIImport to set a GOP size for the output video by setting the mGop attribute of an AliyunVideoParam object.


**Note:** To use the reverse playback feature during editing, you must transcode an imported video first if the video has a large GOP size.

## Scaling mode

If the aspect ratio of a material, such as an image or a video, is different from that of the output video, you must select a scaling mode.

The following table describes the scaling modes that are supported by the short video SDK.

|Scaling mode|Solution|
|------------|--------|
|Cropping mode|Maintains the original aspect ratio and crops the material to display only the content in the middle area.|
|Padding mode|Maintains the original aspect ratio and displays the complete material by filling the blank area with a specified color.|

-   **Cropping module**

    You can use the setCropParam\(CropParam param\) method of AliyunICrop to set a scaling mode for the output video by setting the mScaleMode attribute of a CropParam object.

-   **Editing module**

    You can use the setVideoParam\(AliyunVideoParam param\) method of AliyunIImport to set a scaling mode for the output video by setting the mScaleMode attribute of an AliyunVideoParam object.


## Encoding mode

The following table describes the encoding modes that are supported by the short video SDK.

|Encoding mode|Description|
|-------------|-----------|
|Software encoding|Software encoding is completed by using the CPU. Compared with hardware encoding, software encoding allows you to set more parameters. At the same bitrate, a software-encoded video is clearer. However, software encoding is slow, the CPU load is high, and the mobile phone gets hot.|
|Hardware encoding|Hardware encoding is completed by other hardware instead of the CPU. Hardware encoding is faster, and the CPU load is low. However, the clearness of a hardware-encoded video is slightly lower than that of a software-encoded video. In addition, hardware encoding may fail on some Android devices.|

## Resources

Resources of the short video SDK include face recognition models, common filters, and animated filters. These SDK resources can be stored on the network or packaged into an Android package. Considering the size of the SDK resources, we recommend that you store the resources on the network and enable your application to download the resources when the application starts.

**Note:** The short video SDK cannot read resources from the assets folder. If the resources are packaged into an Android package, they must be copied to the SD card after the application starts. You can obtain the resource files and usage instructions from the downloaded SDK package.

## Supported formats

|Type|Format|
|----|------|
|Video|MP4, MOV, and FLV|
|Audio|MP3, AAC, and PCM|
|Image|JPG, PNG, and GIF|

