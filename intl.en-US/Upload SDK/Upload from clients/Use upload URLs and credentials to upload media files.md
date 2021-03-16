# Use upload URLs and credentials to upload media files

This topic shows you how to use upload URLs and credentials to upload media files.

## Overview

Upload URLs and credentials are issued by ApsaraVideo VOD to authorize users to upload media files to Object Storage Service \(OSS\) buckets allocated by ApsaraVideo VOD. Using upload URLs and credentials to upload media files is more advantageous over using Security Token Service \(STS\). For more information, see [Comparison between credentials and STS](/intl.en-US/Developer Guide/Access authorization/Comparison between credentials and STS.md).

## Procedure

1.  Access ApsaraVideo VOD. We recommend that you use a RAM user to access ApsaraVideo VOD. You must attach the AliyunVODFullAccess policy to the RAM user. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).
2.  Deploy the authorization service on the AppServer and obtain an upload URL and an upload credential. We recommend that you use a server SDK to obtain the upload URL and credential. For more information, see [Upload URLs and credentials](/intl.en-US/Developer Guide/Upload Medias/Upload URLs and credentials.md).
3.  Before you upload media files from the client, obtain the upload URL and credential from the AppServer. For more information, see [Upload URLs and credentials](/intl.en-US/Developer Guide/Upload Medias/Upload URLs and credentials.md).
4.  Add an on-premises file on the client, specify the upload URL and credential, and then start the upload.

![client_upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6505785161/p183800.png)

## Specify the upload URL and credential

Each file requires an upload URL and an upload credential. Therefore, you must obtain the upload URL and credential from the AppServer in the onUploadStarted callback and specify them in the upload instance. The following section provides the sample code for different platforms:

-   Sample code for iOS

    ```
    //create VODUploadClient object
    self.uploader = [VODUploadClient new];
    //weakself
    __weak typeof(self) weakSelf = self;
    //setup callback
    OnUploadFinishedListener FinishCallbackFunc = ^(UploadFileInfo* fileInfo, VodUploadResult* result){
        NSLog(@"upload finished callback videoid:%@, imageurl:%@", result.videoId, result.imageUrl);
    };
    OnUploadFailedListener FailedCallbackFunc = ^(UploadFileInfo* fileInfo, NSString *code, NSString* message){
        NSLog(@"upload failed callback code = %@, error message = %@", code, message);
    };
    OnUploadProgressListener ProgressCallbackFunc = ^(UploadFileInfo* fileInfo, long uploadedSize, long totalSize) {
        NSLog(@"upload progress callback uploadedSize : %li, totalSize : %li", uploadedSize, totalSize);
    };
    OnUploadTokenExpiredListener TokenExpiredCallbackFunc = ^{
        NSLog(@"upload token expired callback.");
        // Specify a new upload credential to resume the upload upon credential expiration.
    };
    OnUploadRertyListener RetryCallbackFunc = ^{
        NSLog(@"upload retry begin callback.") ;
    };
    OnUploadRertyResumeListener RetryResumeCallbackFunc = ^{
        NSLog(@"upload retry end callback.") ;
    };
    OnUploadStartedListener UploadStartedCallbackFunc = ^(UploadFileInfo* fileInfo) {
        NSLog(@"upload upload started callback.") ;
        // Specify the upload URL and credential.
        [weakSelf.uploader setUploadAuthAndAddress:fileInfo uploadAuth:`upload auth` uploadAddress:`upload address`];
    };
    VODUploadListener *listener = [[VODUploadListener alloc] init];
    listener.finish = FinishCallbackFunc;
    listener.failure = FailedCallbackFunc;
    listener.progress = ProgressCallbackFunc;
    listener.expire = TokenExpiredCallbackFunc;
    listener.retry = RetryCallbackFunc;
    listener.retryResume = RetryResumeCallbackFunc;
    listener.started = UploadStartedCallbackFunc;
    // init with upload address and upload auth
    [self.uploader init:listener];
                        
    ```

-   Sample code for Android

    ```
    VODUploadClient uploader = new VODUploadClientImpl(getApplicationContext());
    VODUploadCallback callback = new VODUploadCallback() {
        public void onUploadSucceed(UploadFileInfo info) {
            // This callback is fired when the upload succeeds.
        }
        public void onUploadFailed(UploadFileInfo info, String code, String message) {
              // This callback is fired when the upload fails.
        }
        public void onUploadProgress(UploadFileInfo info, long uploadedSize, long totalSize) {
            // This callback is fired when the default or custom upload progress is reached.
        }
        public void onUploadTokenExpired() {
            // This callback is fired when the upload credential expires. The operation for updating the credential needs to be called.
        }
        public void onUploadRetry(String code, String message) {
            // This callback is fired when the system retries the upload.
        }
        public void onUploadRetryResume() {
        }
        public void onUploadStarted(UploadFileInfo uploadFileInfo) {
            OSSLog.logError("onUploadStarted ------------- ");
            // This callback is fired when the upload starts. Obtain the upload URL and credential from the AppServer in this callback.
            // Set the uploadAuth and uploadAddress parameters.
            uploader.setUploadAuthAndAddress(uploadFileInfo, uploadAuth, uploadAddress);
        }
    };
    uploader.init(callback);
    ```

-   Sample code for HTML5 and JavaScript

    ```
    var uploader = new AliyunUpload.Vod({
        partSize: 1048576,// The size of each part in multipart upload. The default size is 1 MB. The size cannot be smaller than 100 KB.
           parallel: 5,// The maximum number of parts that can be uploaded in parallel. Default value: 5.
        retryCount: 3,// The maximum number of attempts to retry the upload upon a network exception. Default value: 3.
        retryDuration: 2,// The intervals at which the system retries the upload upon a network exception. Default value: 2. Unit: seconds.
        'onUploadstarted': function (uploadInfo) {
              uploader.setUploadAuthAndAddress(
                  uploadInfo,
                uploadAuth,
                uploadAddress,
                videoId);
        }
        ... // Set other callbacks.
    });
    ```


## References

For more information about how to integrate SDKs, manage upload lists, and handle callbacks when the upload succeeds or the credential expires, see the documentation of upload SDKs for different platforms.

-   [Upload SDK for Android](/intl.en-US/Upload SDK/Upload from clients/Upload SDK for Android/Upload a file.md)
-   [Upload SDK for iOS](/intl.en-US/Upload SDK/Upload from clients/Upload SDK for iOS/Upload a file.md)
-   [Use the upload SDK for JavaScript](/intl.en-US/Upload SDK/Upload from clients/Use the upload SDK for JavaScript.md)

