# Windows播放器SDK

本文为您介绍了阿里云Windows播放器在不同更新时间对应的更新功能。

|**日期**|**版本**|**修改内容**|**历史版本**|
|------|------|--------|--------|
|2020-10-10|V5.2.1|-   修改Bug：Setview切换窗口后，窗口不显示播放的视频。
-   修改Bug：在播放过程中暂停播放，然后更改播放器尺寸，画面不会自动改变尺寸。
-   修改Bug：销毁播放器后再创建，在Prepare时崩溃。
-   修改Bug：暂停时，如果调节播放进度到其他位置，截图仍然显示暂停时的画面。
-   修改Bug: 音频设备打开失败，进度条没有正常显示。
-   添加Destroy Downloader和Player的静态方法。

|[Windows播放器SDK 5.2.1](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.2.1/ApsaraVideo_videoPlay_v5.2.1_Windows_20201010.zip)|
|2020-07-17|V5.2.0|Windows版本首次发布，主要功能如下所示：-   多种方式播放：URL播放、vid播放、本地视频播放。
-   播放控制：开始、暂停、恢复、停止、Seek和精确Seek。
-   播放器基本功能：切换多码率、自动播放、循环播放、画面旋转、填充模式、镜像操作、静音、音量控制（0~2.0）、倍数播放、边播边缓存、试看和截图。
-   视频下载功能：支持安全下载和普通下载。
-   设置播放器配置：设置Referer、设置UserAgent、配置网络重试时间和次数、配置缓存和延迟控制和HTTP Header设置。

|[Windows播放器SDK 5.2.0](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.2.0/ApsaraVideo_videoPlay_v5.2.0_Windows_20200717.zip)|

