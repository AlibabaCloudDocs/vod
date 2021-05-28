Configure the playback delay 
=================================================

ApsaraVideo Player V2.1.0 and later allow you to configure the playback delay and the message that notifies users of the playback delay. This feature can be used to play videos during transcoding. 

Configuration method 
-----------------------------------------

The infoDisplay component is used to display the message that notifies users of the playback delay. 

To enable the playback delay, set the autoplay attribute of the infoDisplay component to true. 

* If you use the skinLayout attribute to customize the player skin, you need to enable the infoDisplay component in the skinLayout attribute. The following code shows how to enable the infoDisplay component when you configure the skinLayout attribute: 

      skinLayout:[
          ......
          {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
          {name: "infoDisplay", align: "cc"},
          ......
        ]

  

  For more information about the skinLayout attribute, see [Configure the skinLayout attribute]().
  

* The infoDisplay component provides two attributes for you to specify the playback delay and message. 

  * autoPlayDelay: the playback delay, in seconds.

    
  
  * autoPlayDelayDisplayText: the message that notifies users of the playback delay. Example: "Transcoding" or "Please wait".

    
  

  



