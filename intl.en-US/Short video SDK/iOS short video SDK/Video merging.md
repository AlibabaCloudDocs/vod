# Video merging

AliyunMixComposer is an underlying class that allows you to merge multiple videos on the same screen in different layouts, such as the left-right split-screen, picture-in-picture, and nine-square grid.

## AliyunMixStream \(video streams\)

Aliyunmixstream specifies a video stream to be added to a video track for video merging.

## Initialize the AliyunMixComposer class and set parameters

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
 The group of pictures (GOP). Default value: 5. 
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

Parse the AliyunMixStream object:

```
/**
 The path of the video file.
 */
@property(nonatomic, copy) NSString *filePath;

/**
 Optional.
 The cropping range of the video that is displayed in the track, which takes effect in cropping mode.
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
 The scaling mode of the video in the track, including the padding mode and cropping mode.
  
 */
@property(nonatomic, assign) AlivcContentMode mode;
```

Add a video stream

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
AliyunMixComposer *mixComposer = [[AliyunMixComposer alloc] init];
    mixComposer.outputPath = self.outputPath;
    mixComposer.outputSize = CGSizeMake(720,720);
    mixComposer.fps = 30;
    mixComposer.bitrate = 10000000;
    mixComposer.videoQuality = AliyunVideoQualityHight;
    mixComposer.gop = 5;
    mixComposer.delegate = (id)self;

    AliyunMixTrack *recordTrack = [mixComposer createTrack:CGRectMake(0,0,360,720)];

  NSString *videoPath = [videoAbsPaths objectAtIndex:idx];
    AliyunMixStream *recordStream = [[AliyunMixStream alloc] init];
    recordStream.filePath = videoPath;
    recordStream.mode = AlivcContentModeScaleAspectFit;
    [recordTrack addStream:recordStream];

AliyunMixTrack *playerTrack = [mixComposer createTrack:CGRectMake(360,0,360,720)];
    AliyunMixStream *playerStream = [[AliyunMixStream alloc] init];
    playerStream.filePath = mixVideoFilePath;
    playerStream.mode = AlivcContentModeScaleAspectFit;
    [playerTrack addStream:playerStream];

    [mixComposer setOutputAudioReferenceTrack:playerTrack];

    [mixComposer start];
```

