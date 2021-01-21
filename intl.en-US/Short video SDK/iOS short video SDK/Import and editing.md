# Import and editing

## Overview

The short video SDK allows you to import videos or images and produce videos with extensive effects such as filters, dubbing, time effects, and transitions. The core editing class is AliyunEditor.

## Edition difference

|Edition|Description|
|-------|-----------|
|Professional Edition|All features are supported.|
|Standard Edition|Basic features are supported. A license is required to use advanced features.|
|Basic Edition|The import and editing features are not supported.|

## Import and editing

The following figure shows the import and editing process.

![Import and editing](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9848911161/p181691.png)

**Note:**

-   The startEdit and stopEdit methods must be called in pairs. After you call the startEdit method, the SDK internally creates resources. After you call the stopEdit method, the SDK internally releases the resources. You must call the stopEdit method before an editor is destroyed. Otherwise, memory leak occurs.
-   Media clips must be determined before editing. Call the media clip management method AliyunIClipConstructor before you call the startEdit method.
-   Call the playback control, editing, and production methods after you call the startEdit method and before you call the stopEdit method.

## Initialization

**Set the TaskPath parameter**

The TaskPath parameter specifies the path of the folder that stores configuration files and temporary files. The configuration files contain the video material information such as the path, output bitrate, group of pictures \(GOP\) value, and resolution. AliyunEditor reads parameter settings from the configuration files in the folder that is specified by the TaskPath parameter. You can set the TaskPath parameter in the following ways:

-   When you record videos for editing, initialize an AliyunIRecorder object and set the TaskPath parameter to the path of an empty folder. When you call recording methods, a configuration file is automatically created and video resources are automatically added.
-   When you import videos for editing, initialize an AliyunImporter object and set the TaskPath parameter to the path of an empty folder. Call the methods of the AliyunIClipConstructor protocol to add video resources. Then, call the `- (void)generateProjectConfigure` method to create a configuration file.

AliyunImporter is used to generate the editing configuration file. The following table describes the actions that are supported by AliyunImporter.

|Action|Sample code|
|------|-----------|
|Initialize an instance.|```
/**
 Initialize an AliyunImporter instance. @param TaskPath The path of the folder. Make sure that the folder exists. 
@param outputSize The resolution of the output video, in even numbers. 
@return AliyunImporter
 */
- (instancetype)initWithPath:(NSString *)TaskPath outputSize:(CGSize)outputSize;
``` |
|Set video output parameters.|```
/**
 Set video output parameters.
 @param videoParam The video output parameters. 
*/
- (void)setVideoParam:(AliyunVideoParam *)videoParam;
``` |
|Generate a configuration file.|```
/**
/**
 Generate a configuration file in the folder that is specified by the TaskPath parameter.
 */
- (void)generateProjectConfigure;
``` |
|Add a media clip.|AliyunImporter implements the AliyunIClipConstructor protocol and is used to configure media clips.

AliyunClip indicates a video clip or an image clip. You can call the initialization method to create an AliyunClip object.

```
- (void)addMediaClip:(AliyunClip *)clip;
``` |
|Create a video clip.|```
/**
 Create a video clip.
 @param path The path of the video.
 @param animDuration The duration of the transition animation.
 @return The video clip.
 */
- (instancetype)initWithVideoPath:(NSString *)path
                     animDuration:(CGFloat)animDuration;
``` |
|Create an image clip.|```
/**
 Create an image clip.
 @param path The path of the image.
 @param duration The display duration of the image.
 @param animDuration The duration of the transition animation.
 @return The image clip.
 */
- (instancetype)initWithImagePath:(NSString *)path
                         duration:(CGFloat)duration
                     animDuration:(CGFloat)animDuration;
``` |
|Create a GIF clip.|```
 Create a GIF clip.
@param path The path of the GIF file. 
@ return The GIF clip.
 */
- (instancetype)initWithGifPath:(NSString *)path;
``` |

**Initialize an editor**

Call the initialization method to create an AliyunEditor object.

```
 /**
 @param TaskPath The path of the folder.
 @param preview The view for previewing the editing.
 @return Editor
 */
 - (instancetype)initWithPath:(NSString *)TaskPath preview:(UIView *)preview;
```

**Note:** The TaskPath parameter must be set to the path of the folder where a configuration file has been generated. The preview parameter specifies the user interface \(UI\) view for preview. The aspect ratio of the UI view for preview must be the same as that of the output video. If you want to produce a video without the need to preview it, set the preview parameter to nil.

**Manage media clips**

The editor can call the `-(id<AliyunIClipConstructor>)getClipConstructor` method to obtain the media clip manager for managing media clips. AliyunIClipConstructor is used to add and remove media clips. The following table describes the actions that are supported by AliyunIClipConstructor.

|Action|Sample code|
|------|-----------|
|Add a media clip.|```
/**
@param clip The media clip.
*/
- (void)addMediaClip:(AliyunClip *)clip;
``` |
|Specify all media clips.|```
/**
@param clips The list of media clips.
*/
- (void)setMediaClips:(NSArray<AliyunClip *> *)clips;
``` |
|Add a media clip to the specified position.|```
/**
@param clip The media clip.
@param index index
*/
- (void)addMediaClip:(AliyunClip *)clip atIndex:(NSInteger)index;
``` |
|Update a media clip.|```
/**
@param clip The media clip.
@param index index
*/
- (void)updateMediaClip:(AliyunClip *)clip atIndex:(NSInteger)index;
``` |
|Remove a media clip.|```
/**
@param index index
*/
- (void)deleteMediaClipAtIndex:(NSInteger)index;
``` |
|Remove all media clips.|```
- (void)deleteAllMediaClips;
``` |
|Obtain a media clip.|```
/**
@param index index
@return The media clip.
*/
- (AliyunClip *)mediaClipAtIndex:(NSInteger)index;
``` |
|Obtain all media clips.|```
/**
@return The list of media clips.
*/
- (NSArray<AliyunClip *> *)mediaClips;
``` |

