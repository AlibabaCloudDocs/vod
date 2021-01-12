# Import and editing

## Features

The short video SDK allows you to import videos or images and produce videos with extensive effects such as filters, dubbing, time effects, and transitions. The core editing class is AliyunIEditor.

## Edition difference

|Edition|Description|
|-------|-----------|
|Professional Edition|All features are supported.|
|Standard Edition|Features except subtitles, animated stickers, and MVs are supported.|
|Basic Edition|The import and editing features are not supported.|

## Editing processes

|Editing process|Description|
|---------------|-----------|
|[Set parameters](#title_kv3_8vg_1wz)|The methods in this module are used to create or destroy an editor instance.|
|[Import videos](#title_4rx_i8w_1u0)|The methods in this module are used to import videos and images as media clips and assemble the media clips before editing to obtain the URL that is required for initialization.|
|[Edit media clips](#title_cej_ewy_5ku)|The methods in this module are used to dynamically crop and replace the media clips and adjust the transition duration and effects during editing.|
|[Configure effects](#title_8ko_4rr_147)|The methods in this module are used to configure common filter effects, animated filter effects such as spirit freed from the body, and animated sticker effects.|
|[Configure preview](#title_1jn_o7r_bub)|The methods in this module are used to configure preview in the editor.|
|[Produce a video](#title_eis_wzl_zo8)|The methods in this module are used to produce a video.|

## Set parameters

|Action|Sample code|
|------|-----------|
|Create an editor instance.|```
AliyunEditorFactory#creatAliyunEditor(Uri uri);
``` |
|Initialize an editor instance.|```
AliyunIEditor#init(SurfaceView surfaceView);// Sets the preview window.
``` |

## Import videos

|Action|Sample code|
|------|-----------|
|Add a media clip.|```
AliyunIImport#addMediaClip(AliyunClip clip);
``` |
|Remove a media clip.|```
AliyunIImport#removeMedia(int id);
``` |
|Swap the positions of media clips.|```
AliyunIImport#swap(int pos1, int pos2);
``` |
|Generate the configuration file of media clips.|```
AliyunIImport#generateProjectConfigure();
``` |
|Set production parameters, including the frame rate, bitrate, size of a group of pictures \(GOP\), output resolution, encoder, quality level, and video display mode.|```
AliyunIImport#setVideoParam(AliyunVideoParam param);
``` |

## Edit media clips

|Action|Sample code|
|------|-----------|
|Obtain the media clip manager.|```
AliyunIEditor#getSourcePartManager();// Obtains the media clip manager.
``` |
|Add a media clip to the end of the media clip list.|```
AliyunIClipConstructor#addMediaClip(AliyunClip clip);
``` |
|Add a media clip to the specified position.|```
AliyunIClipConstructor#addMediaClip(int index, AliyunClip clip);
``` |
|Update and replace the media clip at the specified position.|```
AliyunIClipConstructor#updateMediaClip(int index, AliyunClip clip);
``` |
|Delete the last media clip.|```
AliyunIClipConstructor#deleteMediaClip();
``` |
|Delete the specified media clip.|```
AliyunIClipConstructor#deleteMediaClip(int index);
``` |
|Apply the updated media clip list and clear the previous one.|```
AliyunIClipConstructor#updateAllClips(List<AliyunClip> clips);
``` |
|Obtain the number of current media clips.|```
AliyunIClipConstructor#getMediaPartCount();
``` |
|Obtain the current media clip list.|```
AliyunIClipConstructor#getAllClips();
``` |
|Swap the positions of media clips.|```
AliyunIClipConstructor#swap(int pos1, int pos2);
``` |
|Apply the updated media clips.|```
AliyunIEditor#applySourceChange();// Applies the updated media clips.
``` |

## Configure effects

-   **Common filters**

    The methods in this module are used to configure common filter effects.

    |Action|Sample code|
    |------|-----------|
    |Add a common filter.|    ```
AliyunIEditor#applyFilter(EffectBean effect);
    ``` |
    |Remove a common filter.|    ```
AliyunIEditor#applyFilter(new EffectBean());// Removes a common filter by setting the filter path to null.
    ``` |

-   **Animated filters**

    The methods in this module are used to configure animated filter effects, such as spirit freed from the body.

    |Action|Sample code|
    |------|-----------|
    |Add an animated filter.|    ```
AliyunIEditor#addAnimationFilter(EffectFilter filter);
    ``` |
    |Remove an animated filter.|    ```
AliyunIEditor#removeAnimationFilter(EffectFilter filter);
    ``` |
    |Clear all animated filters.|    ```
AliyunIEditor#clearAllAnimationFilter();
    ``` |

-   **Animated stickers, bubbles, and text**

    The methods in this module are used to configure animated sticker effects.

    -   **By using the UI controller**

        In the short video SDK, the user interface \(UI\) controller is a framework that is used to manage animated stickers. It encapsulates common interaction logic, such as resizing, rotating, and mirroring, of animated stickers in short videos. The core classes involved are AliyunIEditor, AliyunPasterManager, AliyunPasterController, and AliyunPasterBaseView. Animated sticker interactions within the UI controller comply with the interaction rules shown in the demo.

        -   AliyunIEditor: the core editing class.
        -   AliyunPasterManager: the sticker and subtitle manager in the UI controller, which is used to add stickers.
        -   AliyunPasterController: the controller for managing a single sticker, which is used to display, hide, or remove a sticker. You can also use this controller to obtain attributes of a sticker, such as the display duration.
        -   AliyunPasterBaseView: the interface of the sticker display view in the UI controller. Only this interface needs to be implemented if you want to customize the sticker display UI without changing the interaction logic.
        |Action|Sample code|
        |------|-----------|
        |Obtain the animated sticker manager AliyunPasterManager.|        ```
AliyunIEditor#createPasterManager();
        ``` |
        |Set the size of the animated sticker display area. This method must be called before AliyunIEditor\#init.|        ```
AliyunPasterManager#setDisplaySize(int width, int height);
        ``` |
        |Add a common animated sticker or a bubble animated sticker. The sticker UI controller AliyunPasterController is returned.|        ```
AliyunPasterManager#addPaster(String path);// Adds an animated sticker that is displayed all the time.
AliyunPasterManager#addPasterWithStartTime(String path, long startTime, long duration);// Adds an animated sticker that is displayed within the specified time period.
        ``` |
        |Add text.|        ```
AliyunPasterManager#addSubtitle(String text, String font);// Adds text that is displayed all the time.
AliyunPasterManager#addSubtitleWithStartTime(String text, String font, long startTime, long duration);// Adds text that is displayed within the specified time period.
        ``` |
        |Set the UI view AliyunPasterBaseView that displays animated stickers, bubbles, and text. This method must be called.|        ```
AliyunPasterController#setPasterView(AliyunPasterBaseView pasterView);
        ``` |
        |Set the callback to be called when an animated sticker is restored.|        ```
AliyunPasterManager#setOnPasterRestoreListener(OnPasterRestored listener);
        ``` |
        |Remove an animated sticker from the UI controller.|        ```
AliyunPasterController#removePaster();
        ``` |
        |Display an animated sticker. The animated sticker is applied to the video and disappears from the UI layer.|        ```
AliyunPasterController#editCompleted();
        ``` |
        |Hide an animated sticker. The animated sticker is removed from the video and displayed at the UI layer.|        ```
AliyunPasterController#editStart();
        ``` |
        |Create a preview player at the sticker view layer.|        ```
AliyunPasterController#createPasterPlayer(TextureView view);
        ``` |
        |Remove an animated sticker.|        ```
AliyunPasterController#removePaster();
        ``` |

    -   **Without using the UI controller**

        If you do not want to use the UI controller, you must independently implement the logic for editing and interacting with animated stickers on the UI. This is complex and not recommended. To render an animated sticker, you only need to pass the object, position, and size of the animated sticker to the renderer.

        You can directly use the sticker rendering methods provided by the short video SDK to render stickers without using the UI controller. In fact, the UI controller uses exactly the same methods to render stickers. The core classes involved are AliyunIEditor, AliyunPasterManager, and AliyunPasterRender.

        -   AliyunIEditor: the core editing class. AliyunPasterManager: the sticker and subtitle manager in the UI controller, which is used to add stickers.
        -   AliyunPasterRender: the core sticker rendering class. The methods in this class only apply stickers to videos. You must implement the logic for interacting with animated stickers on the UI and calculate information such as the position, size, and rotation angle.
        |Action|Sample code|
        |------|-----------|
        |Obtain the animated sticker manager AliyunPasterManager.|        ```
AliyunIEditor#createPasterManager();
        ``` |
        |Obtain the sticker renderer AliyunPasterRender.|        ```
AliyunIEditor#getPasterRender();
        ``` |
        |Set the size of the animated sticker display area. These methods must be called before AliyunIEditor\#init.|        ```
AliyunPasterRender#setDisplaySize(int width, int height);
AliyunPasterManager#setDisplaySize(int width, int height);
        ``` |
        |Add an animated sticker.|        ```
AliyunPasterRender#addEffectPaster(EffectPaster paster);
        ``` |
        |Display an animated sticker.|        ```
AliyunPasterRender#showPaster(EffectPaster paster);
        ``` |
        |Hide an animated sticker.|        ```
AliyunPasterRender#hidePaster(EffectPaster paster);
        ``` |
        |Remove an animated sticker.|        ```
AliyunPasterRender#removePaster(EffectPaster paster);
        ``` |
        |Set the callback to be called when an animated sticker is saved and restored.|        ```
AliyunPasterRender#setOnPasterResumeAndSave(OnPasterResumeAndSave listener);
        ``` |

-   **Static stickers**

    |Action|Sample code|
    |------|-----------|
    |Add a static sticker.|    ```
AliyunIEditor#addImage(EffectPicture picture);
    ``` |
    |Remove a static sticker.|    ```
AliyunIEditor#removeImage(EffectPicture picture);
    ``` |

-   **Watermarks**

    |Action|Sample code|
    |------|-----------|
    |Add a watermark.|    ```
AliyunIEditor#applyWaterMark(String imgPath, float sizeX, float sizeY, float posX, float posY);
    ``` |
    |Add an end watermark.|    ```
AliyunIEditor#addTailWaterMark(String imagePath, float sizeX, float sizeY, float posX, float posY, long durationUs);
    ``` |

-   **Transitions**

    |Action|Sample code|
    |------|-----------|
    |Add a transition. You can set a transition when you import or add a video or an image.|    ```
AliyunVideoClip#setTransition(TransitionBase transition); // Sets a transition for a video.
AliyunImageClip#setTransition(TransitionBase transition); // Sets a transition for an image.
    ``` |
    |Update transition configuration. You can modify and update transition configuration when you update media clips.|    ```
AliyunEditor#setTransition(int index, TransitionBase transition); // Sets a transition. The index parameter indicates the transition position, which starts from 0.
AliyunEditor#setTransition(Map<Integer, TransitionBase> transitions); // Sets multiple transitions.
    ``` |

-   **Frame animations**

    |Action|Sample code|
    |------|-----------|
    |Add a frame animation.|    ```
AliyunEditor#addFrameAnimation(ActionBase action);
    ``` |
    |Remove a frame animation.|    ```
removeFrameAnimation(ActionBase action);
    ``` |

-   **MV**

    |Action|Sample code|
    |------|-----------|
    |Add an MV.|    ```
AliyunIEditor#applyMV(EffectBean effect);
    ``` |
    |Remove an MV.|    ```
AliyunIEditor#applyMV(null);// Removes the MV effect by setting the parameter to null.
    ``` |

-   **Background music and multi-track dubbing**

    |Action|Sample code|
    |------|-----------|
    |Add background music or dubbing. The background music is not affected by time effects, while the dubbing is.|    ```
AliyunIEditor#applyMusic(EffectBean effect);// Adds background music.
AliyunIEditor#applyDub(EffectBean effect);// Adds dubbing.
    ``` |
    |Remove background music or dubbing.|    ```
AliyunIEditor#removeMusic(EffectBean effect);// Removes background music.
AliyunIEditor#removeDub(EffectBean effect);// Removes dubbing.
    ``` |
    |Adjust the weight of the background music or dubbing when the background music or dubbing is mixed with the original audio.|    ```
AliyunIEditor#applyMusicMixWeight(int id, int weight);
    ``` |
    |Adjust the volume of the specified audio stream, such as background music, dubbing, or original audio.|    ```
AliyunIEditor#applyMusicWeight(int id, int weight);
    ``` |
    |Denoise an audio stream. Perform this operation with caution because it consumes a large amount of resources.|    ```
AliyunIEditor#denoise(int id, boolean needDenoise);
    ``` |

-   **Sound effects**

    The short video SDK allows you to add sound effects to each audio stream and provides various sound effects such as lolita, uncle, reverberation, and echo.

    |Action|Sample code|
    |------|-----------|
    |Set the sound effect of a single stream.|Sound effects can be overlaid. To switch to a new sound effect, you must remove the existing sound effect.

    -   id: the ID of the specified audio stream.
    -   type: the type of the sound effect.
    -   weight: the weight of the sound effect. Valid values: 0 to 100.
    ```
int audioEffect(int id, AudioEffectType type, int weight);
    ``` |
    |Delete a sound effect.|Sound effects can be overlaid. To switch to a new sound effect, you must remove the existing sound effect.

    ```
int removeAudioEffect(int id, AudioEffectType type);
    ``` |

-   **Time effects**

    |Action|Sample code|
    |------|-----------|
    |Adjust the speed.|    ```
AliyunIEditor#rate(float rate, long startTime, long duration, boolean needOriginDuration);
// Since V3.7.0, you can call this method to adjust the playback speed for multiple videos or images.
    ``` |
    |Repeat the media clip.|    ```
AliyunIEditor#repeat(int times, long startTime, long duration, boolean needOriginDuration);
    ``` |
    |Reversely play a media clip.|    ```
AliyunIEditor#invert();
Videos whose GOP size is greater than 5 must be transcoded before reverse playback. You can call the NativeParser#getMaxGopSize() method to view the GOP size of a video. During transcoding, call the CropParam#setGop(1) method to set the GOP size to 1.
    ``` |
    |Remove the time effect.|    ```
AliyunIEditor#deleteTimeEffect(int id);
    ``` |

-   **Doodles**

    The short video SDK encapsulates a set of doodle methods, including those for configuring the canvas and paint brush. All doodling operations are completed by using the doodle controller AliyunICanvasController. Canvas: a UI interaction view for doodling. You can add the UI interaction view to the UI interaction view group. Paint brush: an android.graphics.Paint object. You can set an external paint brush or use the default one.

    |Action|Sample code|
    |------|-----------|
    |Obtain the doodle controller AliyunICanvasController.|    ```
AliyunIEditor#obtainCanvasController(Context context, int w, int h);
    ``` |
    |Obtain the canvas.|    ```
AliyunICanvasController#getCanvas();
    ``` |
    |Check whether a doodle exists in the video.|    ```
AliyunICanvasController#hasCanvasPath();
    ``` |
    |Apply the doodle to the video.|    ```
AliyunICanvasController#applyPaintCanvas();
    ``` |
    |Remove the doodle applied to the video.|    ```
AliyunICanvasController#removeCanvas();
    ``` |
    |Undo the previous doodling operation.|    ```
AliyunICanvasController#undo();
    ``` |
    |Clear the canvas.|    ```
AliyunICanvasController#clear();
    ``` |
    |Set a color for the current paint brush.|    ```
AliyunICanvasController#setCurrentColor(int color);
    ``` |
    |Set a line width for the current paint brush.|    ```
AliyunICanvasController#setCurrentSize(float size);
    ``` |
    |Set a custom paint brush.|    ```
AliyunICanvasController#setPaint(Paint paint);
    ``` |
    |Reset the canvas.|    ```
AliyunICanvasController#resetPaintCanvas();
    ``` |
    |Undo all doodling operations.|    ```
AliyunICanvasController#cancel();
    ``` |
    |Confirm all doodling operations.|    ```
AliyunICanvasController#confirm();
    ``` |
    |Release resources.|    ```
AliyunICanvasController#release();
    ``` |

-   **Others**

    |Action|Sample code|
    |------|-----------|
    |Set the dynamic display mode.|    ```
AliyunIEditor#addRunningDisplayMode(VideoDisplayMode mode, int streamId, long startTimeMills, long durationMills);
    ``` |
    |Set a blur background. This effect is visible in padding mode.|    ```
AliyunIEditor#applyBlurBackground(int streamId, long startTimeMills, long durationMills, float blurRadius);
    ``` |


## Configure preview

|Action|Sample code|
|------|-----------|
|Replace the display window.|```
AliyunIEditor#setDisplayView(SurfaceView surfaceView);
AliyunIEditor#setDisplayView(TextureView textureView);// Unless otherwise specified, we recommend that you do not call this method.
``` |
|Start the playback.|```
AliyunIEditor#play();
``` |
|Seek|```
AliyunIEditor#seek();
``` |
|Forcibly draw a frame.|```
AliyunIEditor#draw();
``` |
|Pause the playback.|```
AliyunIEditor#pause();
``` |
|Resume the playback.|```
AliyunIEditor#resume();
``` |
|Stop the playback.|```
AliyunIEditor#stop();
``` |
|Obtain the current position in the stream, which is not affected by time effects.|```
AliyunIEditor#getCurrentStreamPosition();
``` |
|Obtain the current playback position, which is affected by time effects.|```
AliyunIEditor#getCurrentPlayPosition();
``` |
|Obtain the stream duration, which is not affected by time effects.|```
AliyunIEditor#getStreamDuration();
``` |
|Obtain the total playback duration, which is affected by time effects.|```
AliyunIEditor#getDuration();
``` |
|Specify whether to mute the audio.|```
AliyunIEditor#setAudioSilence(boolean silence);
``` |
|Set the volume.|```
AliyunIEditor#setVolume(int volume);
``` |
|Set the video display mode.|```
AliyunIEditor#setDisplayMode(VideoDisplayMode mode);
``` |
|Set the background filling color in padding mode.|```
AliyunIEditor#setFillBackgroundColor(int color);
``` |

## Produce a video

|Action|Sample code|
|------|-----------|
|Start the production.|```
AliyunIEditor#compose(AliyunVideoParam param, String outputPath, AliyunIComposeCallBack callback);
``` |
|Cancel the production.|```
AliyunIEditor#cancelCompose();
``` |

