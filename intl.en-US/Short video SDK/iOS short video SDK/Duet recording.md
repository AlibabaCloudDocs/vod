# Duet recording

## Overview

The short video SDK provides the duet feature for recording a duet that consists of two videos. The core classes are AliyunMixRecorder and AliyunMixComposer.

## Edition difference

|Edition|Description|
|-------|-----------|
|Professional Edition|All features are supported.|
|Standard Edition|All features are supported.|
|Basic Edition|The duet feature is not supported.|

## Related classes

|Class|Description|
|-----|-----------|
|AliyunMixRecorder|The core class for recording a duet.|
|AliyunMixComposer|The core class for producing a video from multiple videos.|

## Terms

This section describes the terms that help you better understand the duet feature.

-   **Duet \(AliyunMixRecorder\)**

    The duet feature allows you to produce a video from two videos. One is a sample video and the other is taken by the camera. The two videos are arranged in the specified layout, such as left-right split-screen, up-down split-screen, or picture-in-picture. Each frame of the produced video contains images from the two videos, and the audio of the sample video is used as the audio of the produced video. The following figure shows sample layouts. The short video SDK allows you to customize the layout, which is described later in this topic.

    ![Duet](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7178911161/p181623.png)

-   **Track \(AliyunMixTrack\)**

    The two videos mentioned earlier are abstracted to two tracks in the short video SDK: Track A and Track B. Track A stores the video that is collected by the camera and Track B stores the sample video. This abstraction helps you better understand the concept of track layout.

-   **Track layout \(CGRect:trackDisplayFrame\)**

    In iOS, a track contains the trackDisplayFrame property when the track is created. This property specifies the position and size of the area for displaying the track in the produced video. The position and size are represented in a coordinate system with the upper-left corner of the screen as the origin \(0,0\), as shown in the following figure.

    ![Track layout](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7178911161/p181626.png)

    In the preceding figure, the resolution of the produced video is 640 × 640. Track A is displayed in the area of \(0,0,320,640\). Track B is displayed in the area of \(320,0,320,640\). You can add videos to the specified areas.


## Use AliyunMixRecorder to record a video

AliyunMixRecorder allows you to record a video and play another video simultaneously. For example, you can record a video by using the camera in the left part of the screen, and play another video in the right part of the screen.

## Initialize settings

-   Create an AliyunMixRecorder object and initialize it.

    ```
    /**
     The initialization method.
     @param param The media information.
     @param outputSize The resolution of the produced video. 
    @return The AliyunMixRecorder object. 
    */
    - (instancetype)initWithMediaInfo:(AliyunMixMediaInfoParam *)param outputSize:(CGSize)outputSize;
    ```

-   An AliyunMixMediaInfoParam object specifies the window for recording a duet, the position and size of the window, and the position and size of the sample video. The following code describes the properties:

    ```
    /**
     Required. The view of the window for recording a duet.
     */
    @property(nonatomic, strong) UIView *outputSizeView;
    
    /**
     The position and size of the window for playing the sample video.
     The SDK displays this window in the view that is specified by outputSizeView based on the value of this property.
     */
    @property(nonatomic, assign) CGRect mixVideoViewFrame;
    
    /**
     The position and size of the window for recording a video by using the camera.
     The SDK displays this window in the view specified by outputSizeView based on value of this property.
     */
    @property(nonatomic, assign) CGRect previewViewFrame;
    
    /**
     The resolution of the video that is recorded by the camera.
     */
    @property(nonatomic, assign) CGSize previewVideoSize;
    
    /**
     The path of the sample video to be added to the duet.
     */
    @property(nonatomic, copy) NSString *mixVideoFilePath;
    
    /**
     The path of the sample video to be added to the duet.
     */
    @property(nonatomic, copy) NSString *mixVideoFilePath;
    
    /**
     The start time of the sample video to be added to the duet.
     */
    @property(nonatomic, assign) CGFloat streamStartTime;
    
    /**
     The end time of the sample video to be added to the duet.
     */
    @property(nonatomic, assign) CGFloat streamEndTime;
    ```


Other properties and methods of the AliyunMixRecorder class are similar to those of the AliyunIRecorder class. The recording process that is implemented by using the AliyunMixRecorder class is similar to the one that is implemented by using the AliyunIRecorder class.

## Control preview

|Action|Sample code|
|------|-----------|
|Start the preview.|```
/** 
Start the preview.

@param cameraPosition The camera to be used for recording, which is the front or rear camera.
 */
- (void)startPreviewWithPositon:(AliyunIRecorderCameraPosition)cameraPosition;

/**
 Start the preview. By default, the front camera is used.
 */
- (void)startPreview;
``` |
|Stop the preview.|```
- (void)stopPreview;
``` |
|Destroy the recording object.|```
- (void)destroyRecorder;
``` |

## Record a video

|Action|Sample code|
|------|-----------|
|Start recording a video clip.|```
  - (int)startRecording;
``` |
|Stop recording a video clip.|```
  - (void)stopRecording;
``` |

**Note:** The startRecording and stopRecording methods must be called in pairs.

## Set other parameters

Other parameters are the same as those for recording a video by using the AliyunIRecorder class. For more information, see [Video recording](/intl.en-US/Short video SDK/iOS short video SDK/Recording.md).

