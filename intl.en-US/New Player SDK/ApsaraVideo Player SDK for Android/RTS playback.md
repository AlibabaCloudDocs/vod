# RTS playback

This topic shows you how to integrate Real Time Streaming \(RTS\) SDK into ApsaraVideo Player SDK for Android to play RTS media.

## Integrate RTS SDK

You can integrate RTS SDK into ApsaraVideo Player SDK for Android to play RTS media. For more information about how to integrate ApsaraVideo Player SDK for Android, see [Integration](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/Integration.md).

The following section describes how to integrate RTS SDK into ApsaraVideo Player SDK for Android.

1.  Add the RTS SDK dependency in your project.

    You can add the RTS SDK dependency by using the following methods:

    -   Download [RTS SDK](https://help.aliyun.com/document_detail/177373.html), add the required AAR packages that RTS SDK contains to the libs directory of your project, and then add the reference to the packages to the Gradle dependencies part.
    -   Add Maven dependencies. For more information, see [Integrate RTS SDKs for mobile clients](https://help.aliyun.com/document_detail/185582.html).
2.  Load low-latency SO libraries.

    Add the following code to load low-latency SO libraries for the activities of ApsaraVideo Player SDK for Android:

    ```
    static { System.loadLibrary("RtsSDK"); }
    ```

3.  Set the maximum buffer delay for RTS playback.

    ApsaraVideo Player SDK for Android provides the MaxDelayTime parameter of the PlayerConfig method to set the maximum buffer delay for RTS playback. We recommend that you use the following values of the parameters for RTS playback:

    ```
    // Query the configuration.
    PlayerConfig config = mAliyunVodPlayer.getConfig();
    // Set the maximum buffer delay to 1000.
    config.mMaxDelayTime = 1000;
    // Set the buffer period to 10 ms. The RTS protocol controls the buffer period.
    config.mHighBufferDuration = 10;
    config.mStartBufferDuration = 10;
    // Set other parameters.
    //....
    // Specify the settings for the player.
    mAliyunVodPlayer.setConfig(config);
    ```


