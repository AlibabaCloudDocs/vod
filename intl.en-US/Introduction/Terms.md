# Terms

This topic describes the common terms that are used in ApsaraVideo VOD, such as format, encoding, and transcoding, to help you understand ApsaraVideo VOD.

## File format

Most file names in an operating system have a file name extension, such as .doc, .jpg, and .avi. File name extensions indicate the file formats, which are used to associate files with applications in the operating systems. This way, the files can be recognized and opened by the corresponding applications. Common file name extensions for videos include .avi, .mpg, and .mp4. Video files can be associated with and played by the video players that are installed on your computer.

## Container format

A container format, or multimedia container, describes the specifications for packaging compressed video and audio tracks and metadata to a file. Metadata summarizes basic information about videos, such as the titles and subtitles.

Container formats are classified into two types: storage-oriented formats and streaming media-oriented formats.

-   Common storage-oriented formats include AVI, ASF \(WMA or WMV\), MP4, MKV, and RMVB \(RM or RA\).
-   Common streaming media-oriented formats include FLV, TS \(which must be used with streaming media network transmission protocols, such as HLS and RTMP\), and MP4 \(which must be used with HTTP\). HLS is short for HTTP Live Streaming, and RTMP is short for Real-Time Messaging Protocol.

The following examples describe some key streaming media network transmission protocols and streaming media-oriented container formats:

-   MP4: a classic video container format that is supported by multiple terminals, including mobile devices \(iOS and Android\) and web browsers on PCs. However, the file header of an MP4 file is large and complex. If the duration of an MP4 file is long \(for example, lasting several hours\), the large file header decreases the video loading speed. Therefore, the MP4 format is more suitable for short videos.

    > An MP4 file consists of boxes \(formerly known as atoms\) that include all media description metadata, such as the media arrangement information and time information. The metadata provides references to media data such as video frames, and the arrangement of media data in the boxes is described in the metadata of the primary file. The longer the duration of a video, the larger the file header, and the slower the loading speed.

-   HLS: an HTTP-based streaming media network transmission protocol developed by Apple Inc. By default, this protocol uses the TS container format to divide a stream into multiple TS fragments. It also defines an M3U8 index file \(text file\) to control playback. Compared with the MP4 format, the TS format does not require a long time to buffer header data, and is applicable to ApsaraVideo VOD scenarios. HLS is supported on mobile devices \(iOS and Android\). However, it is incompatible with Internet Explorer on PCs. Therefore, HLS requires a custom player that is developed for PCs. We recommend that you use ApsaraVideo Player for web.
-   FLV: a standard introduced by Adobe. It is supported by Flash Player on PCs, but can be supported on mobile devices only after a player is implemented for the applications. Browsers on most mobile devices, iOS devices in particular, do not support FLV. We recommend that you use ApsaraVideo Player.
-   Dynamic Adaptive Streaming over HTTP \(DASH\): a standard using the fragmented MP4 \(fMP4\) format to divide an MP4 video into multiple fragments. Each fragment can have its own codec settings, such as resolution and bitrate. A player can play the required fragment to achieve adaptive bitrate streaming and seamless switching between different resolutions, providing a better playback experience. In DASH, the media presentation description \(MPD\) file provides features similar to those of the M3U8 file in HLS. Many video websites, such as YouTube and Netflix, use DASH to stream their content.
-   HLS with fragmented MP4 \(HLS + fMP4\): the HLS protocol in essence. During the Apple Worldwide Developers Conference \(WWDC\) 2016, Apple Inc. announced that the new HLS standard supports the fMP4 format in a similar way as the TS format. This means that a video file can be transcoded and packaged in DASH and HLS at the same time.

    > We recommend that you use HLS \(including HLS + fMP4\) and DASH because both are the most commonly used adaptive streaming media technologies.


## Codec

A codec is a program or device that can compress or decompress \(or decode\) digital videos. Generally, such compression is lossy compression. A codec also refers to a compression technology for converting a video from one format to another. The following examples describe common codecs:

1.  H.26X family: led by International Telecommunication Union \(ITU\). This family includes H.261, H.262, H.263, H.264, and H.265.

    -   H.261: used in earlier video conferences and video calls.
    -   H.263: used in video conferences, video calls, and online videos.
    -   H.264: also known as MPEG-4 Part 10, or MPEG-4 Advanced Video Coding \(MPEG-4 AVC\). It is a video compression standard and a format widely used for recording, compressing, and publishing high-precision videos.
    -   H.265: also known as High Efficiency Video Coding \(HEVC\). It is a video compression standard that is successor to H.264 or MPEG-4 AVC. Compared with H.264 or MPEG-4 AVC, HEVC improves video quality and achieves twice the compression ratio, which is a bitrate reduction by 50% at the same level of video quality. HEVC supports resolutions up to 8192 × 4320, including 8K ultra high definition \(UHD\), which is the current development trend.
