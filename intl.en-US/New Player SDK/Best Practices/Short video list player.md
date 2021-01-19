# Short video list player

You can create a short video list player by using ApsaraVideo Player SDK. This topic shows you how to create a short video list player for Android or iOS. This topic also provides sample code.

## Effect example



**Note:** The short video list player is optimized only for MP4 videos. We recommend that you use multiple players instead of a short video list player to play HLS streams.

## Key implementation on Android

1.  Create a short video list player.

    Create a short video list player and set required parameters. The following code provides an example:

    ```
    private AliListPlayer mVideoListPlayer;
    ……
    // Required. Create a short video list player.
    mVideoListPlayer = AliPlayerFactory.createAliListPlayer(mContext);
    // Enable hard decoding.
    mVideoListPlayer.enableHardwareDecoder(true);
    // Set player parameters.
    PlayerConfig config = mVideoListPlayer.getConfig();
    // Clear video frames after the video playback stops. We recommend that you add this configuration to prevent residual frames.
    config.mClearFrameWhenStop = true;
    mVideoListPlayer.setConfig(config);
    // Enable loop playback. Generally, short videos are played in loop playback mode.
    mVideoListPlayer.setLoop(true);
    // Enable autoplay.
    mVideoListPlayer.setAutoPlay(true);
    // Specify the number of the short videos to be preloaded. This example preloads three videos: the video that is being played, the played video, and the video to be played.
    mVideoListPlayer.setPreloadCount(1);
    ```

2.  Add multiple video sources.

    The short video list player can play videos from specified URLs or videos with specified video IDs \(VIDs\) from ApsaraVideo VOD. You must use Security Token Service \(STS\) tokens to play videos from ApsaraVideo VOD. The following code provides an example:

    ```
    // Add a video from ApsaraVideo VOD.
     mVideoListPlayer.addVid("VID of the video from ApsaraVideo VOD", "Unique ID of the video");
    // Add a video from a specified URL.
    mVideoListPlayer.addUrl("URL of the video", "Unique ID of the video");
    ```

    **Note:** The short video list player distinguishes videos based on their unique IDs. An unexpected video may be played if you add video sources with the same unique ID. Make sure that video sources that are added to the player at a time have unique IDs.

3.  Start the playback.

    The short video list player provides the following methods for you to locate and play videos. The following code provides an example:

    ```
    // Locate a video and play it.
    mVideoListPlayer.moveTo("Unique ID of the video", STS token) // Use the STS token to play the video with the specified VID from ApsaraVideo VOD.
    mVideoListPlayer.moveTo("Unique ID of the video") // Play the video from the specified URL.
    // Play the previous video in the list.
    mVideoListPlayer.moveToPrev("Unique ID of the video", STS token) // Use the STS token to play the video with the specified VID from ApsaraVideo VOD.
    mVideoListPlayer.moveToPrev("Unique ID of the video") // Play the video from the specified URL.
    // Play the next video in the list.
    mVideoListPlayer.moveToNext("Unique ID of the video", STS token) // Use the STS token to play the video with the specified VID from ApsaraVideo VOD.
    mVideoListPlayer.moveToNext("Unique ID of the video") // Play the video from the specified URL.
    ```

