Configure the player skin 
==============================================

You can configure the skin for ApsaraVideo Player in HTML5 mode and Flash mode. This topic describes how to configure the player skin. 

Configure the skin for the HTML5 player 
------------------------------------------------------------

**Reference the CSS file that defines the default layout.** 

    <link rel="stylesheet" href="//g.alicdn.com/de/prismplayer/{SDK version number}/skins/default/aliplayer.css" />



The CSS file contains skin materials: `http://gw.alicdn.com/tps/TB1YuE3KFXXXXaAXFXXXXXXXXXX-256-512.png`.

**Configure all internal components. The following table describes the components that you can configure.** 


|            Component             |                                      Description                                      |
|----------------------------------|---------------------------------------------------------------------------------------|
| prism-player                     | Player configuration                                                                  |
| prism-big-play-btn               | Large play button                                                                     |
| prism-play-btn                   | Play button                                                                           |
| prism-play-btn.playing           | Pause button that is used during playback                                             |
| prism-live-display               | Live streaming button that occupies the position of play button during live streaming |
| prism-fullscreen-btn             | Full screen button                                                                    |
| prism-fullscreen-btn.fullscreen  | Full screen button after it is clicked                                                |
| prism-volume                     | Volume button                                                                         |
| prism-volume.mute                | Volume button after the mute mode is enabled                                          |
| prism-cover                      | Thumbnail configuration before playback                                               |
| prism-controlbar                 | Control bar of the player                                                             |
| prism-time-display               | Total duration                                                                        |
| prism-time-display .current-time | Current time                                                                          |
| prism-progress                   | Progress bar                                                                          |
| prism-progress-loaded            | Loading progress                                                                      |
| m-progress-cursor                | Position of the progress bar                                                          |
| prism-speed-selector             | Playback speed                                                                        |
| prism-stream-selector            | Resolution switching                                                                  |
| prism-snapshot-btn               | Snapshot button                                                                       |
| prism-ErrorMessage               | Error message                                                                         |
| prism-info-display               | Additional information about an error                                                 |



**Configuration method** 

For more information, see the CSS file of the player: aliplayer-min.css.

The following sample code shows how to configure a large play button: 

    .prism-player .prism-big-play-btn {
      width: 90px;
      height: 90px;
      background: url("//gw.alicdn.com/tps/TB1YuE3KFXXXXaAXFXXXXXXXXXX-256-512.png") no-repeat -2px -2px;
    }



The following table describes the parameters in the sample code. 


| Parameter  |                                 Description                                 |
|------------|-----------------------------------------------------------------------------|
| width      | The width of the large play button. Unit: pixel.                            |
| height     | The height of the large play button. Unit: pixel.                           |
| background | The image URL of the large play button.                                     |
| no-repeat  | Specifies not to tile the image. CSS also supports the no-repeat parameter. |
| -2px       | The x and y coordinates of the large play button.                           |



Configure the skin for the Flash player 
------------------------------------------------------------

**Prepare default files to be used** 

    http://g.alicdn.com/de/prismplayer-flash/{SDK version number}/atlas/defaultSkin.xml
    http://g.alicdn.com/de/prismplayer-flash/{SDK version number}/atlas/defaultSkin.png



The `.png` file contains the materials that can be used as buttons on the skin. The `.xml` file specifies the locations of the buttons on the skin.
By default, the player searches for the defaultSkin.xml and defaultSkin.png files in the `http://g.alicdn.com/de/prismplayer-flash/{SDK version number}/atlas/` directory. 

**Configure components** 

Use the following code to reference the images to be used as components:

    <TextureAtlas imagePath="defaultSkin.png">



The following table describes the components that you can configure.