2.  MPEG family: led by Moving Picture Experts Group \(MPEG\) affiliated with the International Organization for Standardization \(ISO\). This family includes the following video compression standards:

    -   MPEG-1 Part 2: used in VCD and some online videos. The video quality provided by this standard is similar to that of VHS.
    -   MPEG-2 Part 2: the equivalent of H.262 and used in DVD, SVCD, and most digital video broadcast systems and cable distribution systems.
    -   MPEG-4 Part 2: used in network transmission, broadcast, and media storage. This standard provides better compression performance than MPEG-2 and H.263 V1.
    -   MPEG-4 Part 10: the same technical content as H.264 of ITU-T. ITU-T and MPEG work together to develop the H.264 or MPEG-4 AVC standard. ITU-T named this standard H.264, while ISO and IEC named it MPEG-4 AVC.
3.  Audio Video Coding Standard \(AVS\): a series of digital audio and video coding standards formulated by a workgroup of China. It is a collection of source coding standards that are introduced in the Information Technology: Advanced Coding of Audio and Video. Two generations of AVS standards have been formulated.

    -   The first-generation AVS includes "Information Technology: Advanced Coding of Audio and Video, Part 2: Video" \(AVS1\) and "Information Technology: Advanced Coding of Audio and Video, Part 16: Radio Television Video" \(AVS+\). AVS+ provides the same compression efficiency as H.264 or MPEG-4 AVC High Profile.
    -   The second-generation AVS \(AVS2\) is designed for efficient compression of UHD \(4K or higher\) and high dynamic range \(HDR\) videos. The compression efficiency of AVS2 is twice that of AVS+ and H.264 or MPEG-4 AVC, and surpasses that of H.265 or HEVC.
4.  Other series: such as VP8, VP9 \(which is developed under the lead of Google\), and RealVideo \(which is introduced by RealNetworks\). These are rarely used in online videos and are not described in this topic.


> When you select a codec, you must consider its compatibility with terminals, such as mobile applications and web browsers. Whenever possible, use the most common and widely supported codecs. ApsaraVideo VOD supports the following video codecs: H.264 or MPEG-4 AVC \(default\), and H.265 or HEVC. ApsaraVideo VOD also supports the following audio codecs: MP3 \(default\), AAC, VORBIS, and FLAC.

## Transcoding

Video transcoding refers to the process of converting a coded video stream to another video stream to adapt to different network bandwidths, terminal processing capabilities, and user needs. Transcoding is essentially a process of decoding and encoding. Streams before and after transcoding may use the same or different video encoding standards.

## Container format conversion

Container format conversion refers to the process of converting an audio or video file from one container format to another, for example, from AVI to MP4. The compressed video and audio streams are obtained from the file in the original container format and then packaged into a file in the destination container format. No encoding or decoding is involved in this process. Compared with transcoding, container format conversion has the following features:

-   Fast processing. Decoding and encoding audio and video files is a complex process, and this occupies most of the transcoding time. Container format conversion does not require encoding or decoding, which reduces the processing time.
-   No loss of audio or video quality. Without the decoding \(decompression\) and encoding \(compression\) process, container format conversion has no impact on the original audio or video quality.

The new file is almost the same as the original file in terms of resolution and bitrate. Therefore, the new file is also called the original-quality file when it is played.

## Bitrate

Bitrate refers to the data traffic that video files use per unit of time. It is the most important item for image quality control in video encoding. The bitrate is measured in bits per second \(bit/s\), and often used in the units of Kbit/s and Mbit/s. The higher the bitrate of a video file with the same resolution, the smaller the compression ratio, and the higher the image quality. It is important to note that the higher the bitrate, the higher the sample rate per unit of time, the higher the data stream accuracy, the closer the processed file is to the original file, the better the image quality, the higher the video definition, and the higher the requirement on the decoding capability of the playback device.

> However, the higher the bitrate, the larger the file size. You can refer to this formula: File size = Time × Bitrate/8. For example, if a 60-minute 720p online video file has a bitrate of 1 Mbit/s, its size is about 450 MB \(3,600 seconds × 1 Mbit/s/8\).

## Resolution

Resolution refers to the capability to distinguish the details of a video. It is the number of pixels in each direction. For example, 1,280 × 720 refers to a width of 1,280 pixels and a height of 720 pixels. The resolution determines the image detail fineness of a video. A video with higher resolution contains more pixels and has clearer images.

