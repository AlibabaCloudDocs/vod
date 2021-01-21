# Video recording

## Overview

The short video SDK provides the basic recording feature and allows you to add recording effects such as music, speed adjustment, and face stickers. The core recording class is AliyunIRecorder.

## Edition difference

|Edition|Description|
|-------|-----------|
|Professional Edition|All features are supported.|
|Standard Edition|The basic recording and music features are supported. The facial recognition feature is not supported.|
|Basic Edition|The basic recording feature is supported. The music and facial recognition features are not supported.|

## Related classes

|Class|Description|
|-----|-----------|
|AliyunIRecorder|The core recording class.|
|AliyunClipManager|The clip manager class. It is used to obtain clip information and delete video clips.|
|AliyunIRecorderDelegate|The recording delegation protocol.|

## Recording process

**Note:** The camera and microphone permissions are required for recording. Otherwise, the recording fails.

The following figure shows the recording process.

![Recording process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0978911161/p185015.png)

## Initialize settings

**Note:**

-   taskPath specifies the path of the folder for storing recording-related configuration information.
-   The aspect ratio of the preview object must be the same as that of the videoSize object.

|Action|Sample code|
|------|-----------|
|Initialize an instance.|```
- (instancetype)initWithDelegate:(id<AliyunIRecorderDelegate>)delegate videoSize:(CGSize)videoSize;
``` |
|Set taskPath.|```
@property (nonatomic, copy) NSString *taskPath;
``` |
|Set the path of the recorded video.|```
@property (nonatomic, copy) NSString *outputPath;
``` |
|Set the preview view.|```
@property (nonatomic, strong) UIView *preview;
``` |

## Control preview

|Action|Sample code|
|------|-----------|
|Start the preview.|```
- (void)startPreview;
- (void)startPreviewWithPositon:(AliyunIRecorderCameraPosition)cameraPosition;
``` |
|Stop the preview.You must stop the preview when the recording is completed or the application is switched to the background.

|```
- (void)stopPreview;
``` |
|Destroy the recording object.After the preview is completed, destroy the recording object to release recording resources.

|```
- (void)destroyRecorder;
``` |

## Set recording parameters

**Note:** You can set multiple recording parameters. You can set the parameters only during preview, but not during recording.

|Action|Sample code|
|------|-----------|
|Set the exposure value.|```
@property (nonatomic, assign) CGFloat exposureValue;
``` |
|Set the resolution of the video that is collected by using the front camera.|Default value: AVCaptureSessionPreset640x480. For more information, see the AVCaptureSession.h file.

```
@property (nonatomic, copy) NSString *frontCaptureSessionPreset;
``` |
|Set the resolution of the video that is collected by using the rear camera.|Default value: AVCaptureSessionPreset1280x720. For more information, see the AVCaptureSession.h file.

```
@property (nonatomic, copy) NSString *backCaptureSessionPreset;
``` |
|Set the camera angle.|```
@property (nonatomic, assign) int cameraRotate;
``` |
|Set the manual focus point.|```
@property (nonatomic, assign) CGPoint focusPoint;
``` |
|Set the zoom factor.|Each time you call the videoZoomFactor method, the actual zoom factor is 1/100 of the specified value. For example, if you set the value of videoZoomFactor to 10.0f, the actual zoom factor is 0.1f.

If the front camera is used to record the video, this setting is invalid.

```
@property (nonatomic, assign) CGFloat videoZoomFactor;
``` |
|Set the encoding mode.|```
/**
0: software encoding. 1: hardware encoding.*/
@property (nonatomic, assign) int encodeMode;
``` |
|Set the keyframe interval.|Default value: 5. Recommended values: 1 to 300.

```
@property (nonatomic, assign) int GOP;
``` |
|Set the recording frame rate.|Default value: 25.

```
@property (nonatomic, assign) int recordFps;
``` |
|Specify whether to mute the audio during recording.|If music is added during recording, this setting is invalid.

```
@property (nonatomic, assign) BOOL mute;
``` |
|Set the video quality.|If the bitrate parameter is set, this setting is invalid.

```
@property (nonatomic, assign) AliyunVideoQuality videoQuality;
``` |
|Set the bitrate of the output video. Unit: bit/s.|```
@property (nonatomic, assign) int bitrate;
``` |
|Set the video format.|The short video SDK supports the following video formats:

-   kCVPixelFormatType\_420YpCbCr8BiPlanarFullRange
-   kCVPixelFormatType\_420YpCbCr8BiPlanarVideoRange
-   kCVPixelFormatType\_ 32BGRA

Default format: kCVPixelFormatType\_420YpCbCr8BiPlanarFullRange.

```
@property (nonatomic, assign) AliyunIRecorderVideoOutputPixelFormatType outputType;
``` |
|Asynchronously obtain an image that is taken.|```
/**
image: the rendered image that is collected.
rawImage: the raw image that is collected.
*/
- (void)takePhoto:(void (^)(UIImage *image, UIImage *rawImage))handler;
``` |
|Switch between the front and rear cameras.|```
/**
@return The camera position after switching.
*/
- (AliyunIRecorderCameraPosition)switchCameraPosition;
``` |
|Circularly switch among flash modes.|The following flash modes are supported: off, on, and auto. Switching order: off -\> on -\> auto. Default value: off.