**Note:** Manage media clips before you call the startEdit method or after you call the stopEdit method.

## Playback control

**Control playback**

|Action|Sample code|
|------|-----------|
|Obtain the player.|```
 - (id<AliyunIPlayer>)getPlayer;
``` |
|Start the playback.|```
- (int)play;
``` |
|Seek to a point in time.|```
/**
@param time The point in time. Unit: seconds.
*/
-(int)seek:(float)time;
``` |
|Draw a frame.|```
/**
@param time The point in time. Unit: seconds.
*/
-(int)draw:(float)time;
``` |
|Pause the playback.|```
- (int)pause;
``` |
|Resume the playback.|```
- (int)resume;
``` |
|Check whether the player is playing a video.|```
/**
@return The player is playing a video.
*/
- (BOOL)isPlaying;
``` |
|Start the playback all over again.|```
- (int)replay;
``` |
|Stop the playback.|```
/**
* If the status is normal, ALIVC_COMMON_RETURN_SUCCESS is returned.
* If the status is invalid, ALIVC_COMMON_INVALID_STATE is returned.
*/
- (int)stop;
``` |
|Obtain the total playback duration, in seconds.|```
/**
@return The total duration.
*/
- (double)getDuration;
``` |
|Obtain the current playback position, in seconds.|```
- (double)getCurrentTime;
``` |
|Obtain the duration of the original video stream, in seconds.|```
/**
@return The total duration.
*/
- (double)getStreamDuration;
``` |
|Obtain the playback position in the original video stream, in seconds.|```
- (double)getCurrentStreamTime;
``` |
|Obtain the time at which a video clip starts to be played in the playback timeline, in seconds.|```
/**
@param idx The index of the video clip.
@return The point in time. Unit: seconds.
*/
- (double)getClipStartTimeAtIndex:(int)idx;
``` |
|Set the refresh rate of the player.|Default value: 30. Maximum value: 60. Unit: frames per second. We recommend that you set the fps parameter to a value greater than or equal to 20.

```
/**
@param fps The refresh rate.
*/
- (void)setRefreshFps:(double)fps;
``` |

**Listen to playback callbacks**

The delegate object needs to implement the AliyunIPlayerCallback protocol to monitor the playback status. The following table describes the related callback events.

|Callback event|Sample code|
|--------------|-----------|
|The playback starts.|```
- (void)playerDidStart;
``` |
|The playback ends.|To play a video again from the start after the playback ends, call the replay method.

```
- (void)playerDidEnd;
``` |
|The seeking ends.|```
- (void)seekDidEnd;
``` |
|The playback progress is returned.|```
/**
@param playSec The playback position.
@param streamSec The playback duration of the stream.
*/
- (void)playProgress:(double)playSec streamProgress:(double)streamSec;
``` |
|A playback error occurs.|```
/**
@param errorCode The error code.
*/
- (void)playError:(int)errorCode;
``` |

**Note:**

-   The play and stop methods must be called in pairs. The pause and resume methods must be called in pairs.
-   If you call the seek method or add an effect such as music video \(MV\) or music, the player is paused. You must call the resume method to resume the playback.
-   Time effects affect the playback timeline. The following examples show the differences between getDuration and getStreamDuration and between getCurrentTime and getCurrentStreamTime:
    -   The duration of a video is 15s and the entire video is played at twice the speed. In this case, getDuration returns 7.5s and getStreamDuration returns 15s. If getCurrentTime returns 3.5s, getCurrentStreamTime returns 7s.
    -   The duration of a video is 15s and the entire video is played at half the speed. In this case, getDuration returns 30s and getStreamDuration returns 15s. If getCurrentTime returns 10s, getCurrentStreamTime returns 7.5s.
    -   The duration of a video is 15s and the entire video is reversely played. In this case, getDuration returns 15s and getStreamDuration returns 15s. If getCurrentTime returns 6s, getCurrentStreamTime returns 9s.

## Effect settings

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
- (int)removeFilter;
    ``` |

-   **Time effect**

    A time effect refers to repetition, speed adjustment, or reverse playback of a video. AliyunEffectTimeFilter indicates a time effect. You can run the following sample code to add a time effect:

    ```
    AliyunEffectTimeFilter *timeFilter = [[AliyunEffectTimeFilter alloc] init];
      // Specify the start time of the time effect.
      timeFilter.startTime = 1;
      // Specify the end time of the time effect.
      timeFilter.endTime = 2;
      // Add a speed adjustment effect.
      timeFilter.type = TimeFilterTypeSpeed;
      // Play the video at half the speed.
      timeFilter.param = 0.5;
      // Apply the time effect.
      [self.editor applyTimeFilter:timeFilter];
      // The playback is paused after you apply the time effect. Call the resume method to resume the playback.
      [self.player resume];
    ```

    The time effect types include TimeFilterTypeSpeed, TimeFilterTypeRepeat, and TimeFilterTypeInvert. A value of TimeFilterTypeSpeed indicates speed adjustment. A value of TimeFilterTypeRepeat indicates repetition. A value of TimeFilterTypeInvert indicates reverse playback. If the time effect type is set to TimeFilterTypeSpeed, set the param parameter to a specific playback speed. If the time effect type is set to TimeFilterTypeRepeat, set the param parameter to a specific number of repetitions.

    **Note:** The reverse playback and repetition effects apply only to a single video clip, and cannot be overlaid with other time effects. We recommend that you transcode the video before you apply the reverse playback effect. Otherwise, video stuttering may occur.

-   **MV**

    The MV resources of the short video SDK are stored in the MV folder. The MV folder contains a configuration file and related resources. The downloaded MV package contains four folders with MV resources in different aspect ratios to apply to different output resolutions. AliyunEffectMV indicates an MV resource. You can call the initialization method to create an MV instance. The path parameter specifies the path of the folder that stores the MV resource.

    |Action|Sample code|
    |------|-----------|
    |Generate an MV object.|    ```
- (id)initWithFile:(NSString *)path;
    ``` |
    |Add an MV.|MVs cannot be overlaid. The new MV replaces the existing one each time you call the applyMV method.

    ```