> The resolution is a main factor that determines the bitrate. Videos with different resolutions use different bitrates. The higher the resolution of a video, the higher the required bitrate. However, this is not always the case. Each resolution corresponds to a proper range of bitrates. The so-called proper range means that if the bitrate is below the lower limit of this range, the resolution is low, and the video quality is poor. In contrast, if the bitrate is higher than the upper limit of this range, the network traffic and storage space are wasted, while the video quality improves a little or not at all.

## Frame rate

The frame rate is used to measure the number of video display frames per unit of time or the number of frames of images refreshed per second. The unit is frame per second \(FPS\) or Hz.

> A higher frame rate makes a video smoother and more lifelike. In general, 25 to 30 FPS is an acceptable range. A frame rate at 60 FPS makes the video significantly more immersive and lifelike. However, when the frame rate exceeds 75 FPS, the improvement in fluidity of motion is no longer noticeable. The use of a frame rate higher than the refresh rate of your display is a waste of graphics processing capability because the display is unable to refresh itself at that frame rate. Higher frame rates at the same resolution require greater processing capabilities from the graphics cards.

## GOP

A Group of Pictures \(GOP\) is a group of continuous images in an MPEG-encoded video or video stream. It starts with an I-frame and ends with the next I-frame. A GOP contains the following image types:

-   I-frame \(intra coded picture\): the keyframe. An I-frame contains all the information that is needed to produce the picture for that frame. It is independently decoded and can be regarded as a static picture. The first frame in the video sequence is always an I-frame, and each GOP starts with an I-frame.
-   P-frame \(predictive coded picture\): A P-frame must be encoded with reference to the preceding I-frame. A P-frame contains motion-compensated difference information relative to the previous frame, which may be an I-frame or a P-frame. During decoding, the difference defined by the current P-frame is superimposed with the previously cached image to generate the final image. P-frames occupy fewer data bits than I-frames. However, P-frames are sensitive to transmission errors because of their complex dependencies on the previous P and I reference frames.
-   B-frame \(bidirectionally predictive coded picture\): A B-frame contains motion-compensated difference information relative to the previous and subsequent frames. During decoding, the data of the current B-frame is superimposed with both the previously cached image and the decoded subsequent image to generate the final image. B-frames provide a high compression ratio, but require high decoding performance.

The GOP value indicates the interval of keyframes, which is the distance between two Instantaneous Decoding Refresh \(IDR\) frames or the maximum number of frames in a frame group. At least one keyframe is required for each second of video. The addition of more keyframes improves video quality, but results in increased bandwidth consumption and higher network load. The GOP value \(number of frames\) divided by the frame rate is the time interval. For example, the default GOP value of ApsaraVideo VOD is 250 frames and the frame rate is 25 FPS. Therefore, the time interval is 10 seconds.

The GOP value must be within a proper range to achieve a balance among the video quality, file size \(indicating the bandwidth consumption\), and seeking effect \(indicating the speed of response to the drag and fast-forward operations\).

-   Increasing the GOP value reduces the file size. However, if the GOP value is too large, the last frames of a GOP are distorted, thus reducing the video quality.
-   The GOP value is also a key factor in determining the speed of response to seeking in a video. During seeking, the player needs to locate the closest keyframe before the specified position. The larger the GOP value, the longer the distance between the specified position and the closest keyframe, and the more predictive frames need to be decoded. As a result, it takes a long buffering time to respond to seeking.
-   Encoding P-frames and B-frames is more complex than encoding I-frames. A large GOP value results in many P-frames and B-frames, which reduces the encoding efficiency.
-   However, if the GOP value is too small, the bitrate of the video must be increased to ensure that the image quality is not reduced. This process increases the bandwidth consumption.

## IDR frame alignment

An IDR frame is a special type of I-frame. P-frames and B-frames after a normal I-frame can reference other I-frames before this I-frame. However, no frame after an IDR frame can reference other frames before this IDR frame. For the purpose of controlling encoding and decoding, the first I-frame of a frame sequence is specified as an IDR frame.

An IDR frame tells the codec to immediately refresh the reference frame buffer. This way, errors in the frames before the IDR frame are not propagated to frames after the IDR frame. An IDR frame and the frames after it are coded as a new sequence. An IDR frame can also be used for random access, while a normal I-frame does not support this feature. A player often allows users to seek \(or to drag the progress slider\) to a random position. In this case, it is more convenient for the player to play from an IDR frame near the specified position. This avoids complicated reverse parsing because all frames after the IDR frame do not reference other I-frames before it.

When you transcode a video to multiple videos in different bitrates, you can enable IDR frame alignment. This way, the IDR frames of all output videos are accurately aligned in terms of the time and frame content. Then, a player can smoothly switch among the videos in different bitrates without obvious lags.

## Profile

A profile defines a set of capabilities that focus on a specific class of applications. H.264 includes the following three profiles:

-   Baseline Profile: uses I-frames and P-frames and supports only progressive videos and context-adaptive variable-length coding \(CAVLC\). This profile is used in low-cost applications or applications that require additional data loss robustness, for example, some video calls and mobile video applications.
-   Main Profile: uses I-frames, P-frames, and B-frames, and supports progressive and interlaced videos. It also supports CAVLC and context-adaptive binary arithmetic coding \(CABAC\). This profile is used in mainstream consumer electronic products, such as MP4 players, portable video players, PSPs, and iPods with relatively low decoding capabilities.
-   High Profile: supports 8 × 8 inter-prediction, custom quantization, lossless video coding, and more YUV formats \(such as 4:4:4\) as well as features of the main profile. It is used in broadcast and disc storage applications, particularly in high-definition television applications. For example, Blu-ray Disc storage format adopts this profile.

## Bit rate

The bit rate refers to the number of bits transmitted per second. The unit is bit per second \(bit/s\). The higher the bit rate, the larger amount of the data transmitted. In this video field, **the bit rate is equivalent to the bitrate**. The bit rate indicates the number of bits required for representing coded \(compressed\) audio or video data per second. The bit is the smallest binary unit, with a value of either 0 or 1. Similar to the bitrate, the higher the bit rate, the better the audio or video quality, but the larger the coded file. The smaller the bit rate, the smaller the file size.

## Bitrate control method

Bitrate control methods refer to the methods of controlling the bitrate of a coded stream. Here are the common bitrate control methods:

-   Variable bit rate \(VBR\): When this method is used, the bitrate is not fixed. When it is time to compress a video or audio file, the video or audio compression software determines the bitrate based on the complexity of the video or audio data. This method considers both the quality and the file size.

-   Constant bit rate \(CBR\): When this method is used, the bitrate is fixed throughout the coded stream. CBR-compressed files are larger in size than VBR- and ABR-compressed files, and do not have much improvement in quality.

-   Average bit rate \(ABR\): This method is a variation of VBR with interpolation parameters added. It is created by LAME to get rid of the poor size-quality ratio of CBR and the unpredictable file size of VBR. In a given file size, ABR divides a stream into parts in the unit of 50 frames \(at about 30 frames per second\), and uses relatively low bitrates to code the less complex segments and high bitrates to code the more complex parts. ABR can be regarded as a compromise between VBR and CBR.

    The bitrate can reach the specified value within a specific time range, but the peak bitrate in some parts can exceed the specified bitrate. The average bitrate is constant. ABR is a modified version of VBR. It ensures that the average output bitrate is within a proper range and codes videos within this range based on the complexity. By default, Alibaba Cloud uses ABR as the bitrate control method.


## Audio codecs

For more information, see the description of codecs in the preceding section. Audio codecs are classified into lossy codecs and lossless codecs. Based on the sampling theorem, an audio codec can generate only signals that are infinitely close to natural signals. Therefore, all audio codecs are lossy codecs. In the computer field, pulse-code modulation \(PCM\) is a conventional lossless codec because it achieves the highest fidelity among all the audio codecs. Common audio codecs on the Internet, such as MP3 and AAC, are all lossy codecs.

## Sample rate

The sample rate, or sample frequency, defines the number of samples that are extracted from continuous-time signals every second to form discrete-time signals. The unit is Hz. The sample rate refers to the number of samples per unit of time for an analog signal converted into a digital signal. The higher the sample rate, the more real and natural the sound.

## Bitrate

For more information, see the description of the bitrate in the video encoding terms.

## Sound channel

A sound channel refers to the independent audio signal that is collected or played when the sound is recorded or played in different spatial positions. The number of sound channels refers to the number of sound sources during recording or the number of speakers during playback.

## UTC \(ISO 8601 standard time format\)

Coordinated Universal Time \(UTC\) is also known as the world unified time, world standard time, and international coordinated time. The acronyms of the term in English \(CUT\) and in French \(TUC\) are different. The acronym UTC is used as a compromise. UTC is a time metering system based on atomic seconds, which is as close as possible to the universal time. Greater China adopts the standard of Data Elements and Inter Change Formats-Information Interchange-Representation of Dates and Times \(ISO 8601:1988 or GB/T 7408-1994\), and refers to UTC as international coordinated time.

By default, all time fields that are returned and time parameters in API requests in ApsaraVideo VOD are in the UTC format. The time format is YYYY-MM-DDThh:mm:ssZ in accordance with ISO 8601. For example, 2017-01-11T12:00:00Z indicates 20:00:00 on January 11, 2017 in UTC+8 \(China Standard Time\). The difference between China Standard Time and UTC is eight hours. Therefore, UTC+8 indicates China Standard Time.

