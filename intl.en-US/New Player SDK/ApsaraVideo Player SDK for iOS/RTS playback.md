# RTS playback

This topic shows you how to integrate Real-Time Streaming \(RTS\) SDK into ApsaraVideo Player SDK for iOS to play RTS media.

## Integrate RTS SDK

You can integrate RTS SDK into ApsaraVideo Player SDK for iOS to play RTS media. For more information about how to integrate ApsaraVideo Player SDK for iOS, see [Integration](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/Integration.md).

The following part describes how to integrate RTS SDK into ApsaraVideo Player SDK for iOS.

1.  Add frameworks to your project.

    You can add frameworks by using the following methods:

    -   Download [RTS SDK](/intl.en-US/Real-Time Streaming/SDK download.md). On the General tab, add the RtsSDK.framework and artcSource.framework files to the Embedded Binaries section.
    -   You can import frameworks by using CocoaPods statements. The newly added artcSource and RtsSDK frameworks are used for RTS playback.
2.  Set the maximum buffer delay for RTS playback.

    ApsaraVideo Player SDK for iOS provides the MaxDelayTime parameter of the AVPConfig method to set the maximum buffer delay for RTS playback. The following code provides recommended values of the parameters for RTS playback:

    ```
    // Obtain the configuration information.
    AVPConfig *config = [self.player getConfig];
    // Set the maximum buffer delay to 1000. The RTS protocol controls the delay.
    config.maxDelayTime = 1000;
    // Set the buffer period to 10 ms. The RTS protocol controls the buffer period. 
    config.highBufferDuration = 10;
    config.startBufferDuration = 10;
    // Set other parameters.
    //...
    // Configure the settings for the player.
    [self.player setConfig:config];
    ```