- (int)applyMV:(AliyunEffectMV *)mv;
    ``` |
    |Remove an MV.|    ```
- (int)removeMV;
    ``` |
    |Remove the music of an MV.|    ```
-(int)removeMVMusic;
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
    |Remove a specific music stream.|The short video SDK allows you to overlay multiple music streams. You can run the following sample code to remove a specific music stream:

    ```
- (int)removeMusic:(AliyunEffectMusic *)music;
    ``` |
    |Remove all music streams.|    ```
- (int)removeMusics;
    ``` |

    You can play a specific part of a music stream and play the music stream in a specific time period of a video. You can run the following sample code to configure properties:

    ```
    @property (nonatomic, assign) CGFloat startTime;        // The start time of the part to be played in the music stream.
    @property (nonatomic, assign) CGFloat duration;         // The duration of the part to be played in the music stream.
    @property (nonatomic, assign) CGFloat streamStartTime;  // The time when the music stream starts to be played in the playback timeline.
    @property (nonatomic, assign) CGFloat streamDuration;   // The playback duration of the music stream in the playback timeline.
    ```

    For example, play the part from the fifth second to the tenth second in a music stream and repeat this part of music twice from the eighth second of a video. You can run the following sample code:

    ```
    AliyunEffectMusic *music = [[AliyunEffectMusic alloc] initWithFile: 'The path of the music file'];
    music.startTime = 5;
    music.duration = 5;
    music.streamStartTime = 8;
    music.streamDuration = 10;
    ```

    **Note:** After you call music-related methods, the player is paused. You must call the resume method to resume the playback.

-   **Dubbing**

    AliyunEffectDub indicates a dubbing resource and inherits AliyunEffectMusic. The methods for configuring dubbing are basically the same as those for configuring music. The following table describes the related actions.

    |Action|Sample code|
    |------|-----------|
    |Add dubbing.|    ```
- (int)applyDub:(AliyunEffectDub *)dub;
    ``` |
    |Remove a dubbing track.|    ```
- (int)removeDub:(AliyunEffectDub *)dub;
    ``` |
    |Remove all dubbing tracks.|    ```
- (int)removeDubs;
    ``` |

    **Note:** Dubbing differs from music in that dubbing supports speed adjustment whereas music does not. For example, a video is played at twice the speed. In this case, the dubbing is also played at twice the speed, but the music is played at the normal speed.

-   **Sound effect**

    The short video SDK allows you to add sound effects to each audio stream and provides various sound effects such as lolita, uncle, reverberation, and echo.

    AliyunAudioEffectType indicates a sound effect type. The weight parameter specifies the weight of the sound effect. Valid values: 0 to 100. The stream ID of a music stream is stored in the effectVid property of AliyunEffectMusic. The stream ID of an MV stream is stored in the audioEffectVid property of AliyunEffectMV. The stream ID of a main stream is stored in the streamId property of AliyunClip.

    |Action|Sample code|
    |------|-----------|
    |Set the sound effect of a single stream.|    ```
  - (int)setAudioEffect:(AliyunAudioEffectType)type weight:(int)weight streamId:(int)streamId;
    ``` |
    |Remove the sound effect of a single stream.|Sound effects can be overlaid. To switch to a new sound effect, you must remove the existing sound effect.

    ```
- (int)removeAudioEffect:(AliyunAudioEffectType)type streamId:(int)streamId;
    ``` |
    |Set the sound effect of main streams.|In addition to the sound effect of a single stream, the short video SDK allows you to set the sound effect of main streams.

    ```
- (int)setMainStreamsAudioEffect:(AliyunAudioEffectType)type weight:(int)weight;
    ``` |
    |Remove the sound effect of main streams.|    ```
- (int)removeMainStreamsAudioEffect:(AliyunAudioEffectType)type;
    ``` |

-   **Other audio settings**

    |Action|Sample code|
    |------|-----------|
    |Mute audio.|    ```
- (int)setMute:(BOOL)mute;
    ``` |
    |Set the volume.|Default value: 100. If the volume parameter is set to a value greater than 100, the sound may be distorted. We recommend that you set the volume parameter to a value in the range of 0 to 100.

    ```
- (int)setVolume:(int)volume;
    ``` |
    |Set the volume of main streams.|Main streams refer to one or more video clips that are imported for editing.

    ```
- (int)setMainStreamsAudioWeight:(int)weight;
    ``` |
    |Set the volume of a stream.|Each added video, music, dubbing, or MV stream is assigned a unique stream ID. The stream ID of a music stream is stored in the effectVid property of AliyunEffectMusic. The stream ID of an MV stream is stored in the audioEffectVid property of AliyunEffectMV. The stream ID of a main stream is stored in the streamId property of AliyunClip.

    ```
- (int)setAudioWeight:(int)weight streamId:(int)streamId;
    ``` |
    |Denoise main streams.|    ```
- (int)setMainStreamsAudioDenoise:(BOOL)denoise;
    ``` |
    |Denoise an audio stream.|    ```
- (int)setAudioDenoise:(BOOL)denoise streamId:(int)streamId;
    ``` |

