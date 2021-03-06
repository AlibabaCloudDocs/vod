# RTS播放

您可以阅读本文，了解播放器集成RTS SDK播放RTS的操作步骤。

## 集成RTS SDK

目前播放器支持RTS SDK播放RTS，集成播放器步骤请参见[集成Android播放器](/cn.zh-CN/播放器SDK/Android播放器/集成文档.md)。

下面为您介绍集成RTS SDK播放RTS流的操作步骤：

1.  在项目中添加RTS SDK依赖

    添加RTS SDK依赖有以下两种方式：

    -   下载[RTS SDK](/cn.zh-CN/低延时直播/SDK下载.md)，将RTS SDK的aar文件添加到项目的libs目录下，添加到gradle依赖中即可。
    -   支持Maven依赖，具体操作，请参见[集成移动端](/cn.zh-CN/低延时直播/移动端集成/移动端集成说明.md)。
2.  Load低延迟so库

    在使用播放器的Activity内加入，示例如下：

    ```
    static { System.loadLibrary("RtsSDK"); }
    ```

3.  设置播放器最大缓冲延迟等

    播放器SDK通过PlayerConfig提供了MaxDelayTime等设置播放直播流最大延迟缓存的接口。RTS场景下，建议的参数设置值如下：

    ```
    //先获取配置
    PlayerConfig config = mAliyunVodPlayer.getConfig();
    //设置播放器最大缓存为1000
    config.mMaxDelayTime = 1000;
    //设置播放器启播缓存为10ms，数据控制由RTS控制。
    config.mHighBufferDuration = 10;
    config.mStartBufferDuration = 10;
    //其他设置
    //....
    //设置配置给播放器
    mAliyunVodPlayer.setConfig(config);
    ```


