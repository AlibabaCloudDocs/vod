# Terms

The short video SDK for iOS is a player component that is provided by Alibaba Cloud. It provides powerful video playback features and also supports features such as video recording, duet recording, and merging of video clips.

## Version information

The short video SDK provides the AliyunVideoSDKInfo class that is used to obtain the SDK version information. You can call the methods that are defined in this class to obtain the SDK version information. Such information can help us quickly locate your issues.

|Action|Sample code|
|------|-----------|
|Obtain the version number.|```
+ (NSString *)version;
``` |
|Obtain the alivc commit ID.|```
+ (NSString *)alivcCommitId;
``` |
|Obtain the media core commit ID.|```
+ (NSString *)mediaCoreCommitId;
``` |
|Obtain the video SDK commit ID.|```
+ (NSString *)videoSDKCommitId;
``` |
|Obtain the build ID.|```
+ (NSString *)videoSDKBuildId;
``` |
|Display the version information on the IDE.|```
+ (void)printSDKInfo;
``` |

**Note:** You can also find the version information in the comments of the AliyunVideoSDKInfo.h file.

## License

You need a license to use the short video SDK. For more information about how to apply for a license, see [Introduction](/intl.en-US/Short video SDK/Introduction.md).

**Note:** After you apply for a license, make sure that the bundle ID that you submit is the same as that configured in Xcode.

## TaskPath

taskPath specifies the path of the task folder. taskPath is required to initialize multiple modules of the short video SDK. All configuration files and temporary files that are generated when you use the short video SDK are stored in the folder specified by taskPath. In addition, configurations are transmitted between modules by using this folder. The folder that is specified by taskPath is created and deleted by developers.

## Video resolution

The resolution of a video indicates the effective horizontal and vertical pixels of the video. Theoretically, a higher resolution indicates a clearer video. However, a higher resolution also indicates a larger file size and longer processing time. The performance varies with mobile phones. We recommend that you set the video resolution to 720p or lower. The following table describes the general video resolutions.

|Definition|1:1|3:4|9:16|
|----------|---|---|----|
|480p|480\*480|480\*640|480\*848|
|540p|540\*540|540\*720|540\*960|
|720p|720\*720|720\*960|720\*1280|
|1080p|1080\*1080|1080\*1440|1080\*1920|

-   The recording module allows you to call the initialization method `- (instancetype)initWithDelegate:(id<AliyunIRecorderDelegate>)delegate videoSize:(CGSize)videoSize;` of AliyunIRecorder and set the videoSize property to specify a resolution for the recorded video.
-   The cropping module allows you to set the outputSize property of AliyunCrop to specify a resolution for the output video.
-   The editing module allows you to call the initialization method `- (instancetype)initWithPath:(NSString *)taskPath outputSize:(CGSize)outputSize;` of AliyunImporter and set the outputSize property to specify a resolution for the output video.

**Note:** Do not directly specify the screen resolution in pixels as the video resolution.

## Video rotation angle

A video file may contain the rotation angle information. The short video SDK allows you to set a rotation angle for the recorded video. When you record a video in landscape mode, you can set the cameraRotate property of AliyunIRecorder to specify the rotation angle of the camera. Then, the recorded video contains the rotation angle information.

## Bitrate

The bitrate of a video indicates the number of bits that are transmitted per second. The unit is bit per second \(bit/s\). After you set a bitrate for a video, the video encoder compresses the video to the expected size. In a specified range, a higher bitrate indicates a clearer video but a larger file size. The following table describes the recommended bitrates.

|Definition|Recommended bitrate|
|----------|-------------------|
|480P|1000000-2000000|
|540P|2000000-3000000|
|720P|2000000-4000000|
|1080|2000000-6000000|

-   **Recording module**

    You can set the bitrate property of AliyunIRecorder to specify a bitrate for the recorded video.

-   **Cropping module**

    You can set the bitrate property of AliyunCrop to specify a bitrate for the output video.

-   **Editing module**

    You can call the `- (void)setVideoParam:(AliyunVideoParam *)videoParam;` method of AliyunImporter and set the bitrate property of an AliyunVideoParam object to specify a bitrate for the output video.


## Frame rate

The frame rate of a video indicates the number of image frames that are displayed per second. The unit is frame per second \(fps\). A higher frame rate indicates a smoother video but a larger file size. The recommended video frame rate is 25 to 30 fps.

-   **Recording module**

    You can set the recordFps property of AliyunIRecorder to specify a frame rate for the recorded video.

-   **Cropping module**

    You can set the fps property of AliyunCrop to specify a frame rate for the output video.

-   **Editing module**

    You can call the `- (void)setVideoParam:(AliyunVideoParam *)videoParam;` method of AliyunImporter and set the fps property of an AliyunVideoParam object to specify a frame rate for the output video.


## Keyframe

Frame is the basic unit of video images. A video file is composed of multiple consecutive frames. A keyframe is also called an I-frame and is an important frame for interframe compression and encoding. During decoding, a complete image can be reconstructed only with a keyframe. Keyframes can be generated without the need to reference other images. A keyframe can be used as an image and a reference point for seeking.

## GOP

A Group of Picture \(GOP\) is a collection of successive frames. A GOP starts with a keyframe, followed by a group of B-frames and P-frames. If the GOP size of a video is too small, the number of keyframes increases and the compression ratio decreases. If the GOP size of a video is too large, seeking takes more time, and reverse playback stutters because a GOP must be decoded for playing the frames reversely. In the short video SDK, the default GOP size is 5. We recommend that you set the GOP size to a value within 5 to 30.

-   **Recording module**

    You can set the GOP property of AliyunIRecorder to specify a GOP size for the recorded video.

-   **Cropping module**

    You can set the GOP property of AliyunCrop to specify a GOP size for the output video.

-   **Editing module**

    You can call the `- (void)setVideoParam:(AliyunVideoParam *)videoParam;` method of AliyunImporter and set the GOP property of an AliyunVideoParam object to specify a GOP size for the output video.


**Note:** You can add the reverse playback effect by using the editing module. If an imported video has a large GOP size, you must transcode the video before you add this effect.

## Scaling mode

If the aspect ratio of an image or a video is different from that of the output video, you must select a scaling mode.

The following table describes the two scaling modes that are supported by the short video SDK.

|Padding mode|Description|
|------------|-----------|
|Cropping mode|Maintains the original aspect ratio and crops the image to display only the content in the middle area.|
|Scaling mode|Maintains the original aspect ratio and displays the complete image by filling the blank area with a specified color.|

-   **Cropping module**

    You can set the cropMode property of AliyunCrop to specify a scaling mode for the output video.

-   **Editing module**

    You can call the `- (void)setVideoParam:(AliyunVideoParam *)videoParam;` method of AliyunImporter and set the scaleMode property of an AliyunVideoParam object to specify a scaling mode for the output video.


## Encoding mode

The following table describes the two encoding modes that are supported by the short video SDK.

|Encoding mode|Description|
|-------------|-----------|
|Software encoding|Uses the CPU to encode a video. Compared with hardware encoding, software encoding allows you to set more parameters. At the same bitrate, a software-encoded video is clearer. However, software encoding is slow, the CPU load is high, and the mobile phone easily gets hot.|
|Hardware encoding|Uses other hardware instead of the CPU to encode a video. Hardware encoding is faster and the CPU load is low. However, the definition of a hardware-encoded video is slightly lower than that of a software-encoded video. Hardware encoding may fail on some Android devices.|

## Supported formats

|Type|Format|
|----|------|
|Video|MP4, MOV, and FLV|
|Audio|MP3, AAC, and PCM|
|Image|JPG, PNG, and GIF|

