Handle an error and resume live streaming 
==============================================================

This topic describes how to handle an error and resume live streaming after the error occurred in using ApsaraVideo Player for live streaming. 

Events 
---------------------------

When an error occurred during live streaming, ApsaraVideo Player provides the onM3u8Retry and liveStreamStop events. 

The events are triggered to display custom messages and switch the live stream 

* onM3u8Retry: If an error occurred during live streaming, ApsaraVideo Player tries to restore data for five times and trigger the onM3u8Retry event at the same time. You can subscribe to the onM3u8Retry event to customize a message that is displayed, such as "The streamer leaves for a while."

  

* liveStreamStop: If the player fails to restore data, the liveStreamStop event is triggered. You can subscribe to the liveStreamStop event to customize a message such as "The live streaming failed or finished.", or switch to another stream for playback.

  




Sample code 
--------------------------------

**onM3u8Retry** 

    player.on('onM3u8Retry',function(){
       console.log('The streamer leaves for a while. Please wait.');
     });



**liveStreamStop** 

* Display a message, indicating that the live streaming ends.

  




    player.on('liveStreamStop',function(){
       console.log('The live streaming failed or finished.');
     });



* Switch to another available stream

  




    player.on('liveStreamStop',function(){
       var newUrl = "New streaming URL";
       player.loadByUrl(newUrl);
     });