-   **Animated sticker**

    The short video SDK supports three types of stickers: common sticker, subtitle, and bubble subtitle. You can add stickers by using the AliyunPasterManager class or the underlying class AliyunPasterRender.

    -   Use AliyunPasterManager

        The following table describes the related classes.

        |Class|Description|
        |-----|-----------|
        |AliyunPasterManager|Creates an AliyunPasterController object.|
        |AliyunPasterBaseView|Obtains the status of the upper-layer UI.|
        |AliyunPasterBaseView|Informs the short video SDK of user modifications on the UI. Then, the short video SDK synchronizes the UI status to the renderer to complete sticker rendering.|

        You can use AliyunPasterManager to add stickers. The following figure shows the schematic diagram of the model-view-controller \(MVC\) design.

        ![Schematic diagram of the MVC design](../images/p181774.png)

        You can learn from the preceding schematic diagram that AliyunPasterManager is used to create an AliyunPasterController object. The controller calls the AliyunPasterBaseView method to obtain the upper-layer UI status. User modifications on the UI are sent to the controller by using AliyunPasterBaseView. Then, the controller synchronizes the UI status to the renderer to complete sticker rendering. This way, you can customize the UI as needed, provided that AliyunPasterUIEventProtocol is implemented.

        AliyunPasterViewUIEventProtocol supports the following actions:

        ```
          - (void)eventBoundsDidChanged:(CGRect)aBounds; // Synchronize the size of the animated sticker to the controller for rendering.
          - (void)eventCenterDidChanged:(CGPoint)aCenter; // Synchronize the center point of the animated sticker to the controller for rendering.
          - (void)eventRotateDidChanged:(CGFloat)aRotate; // Synchronize the rotation angle of the animated sticker to the controller for rendering.
          - (void)eventTextBoundsDidChanged:(CGRect)aBounds; // Synchronize the text size to the controller for rendering.
          - (void)eventTextCenterDidChanged:(CGPoint)aCenter; // Synchronize the text position to the controller for rendering.
          - (void)eventMirrorChanged:(BOOL)isMirror; // Specify whether mirroring is enabled.
          - (void)eventPasterViewClosed:(UIView *)pasterView; // Close the animated sticker UI.
          - (void)eventEditDidEnd; // Complete the editing.
        ```

        AliyunPasterManager manages all animated stickers. To ensure that the position and size of each animated sticker are correctly rendered, first specify the editing area and rendering area. The following table describes the related actions.

        |Action|Sample code|
        |------|-----------|
        |Specify the editing area.|        ```
/**
In general, the editing area needs to cover the entire video area, and all the upper-layer animated stickers are added to the editing area.
*/
@property (nonatomic, assign) CGSize displaySize;
        ``` |
        |Set the resolution of the output video.|        ```
/**
During production, the size of the rendering area is calculated based on the output resolution.
*/
@property (nonatomic, assign) CGSize outputSize;
        ``` |
        |Specify the rendering area.|The rendering area is used to convert logical pixels to physical pixels.

        ```
/**
The rendering area is used to convert logical pixels to physical pixels. You can call the [_editor getPreviewRenderSize] method to obtain the size of the rendering area.
*/
@property (nonatomic, assign) CGSize previewRenderSize;
        ``` |
        |Add an animated sticker.|        ```
/**
@param filePath The path of the animated sticker file.
@param st The time when the animated sticker starts to be displayed.
@param duration The display duration of the animated sticker.
@return The animated sticker controller.
*/
- (AliyunPasterController *)addPaster:(NSString *)filePath startTime:(double)st duration:(double)duration;
        ``` |
        |Add a subtitle.|        ```
/**
@param text The text. If no text is specified, you can edit text when the subtitle is displayed for the first time. If text is specified, the text is displayed and not editable.
@param bounds The size of the subtitle.
@param st The time when the subtitle starts to be displayed.
@param duration The display duration of the subtitle.
@return The animated sticker controller.
*/
- (AliyunPasterController *)addSubtitle:(NSString *)text bounds:(CGRect)bounds startTime:(CGFloat)st duration:(CGFloat)duration;
        ``` |
        |Obtain all animated sticker controllers.|        ```
/**
@return The array of animated sticker controllers.
*/
- (NSArray *)getAllPasterControllers;
        ``` |
        |Obtain an animated sticker controller based on the ID.|        ```
/**
@param obj id
@return pasterController
*/
- (AliyunPasterController *)getPasterControllerByObj:(id)obj;
        ``` |
        |Check whether an animated sticker exists in a specific position.|        ```
/**
@param point The position that you click.
@param time The current playback position in the video.
@return The animated sticker controller is returned if an animated sticker exists in this position at the moment. Otherwise, nil is returned.
*/
- (AliyunPasterController *)touchPoint:(CGPoint)point atTime:(double)time;
        ``` |
        |Remove all animated stickers.|        ```
- (void)removeAllPasterControllers;
        ``` |
        |Remove an animated sticker controller.|        ```
/**
API_AVAILABLE(3.7.0)
@param pasterController The animated sticker controller to be removed.
*/
- (void)removePasterController:(AliyunPasterController *)pasterController;
        ``` |
        |Remove all common animated stickers.|        ```
- (void)removeAllNormalPasterControllers;
        ``` |
        |Remove all animated subtitle stickers.|        ```
- (void)removeAllCaptionPasterControllers;
        ``` |
        |Remove all animated text stickers.|        ```
- (void)removeAllSubtitlePasterControllers;
        ``` |
        |Obtain the animated sticker controller in editing.|        ```
/**
@return The animated sticker controller.
*/
- (AliyunPasterController *)getCurrentEditPasterController;
        ``` |

        The addPaster and addSubtitle methods are used to create animated stickers. The returned AliyunPasterController object is an animated sticker controller from which you can obtain the parameters for internally rendering animated stickers. AliyunPasterController defines the position, size, display start time, and display end time of an animated sticker.

        The following table describes the actions that are supported by AliyunPasterController.

        |Action|Sample code|
        |------|-----------|
        |Set the view of the animated sticker.|        ```
/**
@warning: required.
*/
@property (nonatomic, strong) UIView *pasterView;
        ``` |
        |Set the type of the animated sticker.|        ```
@property (nonatomic, assign, readonly) AliyunPasterEffectType pasterType;
        ``` |
        |Set the rotation angle \(radian\) of the animated sticker.|All the values that are related to positions and sizes are logical pixels, which are converted to physical pixels for internal rendering.

        ```
@property (nonatomic, assign) CGFloat pasterRotate;
        ``` |
        |Set the position \(x, y\) of the animated sticker.|        ```
@property (nonatomic, assign) CGPoint pasterPosition;
        ``` |
        |Set the width and height of the animated sticker.|        ```
@property (nonatomic, assign) CGSize pasterSize;
        ``` |
        |Set the position and size of the animated sticker.|        ```
@property (nonatomic, assign) CGRect pasterFrame;
        ``` |
        |Set the mirroring mode of the animated sticker.|        ```
@property (nonatomic, assign) BOOL mirror;
        ``` |
        |Set the text content.|        ```
@property (nonatomic, copy) NSString *subtitle;
        ``` |
        |Set the text position.|The text position is the position of the text on the animated sticker.

        ```
@property (nonatomic, assign) CGRect subtitleFrame;
        ``` |
        |Set the background font name of the text.|        ```
@property (nonatomic, copy, readonly) NSString *subtitleConfigFontName;
        ``` |
        |Set the background font ID of the text.|        ```
@property (nonatomic, assign, readonly) NSInteger subtitleConfigFontId;
        ``` |
        |Specify whether to outline the text.|        ```
@property (nonatomic, assign) BOOL subtitleStroke;
        ``` |
        |Set the text color.|        ```
@property (nonatomic, strong) UIColor *subtitleColor;
        ``` |
        |Set the color of the text outline.|        ```
@property (nonatomic, strong) UIColor *subtitleStrokeColor;
        ``` |
        |Set the background color of the text.|        ```
@property (nonatomic, strong) UIColor *subtitleBackgroundColor;
        ``` |
        |Set the text font.|        ```
@property (nonatomic, copy) NSString *subtitleFontName;
        ``` |
        |Set the keyframe image.|        ```
@property (nonatomic, strong, readonly) UIImage *kernelImage;
        ``` |
        |Set the start time of the animated sticker, in seconds.|        ```
@property (nonatomic, assign) CGFloat pasterStartTime;
        ``` |
        |Set the end time of the animated sticker, in seconds.|        ```
@property (nonatomic, assign) CGFloat pasterEndTime;
        ``` |
        |Set the duration of the animated sticker, in seconds.|        ```
@property (nonatomic, assign) CGFloat pasterDuration;
        ``` |
        |Set the minimum duration of the animated sticker, in seconds.|        ```
@property (nonatomic, assign) CGFloat pasterMinDuration;
        ``` |
        |Specify the editing area.|        ```
@property (nonatomic, assign) CGSize displaySize;
        ``` |
        |Set the resolution of the output video.|        ```
@property (nonatomic, assign) CGSize outputSize;
        ``` |
        |Set the preview size.|        ```
@property (nonatomic, assign) CGSize previewRenderSize;
        ``` |

        **Note:** All the values that are related to positions and sizes are logical pixels, which are converted to physical pixels for internal rendering.

        AliyunPasterController provides methods for managing the editing status. You must call related methods to instruct an animated sticker controller to change the status when you start or stop the editing. The following table describes the related actions.

        |Action|Sample code|
        |------|-----------|
        |Prepare for editing.|        ```
/**
Before an animated sticker enters the editing status, the existing animated sticker that is rendered is internally removed.
*/
- (void)editWillStart;
        ``` |
        |Enter the editing status.|        ```
- (void)editDidStart;
        ``` |
        |Start the editing.|        ```
- (void)editProcess;
        ``` |
        |Complete the editing.|        ```
/**
After the editing is completed, the modifications are synchronized to the properties of the animated sticker controller and the animated sticker is internally rendered.
*/
- (void)editCompleted;
        ``` |
        |Complete subtitle editing.|        ```
/**
This method provides the same feature as the previous method, and will be deprecated in later versions of the short video SDK.
@param image The subtitle image.
*/
- (void)editCompletedWithImage:(UIImage *)image;
        ``` |

        You can use AliyunPasterControllerDelegate to fire callbacks to monitor the status of an animated sticker. The following table describes the related callback events.

        |Callback event|Sample code|
        |--------------|-----------|
        |The animated sticker controller is removed.|        ```
/**
@param obj The animated sticker controller.
*/
 - (void)onRemove:(id)obj;
        ``` |
        |The editing preparation is completed.|        ```
/**
@param obj The animated sticker controller.
*/
- (void)onEditWillBegin:(id)obj;
        ``` |
        |The editing starts.|        ```
/**
@param obj The animated sticker controller.
*/
- (void)onEditDidBegin:(id)obj;
        ``` |
        |The editing is completed.|        ```
/**
@param obj The animated sticker controller.
*/
- (void)onEditEnd:(id)obj;
        ``` |
        |The image rendering is completed.|        ```
/**
@param obj The animated sticker controller.
@param image The image to be rendered.
*/
- (void)onEditEnd:(id)obj image:(UIImage *)image;
        ``` |

        **Sample code:**

        ```
            AliyunPasterController *pasterController = [self.pasterManager addPaster:pasterInfo.resourcePath startTime:range.startTime duration:range.duration]; // Initialize an AliyunPasterController object.
            AliyunPasterView *pasterView = [[AliyunPasterView alloc] initWithPasterController:pasterController]; // Use the AliyunPasterController object to generate an AliyunPasterView object.
            pasterController.subtitleFontName = pasterView.textFontName; // Set the text font.
            pasterController.subtitleStroke = pasterView.textColor.isStroke; // Specify whether to outline the text.
            pasterController.subtitleColor = [pasterView contentColor]; // Set the text color.
            pasterController.subtitleStrokeColor = [pasterView strokeColor]; // Set the color of the text outline.
            pasterController.subtitleBackgroundColor = [pasterView textBackgroundColor]; // Set the background color of the text.
        
            pasterView.delegate = (id)pasterController;
            pasterView.actionTarget = (id)self;
        
            [pasterController setPasterView:pasterView];
            [pasterController editCompleted]; // Complete the editing for rendering.
        ```

    -   Use AliyunPasterRender

        AliyunPasterManager uses the default UI that is provided by the short video SDK to add animated stickers. If you need to customize the UI, use AliyunPasterRender. The following table describes the related actions.

        |Action|Sample code|
        |------|-----------|
        |Obtain the AliyunPasterRender instance.|        ```
- (AliyunPasterRender *)getPasterRender;
        ``` |
        |Add an animated sticker.|        ```
@ param paster The animated sticker object.
* If the status is normal, ALIVC_COMMON_RETURN_SUCCESS is returned.
* If the status is invalid, ALIVC_COMMON_INVALID_STATE is returned.
* If the file does not exist, ALIVC_SVIDEO_EDITOR_FILE_NOT_EXIST is returned.
* If the animated sticker fails to be parsed, ALIVC_SVIDEO_EDITOR_PARSE_RESOURCE_FAILED is returned.
* ALIVC_FRAMEWORK_RENDER_ERROR_SCENE_INVALID
*/
- (int)addGifPaster:(AliyunEffectPaster *)paster;
        ``` |
        |Add text.|        ```
@param subtitle The text object.
@param textImage The text snapshot.
* If the status is normal, ALIVC_COMMON_RETURN_SUCCESS is returned.
* If the status is invalid, ALIVC_COMMON_INVALID_STATE is returned.
* ALIVC_FRAMEWORK_RENDER_ERROR_SCENE_INVALID
*/
- (int)addSubtitlePaster:(AliyunEffectSubtitle *)subtitle textImage:(UIImage *)textImage;
        ``` |
        |Add an animated subtitle sticker.|        ```
@param caption The animated subtitle sticker.
@param textImage The text snapshot.
* If the status is invalid, ALIVC_COMMON_INVALID_STATE is returned.
* If the file does not exist, ALIVC_SVIDEO_EDITOR_FILE_NOT_EXIST is returned.
* If the animated sticker fails to be parsed, ALIVC_SVIDEO_EDITOR_PARSE_RESOURCE_FAILED is returned.
* ALIVC_FRAMEWORK_RENDER_ERROR_SCENE_INVALID
*/
- (int)addCaptionPaster:(AliyunEffectCaption *)caption textImage:(UIImage *)textImage;
        ``` |
        |Remove an animated sticker.|        ```
@param basePaster The animated sticker object.
* If the status is normal, ALIVC_COMMON_RETURN_SUCCESS is returned.
* If the status is invalid, ALIVC_COMMON_INVALID_STATE is returned.
* ALIVC_FRAMEWORK_RENDER_ERROR_SCENE_INVALID
*/
- (int)removePaster:(AliyunEffectPasterBase *)basePaster;
        ``` |

