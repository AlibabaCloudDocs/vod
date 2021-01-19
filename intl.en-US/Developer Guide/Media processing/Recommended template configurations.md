Recommended template configurations 
========================================================

This topic describes some recommended template configurations for media processing.

Transcoding templates 
------------------------------------------

**Video parameters** 

* Disable Video

  If you select this check box, the transcoded stream does not contain video information. You can select this check box to extract audio in scenarios such as a radio broadcast.
  

* Bitrate and Resolution

  * Bitrate refers to the data traffic that video files use per unit of time. It is the most important item for image quality control in video encoding. The bitrate is measured in bits per second (bit/s), and is often used in the units of Kbit/s and Mbit/s.

    The higher the bitrate of a video file with the same resolution, the smaller the compression ratio and the higher the image quality. The higher the bitrate, the higher the sample rate per unit of time, the higher the data stream accuracy, the closer the processed file is to the original file, the better the image quality, the higher the video definition, and the higher the requirement on the decoding capability of the playback device.
    
  
  * Resolution refers to the capability to distinguish details of a video. It is the number of pixels in each direction. For example, 1280 × 720 refers to a width of 1,280 pixels and a height of 720 pixels.

    The resolution determines the image detail fineness of a video. A video with a higher resolution contains more pixels and has clearer images. The resolution is a main factor that determines the bitrate. Videos with different resolutions use different bitrates.
    
  
  * The higher the resolution of a video, the higher the required bitrate. However, this is not always true. Each resolution corresponds to a proper range of bitrates. If the bitrate is below the lower limit of this range, the video quality is poor. However, if the bitrate is higher than the upper limit of this range, the network traffic and storage space are wasted, and the improvement to image quality is limited.

    
  
  * The following table lists the recommended bitrate and resolution for each definition.

    

    |      Definition       | Recommended bitrate | Recommended resolution |   Resolution range   |
    |-----------------------|---------------------|------------------------|----------------------|
    | Low Definition        | 400                 | 640×360                | 128×128\~640×360     |
    | Standard Definition   | 900                 | 960×540                | 641×361\~960×540     |
    | High Definition       | 1500                | 1280×720               | 961×541\~1280×720    |
    | Ultra High Definition | 3000                | 1920×1080              | 1281×721\~1920×1080  |
    | 2K                    | 3500                | 2560×1440              | 1920×1080\~2560×1440 |
    | 4K                    | 6000                | 2560×1440              | 2560×1440\~3840×2160 |

    
    **Note**

    
    * The width and height of the resolution are optional. If only the width is set, the height is automatically set based on the aspect ratio of the video mezzanine file. If neither the width nor the height is set, the width and height of the video mezzanine file are used.

      
    
    * The unit of the bitrate is Kbit/s.

      
    
    * The unit of the resolution (width × height) is pixel.

      
    

    
    
  

  

* Frame Rate

  The frame rate is used to measure the number of video display frames per unit of time or the number of frames of images refreshed per second. The unit is frame per second (fps) or Hz.

  A higher frame rate makes a video smoother and more lifelike. In general, 25 to 30 fps is an acceptable range. A frame rate at 60 fps makes the video significantly more immersive and lifelike. However, when the frame rate exceeds 75 fps, the improvement in fluidity of motion is no longer noticeable. The use of a frame rate higher than the refresh rate of your display is a waste of graphic processing capability because the display is unable to refresh itself at that frame rate. Higher frame rates at the same resolution require greater processing capabilities from the graphics cards.

  **In ApsaraVideo VOD, the recommended frame rate is 25 fps.**
  

* Maximum Keyframe Interval (the number of frames in a GOP)

  A Group of Pictures (GOP) is a group of continuous images in an MPEG-encoded video or video stream. It starts with an I-frame and ends with the next I-frame. A GOP contains the following image types:
  * I-frame (intra coded picture): the keyframe. An I-frame contains all the information needed to produce the picture for that frame. It is decoded independently of all other pictures. It can be regarded as a static picture. The first frame in the video sequence is always an I-frame, and each GOP starts with an I-frame.

    
  
  * P-frame (predictive coded picture): A P-frame must be encoded with reference to the preceding I-frame. A P-frame contains motion-compensated difference information relative to the previous frame, which may be an I-frame or a P-frame. During decoding, the difference defined by the current P-frame is superimposed with the previously cached image to generate the final image. P-frames occupy fewer data bits than I-frames. However, P-frames are sensitive to transmission errors because of their complex dependencies on the previous P and I reference frames.

    
  
  * B-frame (bidirectionally predictive coded picture): A B-frame contains motion-compensated difference information relative to the previous and subsequent frames. During decoding, the data of the current B-frame is superimposed with both the previously cached image and the decoded subsequent image to generate the final image. B-frames provide a high compression ratio, but require high decoding performance.

    
  

  

  The GOP value indicates the interval of keyframes, the distance between two Instantaneous Decoding Refresh (IDR) frames, or the maximum number of frames in a frame group. At least one keyframe is required for each second of video. The addition of more keyframes improves video quality, but results in increased bandwidth consumption and higher network load. The GOP value (number of frames) divided by the frame rate is the interval.

  **In ApsaraVideo VOD, the recommended GOP value is 250 frames and the recommended frame rate is 25 fps. Therefore, the recommended interval is 10 seconds.**
  




**Audio parameters:** 

* Disable Audio

  If you select this check box, the transcoded stream does not contain audio information. You can select this check box if you want to disable the audio in the video mezzanine file.
  

* Sample Rate

  The sample rate, or sample frequency, defines the number of samples that are extracted from continuous-time signals every second to form discrete-time signals. The unit is Hz. The sample rate refers to the number of samples per unit of time for an analog signal converted into a digital signal. The higher the sample rate, the more real and natural the sound.

  **In ApsaraVideo VOD, the recommended sample rate is 44,100 Hz.**
  

* Bitrate

  

  |  Sound quality   | Recommended bitrate |
  |------------------|---------------------|
  | Standard Quality | 128                 |
  | High Quality     | 320                 |

  
  **Note**

  The unit of the bitrate is Kbit/s. The audio bitrate can range from 8 to 1,000 Kbits/s.
  

* Audio Channels

  **In ApsaraVideo VOD, the recommended number of audio channels is 2.**
  




Snapshot template configuration 
----------------------------------------------------

* Normal snapshots

  Set parameters for normal snapshots based on your business requirements. For more information, see [Parameters for normal snapshots (SnapshotConfig)](/intl.en-US/API Reference/Appendix/Media processing parameters.md). If the width and height of snapshots must be the same as those of the video mezzanine file, we recommend that you do not set the Width and Height parameters.
  

* Sprite snapshots

  Set parameters for sprite snapshots based on your business requirements. For more information, see [Parameters for sprite snapshots (SpriteSnapshotConfig)](/intl.en-US/API Reference/Appendix/Media processing parameters.md). If you do not have special requirements for the KeepCellPic parameter, we recommend that you set its value to delete so that the original small image files used to generate the sprite snapshots are deleted.
  




Watermark configuration 
--------------------------------------------

* Image watermarks

  To ensure the display quality of image watermarks at different video resolutions, we recommend that you set the Width, Height, Dx, and Dy parameters based on image proportions. For more information, see [Parameters for image watermarks](/intl.en-US/API Reference/Appendix/Media processing parameters.md).
  

* Text watermarks

  For more information about the parameters of text watermarks, see [Parameters for text watermarks](/intl.en-US/API Reference/Appendix/Media processing parameters.md). Unless otherwise required, we recommend that you set parameters other than Content to the default values.
  