```
/**
@return The flash mode after switching.
*/
- (AliyunIRecorderTorchMode)switchTorchMode;
``` |
|Switch to the specified flash mode.|```
/**
@param torchMode The specified flash mode.
@return  return YES if success
*/
- (BOOL)switchTorchWithMode:(AliyunIRecorderTorchMode)torchMode;
``` |

## Configure recording effects

-   **Beautification**

    |Action|Sample code|
    |------|-----------|
    |Turn on or off beautification.|    ```
@property (nonatomic, assign) BOOL beautifyStatus;
    ``` |
    |Set the beautification level.|Valid values: \[0, 100\].

    ```
@property (nonatomic, assign) int beautifyValue;
    ``` |

-   **Filter**

    The filter resources of the short video SDK are stored in the filter folder. The filter folder contains a configuration file and related resources. AliyunEffectFilter indicates a filter resource. You can call the initialization method to create a filter instance. The path parameter specifies the path of the folder that stores the filter resource.

    |Action|Sample code|
    |------|-----------|
    |Generate a filter object.|    ```
- (id)initWithFile:(NSString *)path;
    ``` |
    |Add a filter.|Filters cannot be overlaid. The new filter replaces the existing one each time you call the applyFilter method.

    ```
- (int)applyFilter:(AliyunEffectFilter *)filter;
    ``` |
    |Remove a filter.|    ```
- (void)deleteFilter;
    ``` |

-   **Animated filter**

    Both animated filters and regular filters are created by using AliyunEffectFilter, but they use different resources. The demo provides the resource files of several animated filters, such as jitter, phantom, sci-fi, hazy, and ghost.

    |Action|Sample code|
    |------|-----------|
    |Add an animated filter.|    ```
- (int)applyAnimationFilter:(AliyunEffectFilter *)filter;
    ``` |
    |Remove an animated filter.|    ```
- (void)deleteAnimationFilter;
    ``` |

-   **Music**

    AliyunEffectMusic indicates a music resource. You can call the initialization method to create a music instance. The path parameter specifies the path of the music resource file.

    |Action|Sample code|
    |------|-----------|
    |Generate a music object.|    ```
- (id)initWithFile:(NSString *)path;
    ``` |
    |Add music.|    ```
- (int)applyMusic:(AliyunEffectMusic *)music;
    ``` |

    **Note:** You can call this method only before recording starts. This method cannot be called during or after recording.

-   **MV**

    The music video \(MV\) resources of the short video SDK are stored in the MV folder. The MV folder contains a configuration file and related resources. The downloaded MV package contains four folders with MV resources in different aspect ratios to apply to different output resolutions. AliyunEffectMV indicates an MV resource. You can call the initialization method to create an MV instance. The path parameter specifies the path of the folder that stores the MV resource.

    |Action|Sample code|
    |------|-----------|
    |Generate an MV object.|    ```
- (id)initWithFile:(NSString *)path;
    ``` |
    |Add an MV.|    ```
- (int)applyMV:(AliyunEffectMV *)mv;
    ``` |
    |Remove an MV.|    ```
[recorder applyMV:nil]
    ``` |

-   **Sticker and facial recognition**

    The sticker base class is AliyunEffectPaster.

    |Action|Sample code|
    |------|-----------|
    |Add an animated sticker.|    ```
/**
@param paster The animated sticker.
*/
- (int)applyPaster:(AliyunEffectPaster *)paster;
    ``` |
    |Specify whether to enable facial recognition.|After facial recognition is enabled, the system automatically tracks faces when animated face stickers are detected.

    ```
@property (nonatomic, assign) BOOL useFaceDetect;
    ``` |
    |Set the maximum number of faces that can be recognized.|    ```
/**
Maximum value: 3. Minimum value: 1. If facial recognition is not required, set the useFaceDetect parameter to NO.
*/
@property (nonatomic, assign) int faceDetectCount;
    ``` |
    |Specify whether animated face stickers are attached to faces in real time.|Default value: YES. If animated face stickers are attached to faces in real time, the effect is better, but the video may stutter on earlier devices. If animated face stickers are not attached to faces in real time, the video is smooth, but the effect is poor.

We recommend that you set this parameter to YES for iPhone 6 and later models and to NO for models earlier than iPhone 6.

    ```
@property (nonatomic, assign) BOOL faceDectectSync;
    ``` |
    |Remove an animated sticker.|    ```
`- (void)deletePaster:(AliyunEffectPaster *)paster;`
    ``` |

-   **Watermark**

    You can set a watermark by adding an image and rendering it.

    Set the position of an animated sticker or a watermark.

    ```
    /**
    @param rect The position in the format of (x,y,width,height), where x, y, width, and height are all ratios.
    @param effect The specified effect. Only the watermark and regular animated sticker effects are supported.
    */
    - (void)setEffectView:(CGRect)rect effect:(AliyunEffect *)effect;
    ```

    **Note:** The rect parameter specifies the position in the format of \(x,y,width,height\), where x, y, width, and height are all ratios. For example, if the size of the video view is \(400,400\) and the animated sticker position is \(50,50,100,100\), the value of the rect parameter is \(0.125,0.125,0.25,0.25\). The effect parameter specifies the effect. Only the watermark and regular animated sticker effects are supported.

