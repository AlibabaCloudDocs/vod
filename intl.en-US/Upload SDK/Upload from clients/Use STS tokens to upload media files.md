# Use STS tokens to upload media files

This topic shows you how to use Security Token Service \(STS\) tokens to upload media files.

## Overview

STS provides a universal service for authenticating the access to Alibaba Cloud services. An SDK for uploading media files by using STS encapsulates all the upload logic. You only need to focus on the configurations for obtaining the STS token, updating the STS token when it expires, and setting the callback for upload completion. For more information, see [What is STS?](/intl.en-US/API Reference/API Reference (STS)/What is STS?.md).

## Procedure

1.  Grant permissions on ApsaraVideo VOD by using STS in the Resource Access Management \(RAM\) console and send a request for an STS token to the AppServer. For more information, see [Create a role and grant temporary access permissions to the role by using STS](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md).
2.  The AppServer sends a request for the STS token to RAM or STS.
3.  The AppServer obtains the STS token from STS. For more information about the sample code, see [Create a role and grant temporary access permissions to the role by using STS](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md).
4.  The AppServer returns the STS token to the client.
5.  Add an on-premises file on the client, specify the STS token, and then start the upload.

![sts_upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1679124161/p183822.png)

**Note:** The AppServer sends a request to RAM or STS to obtain the STS token from RAM or STS. If you want to improve efficiency and prevent failures due to throttling limits imposed by RAM or STS on requests, you must cache the STS token on the AppServer.

## Specify the STS token



Specify the STS token when you initialize the upload instance. The following section provides the sample code for different platforms:

-   Sample code for iOS

    ```
    [self.uploader
         init:`STS Key Id`
         accessKeySecret:`STS Key Secret`
         secretToken:STS Secret Token`
         expireTime:`STS Expire Time`
         listener:listener
    ];                 
    ```

-   Sample code for Android

    ```
    VODUploadClient uploader = new VODUploadClientImpl(getApplicationContext());
    uploader.init(accessKeyId,
                  accessKeySecret,
                  secretToken,
                  expireTime,
                  callback);
    ```

-   Sample code for HTML5 and JavaScript

    ```
    var uploader = new AliyunUpload.Vod({
        partSize: 1048576,// The size of each part in multipart upload. The default size is 1 MB. The size cannot be smaller than 100 KB.
           parallel: 5,// The maximum number of parts that can be uploaded in parallel. Default value: 5.
        retryCount: 3,// The maximum number of attempts to retry the upload upon a network exception. Default value: 3.
        retryDuration: 2,// The intervals at which the system retries the upload upon a network exception. Default value: 2. Unit: seconds.
        'onUploadstarted': function (uploadInfo) {
              uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret,secretToken);
        }
        ... // Set other callbacks.
    });
    ```


## References

For more information about how to manage upload lists and handle callbacks when the upload succeeds or the credential expires, see the documentation of upload SDKs for different platforms.

-   [Upload SDK for Android](/intl.en-US/Upload SDK/Upload from clients/Upload SDK for Android/Upload a file.md)
-   [Upload SDK for iOS](/intl.en-US/Upload SDK/Upload from clients/Upload SDK for iOS/Upload a file.md)
-   [Use the upload SDK for JavaScript](/intl.en-US/Upload SDK/Upload from clients/Use the upload SDK for JavaScript.md)

