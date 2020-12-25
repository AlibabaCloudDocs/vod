# Configure offline download

ApsaraVideo VOD provides the offline download feature for mobile clients. You can enable offline download based on your business requirements so that users can cache videos for offline playback.

**Note:** The offline download SDK is integrated into ApsaraVideo Player SDK. Therefore, to use the offline download feature, you must use ApsaraVideo Player SDK. For more information, see [ApsaraVideo Player SDK](/intl.en-US/New Player SDK/Overview.md).

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Download** to go to the Download page.

    ![Download page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4974888061/p183306.png)

4.  Turn on **Download** and select a download mode.

    Offline download is disabled by default.

    Two download modes are supported.

    -   Normal: Downloaded video files are not encrypted, can be copied, and can be played on any player. Proceed with caution.
    -   Encrypted: Downloaded video files are encrypted by using a key file and can be decrypted only by using the same key file. This ensures video security. You can use only ApsaraVideo Player SDK to decrypt and play the downloaded video files. In addition, a tool is provided for you to generate private keys for offline video encryption.
    ![Download mode](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4974888061/p183310.png)


## Generate the private key

If you select Encrypted for the Download Mode parameter, private keys are required to decrypt the downloaded videos.

A private key for offline video encryption is contained in a binary file. The system uses a private algorithm to generate a private key file based on the specified application unique identifier \(UID\) and a custom private key string for encryption. The private key string for encryption must be 16 to 32 characters in length, and can contain only and must contain uppercase letters, lowercase letters, and digits. You can download the private key file as needed. The downloaded private key file must be securely stored in client applications. This way, ApsaraVideo Player SDK can use the file for offline download and playback.

![Generate the private key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5974888061/p183341.png)

