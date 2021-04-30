# Secure download

ApsaraVideo Player SDK allows you to download videos from ApsaraVideo VOD. This topic shows you how to securely download videos on Android and iOS terminals by using ApsaraVideo Player SDK and provides sample code.

## Overview

ApsaraVideo Player SDK allows you to download videos from ApsaraVideo VOD by using VidSts and VidAuth sources. In secure download mode, a downloaded video is saved as an encrypted video. The encrypted video can be played only on the application that is associated with the bundle ID or signature that is specified in the console when you download the encrypted file.

**Note:**

-   This mode protects video copyrights and can be used only by ApsaraVideo VOD users.
-   To use ApsaraVideo Player to cache a video encrypted by HTTP Live Streaming \(HLS\) Encryption on an on-premises device, you must enable the secure download feature in the ApsaraVideo VOD console.
-   Videos that are downloaded in secure download mode are encrypted. For more information, see [HLS Encryption](/intl.en-US/Developer Guide/Video security/HLS Encryption.md).
-   Videos that are encrypted by proprietary cryptography cannot be played in a web browser in iOS.

## Key implementation in Android

1.  Create and configure a download object.

    Use the AliDownloaderFactory class to create a download object. Sample code:

    ```
    AliMediaDownloader mAliDownloader = null;
    ......
    // Create a download object.
    mAliDownloader = AliDownloaderFactory.create(getApplicationContext());
    // Set the path for storing downloaded files.
    mAliDownloader.setSaveDir("The path of the folder for storing downloaded files");
    ```

    To download videos that are encrypted and transcoded by Alibaba Cloud, you must configure a security file encryptedApp.dat for encryption verification. For more information, see [How can I obtain a security file?](/intl.en-US/FAQ/Player/How can I obtain a security file?.md). Sample code:

    ```
     PrivateService.initService(getApplicationContext(), "The path of the encryptedApp.dat file");
    ```

2.  Set listeners.

    The download object provides multiple listeners. Sample code:

    ```
            mAliDownloader.setOnPreparedListener(new AliMediaDownloader.OnPreparedListener() {
                @Override
                public void onPrepared(MediaInfo mediaInfo) {
                    // Indicate that download tasks are prepared.
                }
            });
            mAliDownloader.setOnProgressListener(new AliMediaDownloader.OnProgressListener() {
                @Override
                public void onDownloadingProgress(int percent) {
                    // Specify the percentage of the download progress.
                }
                @Override
                public void onProcessingProgress(int percent) {
                   // Specify the percentage of the processing progress.
                }
            });
            mAliDownloader.setOnErrorListener(new AliMediaDownloader.OnErrorListener() {
                @Override
                public void onError(ErrorInfo errorInfo) {
                    // Indicate that a download error occurs.
                }
            });
            mAliDownloader.setOnCompletionListener(new AliMediaDownloader.OnCompletionListener() {
                @Override
                public void onCompletion() {
                    // Indicate that the download is successful.
                }
            });
    ```

    **Note:** The difference between callbacks for download progress and processing progress lies in that the callback for download progress requires online data before the download is complete. However, the callback for processing progress does not require online data.

3.  Prepare the download source.

    Call the prepare method to prepare the download source. VidSts and VidAuth sources are supported. In this example, a VidSts source is used. Sample code:

    ```
    // Create a VidSts object.
     VidSts aliyunVidSts = new VidSts();
     aliyunVidSts.setVid(Video ID);
     aliyunVidSts.setAccessKeyId(Temporary AccessKey ID);
     aliyunVidSts.setAccessKeySecret(Temporary AccessKey secret);
     aliyunVidSts.setSecurityToken(Security token);
     aliyunVidSts.setRegion(Access region);
    // Prepare the download source.
     mAliDownloader.prepare(aliyunVidSts)
    ```

4.  Select a download task.

    After the preparation, the OnPreparedListener callback is fired. Select a track for download. Sample code:

    ```
    public void onPrepared(MediaInfo mediaInfo) {
          // Indicate that download tasks are prepared.
          List<TrackInfo> trackInfos = mediaInfo.getTrackInfos();
         // Download the information about tracks, such as the first track.
          mAliDownloader.selectItem(trackInfos.get(0).getIndex());
    }
    ```

