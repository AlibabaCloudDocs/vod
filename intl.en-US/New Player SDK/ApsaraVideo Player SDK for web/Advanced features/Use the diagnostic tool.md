Use the diagnostic tool 
============================================

This topic describes how to open the diagnostic tool that is provided by ApsaraVideo Player and diagnose a video. 

Open the diagnostic tool 
---------------------------------------------

You can open the diagnostic tool that is provided by ApsaraVideo Player by using one of the following methods: 

* Click **Diagnosis** when a video fails to be played.![Error](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4942526261/p269989.png)

  

* Open the diagnostic tool by accessing the following URL: [Diagnostic tool](http://player.alicdn.com/detection.html).

  




Use the diagnostic tool 
--------------------------------------------

**View the diagnostic information** 

The diagnostic information includes the operating system, browser, IP address, and operator.![Basic diagnosis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5942526261/p271371.png)

**Configure the domain name for playback before video diagnosis** 

You need to configure the following items to obtain a more accurate diagnosis result: 

* If Referer-based hotlink protection is enabled for the domain name for playback, add `player.alicdn.com` to the whitelist. For more information, see [IP address blacklist or whitelist](/intl.en-US/User Guide/Domain management/Access control/IP address blacklist or whitelist.md).![Add the domain name for playback to the whitelist](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9601442261/p271381.png)

  

* Add the Access-Control-Allow-Origin HTTP header for the domain name for playback. This header specifies the domain name from which cross-origin requests are allowed. For more information, see [Configure CORS](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure CORS.md).

  






Diagnose a video

The diagnostic tool supports the following three playback modes. To start diagnostics, you need only to set the Source parameter to specify the streaming URL. Alternatively, you can set both the Vid and playAuth parameters if you do not have a streaming URL. 
**Note**

The Source parameter has the highest priority.

* Native HTML5 player

  

* ApsaraVideo Player in HTML5 mode

  

* ApsaraVideo Player in Flash mode

  




You can view the playback log after the diagnostics start. 

![Diagnose a video](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5942526261/p271399.png)