-   **Custom rendering**

    The short video SDK provides multiple rendering callbacks. The rendering callbacks include audio callbacks for services such as audio rendering, and video callbacks such as data and texture callbacks.

    |Action|Sample code|
    |------|-----------|
    |Return the raw video data.|    ```
/**
@param sampleBuffer The video data.
*/
- (void)recorderOutputVideoRawSampleBuffer:(CMSampleBufferRef)sampleBuffer;
    ``` |
    |Return the raw audio data.|    ```
/**
@param sampleBuffer The audio data.
*/
- (void)recorderOutputAudioRawSampleBuffer:(CMSampleBufferRef)sampleBuffer;
    ``` |
    |Perform custom rendering 1.|    ```
/**
@param sampleBuffer The raw data.
@return The pixel buffer after custom rendering.
*/
- (CVPixelBufferRef)customRenderedPixelBufferWithRawSampleBuffer:(CMSampleBufferRef)sampleBuffer;
    ``` |
    |Perform custom rendering 2.|Use the pixel buffer and the ID of the texture. Only the BGRA format is supported.

    ```
/**
@param pixelBuffer The camera data.
@param textureName The texture of the camera data.
@return The ID of the texture after custom rendering.
*/
- (NSInteger)recorderOutputVideoPixelBuffer:(CVPixelBufferRef)pixelBuffer textureName:(NSInteger)textureName;
    ``` |
    |Perform custom rendering 3.|    ```
/**
@param srcTexture The ID of the texture for the raw video frame.
@param size The size of the texture for the raw video frame. @return The ID of the texture.
*/
- (int)customRender:(int)srcTexture size:(CGSize)size;
    ``` |
    |Perform custom rendering 4.|    ```
/**
This method must be implemented when the camera data is in BGRA or YUV format.
@param textureName The ID of the raw texture.
@return The ID of the texture after custom rendering.
*/
- (NSInteger)recorderOutputVideoTextureName:(NSInteger)textureName textureSize:(CGSize)textureSie;
    ```

    ```
/**
This method must be implemented only when the camera data is in YUV format.
@param textureName The ID of the raw UV texture.
@return The ID of the texture after custom rendering.
*/
- (NSInteger)recorderOutputVideoUVTextureName:(NSInteger)textureName;
    ``` |


## Record a video

|Action|Sample code|
|------|-----------|
|Start recording a video clip.|The short video SDK allows you to record a single video clip or multiple video clips. Call this method in the preview status to start recording.

```
- (int)startRecording;
``` |
|Stop recording a video clip.|```
- (void)stopRecording;
``` |

**Note:**

-   After you call the stopRecording method, the short video SDK saves the recorded video. You can perform other operations only after you receive the - \(void\)recorderDidStopRecording callback of AliyunIRecorderDelegate.
-   The startRecording and stopRecording methods must be called in pairs. They can be called one or more times. The short video SDK generates one or more temporary video files.

## Complete recording

Complete recording.

```
- (void)finishRecording;
```

**Note:** After the - \(void\)recorderDidFinishRecording callback of AliyunIRecorderDelegate is received, the recording is completed and the recorded video file is saved in the path that is specified by outputPath.

## Handle events

You must handle special events, for example, the screen is locked, a call comes in, or the application is switched to the background.

You must monitor the UIApplicationWillResignActiveNotification event. Before the application enters the Inactive state, call the stopRecording and stopPreview methods to stop the preview. You must also monitor the UIApplicationDidBecomeActiveNotification event. After the application enters the Active state, call the startPreview method to start preview again.

## Sample

```
- (void)viewDidLoad {

    // Initialize an AliyunIRecorder instance.
    self.recorder = [[AliyunIRecorder alloc] initWithDelegate:self videoSize:CGSizeMake(720,1280)];
    self.recorder.preview = self.previewView;
    self.recorder.outputPath = The path of the recorded video;
    self.recorder.outputType = AliyunIRecorderVideoOutputPixelFormatType420f; // The facial recognition feature supports only the data in YUV format.
    self.recorder.taskPath = taskPath;
    // Set video clip parameters.
    self.clipManager = self.recorder.clipManager;
    self.clipManager.maxDuration = 15;
    self.clipManager.minDuration = 0.5;
}

- (void)recordButtonTouchesBegin {
    // Start recording when the recording button is tapped.
    [self.recorder startRecording];
}

- (void)recordButtonTouchesEnd {
    // Stop recording when the recording button is tapped again.
    [self.recorder stopRecording];
}

- (void)recorderDidStopRecording {
    // Complete recording when the recording completion callback is received.
    [self.recorder finishrecording]
}

- (void)recorderDidStopWithMaxDuration {
    // Complete recording when a callback is received indicating that the maximum duration is reached.
    [self.recorder finishrecording]
}

- (void)recorderDidFinishRecording {
    // The recording is completed and the video has been saved to the specified path.
}
```