5.  Update the download source and start the download.

    After you perform the preceding steps, start the download. Sample code:

    ```
    // Update the download source.
      mAliDownloader.updateSource(mVidSts);
    // Start the download.
      mAliDownloader.start();
    ```

    **Note:** Update the download source information to ensure that the VidSts or VidAuth source is valid.

6.  Release the download object after the download succeeds or fails.

    After the download succeeds, call the release method to release the download object. The download object is released when the onCompletion or onError callback is fired. Sample code:

    ```
    mAliDownloader.stop();
    mAliDownloader.release();
    ```


## Key implementation in iOS

1.  Create and configure a download object.

    Create a download object. Sample code:

    ```
    AliMediaDownloader *downloader = [[AliMediaDownloader alloc] init];
    [downloader setSaveDirectory:self.downLoadPath];
    [downloader setDelegate:self];
    ```

    To download videos that are encrypted and transcoded by Alibaba Cloud, you must configure a security file encryptedApp.dat for encryption verification. For more information, see [How can I obtain a security file?](/intl.en-US/FAQ/Player/How can I obtain a security file?.md). Sample code:

    ```
    NSString *encrptyFilePath = [[NSBundle mainBundle] pathForResource:@"encryptedApp" ofType:@"dat"];
    [AliPrivateService initKey:encrptyFilePath];
    ```

2.  Set listeners.

    The download object provides multiple listeners. Sample code:

    ```
    -(void)onPrepared:(AliMediaDownloader *)downloader mediaInfo:(AVPMediaInfo *)info {
        // Indicate that download tasks are prepared.
    }
    -(void)onError:(AliMediaDownloader *)downloader errorModel:(AVPErrorModel *)errorModel {
        // Indicate that a download error occurs.
    }
    -(void)onDownloadingProgress:(AliMediaDownloader *)downloader percentage:(int)percent {
        // Specify the percentage of the download progress.
    }
    -(void)onProcessingProgress:(AliMediaDownloader *)downloader percentage:(int)percent {
        // Specify the percentage of the processing progress.
    }
    -(void)onCompletion:(AliMediaDownloader *)downloader {
        // Indicate that the download is successful.
    }
    ```

    **Note:** The difference between callbacks for download progress and processing progress lies in that the callback for download progress requires online data before the download is complete. However, the callback for processing progress does not require online data.

3.  Prepare the download source.

    Call the prepare method to prepare the download source. AVPVidStsSource and AVPVidAuthSource are supported. In this example, AVPVidStsSource is used. Sample code:

    ```
    // Create a VidSts object.
    AVPVidStsSource* stsSource = [[AVPVidStsSource alloc] init];
    stsSource.vid = source.vid;// The video ID.
    stsSource.region = DEFAULT_SERVER.region;// The access region.
    stsSource.securityToken = DEFAULT_SERVER.securityToken;// The security token.
    stsSource.accessKeySecret = DEFAULT_SERVER.accessKeySecret;// The temporary AccessKey secret.
    stsSource.accessKeyId = DEFAULT_SERVER.accessKeyId;// The temporary AccessKey ID.
    // Prepare the download source.
    [downloader prepareWithVid:stsSource];
    ```

4.  Prepare the download source.

    After the preparation, the onPrepared callback is fired. Select a track for download. Sample code:

    ```
    -(void)onPrepared:(AliMediaDownloader *)downloader mediaInfo:(AVPMediaInfo *)info {
        NSArray<AVPTrackInfo*>* tracks = info.tracks;
        // Download the information about tracks, such as the first track.
        [downloader selectTrack:[tracks objectAtIndex:0].trackIndex];
    }
    ```

5.  Update the download source and start the download.

    After you perform the preceding steps, start the download. Sample code:

    ```
    // Update the download source.
      [downloader updateWithVid:vidSource]
    // Start the download.
      [downloader start];
    ```

    **Note:** Update the download source information to ensure that the VidSts or VidAuth source is valid.

6.  Release the download object after the download succeeds or fails.

    After the download succeeds, call the release method to release the download object. The download object is released when the onCompletion or onError callback is fired. Sample code:

    ```
    [self.downloader destroy];
    self.downloader = nil;
    ```

    **Note:** To redownload a file, you must create a download object again.


