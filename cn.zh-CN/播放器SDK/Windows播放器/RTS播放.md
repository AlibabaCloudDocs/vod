# RTS播放

您可以阅读本文，了解播放器集成RTS SDK播放RTS的操作步骤。

## 集成RTS SDK

下面为您介绍集成RTS SDK播放RTS流的操作步骤：

1.  集成Windows播放器。

    集成Windows播放器，具体操作，请参见[集成Windows播放器](/cn.zh-CN/播放器SDK/Windows播放器/集成文档.md)。

    **说明：** Windows播放器SDK自带RTS SDK（RtsSDK.dll 、cicada\_plugin\_artcSource.dll），不需要额外下载配置。

2.  设置播放器最大缓冲延迟等。

    播放器SDK通过AVPConfig提供了MaxDelayTime等参数设置播放直播流最大延迟缓存的接口。RTS场景下，建议的参数设置值如下：

    ```
    //先获取配置
    AVPConfig *pConfig = mPlayerPtr->getConfig();
    //设置最大延迟为1000，延迟控制交由RTS控制
    pConfig->maxDelayTime = 1000;
    //设置播放器启播缓存为10ms，数据控制由RTS控制。
    pConfig->highBufferDuration = 10;
    pConfig->startBufferDuration = 10;
    //其他设置
    //...
    //设置配置给播放器
    mPlayerPtr->setConfig(pConfig);
    ```


