# Video merging

## Overview

The AliyunIMixComposer operation is used to produce a video from multiple videos offline. The videos can be arranged in the specified layout, such as picture-in-picture, nine-square grid, left-right split-screen, or up-down split-screen. You can use this operation to produce a video from two or more videos, not only two videos in a duet.

## Merging process

-   **Initialize a merging instance**

    ```
    AliyunMixComposerCreator.createMixComposerInstance();
    ```

-   **Create tracks**

    ```
    AliyunIMixComposer#createTrack(AliyunMixTrackLayoutParam layoutParam);
    ```

-   **Add video streams to the tracks**

    |Action|Sample code|
    |------|-----------|
    |Create a video stream.|    ```
new AliyunMixStream.Builder().build();
    ``` |
    |Add the video stream to a track.|    ```
AliyunMixTrack#addStream(AliyunMixStream stream);
    ``` |

-   **Set output parameters**

    ```
    AliyunIMixComposer#setOutputParam(AliyunMixOutputParam param);
    ```

-   **Start merging**

    ```
    AliyunIMixComposer#start(AliyunMixCallback callback);
    ```

-   **Pause merging**

    ```
    AliyunIMixComposer#pause();
    ```

-   **Resume merging**

    ```
    AliyunIMixComposer#resume();
    ```

-   **Cancel merging**

    ```
    AliyunIMixComposer#cancel();
    ```

-   **Destroy the merging instance**

    ```
    AliyunIMixComposer#release();
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
        .outputAudioReferenceTrack(track2)// Specify that the audio of Track 2 is used as the audio of the produced audio. The produced video supports only one audio stream. Therefore, the audio of the second video stream of Track 2 is not added to the produced video.
        .outputDurationReferenceTrack(track2) // Specify that the duration of Track 2 is used as the duration of the produced video. If the duration of Track 1 is shorter than this value, the video of Track 1 stops at the last frame.
        .crf(6)
        .videoQuality(VideoQuality.HD)
        .outputWidth(720)
        .outputHeight(1280)
        .fps(30)
        .gopSize(30)
        .build();
mixComposer.setOutputParam(outputParam);

// Start the merging.
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