-   **Doodle**

    Doodles involve the AliyunIPaint and AliyunICanvasView classes. AliyunIPaint indicates a paint brush and AliyunICanvasView indicates a canvas.

    -   The following table describes the actions that are supported by AliyunIPaint.

        |Action|Sample code|
        |------|-----------|
        |Set the line color.|        ```
@property (nonatomic, strong) UIColor *lineColor;
        ``` |
        |Set the line width.|        ```
@property (nonatomic, assign) CGFloat lineWidth;
        ``` |
        |Set the line shadow color.|        ```
@property (nonatomic, strong) UIColor *shadowColor;
        ``` |
        |Set the line shadow width.|        ```
@property (nonatomic, assign) CGFloat shadowWidth;
        ``` |
        |Initialize the line width and color.|        ```
/**
@param lineWidth The line width.
@param lineColor The line color.
@return self
*/
- (instancetype)initWithLineWidth:(CGFloat)lineWidth
                      lineColor:(UIColor *)lineColor;
        ``` |

        **Note:** You can set the line color, line width, line shadow color, and line shadow width for a paint brush.

    -   The following table describes the actions that are supported by AliyunICanvasView.

        |Action|Sample code|
        |------|-----------|
        |Set callbacks.|        ```
@property (nonatomic, weak) id<AliyunICanvasViewDelegate> delegate;
        ``` |
        |Enable cross-border painting.|By default, cross-border painting is disabled.

        ```
@property (nonatomic, assign) BOOL enableCrossBorder;
        ``` |
        |Set the paint brush.|        ```
@property (nonatomic, strong) AliyunIPaint *paint;
        ``` |
        |Initialize the paint brush and canvas.|        ```
/**
@param frame The canvas.
@param paint The paint brush.
@return self
*/
- (instancetype)initWithFrame:(CGRect)frame
                      paint:(AliyunIPaint *)paint;
        ``` |
        |Modify the paint brush configuration.|        ```
/**
@param paint The paint brush.
*/
- (void)changePaint:(AliyunIPaint *)paint;
        ``` |
        |Clear all lines. This operation cannot be undone.|        ```
- (void)remove;
        ``` |
        |Undo the previous step.|        ```
- (void)undo;
        ``` |
        |Redo the previous step.|        ```
- (void)redo;
        ``` |
        |Undo all doodle operations.|        ```
- (void)undoAllChanges;
        ``` |
        |Complete the configuration.|        ```
/**
@return The doodle image.
*/
- (UIImage *)complete;
        ``` |

        The following table describes the callback events related to doodling.

        |Callback event|Sample code|
        |--------------|-----------|
        |The painting starts.|        ```
/**
@param startPoint The point where the painting starts.
*/
- (void)startDrawingWithCurrentPoint:(CGPoint)startPoint;
        ``` |
        |The painting ends.|        ```
/**
@param endPoint The point where the painting ends.
*/
- (void)endDrawingWithCurrentPoint:(CGPoint)endPoint;
        ``` |

