# Duet recording

The short video SDK provides the AliyunIMixRecorder operation for you to record a duet that consists of an existing sample video and a video that is being taken by the camera. The two videos are arranged in the specified layout, such as left-right split-screen, up-down split-screen, or picture-in-picture.

## Terms

This section describes the terms that help you better understand the duet feature.

-   Duet feature

    The duet feature allows you to produce a video from two videos. One is a sample video and the other is taken by the camera. The two videos are arranged in the specified layout, such as left-right split-screen, up-down split-screen, or picture-in-picture. Each frame of the produced video contains images from the two videos, and the audio of the sample video is used as the audio of the produced video. The following figure shows sample layouts. The short video SDK allows you to customize the layout, which is described later in this topic.

    ![Duet feature](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1148911161/p180476.png)

-   Track

    The two videos that are mentioned earlier are abstracted to two tracks in the short video SDK: Track A and Track B. Track A stores the video that is collected by the camera and Track B stores the sample video. This abstraction helps you better understand the concept of track layout.

-   Track layout

    The track layout is a property of a track, which specifies the position of the track in the produced video. This property uses a normalized coordinate system to describe the center point of the track and its size. The size of a track indicates the width and height of the track.

    The following figure shows that Track A occupies the left half of the screen and Track B occupies the right half of the screen. Therefore, the width of both tracks is 0.5 and the height is 1.0. The center point of Track A is \(0.25, 0.5\) and the center point of Track B is \(0.75, 0.5\).

    The track layout involves the following two classes:

    -   AliyunMixTrackLayoutParam specifies the center point and size of a track.
    -   AliyunMixRecorderDisplayParam provides the displayMode and layoutLevel attributes to specify more information in addition to the information that is specified by AliyunMixTrackLayoutParam. The displayMode attribute specifies the scaling mode that is used when the aspect ratio of the video in a track differs from that of the track. For example, you can specify padding or cropping as the scaling mode. The layoutLevel attribute specifies the layout level. If two tracks overlap, the track with a higher layout level is displayed above the other.

![Duet recording](../images/p213140.jpg)

## Differences among editions

|Edition|Description|
|-------|-----------|
|Professional Edition|The duet feature is supported.|
|Standard Edition|The duet feature is supported.|
|Basic Edition|The duet feature is not supported.|

## Duet recording

**Note:** The camera and microphone permissions are required for duet recording. Otherwise, the recording fails.

