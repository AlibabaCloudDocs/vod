# RTS播放

您可以阅读本文，了解播放器集成RTS SDK播放RTS的操作步骤。

## 集成RTS SDK

目前播放器支持RTS SDK播放RTS，集成播放器步骤请参见[集成iOS播放器](/intl.zh-CN/播放器SDK/iOS播放器/集成文档.md)。

下面为您介绍集成RTS SDK播放RTS流的操作步骤：

1.  添加Framework到项目中

    添加framework有以下两种方式：

    -   下载[RTS SDK](/intl.zh-CN/低延时直播/SDK下载.md)，将RtsSDK.framework文件和和artcSource.framework 添加到General里的Embedded Binaries栏目。
    -   支持pod导入，动态将framework导入的方式。新增的artcSource.framework和RtsSDK.framework用以支持RTS。
2.  设置播放器最大缓冲延迟等

    播放器SDK通过AVPConfig提供了MaxDelayTime等参数设置播放直播流最大延迟缓存的接口。RTS场景下，建议的参数设置值如下：

    ```
    //先获取配置
    AVPConfig *config = [self.player getConfig];
    //设置最大延迟为1000，延迟控制交由RTS控制
    config.maxDelayTime = 1000;
    //设置播放器启播缓存为10ms，数据控制由RTS控制。
    config.highBufferDuration = 10;
    config.startBufferDuration = 10;
    //其他设置
    //...
    //设置配置给播放器
    [self.player setConfig:config];
    ```