-   **Watermark**

    AliyunEffectImage indicates an image resource. You can call the initialization method to create a watermark image instance. The path parameter specifies the path of the watermark image file.

    |Action|Sample code|
    |------|-----------|
    |Initialize an instance.|    ```
- (instancetype)initWithFile:(NSString *)path;
    ```

After initialization, you must set the frame parameter to specify the size and position of the watermark relative to the output resolution that is specified by the outputSize parameter. The aspect ratio of the watermark must be the same as that of the original image. |
    |Set a watermark.|    ```
- (int)setWaterMark:(AliyunEffectImage *)waterMark;
    ``` |
    |Set an end watermark.|    ```
- (int)setTailWaterMark:(AliyunEffectImage *)waterMark;
    ```

You can set the endTime parameter of AliyunEffectMusic to set the duration of the end watermark. |

-   **Transition**

    The short video SDK V3.7.0 and later provide the transition feature. The transition base class is AliyunTransitionEffect.

    The following table describes the actions that are supported by AliyunTransitionEffect.

    |Action|Sample code|
    |------|-----------|
    |Set the transition duration.|    ```
/**
Make sure that the transition duration is greater than or equal to the video clip duration.
*/
@property (nonatomic, assign) float overlapDuration;
    ``` |
    |Customize a transition effect.|    ```
@property (nonatomic, copy) NSString *customShader;
    ``` |
    |Set custom transition fields.|    ```
@property (nonatomic, strong) NSDictionary *transitionParam;
    ``` |

    The short video SDK supports the following transition types:

    ```
        AliyunTransitionEffectShuffer: the shutter transition.
        AliyunTransitionEffectTranslate: the translation transition, in up, down, left, and right directions.
        AliyunTransitionEffectCircle: the circular transition.
        AliyunTransitionEffectPolygon: the polygon transition, with more than two edges.
        AliyunTransitionEffectFade: the fade transition.
    ```

    **Note:** If you are familiar with OpenGL Shading Language, you can use transitionParam and customShader to customize transition settings.

    When you create an AliyunImporter instance, you can run the following sample code to add a transition effect to the video clip:

    ```
    AliyunClip *clip = [[AliyunClip alloc] initWithImagePath:info.sourcePath duration:info.duration animDuration:i == 0 ? 0 : 1];
    AliyunTransitionEffectFade *transitionEffect = [[AliyunTransitionEffectFade alloc] init];
    transitionEffect.overlapDuration = 2;
    clip.transitionEffect = transitionEffect;
    
    // Set the transitionEffect parameter of AliyunClip to set a transition.
    ```

    In addition to AliyunImportor, you can set a transition by using AliyunEditor.

    The following table describes the actions that are supported by AliyunEditor.

    |Action|Sample code|
    |------|-----------|
    |Add a transition.|    ```
/**
API_AVAILABLE(3.7.0)
Note: 1. This method cannot be called if only one video clip exists.
2. The transition duration cannot be longer than the duration of the shorter one between the two involved video clips.
3. Before you call this method, call [_editor stopEdit]. After you call this method, call [_editor startEdit] and [_player play].
[----Video clip A----] [----Video clip B----] [----Video clip C----]...[----Video clip N----]
               ^                ^                 ^
clipIndex:      0                1                N-1
@param transition The transition.
@param clipIdx The index of a video clip intersection.
@return If the transition fails to be set, ALIVC_COMMON_RETURN_FAILED is returned. If the transition is set, ALIVC_COMMON_RETURN_SUCCESS is returned.
*/
- (int)applyTransition:(AliyunTransitionEffect *)transition atIndex:(int)clipIdx;
    ``` |
    |Remove a transition.|    ```
/**
API_AVAILABLE(3.7.0) Note: Before you call this method, call [_editor stopEdit]. After you call this method, call [_editor startEdit] and [_player play].
@param clipIdx The index.
*/
- (int)removeTransitionAtIndex:(int)clipIdx;
    ``` |

    **Sample code**

    ```
    AliyunTransitionEffectFade *fade = [[AliyunTransitionEffectFade alloc] init];
    fade.overlapDuration = 10;
    [self.editor applyTransition:fade atIndex:idx];
    ```

