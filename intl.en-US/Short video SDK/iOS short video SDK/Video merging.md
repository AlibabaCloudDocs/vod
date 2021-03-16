# Video merging

This topic describes the classes that are required for merging videos by using the short video SDK for iOS and shows you how to use these classes to merge videos.

## Related classes

|Class|Description|
|-----|-----------|
|AliyunMixComposer|The underlying class. You can implement this class to merge multiple videos on the same screen in different layouts such as left-right split-screen, picture-in-picture, and nine-square grid. You can also implement this class to join the playback of two involved videos on the same screen.|
|AliyunMixTrack|The class that specifies a video track for video merging. A video track for video merging can be created by using the AliyunMixComposer class. You can add video streams to video tracks.|
|AliyunMixStream|The class that specifies a video stream to be added to a video track for video merging.|

## Initialize the AliyunMixComposer class and set parameters

The following sample code shows you how to configure the AliyunMixComposer class:

```
/**
 The delegate object of the AliyunMixComposer class.
*/
@property(nonatomic, weak) id<AlivcMixComposerDelegate> delegate;

/**
 Required. The resolution of the merged video.
 */
@property(nonatomic, assign) CGSize outputSize;

/**
 Required. The path of the merged video.
 */
@property(nonatomic, copy) NSString *outputPath;

/**
 The bitrate, in bit/s. 
*/
@property(nonatomic, assign) NSInteger bitrate;

/**
 The video quality.
 */
@property(nonatomic, assign) AliyunVideoQuality videoQuality;

/**
 The average frame rate, in FPS. Default value: 30. 
*/
@property(nonatomic, assign) CGFloat fps;

/**
 The group of pictures (GOP) size. Default value: 5. 
*/
@property(nonatomic, assign) NSInteger gop;
```

## Create video tracks

|Action|Sample code|
|------|-----------|
|Create a track.|```
/**
 Initialize the video track of a duet.

@param trackDisplayFrame The resolution of the track. The resolution of the merged video is used as the reference coordinates. For example, the resolution of the merged video is 960 × 960. If the trackDisplayFrame parameter is set to (0,0,480,960), the track is displayed in the left half of the screen.
@return The AlivcMixTrack object.
 */
- (AliyunMixTrack *)createTrack:(CGRect)trackDisplayFrame;
``` |
|Specify the reference duration.|```
/**
 Specify the duration of a specific track as the duration of the merged video.

@param referenceTrack The track.
 */
- (void)setOutputDurationReferenceTrack:(AliyunMixTrack *)referenceTrack;
``` |
|Specify the reference audio.|```
/**
 Specify the audio of a specific track as the audio of the merged video.

 @param referenceTrack The track.
 */
- (void)setOutputAudioReferenceTrack:(AliyunMixTrack *)referenceTrack;
``` |

## Add video streams

The following sample code shows you how to configure the AliyunMixStream class:

```
/**
 The path of the video file.
 */
@property(nonatomic, copy) NSString *filePath;

/**
 Optional.
 The cropping range of the video in the track, which takes effect in cropping mode.
 */
@property(nonatomic, assign) CGRect innerCropFrame;

/**
 The start time of the video playback in the track.
 Unit: seconds.
 */
@property(nonatomic, assign) CGFloat streamStartTime;

/**
 The end time of the video playback in the track.
 Unit: seconds.
 */
@property(nonatomic, assign) CGFloat streamEndTime;

/**
 The scaling mode of the video in the track,
 including the padding mode and cropping mode.
 */
@property(nonatomic, assign) AlivcContentMode mode;
```

You can use the following code to add a video stream:

```
/**
 Add a video stream to a track.

 @param stream The video stream.
 */
- (void)addStream:(AliyunMixStream *)stream;
```

## Start, pause, resume, and cancel the merging

|Action|Sample code|
|------|-----------|
|Start the merging.|```
/**
 Start the merging.
 @return The return value.
 */
- (int)start;
``` |
|Pause the merging.|```
/**
 Pause the merging.
 @return The return value. 
*/
- (int)pause;
``` |
|Resume the merging.|```
/**
 Resume the merging.
 @return The return value. 
*/
- (int)resume;
``` |
|Cancel the merging.|```
/**
 Cancel the merging.
 @return The return value. 
*/
- (int)cancel;
``` |

## Sample code

```
// Step 1: Create an AliyunMixComposer object and set parameters.
AliyunMixComposer *mixComposer = [[AliyunMixComposer alloc] init];
    mixComposer.outputPath = self.outputPath;
    mixComposer.outputSize = CGSizeMake(720,720);
    mixComposer.fps = 30;
    mixComposer.bitrate = 10000000;
    mixComposer.videoQuality = AliyunVideoQualityHight;
    mixComposer.gop = 5;
    mixComposer.delegate = (id)self;

// Step 2: Create Track 1 and add a stream to Track 1.
    AliyunMixTrack *recordTrack = [mixComposer createTrack:CGRectMake(0,0,360,720)];

  NSString *videoPath = [videoAbsPaths objectAtIndex:idx];
    AliyunMixStream *recordStream = [[AliyunMixStream alloc] init];
    recordStream.filePath = videoPath;
    recordStream.mode = AlivcContentModeScaleAspectFit;
    [recordTrack addStream:recordStream];

// Step 3: Create Track 2 and add a stream to Track 2.
AliyunMixTrack *playerTrack = [mixComposer createTrack:CGRectMake(360,0,360,720)];
    AliyunMixStream *playerStream = [[AliyunMixStream alloc] init];
    playerStream.filePath = mixVideoFilePath;
    playerStream.mode = AlivcContentModeScaleAspectFit;
    [playerTrack addStream:playerStream];

// Step 4: Specify that the audio of Track 2 is used as the output audio.
    [mixComposer setOutputAudioReferenceTrack:playerTrack];
// Step 5: Start merging.
    [mixComposer start];
```

