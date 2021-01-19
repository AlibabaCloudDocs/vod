FAQ about media processing 
===============================================



**How do I upload videos without transcoding them?** 
-------------------------------------------------------------------------

You can upload your videos by using the No Transcoding template, which is a special transcoding template supported by ApsaraVideo VOD. If this template is used, ApsaraVideo VOD writes file information to video stream information instead of transcoding the uploaded videos. When you call the GetPlayInfo operation to query playback information, the URLs of the video mezzanine files are returned as playback URLs. This template is often used in scenarios where quick playback is required, such as short video and live-to-VOD scenarios.

How do I configure a video to automatically scale in proportion to its original aspect ratio? 
------------------------------------------------------------------------------------------------------------------

Specify only one of the Width and Height parameters when you configure transcoding templates. The other parameter is automatically set based on the aspect ratio of the input video.

How do I extract the audio track of a video when the video is transcoded? 
----------------------------------------------------------------------------------------------

* Method 1: Add another transcoding template, set Encapsulation Format to mp4 or hls, and then select Disable Video.

  

* Method 2: Add another transcoding template and set Encapsulation Format to mp3.

  




When do I use conditional transcoding? 
-----------------------------------------------------------

Use conditional transcoding when you want to generate streams in higher definitions. For example, if you set the definition to 4K but the resolution of the video mezzanine file is lower than 4K, you can perform one of the following operations: 

* Do not transcode videos of the specified specifications.

  

* Transcode the video and keep the bitrate or resolution of the transcoded stream the same as that of the video mezzanine file.

  



