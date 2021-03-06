常见问题FAQ 
============================



录制时会生成多少点播视频？ 
----------------------------------

在直播进行时，每到达一个录制周期，都会生成一个点播视频。同时，直播默认断流超过3分钟，会认为本次直播结束，也会生成一个点播视频。

如：录制周期设置为30分钟，直播进行了38分钟后断开，那么会在点播生成两个视频，一个30分钟，一个8分钟。

点播转码模板做什么用？ 
--------------------------------

每录制一个点播视频，点播服务可以自动对该视频进行转码处理，点播转码模板就是指定使用哪个转码配置来处理录制的视频。

如：模板包含标清+高清两路流，则每录制一个视频，自动将该视频转出指定两路流。
**注意**

转码模板需要提前在点播控制台进行创建。

可以设置不转码么？ 
------------------------------

使用点播的 **不转码** 模板作为转码模板即可，此时获取播放信息时使用的是原片播放。
**注意**

通常不建议。因为直播码率较高的情况下，卡顿会比较明显。如果使用此项，后续可以手动提交媒体处理任务进行转码。

自动合成是什么意思？ 
-------------------------------

由于每到达一个录制周期，点播会自动生成一个视频。

如：一次直播1个小时，录制周期设置为30分钟，则会生成2个视频。如果开启了自动合成，则在本次直播结束后，点播会自动将2个录制的视频进行合成，同时会将合成后的视频ID进行回调。即用户最后一共可以得到2+1=3个视频。

自动合成有什么用？ 
------------------------------

通常为了快速回看，用户可能会将录制周期设置较短。

如：设置成10分钟，那么每过10分钟，则会生成一个点播视频，即10分钟后就可以回看前10分钟的点播内容。同时，整个直播结束后，用户希望得到一个完整的视频，则开启自动合成，可以帮用户自动进行视频合成（用户也可以手动调用云剪辑接口来实现）。

只有一个视频，会合成吗？ 
---------------------------------

开启自动合成后，不管多少个视频，都会进行合成。

如：用户设置录制周期为30分钟，实际直播时间为20分钟，则会在点播生成一个20分钟的录制视频。同时，会合成一个20分钟的视频（原视频只有一个）。

合成是异步的吗？ 
-----------------------------

合成是异步的，需要一定的时间，可以捕捉响应的回调来判断合成状态，详情请参见[场景实践](/cn.zh-CN/开发指南/直播转点播/场景实践.md)。

合成转码模板ID是什么？ 
---------------------------------

是开启自动合成后进行转码的模板ID。和录制设置的转码模板类似，开启自动合成后，点播可以自动对合成后的视频进行转码。
**说明**

此模板ID可以与录制模板ID不同。

如：为了快速回看，录制时使用的转码模板中，只有一路标清输出，但是合成的转码模板中，可以包含高清、超清、2K等清晰度。即优先使用一个低码率用来回看视频，待直播结束后，再对完整视频进行多码率转码处理。

可以仅合成不转码吗？ 
-------------------------------

使用点播的 **不转码** 模板作为转码模板即可。

自动合成最多支持多少视频？ 
----------------------------------

目前自动合成最多支持40个视频。即如果录制周期设置为1小时，则最多支持40个小时的录制自动合成，超出会导致本次自动合成失败。

录制周期设置为多少合适？ 
---------------------------------

每到达一个录制周期，则会在点播生成一个视频。

如果不需要快速将前面的视频进行回看，可以使用默认推荐配置，即1小时。如果需要，视情况而定，通常不建议低于20分钟。
