# Media management and production

You can manage and edit the videos that you upload to ApsaraVideo VOD.

## Media asset management

**Media asset storage**: ApsaraVideo VOD stores multiple copies of data, provides remote disaster recovery and resource isolation, and ensures 99.999999999% \(eleven 9s\) data reliability. It allows you to store and access your data in any application, at any time, from anywhere.

**Media asset management**: You can manage your media assets in the ApsaraVideo VOD console or by calling API operations. For example, you can obtain, update, and search for media asset information, or download or delete media files.

**Video copyright protection**: ApsaraVideo VOD provides the media fingerprint service to uniquely identify a video. The media fingerprint service allows you to extract and compare fingerprint features of images and audio in videos. It helps you find duplicate videos, trace the source of video clips, and identify user-generated contents \(UGCs\).

**Automated review**: ApsaraVideo VOD provides media review features, including automated review, manual review, and security review configuration. Automated review of media resources including videos, audio, images, and text can mitigate the risks of non-compliant content such as pornography and terrorism, and reduce labor costs for video review.

## Media processing

**Audio and video transcoding**: ApsaraVideo VOD allows you to convert an audio or video stream to one or more streams to adapt to different network bandwidths, terminal processing capabilities, and user needs.

**Video snapshot**: You can take video snapshots at specific points in time in a video to generate image files.

**Frame animation**: You can use the frame animation feature to transform a specific part of a video into an animation file.

**Video watermarking**: During video transcoding, you can add images or text to video streams as watermarks and generate new video files that have the watermarks.

**Workflows**: Workflows are designed to streamline and instantiate media processing features. You can customize workflows in advance for one-stop video processing instead of repeatedly calling API operations.

**Adaptive bitrate streaming**: ApsaraVideo VOD transcodes a video into video streams at different bitrates and packages these video streams into a single file. This way, media players can switch to the most appropriate video stream based on the network bandwidth.

## Intelligent production

**Online editing**: The online editing service is the production center of ApsaraVideo VOD. This service supports features that enable you to cut and merge videos, mix audio, add subtitles, overlay images, mask videos, and apply transition effects.

-   Cutting and merging: Merge multiple videos, cut a video with the starting part, ending part, or middle part retained, and merge any part from multiple videos.
-   Audio processing: Implement various audio processing scenarios, such as audio mixing, audio extraction, volume adjustment, and dubbing.
-   Image overlay: Overlay an image on one or more videos from the start time to the end time of each video or in a specified time interval.
-   Text overlay: Overlay text on a video from the start time to the end time of the video or in a specified time interval.

**Media fingerprint**: The media fingerprint service allows you to extract and compare fingerprint features of images and audio in videos. It helps you find duplicate videos, trace the source of video clips, and identify UGCs.

**Smart tag**: The smart tag service automatically generates multi-dimensional content tags by analyzing visual information, text, voice, and behavior in videos and using multimodal information fusion and alignment technology to achieve high accuracy in content recognition. This way, the smart tag service converts unstructured information to structured information.

**Intelligent thumbnail**: The intelligent thumbnail service can analyze and understand video content to extract five snapshots that best represent the video content as alternative thumbnails. This service can also extract snapshots from keyframes of the video content and automatically merge them into a GIF file to serve as the animation thumbnail.

## Video encryption

**Proprietary cryptography**: The proprietary cryptography service converts video files to an encrypted HTTP Live Streaming \(HLS\) format, which can be decrypted and played by ApsaraVideo Player. This way, this service ensures video security on mobile devices and Flash players. This service is appropriate for scenarios such as online education and subscription-based viewing, which require high-level security.

**HLS Encryption**: Video content is encrypted based on the HLS AES-128 standard. The encrypted video can be played by any player that supports HLS streams, which ensures video security on mobile devices. This service offers high-level security and excellent terminal compatibility.

**Commercial digital rights management \(DRM\)**: Many platforms such as Microsoft PlayReady, Apple FairPlay, and Google Widevine provide native support for commercial DRM. Commercial DRM provides high security and meets the requirements of large, copyrighted content providers.

