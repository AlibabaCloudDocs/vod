# Video merging

This topic describes the video merging feature and process. It also provides the sample code to show you how to merge videos by using the short video SDK for Android.

## Overview

The short video SDK provides the AliyunIMixComposer interface for you to merge videos. You can implement this interface to produce a video from multiple videos offline. The videos can be arranged in the specified layout, such as picture-in-picture, nine-square grid, left-right split-screen, or up-down split-screen. Two or more video tracks can be created for video merging.

## Merging process

-   Load files

    Load all files.

    ```
    AlivcSdkCore.register(getApplicationContext());
    ```

-   Create an AliyunIMixComposer instance

    ```
    AliyunMixComposerCreator.createMixComposerInstance();
    ```

-   Create tracks

    ```
    AliyunIMixComposer.createTrack(AliyunMixTrackLayoutParam layoutParam);
    ```

-   Add video streams to tracks

    |Action|Sample code|
    |------|-----------|
    |Create a video stream.|    ```
new AliyunMixStream.Builder().build();
    ``` |
    |Add a video stream to a track.|    ```
AliyunMixTrack.addStream(AliyunMixStream stream);
    ``` |

-   Set output parameters

    ```
    AliyunIMixComposer.setOutputParam(AliyunMixOutputParam param);
    ```

-   Start merging

    ```
    AliyunIMixComposer.start(AliyunMixCallback callback);
    ```

-   Pause merging

    ```
    AliyunIMixComposer.pause();
    ```

-   Resume merging

    ```
    AliyunIMixComposer.resume();
    ```

-   Cancel merging

    ```
    AliyunIMixComposer.cancel();
    ```

-   Destroy the AliyunIMixComposer instance

    ```
    AliyunIMixComposer.release();
    ```


## Sample code

```
// Create an instance.
AliyunIMixComposer mixComposer = AliyunMixComposerCreator.createMixComposerInstance();

// Create Track 1.
AliyunMixTrackLayoutParam track1Layout = new AliyunMixTrackLayoutParam.Builder()
        .centerX(0.25f)
        .centerY(0.5f)
        .widthRatio(0.5f)
        .heightRatio(1.f)
        .build();
// Create the first video stream to be added to Track 1.
AliyunMixStream stream11 = new AliyunMixStream
        .Builder()
        .displayMode(VideoDisplayMode.FILL)
        .filePath("/storage/emulated/0/11.mp4")
        .streamEndTimeMills(20000)
        .build();
// Add the video stream to Track 1.
track1.addStream(stream11);

// Create the second video stream to be added to Track 1.
AliyunMixStream stream12 = new AliyunMixStream
        .Builder()
        .displayMode(VideoDisplayMode.FILL)
        .filePath("/storage/emulated/0/12.mp4")
        .streamEndTimeMills(20000)
        .build();
// Add the video stream to Track 1.
track1.addStream(stream12);

// Create Track 2.
AliyunMixTrackLayoutParam track2Layout = new AliyunMixTrackLayoutParam.Builder()
        .centerX(0.75f)
        .centerY(0.5f)
        .widthRatio(0.5f)
        .heightRatio(1.f)
        .build();
// Create the first video stream to be added to Track 2.
AliyunMixStream stream21 = new AliyunMixStream
        .Builder()
        .displayMode(VideoDisplayMode.FILL)
        .filePath("/storage/emulated/0/21.mp4")
        .streamEndTimeMills(20000)
        .build();
// Add the video stream to Track 2.
track2.addStream(stream21);

// Create the second video stream to be added to Track 2.
AliyunMixStream stream22 = new AliyunMixStream
        .Builder()
        .displayMode(VideoDisplayMode.FILL)
        .filePath("/storage/emulated/0/22.mp4")
        .streamEndTimeMills(20000)
        .build();

// Add the video stream to Track 2.
track2.addStream(stream22);

// Set output parameters.
AliyunMixOutputParam outputParam = new AliyunMixOutputParam.Builder()
        .outputPath("/sdcard/output.mp4")
        .outputAudioReferenceTrack(track2)// Specify that the audio of Track 2 is used as the output audio. The merged video supports only one audio stream. Therefore, the audio of the second video stream of Track 2 is not added to the merged video.
        .outputDurationReferenceTrack(track2) // Specify that the duration of Track 2 is used as the duration of the merged video. If the duration of Track 1 is shorter than this value, the video of Track 1 stops at the last frame.
        .crf(6)
        .videoQuality(VideoQuality.HD)
        .outputWidth(720)
        .outputHeight(1280)
        .fps(30)
        .gopSize(30)
        .build();
mixComposer.setOutputParam(outputParam);

// Start merging.
AliyunMixCallback callback = new AliyunMixCallback() {
            @Override
            public void onProgress(long progress) {// The merging progress.
                Log.e("MixRecord", "onProgress " + progress);
            }

            @Override
            public void onComplete() {
                Log.e("MixRecord", "onComplete");
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        // Do not call this method in a thread that is used by a callback.
                           mixComposer.release();
                    }
                });
            }

            @Override
            public void onError(int errorCode) {
                Log.e("MixRecord", "onError " + errorCode);
            }
};
mixComposer.start(callback);
```