4.  Set the TextureView object for the player.

    Most short video list players use the TextureView object to avoid black screen exceptions when the player is switched back to the foreground from the background. This optimizes user experience during video playback.

    1.  Configure basic settings of the TextureView object. The following code provides an example:

        ```
        TextureView mTextureView = null;
        SurfaceTexture mSurfaceTexture = null;
        Surface mSurface = null;
        ……
        mTextureView = findViewById(R.id.textureView);
        mTextureView.setSurfaceTextureListener(new TextureView.SurfaceTextureListener() {
                    @Override
                    public void onSurfaceTextureAvailable(SurfaceTexture surfaceTexture, int width, int height) {
                      // Cache the SurfaceTexture object so that it can be reused when the player is switched back to the foreground from the background.
                        mSurfaceTexture = surfaceTexture;
                        mSurface = new Surface(surface);
                        // Set the playback surface.
                            mVideoListPlayer.setSurface(mSurface);
                      // Redraw and refresh the user interface (UI) immediately.
                            mVideoListPlayer.redraw();
                    }
                    @Override
                    public void onSurfaceTextureSizeChanged(SurfaceTexture surface, int width, int height) {
                      // Redraw and refresh the UI immediately after the playback screen size changes.
                            mVideoListPlayer.redraw();
                    }
                    @Override
                    public boolean onSurfaceTextureDestroyed(SurfaceTexture surface) {
                      // Make sure that the return value is false. If the return value is not false, the system releases the SurfaceTexture object.
                        return false;
                    }
                    @Override
                    public void onSurfaceTextureUpdated(SurfaceTexture surface) {
                    }
                });
        ```

    2.  Apply the TextureView object upon switchback to the foreground from the background.

        Call the onResume\(\) method to apply the TextureView object when the player is switched back to the foreground from the background. The following code provides an example:

        ```
        public void onResume() {
              ……
              if (mVideoListPlayer ! = null && mSurface ! = null) {
                    mVideoListPlayer.setSurface(mSurface);
                    mVideoListPlayer.redraw();
              }
              ……
        }
        ```

5.  Hide the thumbnail.

    When the player starts to play a video, it hides the video thumbnail and displays the video. The following code provides an example:

    ```
    mVideoListPlayer.setOnRenderingStartListener(new IPlayer.OnRenderingStartListener() {
                @Override
                public void onRenderingStart() {
                   // The player starts to render the first frame of the video. At this time, the player hides the thumbnail.
                }
            });
    ```

6.  Destroy the player.

    You must release the player after use. Otherwise, a memory leakage bug may occur. The following code provides an example:

    ```
    // Release the surface.
    mVideoListPlayer.setSurface(null);
    // If the player uses the TextureView object in Step 4, you must release the cached SurfaceTexture object.
    if (mSurface ! = null) {
                mSurface.release();
    }
    if (mSurfaceTexture ! = null) {
                mSurfaceTexture.release();
    }
    // Release the player.
    mVideoListPlayer.release();
    ```


## Key implementation on iOS

1.  Create a short video list player.

    Create a short video list player and set required parameters. The following code provides an example:

    ```
    // Required. Create a short video list player.
    self.listPlayer = [[AliListPlayer alloc]init];
    // Enable hard decoding.
    self.listPlayer.enableHardwareDecoder = YES;
    // Enable loop playback.
    self.listPlayer.loop = YES;
    // Enable autoplay.
    self.listPlayer.autoPlay = YES;
    // Specify the rendering mode.
    self.listPlayer.scalingMode = AVP_SCALINGMODE_SCALEASPECTFIT;
    // Specify the delegate.
    self.listPlayer.delegate = self;
    // Specify the resolution of the short videos to be preloaded.
    self.listPlayer.stsPreloadDefinition = @"FD";
    // Set the UI view.
    self.listPlayer.playerView = self.simplePlayScrollView.playView;
    // Specify the number of the short videos to be preloaded. This example preloads three videos: the video that is being played, the played video, and the video to be played.
    mVideoListPlayer.setPreloadCount(1);
    ```

2.  Add multiple video sources.

    The short video list player can play videos from specified URLs or videos with specified VIDs from ApsaraVideo VOD. You must use STS tokens to play videos from ApsaraVideo VOD. The following code provides an example:

    ```
    // Add a video from ApsaraVideo VOD.
    [self.listPlayer addVidSource:VID of the video from ApsaraVideo VOD uid:"Unique ID of the video"];
    // Add a video from a specified URL.
    [self.listPlayer addUrlSource:"URL of the video" uid: "Unique ID of the video"];
    ```

    **Note:** The short video list player distinguishes videos based on their unique IDs. An unexpected video may be played if you add video sources with the same unique ID. Make sure that video sources that are added to the player at a time have unique IDs.