-   **Animation**

    In the short video SDK V3.7.0 and later, all objects that inherit AliyunClip and AliyunEffectPasterBase support the animation feature. The animation base class is AliyunAction.

    In the current version, the short video SDK supports the following animation classes:

    ```
    AliyunMoveAction            // The moving animation.
    AliyunScaleAction            // The scaling animation.
    AliyunRotateAction            // The rotation animation.
    AliyunRotateToAction        // The animation for rotating to the specified radian.
    AliyunRotateByAction        // The animation for rotating by the specified radian from the current radian.
    AliyunRotateRepeatAction    // The animation for repeated rotation.
    AliyunAlphaAction            // The alpha animation.
    AliyunCustomAction            // The custom animation.
    ```

    **Note:** For more information about the animation classes, see the SDK documentation.

    The following table describes the animation-related actions that are supported by AliyunEditor.

    |Action|Sample code|
    |------|-----------|
    |Add a frame animation.|    ```
/**
API_AVAILABLE(3.7.0)
Note: Main streams do not support alpha frame animations.
@param obj The object to which the animation applies.
@param action The animation.
*/
- (void)add:(id<AliyunActionProtocol>)obj withFrameAnimation:(AliyunAction *)action;
    ``` |
    |Remove a frame animation.|    ```
/**
API_AVAILABLE(3.7.0)
@param obj The object to which the animation applies.
@param action The animation.
*/
- (void)remove:(id<AliyunActionProtocol>)obj withFrameAnimation:(AliyunAction *)action;
    ``` |

    The following table describes the animation-related actions that are supported by AliyunClip.

    |Action|Sample code|
    |------|-----------|
    |Add an animation.|    ```
/**
API_AVAILABLE(3.7.0)
Note: Main streams do not support alpha frame animations.
@param action The animation.
*/
- (void)runAction:(AliyunAction *)action;
    ``` |
    |Stop an animation.|    ```
/**
API_AVAILABLE(3.7.0)
@param action The animation.
*/
- (void)stopAction:(AliyunAction *)action;
    ``` |
    |Obtain all animations.|    ```
/**
API_AVAILABLE(3.7.0)
@return The array of animations.
*/
- (NSArray *)allActions;
    ``` |

    The following table describes the animation-related actions that are supported by AliyunEffectPasterBase.

    |Action|Sample code|
    |------|-----------|
    |Add an animation.|    ```
/**
API_AVAILABLE(3.7.0)
@param action The animation.
*/
- (void)runAction:(AliyunAction *)action;
    ``` |
    |Stop an animation.|    ```
/**
API_AVAILABLE(3.7.0)
@param action The animation.
*/- (void)stopAction:(AliyunAction *)action;- (void)stopAllActions;
    ``` |

    You can run the following sample code to use AliyunEditor to make a static sticker transparent:

    ```
    AliyunAlphaAction *alphaAction = [[AliyunAlphaAction alloc] init];
    alphaAction.targetID = [_staticImage effectVid]; // Specify the ID of the object to which the animation applies.
    alphaAction.startTime = 3;
    alphaAction.duration = 2;
    alphaAction.fromAlpha = 0.0;
    alphaAction.toAlpha = 1.0;
    [self.editor add:_staticImage withFrameAnimation:alphaAction];
    ```

    You can run the following sample code to use AliyunClip and AliyunEffectPasterBase to make a static sticker transparent:

    ```
    AliyunAlphaAction *alphaAction = [[AliyunAlphaAction alloc] init];
    alphaAction.startTime = [pasterController pasterStartTime];
    alphaAction.duration = 1;
    alphaAction.fromAlpha = 0.0f;
    alphaAction.toAlpha = 1.0f;
    [effectPaster runAction:alphaAction];
    ```

    If you are familiar with OpenGL Shading Language, you can use AliyunCustomAction to customize animations. Sample code:

    ```
    AliyunCustomAction *customAction = [[AliyunCustomAction alloc] init];
    customAction.startTime = [pasterController pasterStartTime];
    customAction.duration = 0.5;
    customAction.fragmentShader = @"precision mediump float; uniform sampler2D inputImageTexture; uniform float uAlpha; varying vec2 textureCoordinate; uniform float offset; float w = 0.2; float g = 1.0; uniform int direction; uniform int wipeMode;const int LEFT = 0;const int TOP = 1;const int RIGHT = 2;const int BOTTOM = 3;const int APPEAR = 0;const int DISAPPEAR = 1;void main(){vec4 gamma = vec4(g, g, g, 1.0);vec4 color0 = pow(texture2D(inputImageTexture, textureCoordinate), gamma);float correction = mix(w, -w, offset);float coord = textureCoordinate.x;if(direction == LEFT){coord = 1.0 - textureCoordinate.x;}else if(direction == RIGHT){coord = textureCoordinate.x;}else if(direction == TOP){coord = 1.0 - textureCoordinate.y;}else if(direction == BOTTOM){coord = textureCoordinate.y;}float choose = smoothstep(offset - w, offset + w, coord + correction); float alpha = choose;if(wipeMode == APPEAR){alpha = 1.0 - choose;}else if(wipeMode == DISAPPEAR){alpha = choose;}gl_FragColor = vec4(color0.r,color0.g,color0.b,color0.a*alpha);}";
    customAction.customUniformsMapper = @{@"direction": @[@0],
                                          @"wipeMode":@[@0],
                                          @"offset":@[@0.0,@1.0],
                                          };[effectPaster runAction:customAction];
    ```

    **Note:** In this example, the customized fragmentShader and customUniformsMapper define the animation effect of a linear eraser.

