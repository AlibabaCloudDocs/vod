# Import and editing

The short video SDK allows you to import videos or images and produce videos with extensive effects such as filters, dubbing, time effects, and transitions.

## Differences among editions

|Edition|Description|
|-------|-----------|
|Professional Edition|All features are supported.|
|Standard Edition|Features except subtitles, animated stickers, and music videos \(MVs\) are supported.|
|Basic Edition|The import and editing features are not supported.|

## Editing processes

|Editing process|Description|
|---------------|-----------|
|[Import videos](#title_067_klv_rn6)|The methods in this module are used to import videos and images as media clips and assemble the media clips before editing to obtain the Uniform Resource Identifier \(URI\) path that is required for initialization.|
|[Set parameters](#title_kv3_8vg_1wz)|The methods in this module are used to destroy an editor instance or create an editor instance based on the URI that is generated when videos or images are imported.|
|[Edit media clips](#title_cej_ewy_5ku)|The methods in this module are used to dynamically crop and replace the media clips and adjust the transition duration and effects during editing. The core editing class is the AliyunIEditor class.|
|[Configure effects](#title_8ko_4rr_147)|The methods in this module are used to configure common filter effects, animated filter effects such as spirit freed from the body, and animated sticker effects.|
|[Configure preview](#title_1jn_o7r_bub)|The methods in this module are used to configure preview in the editor.|
|[Produce a video](#title_eis_wzl_zo8)|The methods in this module are used to produce a video.|

## Import videos

|Action|Sample code|
|------|-----------|
|Add a media clip.|```
AliyunIImport.addMediaClip(AliyunClip clip);
``` |
|Remove a media clip.|```
AliyunIImport.removeMedia(int id);
``` |
|Swap the positions of media clips.|```
AliyunIImport.swap(int pos1, int pos2);
``` |
|Generate the configuration file of media clips.|```
AliyunIImport.generateProjectConfigure();
``` |
|Set production parameters, including the frame rate, bitrate, group of pictures \(GOP\) size, output resolution, encoder, quality level, and video display mode.|```
AliyunIImport.setVideoParam(AliyunVideoParam param);
``` |

## Set parameters

|Action|Sample code|
|------|-----------|
|Create an editor instance.|```
AliyunEditorFactory.creatAliyunEditor(Uri uri);
``` |
|Initialize an editor instance.|```
AliyunIEditor.init(SurfaceView surfaceView);// Sets the preview window.
``` |

## Edit media clips

|Action|Sample code|
|------|-----------|
|Obtain the media clip manager.|```
AliyunIEditor.getSourcePartManager();// Obtains the media clip manager.
``` |
|Add a media clip to the end of the media clip list.|```
AliyunIClipConstructor.addMediaClip(AliyunClip clip);
``` |
|Add a media clip to the specified position.|```
AliyunIClipConstructor.addMediaClip(int index, AliyunClip clip);
``` |
|Update and replace the media clip at the specified position.|```
AliyunIClipConstructor.updateMediaClip(int index, AliyunClip clip);
``` |
|Delete the last media clip.|```
AliyunIClipConstructor.deleteMediaClip();
``` |
|Delete the specified media clip.|```
AliyunIClipConstructor.deleteMediaClip(int index);
``` |
|Apply the updated media clip list and clear the previous one.|```
AliyunIClipConstructor.updateAllClips(List<AliyunClip> clips);
``` |
|Obtain the number of current media clips.|```
AliyunIClipConstructor.getMediaPartCount();
``` |
|Obtain the current media clip list.|```
AliyunIClipConstructor.getAllClips();
``` |
|Swap the positions of media clips.|```
AliyunIClipConstructor.swap(int pos1, int pos2);
``` |
|Apply the updated media clips.|```
AliyunIEditor.applySourceChange();// Applies the updated media clips.
``` |

## Configure effects

-   Common filters

    The methods in this module are used to configure common filter effects.

    |Action|Sample code|
    |------|-----------|
    |Add a common filter.|    ```
AliyunIEditor.applyFilter(EffectBean effect);
    ``` |
    |Remove a common filter.|    ```
AliyunIEditor.applyFilter(new EffectBean());// Removes a common filter by setting the filter path to null.
    ``` |

-   Animated filters

    The methods in this module are used to configure animated filter effects, such as spirit freed from the body.

    |Action|Sample code|
    |------|-----------|
    |Add an animated filter.|    ```
AliyunIEditor.addAnimationFilter(EffectFilter filter);
    ``` |
    |Remove an animated filter.|    ```
AliyunIEditor.removeAnimationFilter(EffectFilter filter);
    ``` |
    |Clear all animated filters.|    ```
AliyunIEditor.clearAllAnimationFilter();
    ``` |

-   Animated stickers, bubbles, and text

    The methods in this module are used to configure animated sticker effects.

    By using the UI controller

    In the short video SDK, the user interface \(UI\) controller is a framework that is used to manage animated stickers. It encapsulates common interaction logic, such as resizing, rotating, and mirroring, of animated stickers in short videos. The core classes involved are AliyunIEditor, AliyunPasterManager, AliyunPasterController, and AliyunPasterBaseView. Animated sticker interactions within the UI controller comply with the interaction rules that are shown in the demo.

    -   AliyunIEditor: the core editing class.
    -   AliyunPasterManager: the sticker and subtitle manager in the UI controller. It is used to add stickers.
    -   AliyunPasterController: the controller for managing a single sticker. It is used to display, hide, or remove a sticker. You can also use this controller to obtain the attributes of a sticker, such as the display duration.
    -   AliyunPasterBaseView: the interface for the sticker display view in the UI controller. Only this interface needs to be implemented if you want to customize the sticker display UI without changing the interaction logic.
    |Action|Sample code|
    |------|-----------|
    |Obtain the animated sticker manager AliyunPasterManager.|    ```
AliyunIEditor.createPasterManager();
    ``` |
    |Set the size of an area for displaying animated stickers. These methods must be called before AliyunIEditor is initialized.|    ```
AliyunPasterManager.setDisplaySize(int width, int height);
    ``` |
    |Add a common animated sticker or a bubble animated sticker. The sticker UI controller AliyunPasterController is returned.|    ```
AliyunPasterManager.addPaster(String path);// Adds an animated sticker that is displayed all the time.
AliyunPasterManager.addPasterWithStartTime(String path, long startTime, long duration);// Adds an animated sticker that is displayed within the specified period.
    ``` |
    |Add text.|    ```
AliyunPasterManager.addSubtitle(String text, String font);// Adds text that is displayed all the time.
AliyunPasterManager.addSubtitleWithStartTime(String text, String font, long startTime, long duration);// Adds text that is displayed within the specified period.
    ``` |
    |Set the UI view AliyunPasterBaseView that displays animated stickers, bubbles, and text. This method must be called.|    ```
AliyunPasterController.setPasterView(AliyunPasterBaseView pasterView);
    ``` |
    |Set the callback to be fired when an animated sticker is restored.|    ```
AliyunPasterManager.setOnPasterRestoreListener(OnPasterRestored listener);
    ``` |
    |Remove an animated sticker from the UI controller.|    ```
AliyunPasterController.removePaster();
    ``` |
    |Display an animated sticker. The animated sticker is applied to the video and disappears from the UI layer.|    ```
AliyunPasterController.editCompleted();
    ``` |
    |Hide an animated sticker. The animated sticker is removed from the video and displayed at the UI layer.|    ```
AliyunPasterController.editStart();
    ``` |
    |Create a preview player at the sticker view layer.|    ```
AliyunPasterController.createPasterPlayer(TextureView view);
    ``` |
    |Remove an animated sticker.|    ```
AliyunPasterController.removePaster();
    ``` |

    Without using the UI controller

    If you do not want to use the UI controller, you must independently implement the logic for editing and interacting with animated stickers on the UI. This is complex and not recommended. To render an animated sticker, you need to pass the object, position, and size of the animated sticker to the renderer.

    You can directly use the sticker rendering methods that are provided by the short video SDK to render stickers without using the UI controller. The UI controller actually uses the same methods to render stickers. The core classes involved are AliyunIEditor, AliyunPasterManager, and AliyunPasterRender.

    -   AliyunIEditor: the core editing class.
    -   AliyunPasterManager: the sticker and subtitle manager in the UI controller. It is used to add stickers.
    -   AliyunPasterRender: the core class for sticker rendering. The methods in this class are used to apply stickers to videos. You must implement the logic for interacting with animated stickers on the UI and calculate information such as the position, size, and rotation angle.
    |Action|Sample code|
    |------|-----------|
    |Obtain the animated sticker manager AliyunPasterManager.|    ```
AliyunIEditor.createPasterManager();
    ``` |
    |Obtain the sticker renderer AliyunPasterRender.|    ```
AliyunIEditor.getPasterRender();
    ``` |
    |Set the size of an area for displaying animated stickers. These methods must be called before AliyunIEditor is initialized.|    ```
AliyunPasterRender.setDisplaySize(int width, int height);
AliyunPasterManager.setDisplaySize(int width, int height);
    ``` |
    |Add an animated sticker.|    ```
AliyunPasterRender.addEffectPaster(EffectPaster paster);
    ``` |
    |Display an animated sticker.|    ```
AliyunPasterRender.showPaster(EffectPaster paster);
    ``` |
    |Hide an animated sticker.|    ```
AliyunPasterRender.hidePaster(EffectPaster paster);
    ``` |
    |Remove an animated sticker.|    ```
AliyunPasterRender.removePaster(EffectPaster paster);
    ``` |
    |Set the callbacks to be fired when an animated sticker is saved and restored.|    ```
AliyunPasterRender.setOnPasterResumeAndSave(OnPasterResumeAndSave listener);
    ``` |

-   Static stickers

    |Action|Sample code|
    |------|-----------|
    |Add a static sticker.|    ```
AliyunIEditor.addImage(EffectPicture picture);
    ``` |
    |Remove a static sticker.|    ```
AliyunIEditor.removeImage(EffectPicture picture);
    ``` |

-   Watermarks

    |Action|Sample code|
    |------|-----------|
    |Add a watermark.|    ```
AliyunIEditor.applyWaterMark(String imgPath, float sizeX, float sizeY, float posX, float posY);
    ``` |
    |Add a watermark to the end of a video.|    ```
AliyunIEditor.addTailWaterMark(String imagePath, float sizeX, float sizeY, float posX, float posY, long durationUs);
    ``` |

-   Transitions

    |Action|Sample code|
    |------|-----------|
    |Set a transition when you import a video or an image.|    ```
AliyunVideoClip.setTransition(TransitionBase transition); // Sets a transition for a video.
AliyunImageClip.setTransition(TransitionBase transition); // Sets a transition for an image.
    ``` |
    |Update transition configuration. You can modify and update transition configuration when you update media clips.|    ```
AliyunEditor.setTransition(int index, TransitionBase transition); // Sets a transition. The index parameter indicates the transition position, which starts from 0.
AliyunEditor.setTransition(Map<Integer, TransitionBase> transitions); // Sets multiple transitions.
    ``` |

-   Frame animations

    |Action|Sample code|
    |------|-----------|
    |Add a frame animation.|    ```
AliyunEditor.addFrameAnimation(ActionBase action);
    ``` |
    |Remove a frame animation.|    ```
removeFrameAnimation(ActionBase action);
    ``` |

-   MV

    |Action|Sample code|
    |------|-----------|
    |Add an MV.|    ```
AliyunIEditor.applyMV(EffectBean effect);
    ``` |
    |Remove an MV.|    ```
AliyunIEditor.applyMV(null);// Removes the MV effect by setting the parameter to null.
    ``` |

-   Background music and multi-track dubbing

    |Action|Sample code|
    |------|-----------|
    |Add background music or dubbing. The background music is not affected by time effects, whereas the dubbing is.|    ```
AliyunIEditor.applyMusic(EffectBean effect);// Adds background music.
AliyunIEditor.applyDub(EffectBean effect);// Adds dubbing.
    ``` |
    |Remove background music or dubbing.|    ```
AliyunIEditor.removeMusic(EffectBean effect);// Removes background music.
AliyunIEditor.removeDub(EffectBean effect);// Removes dubbing.
    ``` |
    |Adjust the weight of the background music or dubbing when the background music or dubbing is mixed with the original audio.|    ```
AliyunIEditor.applyMusicMixWeight(int id, int weight);
    ``` |
    |Adjust the volume of the specified audio stream, such as the background music, dubbing, or original audio.|    ```
AliyunIEditor.applyMusicWeight(int id, int weight);
    ``` |
    |Denoise an audio stream. Perform this operation with caution because it consumes a large quantity of resources.|    ```
AliyunIEditor.denoise(int id, boolean needDenoise);
    ``` |

-   Sound effects

    The short video SDK allows you to add voice effects to each audio stream and provides various voice effects such as lolita, uncle, reverberation, and echo.

    |Action|Sample code|
    |------|-----------|
    |Set the voice effect of a single audio stream.|Voice effects can be overlaid. To switch to a new voice effect, you must remove the existing voice effect.

    -   id: the ID of the specified audio stream.
    -   type: the type of the voice effect.
    -   weight: the weight of the voice effect. Valid values: 0 to 100.
    ```
int audioEffect(int id, AudioEffectType type, int weight);
    ``` |
    |Delete a voice effect.|Voice effects can be overlaid. To switch to a new voice effect, you must remove the existing voice effect.

    ```
int removeAudioEffect(int id, AudioEffectType type);
    ``` |

-   Time effects

    |Action|Sample code|
    |------|-----------|
    |Adjust the playback speed.|    ```
AliyunIEditor.rate(float rate, long startTime, long duration, boolean needOriginDuration);
// By using the SDK V3.7.0 or later, you can call this method to adjust the playback speed for multiple videos or images.
    ``` |
    |Repeat the media clip.|    ```
AliyunIEditor.repeat(int times, long startTime, long duration, boolean needOriginDuration);
    ``` |
    |Reversely play a media clip.|    ```
AliyunIEditor.invert();
Videos whose GOP size is greater than 5 must be transcoded before reverse playback. You can call the NativeParser.getMaxGopSize() method to view the GOP size of a video. During transcoding, call the CropParam.setGop(1) method to set the GOP size to 1.
    ``` |
    |Remove the time effect.|    ```
AliyunIEditor.deleteTimeEffect(int id);
    ``` |

-   Doodles

    The short video SDK encapsulates a set of doodle methods, including those for configuring the canvas and paint brush. All doodling operations are performed by using the doodle controller AliyunICanvasController.

    Canvas: a UI interaction view for doodling. You can add the UI interaction view to the UI interaction view group.

    Paint brush: an android.graphics.Paint object. You can set a custom paint brush or use the default one.

    |Action|Sample code|
    |------|-----------|
    |Obtain the doodle controller AliyunICanvasController.|    ```
AliyunIEditor.obtainCanvasController(Context context, int w, int h);
    ``` |
    |Obtain the canvas.|    ```
AliyunICanvasController.getCanvas();
    ``` |
    |Check whether a doodle exists in the video.|    ```
AliyunICanvasController.hasCanvasPath();
    ``` |
    |Apply the doodle to the video.|    ```
AliyunICanvasController.applyPaintCanvas();
    ``` |
    |Remove the doodle that is applied to the video.|    ```
AliyunICanvasController.removeCanvas();
    ``` |
    |Undo the previous doodling operation.|    ```
AliyunICanvasController.undo();
    ``` |
    |Clear the canvas.|    ```
AliyunICanvasController.clear();
    ``` |
    |Set a color for the current paint brush.|    ```
AliyunICanvasController.setCurrentColor(int color);
    ``` |
    |Set a line width for the current paint brush.|    ```
AliyunICanvasController.setCurrentSize(float size);
    ``` |
    |Set a custom paint brush.|    ```
AliyunICanvasController.setPaint(Paint paint);
    ``` |
    |Reset the canvas.|    ```
AliyunICanvasController.resetPaintCanvas();
    ``` |
    |Undo all doodling operations.|    ```
AliyunICanvasController.cancel();
    ``` |
    |Confirm all doodling operations.|    ```
AliyunICanvasController.confirm();
    ``` |
    |Release resources.|    ```
AliyunICanvasController.release();
    ``` |

-   Others

    |Action|Sample code|
    |------|-----------|
    |Set the dynamic display mode.|    ```
AliyunIEditor.addRunningDisplayMode(VideoDisplayMode mode, int streamId, long startTimeMills, long durationMills);
    ``` |
    |Set a blur background. This effect is visible in padding mode.|    ```
AliyunIEditor.applyBlurBackground(int streamId, long startTimeMills, long durationMills, float blurRadius);
    ``` |


## Configure preview

|Action|Sample code|
|------|-----------|
|Replace the display window.|```
AliyunIEditor.setDisplayView(SurfaceView surfaceView);
AliyunIEditor.setDisplayView(TextureView textureView);// Unless otherwise specified, we recommend that you do not call this method.
``` |
|Start the playback.|```
AliyunIEditor.play();
``` |
|Seek|```
AliyunIEditor.seek();
``` |
|Forcibly draw a frame.|```
AliyunIEditor.draw();
``` |
|Pause the playback.|```
AliyunIEditor.pause();
``` |
|Resume the playback.|```
AliyunIEditor.resume();
``` |
|Stop the playback.|```
AliyunIEditor.stop();
``` |
|Obtain the current position in the stream, which is not affected by time effects.|```
AliyunIEditor.getCurrentStreamPosition();
``` |
|Obtain the current playback position, which is affected by time effects.|```
AliyunIEditor.getCurrentPlayPosition();
``` |
|Obtain the stream duration, which is not affected by time effects.|```
AliyunIEditor.getStreamDuration();
``` |
|Obtain the total playback duration, which is affected by time effects.|```
AliyunIEditor.getDuration();
``` |
|Specify whether to mute the audio.|```
AliyunIEditor.setAudioSilence(boolean silence);
``` |
|Set the volume.|```
AliyunIEditor.setVolume(int volume);
``` |
|Set the video display mode.|```
AliyunIEditor.setDisplayMode(VideoDisplayMode mode);
``` |
|Set the background filling color in padding mode.|```
AliyunIEditor.setFillBackgroundColor(int color);
``` |

## Produce a video

|Action|Sample code|
|------|-----------|
|Start the production.|```
AliyunIEditor.compose(AliyunVideoParam param, String outputPath, AliyunIComposeCallBack callback);
``` |
|Cancel the production.|```
AliyunIEditor.cancelCompose();
``` |

## Sample code

```
// Step 1: Import videos and images as media clips for editing and obtain the URI path that is required for initialization.
//first, import project
AliyunIImport mImport = AliyunImportCreator.getImportInstance(mContext);
mAliyunVideoParam = new AlivcEditInputParam.Builder().build().generateVideoParam();
mImport.setVideoParam(mAliyunVideoParam);
AliyunClip videoClip = new AliyunVideoClip.Builder()
    .source(mYourVideoPath).id(mYourVideoId).displayMode(AliyunDisplayMode.DEFAULT)
    .build();
mImport.addMediaClip(videoClip);
Uri mUri = Uri.parse(mImport.generateProjectConfigure());
mImport.release();

// Step 2: Create an editor instance.
mAliyunIEditor = AliyunEditorFactory.creatAliyunEditor(mUri, mYourEditorCallback);
int ret = mAliyunIEditor.init(mSurfaceView, mContext); //return 0 to success

// Step 3: Configure effects. For more information, see the "Configure effects" section of this topic.

// Step 4: Configure preview.
mAliyunIEditor.play(); // Start the playback.

// Step 5: Produce a video.
mAliyunIEditor.compose(mAliyunVideoParam, mYourOutputPath, mYourComposeCallback);
```

