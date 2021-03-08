# Use the upload SDK for mini programs to upload a file

This topic shows you how to use the upload SDK for mini programs to upload a file.

The following JavaScript code is added. For more information, see [Release notes of the upload SDK for mini programs](/intl.en-US/SDK Downloads/shortvideo-sdk-history/Release notes of the upload SDK for mini programs.md).

```
import VODUpload from 'aliyun-upload-sdk-1.0.0.min.js'
```

## Procedure

1.  Request an upload URL and an upload credential or a Security Token Service \(STS\) token.

    -   Request an upload URL and an upload credential

        You must call different API operations to obtain the upload URLs and credentials for images and videos.

        -   Upload a video: The client sends an upload request to the AppServer. The AppServer calls the `CreateUploadVideo` operation to send a request to ApsaraVideo VOD to obtain an upload URL and an upload credential. If the request succeeds, the AppServer receives the upload URL, upload credential, and the VideoId parameter, and returns them to the client.
        -   Upload an image: The client sends an upload request to the AppServer. The AppServer calls the `CreateUploadImage` operation to send a request to ApsaraVideo VOD to obtain an upload URL and an upload credential. If the request succeeds, the AppServer receives the upload URL, upload credential, and the ImageURL parameter, and returns them to the client.
    -   Request an STS token

        The client sends an upload request to the AppServer. The AppServer sends a request to STS to obtain a temporary STS token. If the request succeeds, the AppServer receives the STS token and returns it to the client.

        ![request_sts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2752815161/p183469.png)

2.  Initialize an upload instance.

    1.  Declare a `VODUpload` initialization callback.

        ```
        var uploader = new VODUpload({
               // Required. The ID of your Alibaba Cloud account.
               userId:"0",
               // The ID of the region where the files are to be uploaded. Default value: cn-shanghai. //eu-central-1, ap-southeast-1.
               region:"",
               // The maximum number of attempts to retry the upload upon a network exception. Default value: 3.
               retryCount: 3,
               // The intervals at which the system retries the upload upon a network exception. Default value: 2. Unit: seconds.
               retryDuration: 2,
              // This callback is fired when the upload starts.
              'onUploadstarted': function (uploadInfo) {
              },
              // This callback is fired when the upload succeeds.
              'onUploadSucceed': function (uploadInfo) {
              },
              // This callback is fired when the upload fails.
              'onUploadFailed': function (uploadInfo, code, message) {
              },
              // This callback is fired when the default or custom upload progress is reached. The progress is measured in bytes.
              'onUploadProgress': function (uploadInfo, totalSize, loadedPercent) {
              },
              // This callback is fired when the upload credential expires.
              'onUploadTokenExpired': function (uploadInfo) {
              },
              // This callback is fired when all files are uploaded.
              'onUploadEnd':function(uploadInfo){
               }
          });
        ```

    2.  Initialize the upload instance by using one of the following methods:

        -   Use the upload URL and credential

            **Note:** We recommend that you use the upload URL and credential to initialize the upload instance.

            You do not need to specify the obtained upload URL and credential during initialization. Instead, specify them in the SDK by calling the `setUploadAuthAndAddress(uploadFileInfo, uploadAuth, uploadAddress,videoId);` method in the `onUploadStarted` callback that is fired when the upload starts.

            When the upload credential expires, the `onUploadTokenExpired` callback is fired. Call the `resumeUploadWithAuth(uploadAuth)` method to resume the upload by using a new upload credential.

            ![upload_address_auth](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2752815161/p183475.png)

            ```
            var uploader = new VODUpload({
                   // Required. The ID of your Alibaba Cloud account.
                   userId:"0",
                   // The maximum number of attempts to retry the upload upon a network exception. Default value: 3.
                   retryCount: 3,
                   // The intervals at which the system retries the upload upon a network exception. Default value: 2. Unit: seconds.
                   retryDuration: 2,
                  // This callback is fired when the upload starts.
                  'onUploadstarted': function (uploadInfo) {
                    log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                    // Use upload mode 1. In this mode, you must call different operations to obtain the values of the uploadAuth and uploadAddress parameters, depending on whether the uploadInfo.videoId parameter has a value.
                    if (uploadInfo.videoId) {
                        // If the uploadInfo.videoId parameter has a value, call the RefreshUploadVideo operation.
                     }
                     else{
                        // If the uploadInfo.videoId parameter does not have a value, call the CreateUploadVideo operation.
                     }
                    // Set the values of the uploadAuth, uploadAddress, and videoId parameters obtained from ApsaraVideo VOD in the SDK.
                     uploader.setUploadAuthAndAddress(uploadInfo, uploadAuth, uploadAddress,videoId);
                  },
                  // This callback is fired when the upload succeeds.
                  'onUploadSucceed': function (uploadInfo) {
                    log("onUploadSucceed: " + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                  },
                  // This callback is fired when the upload fails.
                  'onUploadFailed': function (uploadInfo, code, message) {
                    log("onUploadFailed: file:" + uploadInfo.file.name + ",code:" + code + ", message:" + message);
                  },
                  // This callback is fired when the default or custom upload progress is reached. The progress is measured in bytes.
                  'onUploadProgress': function (uploadInfo, totalSize, loadedPercent) {
                      log("onUploadProgress:file:" + uploadInfo.file.name + ", fileSize:" + totalSize + ", percent:" + Math.ceil(loadedPercent * 100) + "%");
                  },
                  // This callback is fired when the upload credential expires.
                  'onUploadTokenExpired': function (uploadInfo) {
                      console.log("onUploadTokenExpired");
                      // During implementation, call the RefreshUploadVideo operation to obtain a new value of the UploadAuth parameter based on the uploadInfo.videoId parameter.
                      // Set the new value of the uploadAuth parameter obtained from ApsaraVideo VOD in the SDK.
                      uploader.resumeUploadWithAuth(uploadAuth);
                  },
                  // This callback is fired when all files are uploaded.
                  'onUploadEnd':function(uploadInfo){
                       console.log("onUploadEnd: uploaded all the files");
                   }
              });
            ```

        -   Use the STS token

            You do not need to specify the obtained STS token during initialization. Instead, specify it in the SDK by calling the `setSTSToken(uploadInfo, accessKeyId, accessKeySecret, secretToken);` method in the `onUploadStarted` callback that is fired when the upload starts.

            When the STS token expires, the `onUploadTokenExpired` callback is fired. Call the `resumeUploadWithSTSToken(accessKeyId, accessKeySecret, secretToken)` method to resume the upload by using a new STS token.

            ```
            var uploader = new VODUpload({
                   // The maximum number of attempts to retry the upload upon a network exception. Default value: 3.
                   retryCount: 3,
                   // The intervals at which the system retries the upload upon a network exception. Default value: 2. Unit: seconds.
                   retryDuration: 2,
                  // This callback is fired when the upload starts.
                  'onUploadstarted': function (uploadInfo) {
                    log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                    // Obtain the STS token and specify it in the SDK.
                     uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret, secretToken);
                  }
                  // This callback is fired when the upload succeeds.
                  'onUploadSucceed': function (uploadInfo) {
                    log("onUploadSucceed: " + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                  },
                  // This callback is fired when the upload fails.
                  'onUploadFailed': function (uploadInfo, code, message) {
                    log("onUploadFailed: file:" + uploadInfo.file.name + ",code:" + code + ", message:" + message);
                  },
                  // This callback is fired when the default or custom upload progress is reached. The progress is measured in bytes.
                  'onUploadProgress': function (uploadInfo, totalSize, loadedPercent) {
                      log("onUploadProgress:file:" + uploadInfo.file.name + ", fileSize:" + totalSize + ", percent:" + Math.ceil(loadedPercent * 100) + "%");
                  },
                  // This callback is fired when the upload credential expires.
                  'onUploadTokenExpired': function (uploadInfo) {
                      console.log("onUploadTokenExpired");
                      // Obtain a new STS token and uses it to resume the upload.
                      uploader.resumeUploadWithSTSToken(accessKeyId, accessKeySecret, secretToken);
                  },
                  // This callback is fired when all files are uploaded.
                  'onUploadEnd':function(uploadInfo){
                       console.log("onUploadEnd: uploaded all the files");
                   }
              });
            ```