|Duet recording process|Description|
|----------------------|-----------|
|[Set parameters](#title_m6w_pl3_r9q)|This step is performed to create or destroy a recording instance.|
|[Set callbacks](#title_6n9_3dq_4bj)|This step is performed to set callbacks.|
|[Manage preview](#title_zzx_8n8_xkg)|This step is performed to start or stop the preview.|
|[Configure and manage recording](#title_8eo_po7_4em)|This step is performed to configure recording information.|
|[Configure effects](#title_zwq_jza_b48)|This step is performed to configure beautification and filters for recording.|
|[Start recording](#title_h5o_3gy_y2h)|This step is performed to start, cancel, or stop recording a video clip.|

## Set parameters

-   Initialization

    |Action|Sample code|
    |------|-----------|
    |Create a recording instance.|    ```
AliyunIMixRecorder recorder = AliyunMixRecorderCreator.createAlivcMixRecorderInstance(Context context); // We recommend that you use Application Context as the context.
    ``` |
    |Destroy the recording instance.|    ```
AliyunIMixRecorder.release();
    ``` |

-   Output settings

|Action|Sample code|
|------|-----------|
|Set the input and output parameters for duet recording.|```
AliyunIMixRecorder.setMixMediaInfo(AliyunMixMediaInfoParam inputMediaInfo, MediaInfo outputInfo);// For more information, see AliyunMixMediaInfoParam and MediaInfo in the SDK documentation.
``` |
|Set the output path.|```
AliyunIMixRecorder.setOutputPath(String path);
``` |
|Set the quality of the produced video.|```
AliyunIMixRecorder.setVideoQuality(VideoQuality quality);
``` |
|Set the bitrate of the produced video.|```
AliyunIMixRecorder.setVideoBitrate(int bitrate);// Unit: Kbit/s.
``` |
|Set the group of pictures \(GOP\) size of the produced video.|```
AliyunIMixRecorder.setGop(int gop);// Unit: frames.
``` |


## Set callbacks

|Action|Sample code|
|------|-----------|
|Set the recording callback.|```
AliyunIMixRecorder.setRecordCallBack(RecordCallback callBack);
``` |
|Set the callback for video frame collection.|```
AliyunIMixRecorder.setOnFrameCallback(OnFrameCallBack callback);
``` |
|Set the audio collection callback.|```
AliyunIMixRecorder.setOnAudioCallback(OnAudioCallBack callback);
``` |

## Manage preview

|Action|Sample code|
|------|-----------|
|Start the preview.|```
AliyunIMixRecorder.startPreview();
``` |
|Stop the preview.|```
AliyunIMixRecorder.stopPreview();
``` |

## Configure and manage recording

-   Control recording

    |Action|Sample code|
    |------|-----------|
    |Obtain the number of cameras.|    ```
AliyunIMixRecorder.getCameraCount();
    ``` |
    |Set the camera type.|    ```
AliyunIMixRecorder.setCamera(CameraType cameraType);
    ``` |
    |Set the camera preview parameters, including the flash mode, focus mode, zoom factor, and exposure value.|    ```
AliyunIMixRecorder.setCameraParam(CameraParam
cameraParam);// You can also separately set the parameters. For more information, see the following methods.
    ``` |
    |Switch between the front and rear cameras.|    ```
AliyunIMixRecorder.switchCamera();
    ``` |
    |Set the flash mode.|    ```
AliyunIMixRecorder.setLight(FlashType flashType);
    ``` |
    |Set the zoom factor.|    ```
AliyunIMixRecorder.setZoom(float rate);
    ``` |
    |Set the exposure value.|    ```
AliyunIMixRecorder.setExposureCompensationRatio(float value);
    ``` |
    |Set the focus mode.|    ```
AliyunIMixRecorder.setFocusMode(int mode);
    ``` |
    |Set the manual focus point.|    ```
AliyunIMixRecorder.setFocus(float xRatio, float yRatio);
    ``` |
    |Set the preview view.|    ```
AliyunIMixRecorder.setDisplayView(SurfaceView previewView, SurfaceView playView);// **Note: Do not use the GLSurfaceView class or its subclass. **
    ``` |
    |Set the sensor rotation angle. This configuration is very important. We recommend that you carefully read the SDK documentation.|    ```
AliyunIMixRecorder.setRotation(int rotation);
    ``` |
    |Set the face detection angle. This configuration is very important. We recommend that you carefully read the SDK documentation.|    ```
AliyunIMixRecorder.setFaceDetectRotation(int rotation);
    ``` |
    |Set the video recording angle. This configuration is very important. We recommend that you carefully read the SDK documentation.|    ```
AliyunIMixRecorder.setRecordRotation(int rotation);
    ``` |
    |Specify whether to mute the audio during recording.|    ```
AliyunIMixRecorder.setMute(boolean isMute);
    ``` |
    |Specify an audio track for duet recording. By default, the original audio track is used.|    ```
AliyunIMixRecorder.setMixAudioSource(MixAudioSourceType mixAudioSourceType);
    ``` |

-   Manage recording

    |Action|Sample code|
    |------|-----------|
    |Obtain the clip manager.|    ```
AliyunIMixRecorder.getClipManager();// **Note: To delete the last clip, do not call the method of AliyunIClipManager. Instead, you must call the AliyunIMixRecorder.deleteLastPart() method. **
    ``` |
    |Set the maximum recording duration, which is the maximum duration of all video clips instead of a single video clip.|    ```
AliyunIClipManager.setMaxDuration(int maxDurationMs);
    ``` |
    |Set the minimum recording duration, which is the minimum duration of all video clips instead of a single video clip.|    ```
AliyunIClipManager.setMinDuration(int minDurationMs);
    ``` |
    |Obtain the total duration of video clips.|    ```
AliyunIClipManager.getDuration();
    ``` |
    |Obtain the total number of video clips.|    ```
AliyunIClipManager.getPartCount();
    ``` |
    |Delete the last video clip.|    ```
AliyunIMixRecorder.deleteLastPart();// Do not call the AliyunIClipManager.deletePart() method. Otherwise, you cannot seek to the last position where the recording stops in the sample video.
    ``` |
    |Delete the specified video clip.|    ```
AliyunIClipManager.deletePart(int index);// This method only deletes the specified video clip and does not trigger seeking in the sample video.
    ``` |
    |Delete all video clips.|    ```
AliyunIClipManager.deleteAllPart();// This method only deletes the specified video clip and does not trigger seeking in the sample video.
    ``` |
    |Obtain the paths of video clips.|    ```
AliyunIClipManager.getVideoPathList();
    ``` |


## Configure effects

-   Beautification

    |Action|Sample code|
    |------|-----------|
    |Set the beautification level.|    ```
AliyunIMixRecorder.setBeautyLevel(int level);
    ``` |
    |Enable or disable beautification.|    ```
AliyunIMixRecorder.setBeautyStatus(boolean on);
    ``` |

-   **Common filter**

    |Action|Sample code|
    |------|-----------|
    |Add a common filter.|    ```
AliyunIMixRecorder.applyFilter(EffectFilter effectFilter);// You can remove a common filter by setting its path to null.
    ``` |
    |Remove a common filter.|    ```
AliyunIMixRecorder.applyFilter(new EffectFilter(null));
    ``` |

-   Animated filter

    |Action|Sample code|
    |------|-----------|
    |Add an animated filter, such as the filter that provides the effect of spirit freed from the body.|    ```
AliyunIMixRecorder.applyAnimationFilter(EffectFilter effectFilter);
    ``` |
    |Remove an animated filter.|    ```
AliyunIMixRecorder.removeAnimationFilter(EffectFilter effctFilter);
    ``` |

-   **Facial recognition \(supported only in Professional Edition\)**

    |Action|Sample code|
    |------|-----------|
    |Set face coordinates. The coordinates are required by third-party facial recognition products.|    ```
AliyunIMixRecorder.setFaces(float[][] faces);
    ``` |
    |Specify whether to use the built-in facial recognition feature of the SDK.|    ```
AliyunIMixRecorder.needFaceTrackInternal(boolean need);
    ``` |
    |Specify a model file to use the built-in facial recognition feature of the SDK.|    ```
AliyunIMixRecorder.setFaceTrackInternalModelPath(String path);
    ``` |
    |Set the maximum number of faces that can be recognized by using the built-in facial recognition feature of the SDK.|    ```
AliyunIMixRecorder.setFaceTrackInternalMaxFaceCount(int maxFaceCount);
    ``` |

-   Animated sticker \(supported only in Professional Edition\)

    |Action|Sample code|
    |------|-----------|
    |Add an animated face sticker.|    ```
AliyunIMixRecorder.addPaster(EffectPaster effectPaster);
    ``` |
    |Add a common animated sticker.|    ```
AliyunIMixRecorder.addPaster(EffectPaster effectPaster,float sx,float sy,float sw,float sh,float rotation,boolean flip);
    ``` |
    |Remove an animated sticker.|    ```
AliyunIMixRecorder.removePaster(EffectPaster effectPaster);
    ``` |

-   Static watermark and static sticker

    |Action|Sample code|
    |------|-----------|
    |Add a static watermark or static sticker.|    ```
AliyunIMixRecorder.addImage(EffectImage effctImage);
    ``` |
    |Remove a static watermark or static sticker.|    ```
AliyunIMixRecorder.removeImage(EffectImage effctImage);
    ``` |

-   **Background music \(supported in Professional Edition and Standard Edition\)**

    |Action|Sample code|
    |------|-----------|
    |Set the background music.|    ```
AliyunIMixRecorder.setMusic(String path,long startTime,long duration);
    ``` |
    |Remove the background music.|    ```
AliyunIMixRecorder.setMusic(null, 0, 0);
    ``` |

-   Speed adjustment \(supported in Professional Edition and Standard Edition\)

    |Action|Sample code|
    |------|-----------|
    |Set the recording speed.|    ```
AliyunIMixRecorder.setRate(float rate);
    ``` |

-   **Custom rendering**

    |Action|Sample code|
    |------|-----------|
    |Set the callback for custom rendering.|    ```
AliyunIMixRecorder.setOnTextureIdCallback(OnTextureIdCallBack callback);
    ``` |

-   Photo taking

    |Action|Sample code|
    |------|-----------|
    |Take a photo with effects.|    ```
AliyunIMixRecorder.takePhoto(boolean needBitmap);
    ``` |
    |Take a photo by using the system camera feature. In this case, a photo is taken without effects.|    ```
AliyunIMixRecorder.takePicture(boolean needBitmap);
    ``` |
    |Set the photo size. This method is supported only when you use the system camera feature to take a photo.|    ```
AliyunIMixRecorder.setPictureSize(Camera.Size size);
    ``` |

-   Others

    |Action|Sample code|
    |------|-----------|
    |Configure the effect information, including the position and size of a watermark, a static sticker, or an animated sticker.|    ```
AliyunIMixRecorder.setEffectView(float xRatio,float yRatio,float widthRatio,float heightRatio,EffectBase effectBase);
    ``` |


## Start recording

|Action|Sample code|
|------|-----------|
|Start recording a video clip.|```
AliyunIMixRecorder.startRecording();
``` |
|Stop recording a video clip.|```
AliyunIMixRecorder.stopRecording();
``` |
|Stop the recording and merge the recorded video clips into one video.|```
AliyunIMixRecorder.finishRecording();
``` |

## Sample code

```
// Produce a duet. Make sure that a sample video named sample.mp4 is stored in the root directory: /sdcard/sample.mp4.
// The following code describes only the core process. You cannot directly copy and paste the following code for your project. For more information about the detailed process, see the demo.
AliyunIMixRecorder mMixRecorder = AliyunIMixRecorder createAlivcMixRecorderInstance(getApplicationContext());
if(WYSIWYG is required){
    mRecorder.setRecordRotation(0); // This setting enables WYSIWYG so that a video that is recorded in landscape mode is not automatically rotated in the produced video.
    mRecorder.setFaceDetectRotation(getPictureRotation());// For more information about the getPictureRotation() method, see the code of the demo.
}else {
    mRecorder.setRotation(getPictureRotation());
}
mMixRecorder.setDisplayView(mCameraPrvSurfaceView, mPlayPrvSurfaceView);
AliunIClipManager mClipManager = mRecorder.getClipManager();
mClipManager.setMinDuration(mMinDuration);
mClipManager.setMaxDuration(mMaxDuration);
mRecordTimelineView.setMaxDuration(mClipManager.getMaxDuration());
mRecordTimelineView.setMinDuration(mClipManager.getMinDuration());
MediaInfo mOutputInfo = new MediaInfo();
mOutputInfo.setVideoWidth(outputWidth);
mOutputInfo.setVideoHeight(outputHeight);
AliyunMixRecorderDisplayParam recorderDisplayParam = new AliyunMixRecorderDisplayParam.Builder()
        .displayMode(VideoDisplayMode.FILL)
        .layoutParam(
            new AliyunMixTrackLayoutParam.Builder()
            .centerX(0.25f)
            .centerY(0.5f)
            .widthRatio(0.5f)
            .heightRatio(1.0f)
            .build()
        )
        .build();
AliyunMixRecorderDisplayParam sampleDisplayParam = new AliyunMixRecorderDisplayParam
        .Builder()
        .displayMode(VideoDisplayMode.FILL)
        .layoutParam(new AliyunMixTrackLayoutParam.Builder()
                     .centerX(0.75f)
                     .centerY(0.5f)
                     .widthRatio(0.5f)
                     .heightRatio(1.0f)
                     .build())
        .build();
AliyunMixMediaInfoParam mInputInfo = new AliyunMixMediaInfoParam
        .Builder()
        .streamStartTimeMills(0L)
        .streamEndTimeMills(0L) // If you set the two parameters to 0L, the duration of the sample video is automatically applied.
        .mixVideoFilePath("/sdcard/sample.mp4")
        .mixDisplayParam(sampleDisplayParam)
        .recordDisplayParam(recorderDisplayParam)
        .build();
mRecorder.setMixMediaInfo(mInputInfo, mOutputInfo);
mRecorder.setRecordCallback(new RecordCallback() {
            @Override
            public void onComplete(boolean validClip, long clipDuration) {}
            @Override
            public void onFinish(String outputPath) {
                // The production is completed.
            }
            @Override
            public void onProgress(final long duration) {}
            @Override
            public void onMaxDuration() {}
            @Override
            public void onError(int errorCode) {}
            @Override
            public void onInitReady() { }
            @Override
            public void onDrawReady() {}
            @Override
            public void onPictureBack(Bitmap bitmap) { }
            @Override
            public void onPictureDataBack(byte[] data) {}
        });
mRecorder.startPreview();
mRecorder.startRecording();
mRecorder.stopRecording();
mRecorder.finishRecording();
```