-   **Custom rendering**

    The short video SDK allows you to obtain the texture IDs of the raw and rendered videos by using related methods. You can perform custom rendering in the rendering process. To perform custom rendering, you must implement the shader. Otherwise, you do not need to implement the shader.

    To perform custom rendering, you must use the delegate object to implement the AliyunIRenderCallback protocol.

    ```
    /**
     The custom rendering method that is used by the SDK to return the ID of the texture for the raw video.
     @param srcTexture The ID of the texture for the raw video frame.
     @param size The size of the texture for the raw video frame.
     @return The texture ID.
     */
    - (int)customRender:(int)srcTexture size:(CGSize)size;
    ```

    ```
    /**
     The custom rendering method that is used by the SDK to return the ID of the rendered texture.
     @param srcTexture The ID of the texture for the raw video frame.
     @param size The size of the texture for the raw video frame.
     @return The texture ID.
     */
    - (int)textureRender:(int)srcTexture size:(CGSize)size;
    ```

-   **Padding and cropping**

    You can use AliyunEffectRunningDisplayMode to dynamically switch the player to the padding mode or cropping mode during playback. The following related actions are supported:

    ```
    @property(nonatomic, assign) float streamStartTime; // Set the start time.
    @property(nonatomic, assign) float streamEndTime; // Set the end time.
    @property(nonatomic, assign) AliyunRunningMode mode; // Set the playback mode. A value of AliyunRunningModeFit indicates the cropping mode. A value of AliyunRunningModeFill indicates the padding mode.
    @property(nonatomic, assign) int targetStreamId; // Specify the ID of the stream to which the playback mode applies.
    ```

    **Sample code**

    ```
    AliyunEffectRunningDisplayMode *displayMode = [[AliyunEffectRunningDisplayMode alloc ] init];
    displayMode.streamStartTime = 0; // Set the start time of the playback mode.
    displayMode.streamEndTime = 4; // Set the end time of the playback mode.
    displayMode.mode = AliyunRunningModeFill; // Set the playback mode to padding or cropping.
    displayMode.targetStreamId = clip.streamId; // Specify the ID of the stream to which the playback mode applies.
    [self.editor applyRunningDisplayMode:displayMode];
    ```


## Production

|Action|Sample code|
|------|-----------|
|Obtain the production instance.|```
- (id<AliyunIExporter>)getExporter;
``` |
|Start the production.|```
 - (int)startExport:(NSString *)outputPath;
``` |
|Cancel the production.|```
 -(int)cancelExport;
``` |

To monitor the production status, the delegate object needs to implement the AliyunIExporterCallback protocol. The following table describes the related callback events.

|Callback event|Sample code|
|--------------|-----------|
|The production starts.|```
- (void)exporterDidStart;
``` |
|The production is completed.|```
/**
@param outputPath The path of the output file.
*/
- (void)exporterDidEnd:(NSString *)outputPath;
``` |
|The production is canceled.|```
- (void)exporterDidCancel;
``` |
|The production progress is returned.|```
/**
@param progress 0-1
*/
- (void)exportProgress:(float)progress;
``` |
|A production error occurs.|```
/**
@param errorCode The error code.
*/
- (void)exportError:(int)errorCode;
``` |

