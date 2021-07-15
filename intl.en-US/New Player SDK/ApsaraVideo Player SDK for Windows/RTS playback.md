# RTS playback

This topic shows you how to use ApsaraVideo Player SDK for Windows into which Real-Time Streaming \(RTS\) SDK is integrated to play RTS media.

## Integrate RTS SDK

The following part describes how to use ApsaraVideo Player SDK for Windows into which Real-Time Streaming \(RTS\) SDK is integrated to play RTS media.

1.  Integrate ApsaraVideo Player SDK for Windows.

    For more information, see [Integration](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Windows/Integration.md).

    **Note:** RTS SDK that contains the RtsSDK.dll and cicada\_plugin\_artcSource.dll files is built in ApsaraVideo Player SDK for Windows. You do not need to download RTS SDK and integrate it into ApsaraVideo Player SDK for Windows.

2.  Set the maximum buffer delay for RTS playback.

    ApsaraVideo Player SDK for Windows provides the MaxDelayTime parameter of the AVPConfig method to set the maximum buffer delay for RTS playback. We recommend that you use the following values of the parameters for RTS playback:

    ```
    // Obtain the configuration information.
    AVPConfig *pConfig = mPlayerPtr->getConfig();
    // Set the maximum buffer delay to 1000. The RTS protocol controls the delay.
    pConfig->maxDelayTime = 1000;
    // Set the buffer period to 10 ms. The RTS protocol controls the buffer period. 
    pConfig->highBufferDuration = 10;
    pConfig->startBufferDuration = 10;
    // Set other parameters.
    //...
    // Configure the settings for the player.
    mPlayerPtr->setConfig(pConfig);
    ```