|     Component      |                                Description                                |
|--------------------|---------------------------------------------------------------------------|
| bigPlayDown        | Large play button after it is clicked                                     |
| bigPlayOver        | Large play button when the pointer is moved over it                       |
| bigPlayUp          | Large play button before it is clicked                                    |
| clarityBgDown      | Definition indicator after it is clicked                                  |
| clarityBgOver      | Definition indicator when the pointer is moved over it                    |
| clarityBgUp        | Definition indicator before it is clicked                                 |
| followDisabled     | Next button when it is disabled                                           |
| followDown         | Next button after it is clicked                                           |
| followOver         | Next button when the pointer is moved over it                             |
| followUp           | Next button before it is clicked                                          |
| fullScreenDisabled | Full screen button when it is disabled                                    |
| fullScreenDown     | Full screen button after it is clicked                                    |
| fullScreenOver     | Full screen button when the pointer is moved over it                      |
| fullScreenUp       | Full screen button before it is clicked                                   |
| liveicon           | Icon that indicates live streaming                                        |
| muteDown           | Mute button after it is clicked                                           |
| muteOver           | Mute button when the pointer is moved over it                             |
| muteUp             | Mute button before it is clicked                                          |
| normalScreenDown   | Button for exiting the full-screen mode after it is clicked               |
| normalScreenOver   | Button for exiting the full-screen mode when the pointer is moved over it |
| normalScreenUp     | Button for exiting the full-screen mode before it is clicked              |
| pauseDisabled      | Pause button when it is disabled                                          |
| pauseDown          | Pause button after it is clicked                                          |
| pauseOver          | Pause button when the pointer is moved over it                            |
| pauseUp            | Pause button before it is clicked                                         |
| playDisabled       | Play button when it is disabled                                           |
| playDown           | Play button after it is clicked                                           |
| playOver           | Play button when the pointer is moved over it                             |
| playUp             | Play button before it is clicked                                          |
| replayDown         | Replay button after it is clicked                                         |
| replayOver         | Replay button when the pointer is moved over it                           |
| replayUp           | Replay button before it is clicked                                        |
| setDown            | Setting button after it is clicked                                        |
| setOver            | Setting button when the pointer is moved over it                          |
| setUp              | Setting button before it is clicked                                       |
| volMaxDown         | High volume (≥ 50%) button after it is clicked                            |
| volMaxOver         | High volume (≥ 50%) button when the pointer is moved over it              |
| volMaxUp           | High volume (≥ 50%) button before it is clicked                           |
| volMinDown         | Low volume (\< 50%) button after it is clicked                            |
| volMinOver         | Low volume (\< 50%) when the pointer is moved over it                     |
| volMinUp           | Low volume (\< 50%) before it is clicked                                  |
| zoom100Down        | 100% scaling button in full-screen mode after it is clicked               |
| zoom100Over        | 100% scaling button in full-screen mode when the pointer is moved over it |
| zoom100Up          | 100% scaling button in full-screen mode before it is clicked              |
| zoom75Down         | 75% scaling button in full-screen mode after it is clicked                |
| zoom75Over         | 75% scaling button in full-screen mode when the pointer is moved over it  |
| zoom75Up           | 75% scaling button in full-screen mode before it is clicked               |
| zoom50Down         | 50% scaling button in full-screen mode after it is clicked                |
| zoom50Over         | 50% scaling button in full-screen mode when the pointer is moved over it  |
| zoom50Up           | 50% scaling button in full-screen mode before it is clicked               |



**Configuration method** 

Configure components based on the default skin settings. `Store the skin.png and skin.xml files in the http://[domain]/[path]/ directory. In addition, set the skinRes parameter to http://domain/path/skin for the player.` 

The following sample code shows how to configure a large play button: 

    <SubTexture name="bigPlayDown" x="2" y="94" width="90" height="90"/>
    <SubTexture name="bigPlayOver" x="94" y="2" width="90" height="90"/>
    <SubTexture name="bigPlayUp" x="2" y="2" width="90" height="90"/>



The following table describes the parameters in the sample code. 


| Parameter |                   Description                   |
|-----------|-------------------------------------------------|
| x         | The x coordinate of the component in the image. |
| y         | The y coordinate of the component in the image. |
| width     | The width of the component in the image.        |
| height    | The height of the component in the image.       |