3.  Start the playback.

    The short video list player provides the following methods for you to locate and play videos. The following code provides an example:

    ```
    // Locate a video and play it.
    [self.listPlayer moveTo:"Unique ID of the video"]; // Play the video from the specified URL.
    [self.listPlayer moveTo:"Unique ID of the video" accId:accId accKey:accKey token:token region:region]; // Use the STS token to play the video with the specified VID from ApsaraVideo VOD.
    // Play the previous video in the list.
    [self.listPlayer moveToPrev:"Unique ID of the video"]; // Play the video from the specified URL.
    [self.listPlayer moveToPrev:"Unique ID of the video" accId:accId accKey:accKey token:token region:region]; // Use the STS token to play the video with the specified VID from ApsaraVideo VOD.
    // Play the next video in the list.
    [self.listPlayer moveToNext:"Unique ID of the video"]; // Play the video from the specified URL.
    [self.listPlayer moveToNext:"Unique ID of the video" accId:accId accKey:accKey token:token region:region]; // Use the STS token to play the video with the specified VID from ApsaraVideo VOD.
    ```

4.  Scroll the playlist.

    1.  Tap the screen to pause or resume the playback. The following code provides an example:

        ```
        - (void)tap {
            if ([self.delegate respondsToSelector:@selector(AVPSimplePlayScrollViewTapGestureAction:)]) {
                [self.delegate AVPSimplePlayScrollViewTapGestureAction:self];
            }
        }
        - (void)AVPSimplePlayScrollViewTapGestureAction:(AVPSimplePlayScrollView *)simplePlayScrollView {
            if (self.playerStatus == AVPStatusStarted) {
                // Pause the video if the video is being played.
                [self.listPlayer pause];
            }else if (self.playerStatus == AVPStatusPaused) {
                // Play the video if the video is paused.
                [self.listPlayer start];
            }
        }
        ```

    2.  Scroll the playlist.

        If you scroll the playlist so fast that you skip the previous video or the next video, the moveTo method is called to locate and play the specified video. The following code provides an example:

        ```
        - (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView {
            CGFloat indexFloat = scrollView.contentOffset.y/self.frame.size.height;
            NSInteger index = (NSInteger)indexFloat;
            .......
              // Scroll down to the next video.
               if (index - self.currentIndex == 1) {
                    if ([self.delegate respondsToSelector:@selector(AVPSimplePlayScrollView:motoNextAtIndex:)]) {
                        [self.delegate AVPSimplePlayScrollView:self motoNextAtIndex:index];
                    }
                }
                // Scroll up to the previous video.
                else if (self.currentIndex - index == 1){
                    if ([self.delegate respondsToSelector:@selector(AVPSimplePlayScrollView:motoPreAtIndex:)]) {
                        [self.delegate AVPSimplePlayScrollView:self motoPreAtIndex:index];
                    }
                }
                // Scroll the playlist up or down to skip more than one video.
                else {
                    if ([self.delegate respondsToSelector:@selector(AVPSimplePlayScrollView:scrollViewDidEndDeceleratingAtIndex:)]) {
                        [self.delegate AVPSimplePlayScrollView:self scrollViewDidEndDeceleratingAtIndex:index];
                    }
                }
        }
        /**
         Scroll the playlist up or down to skip more than one video.
         @param simplePlayScrollView simplePlayScrollView
         @param index The count from the current video to the destination video in the upward or downward direction.
         */
        - (void)AVPSimplePlayScrollView:(AVPSimplePlayScrollView *)simplePlayScrollView scrollViewDidEndDeceleratingAtIndex:(NSInteger)index {
            // Locate the destination video.
            AVPDemoResponseVideoListModel *model = [self findModelFromIndex:index];
            // Call the moveTo method to scroll to the current video.
            [self moveToCurrentModel];
        }
        ```

5.  Hide the thumbnail.

    When the player starts to play a video, it hides the video thumbnail and displays the video. The following code provides an example:

    ```
    -(void)onPlayerEvent:(AliPlayer*)player eventType:(AVPEventType)eventType {
        switch (eventType) {
            case AVPEventPrepareDone: {
            }
                break;
            case AVPEventFirstRenderedStart: {
                // Hide the thumbnail.
                [self.simplePlayScrollView showPlayView];
            }
                break;
            default:
                break;
        }
    }
    ```

6.  Destroy the player.

    You must release the player after use. Otherwise, a memory leakage bug may occur. The following code provides an example:

    ```
    [self.listPlayer stop];
    [self.listPlayer destroy];
    self.listPlayer = nil;
    ```