3.  Manage the upload list.

    -   Add a file to be uploaded.

        Use wx.chooseImage or wx.chooseVideo to select a file. Obtain the selected file and add it to the upload list.

        ```
            wx.chooseVideo({
                success: function (res) {
                    var file = {url: res.tempFilePath, coverUrl: res.thumbTempFilePath};
                    var userData = '{"Vod":{}}';
                    uploader.addFile(file, null, null, null, userData)
                }
            })
        ```

        During upload, you can specify whether to enable the watermark and job priority features. The value of the userData parameter is a JSON object in string format. In this JSON object, you must set the first Vod parameter, as shown in the following sample code. You can specify attributes in the Vod parameter. For more information about the attributes supported by the userData parameter, see the [createUploadVideo](https://help.aliyun.com/document_detail/55407.html?spm=a2c4g.11186623.6.680.7dda6bd1kRRwXO) operation of ApsaraVideo VOD.

        ```
         var userData = '{"Vod":{"Title":"test","CateId":"234"}"}';
        ```

    -   Remove a file to be uploaded.

        The index parameter indicates the index of a file in the list returned by the listFiles method.

        ```
         uploader.deleteFile(index);
        ```

    -   Cancel the upload of a single file.

        ```
         uploader.cancelFile(index);
        ```

    -   Resume the upload of a single file.

        ```
         uploader.resumeFile(index);
        ```

    -   Query the upload list.

        ```
         uploader.listFiles();
        ```

    -   Clear the upload list.

        ```
         uploader.cleanList();
        ```

4.  Control the upload.

    -   Start the upload.

        ```
          uploader.startUpload();
        ```

    -   Stop the upload.

        ```
         uploader.stopUpload();
        ```

    -   Resume the upload after the upload credential expires.

        ```
         uploader.resumeUploadWithAuth(uploadAuth);
        ```

    -   Specify the upload URL and credential.

        Specify the upload URL and credential in the `onUploadstarted` callback. The callback parameters include the `uploadInfo` parameter.

        ```
         uploader.setUploadAuthAndAddress(uploadInfo,uploadAuth, uploadAddress, videoId);
        ```

    -   Specify the STS token.

        Specify the STS token in the `onUploadstarted` callback. The callback parameters include the `uploadInfo` parameter.

        ```
        uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret,secretToken);
        ```

    -   Resume the upload after the STS token expires

        ```
        uploader.resumeUploadWithSTSToken(accessKeyId, accessKeySecret, secretToken, expireTime);
        ```


