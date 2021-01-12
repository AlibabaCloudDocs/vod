# Video recording

## Overview

The short video SDK provides the basic recording feature and allows you to add recording effects such as music, speed adjustment, and face stickers. The core recording operation is AliyunIRecorder.

## Edition difference

|Edition|Description|
|-------|-----------|
|Professional Edition|All features are supported.|
|Standard Edition|The basic recording and music features are supported. The facial recognition feature is not supported.|
|Basic Edition|The basic recording feature is supported. The music and facial recognition features are not supported.|

## Video recording

|Recording process|Description|
|-----------------|-----------|
|[Set parameters](#title_151_jnn_0zr)|This step is performed to create or destroy a recording instance.|
|[Set callbacks](#title_g9z_jmg_w8z)|This step is performed to set callbacks.|
|[Control preview](#title_ec3_byr_07a)|This step is performed to start or stop the preview.|
|[Control and manage recording](#title_52f_197_i4i)|This step is performed to configure recording information.|
|[Configure effects](#title_pun_6gy_sxf)|This step is performed to configure beautification and filters for recording.|
|[Start recording](#title_k66_w19_uvm)|This step is performed to start, cancel, or stop recording a video clip.|
|[Complete recording](#title_2ov_gfv_kvv)|This step is performed to end recording.|

**Note:** The camera and microphone permissions are required for recording. Otherwise, the recording fails.

## Set parameters

-   **Initialization**

|Action|Sample code|
|------|-----------|
|Create a recording instance.|```
AliyunIRecorder recorder = AliyunRecorderCreator.getRecorderInstance(Context context);// The context parameter indicates the context of the current screen.
``` |
|Destroy the recording instance.|```
AliyunIRecorder#destroy();
``` |

-   **Output settings**

|Action|Sample code|
|------|-----------|
|Set output parameters for the recorded video.|```
AliyunIRecorder#setMediaInfo(MediaInfo mediaInfo);// For more information about the related parameters, see MediaInfo in the SDK documentation.
``` |
|Set the output path.|```
AliyunIRecorder#setOutputPath(String path);
``` |
|Set the quality of the recorded video.|```
AliyunIRecorder#setVideoQuality(VideoQuality quality);
``` |
|Set the bitrate of the recorded video.|```
AliyunIRecorder#setVideoBitrate(int bitrate);// Unit: Kbit/s.
``` |
|Set the group of pictures \(GOP\) size of the recorded video.|```
AliyunIRecorder#setGop(int gop);// Unit: frames.
``` |


## Set callbacks

|Action|Sample code|
|------|-----------|
|Set the recording callback.|```
AliyunIRecorder#setRecordCallBack(RecordCallback callBack);
``` |
|Set the callback for video frame collection.|```
AliyunIRecorder#setOnFrameCallback(OnFrameCallBack callback);
``` |
|Set the audio collection callback.|```
AliyunIRecorder#setOnAudioCallback(OnAudioCallBack callback);
``` |

## Control preview

|Action|Sample code|
|------|-----------|
|Start the preview.|```
AliyunIRecorder#startPreview();
``` |
|Stop the preview.|```
AliyunIRecorder#stopPreview();
``` |

## Control and manage recording

-   **Control recording**

    |Action|Sample code|
    |------|-----------|
    |Obtain the number of cameras.|    ```
AliyunIRecorder#getCameraCount();
    ``` |
    |Set the camera type.|    ```
AliyunIRecorder#setCamera(CameraType cameraType);
    ``` |
    |Set the camera preview parameters, including the flash mode, focus mode, zoom factor, and exposure value.|    ```
AliyunIRecorder#setCameraParam(CameraParam
cameraParam);// You can also separately set the parameters. For more information, see the following methods.
    ``` |
    |Switch between the front and rear cameras.|    ```
AliyunIRecorder#switchCamera();
    ``` |
    |Set the flash mode.|    ```
AliyunIRecorder#setLight(FlashType flashType);
    ``` |
    |Set the zoom factor.|    ```
AliyunIRecorder#setZoom(float rate);
    ``` |
    |Set the exposure value.|    ```
AliyunIRecorder#setExposureCompensationRatio(float value);
    ``` |
    |Set the focus mode.|    ```
AliyunIRecorder#setFocusMode(int mode);
    ``` |
    |Set the manual focus point.|    ```
AliyunIRecorder#setFocus(float xRatio, float yRatio);
    ``` |
    |Set the preview view.|    ```
AliyunIRecorder#setDisplayView(SurfaceView displayView);
    ``` |
    |Set the sensor rotation angle. This configuration is very important. We recommend that you carefully read the SDK documentation.|    ```
AliyunIRecorder#setRotation(int rotation);
    ``` |
    |Set the face detection angle. This configuration is very important. We recommend that you carefully read the SDK documentation.|    ```
AliyunIRecorder#setFaceDetectRotation(int rotation);
    ``` |
    |Set the video recording angle. This configuration is very important. We recommend that you carefully read the SDK documentation.|    ```
AliyunIRecorder#setRecordRotation(int rotation);
    ``` |
    |Specify whether to mute the audio during recording.|    ```
AliyunIRecorder#setMute(boolean isMute);
    ``` |

-   **Manage recording**

    |Action|Sample code|
    |------|-----------|
    |Obtain the clip manager.|    ```
AliyunIRecorder#getClipManager();
    ``` |
    |Set the maximum recording duration, which is the maximum duration of all video clips instead of a single video clip.|    ```
AliyunIClipManager#setMaxDuration(int maxDurationMs);
    ``` |
    |Set the minimum recording duration, which is the minimum duration of all video clips instead of a single video clip.|    ```
AliyunIClipManager#setMinDuration(int minDurationMs);
    ``` |
    |Obtain the total duration of video clips.|    ```
AliyunIClipManager#getDuration();
    ``` |
    |Obtain the total number of video clips.|    ```
AliyunIClipManager#getPartCount();
    ``` |
    |Delete the last video clip.|    ```
AliyunIClipManager#deletePart();
    ``` |
    |Delete the specified video clip.|    ```
AliyunIClipManager#deletePart(int index);
    ``` |
    |Delete all video clips.|    ```
AliyunIClipManager#deleteAllPart();
    ``` |
    |Obtain the paths of video clips.|    ```
AliyunIClipManager#getVideoPathList();
    ``` |


## Configure effects

-   **Beautification**

    |Action|Sample code|
    |------|-----------|
    |Set the beautification level.|    ```
AliyunIRecorder#setBeautyLevel(int level);
    ``` |
    |Turn on or off the beautification switch.|    ```
AliyunIRecorder#setBeautyStatus(boolean on);
    ``` |

-   **Common filter**

    |Action|Sample code|
    |------|-----------|
    |Add a common filter.|    ```
AliyunIRecorder#applyFilter(EffectFilter effectFilter);// You can remove a common filter by setting its path to null.
    ``` |
    |Remove a common filter.|    ```
AliyunIRecorder#applyFilter(new EffectFilter(null));
    ``` |

-   **Animated filter**

    |Action|Sample code|
    |------|-----------|
    |Add an animated filter, such as the filter that provides the effect of spirit freed from the body.|    ```
AliyunIRecorder#applyAnimationFilter(EffectFilter effectFilter);
    ``` |
    |Remove an animated filter.|    ```
AliyunIRecorder#removeAnimationFilter(EffectFilter effctFilter);
    ``` |

-   **Facial recognition \(supported only in Professional Edition\)**

    |Action|Sample code|
    |------|-----------|
    |Set face coordinates. The coordinates are required by third-party facial recognition products.|    ```
AliyunIRecorder#setFace(float[][] faces);
    ``` |
    |Specify whether to use the built-in facial recognition feature of the SDK.|    ```
AliyunIRecorder#needFaceTrackInternal(boolean need);
    ``` |
    |Specify a model file to use the built-in facial recognition feature of the SDK.|    ```
AliyunIRecorder#setFaceTrackInternalModelPath(String path);
    ``` |
    |Set the maximum number of faces that can be recognized by using the built-in facial recognition feature of the SDK.|    ```
AliyunIRecorder#setFaceTrackInternalMaxFaceCount(int maxFaceCount);
    ``` |

-   Animated sticker \(supported only in Professional Edition\)

    |Action|Sample code|
    |------|-----------|
    |Add an animated face sticker.|    ```
AliyunIRecorder#addPaster(EffectPaster effectPaster);
    ``` |
    |Add a common animated sticker.|    ```
AliyunIRecorder#addPaster(EffectPaster effectPaster,float sx,float sy,float sw,float sh,float rotation,boolean flip);
    ``` |
    |Remove an animated sticker.|    ```
AliyunIRecorder#removePaster(EffectPaster effectPaster);
    ``` |

-   **Static watermark and static sticker**

    |Action|Sample code|
    |------|-----------|
    |Add a static watermark or static sticker.|    ```
AliyunIRecorder#addImage(EffectImage effctImage);
    ``` |
    |Remove a static watermark or static sticker.|    ```
AliyunIRecorder#removeImage(EffectImage effctImage);
    ``` |

-   **Background music \(supported in Professional Edition and Standard Edition\)**

    |Action|Sample code|
    |------|-----------|
    |Set the background music.|    ```
AliyunIRecorder#setMusic(String path,long startTime,long duration);
    ``` |
    |Remove the background music.|    ```
AliyunIRecorder#setMusic(null, 0, 0);
    ``` |

-   **Speed adjustment \(supported in Professional Edition and Standard Edition\)**

    |Action|Sample code|
    |------|-----------|
    |Set the recording speed.|    ```
AliyunIRecorder#setRate(float rate);
    ``` |

-   **Custom rendering**

    |Action|Sample code|
    |------|-----------|
    |Set the callback for custom rendering.|    ```
AliyunIRecorder#setOnTextureIdCallback(OnTextureIdCallBack callback);
    ``` |

-   **Photo taking**

    |Action|Sample code|
    |------|-----------|
    |Take a photo with effects.|    ```
AliyunIRecorder#takePhoto(boolean needBitmap);
    ``` |
    |Take a photo by using the system camera feature. In this case, a photo is taken without effects.|    ```
AliyunIRecorder#takePicture(boolean needBitmap);
    ``` |
    |Set the photo size. This method is supported only when you use the system camera feature to take a photo.|    ```
AliyunIRecorder#setPictureSize(Camera.Size size);
    ``` |

-   **Others**

    |Action|Sample code|
    |------|-----------|
    |Configure the effect information, including the position and size of a watermark, a static sticker, or an animated sticker.|    ```
AliyunIRecorder#setEffectView(float xRatio,float yRatio,float widthRatio,float heightRatio,EffectBase effectBase);
    ``` |


## Start recording

|Action|Sample code|
|------|-----------|
|Start recording a video clip.|```
AliyunIRecorder#startRecording();
``` |
|Cancel recording a video clip.|```
AliyunIRecorder#cancelRecording();
``` |
|Stop recording a video clip.|```
AliyunIRecorder#stopRecording();
``` |

## Complete recording

|Action|Sample code|
|------|-----------|
|Stop the recording and merge the recorded video clips into one video.|```
AliyunIRecorder#finishRecording();
``` |
|Stop the recording and generate the configuration information of the recorded video clips without merging the video clips.|```
AliyunIRecorder#finishRecordingForEdit();
``` |

