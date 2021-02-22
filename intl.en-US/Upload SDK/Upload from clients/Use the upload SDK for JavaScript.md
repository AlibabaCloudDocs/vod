# Use the upload SDK for JavaScript

This topic shows you how to install and use the upload SDK for JavaScript.

## Procedure

1.  Import the following JavaScript scripts to your web page. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

    ```
    <! -- The es6-promise file is required for Internet Explorer. -->
      <script src="../lib/es6-promise.min.js"></script>
      <script src="../lib/aliyun-oss-sdk6.10.0.min.js"></script>
      <script src="../aliyun-vod-upload-sdk1.5.2.min.js"></script>
    ```

2.  Request an upload URL and an upload credential or a Security Token Service \(STS\) token.

    -   Request an upload URL and an upload credential

        You must call different API operations to obtain the upload URLs and credentials for images and videos.

        Upload a video: The client sends an upload request to the AppServer. The AppServer calls the `CreateUploadVideo` operation to send a request to ApsaraVideo VOD. If the request succeeds, the AppServer receives the upload URL, upload credential, and the VideoId parameter, and returns them to the client.

        Upload an image: The client sends an upload request to the AppServer. The AppServer calls the `CreateUploadImage` operation to send a request to ApsaraVideo VOD. If the request succeeds, the AppServer receives the upload URL, upload credential, and the ImageURL parameter, and returns them to the client.

    -   Request an STS token

        The client sends an upload request to the AppServer. The AppServer sends a request to STS to obtain a temporary STS token. If the request succeeds, the AppServer receives the STS token and returns it to the client.

3.  Initialize an upload instance.

    1.  Declare an `AliyunUpload.Vod` initialization callback.

        ```
        var uploader = new AliyunUpload.Vod({
               // Required. The ID of your Alibaba Cloud account.
               userId:"122",
             // The ID of the region where the file is to be uploaded to ApsaraVideo VOD. Default value: cn-shanghai. //eu-central-1, ap-southeast-1
             region:"",
               // The size of each part in multipart upload. The default size is 1 MB. The size cannot be smaller than 100 KB.
               partSize: 1048576,
             // The maximum number of parts that can be uploaded in parallel. Default value: 5.
               parallel: 5,
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
              // This callback is fired when the upload credential or STS token expires.
              'onUploadTokenExpired': function (uploadInfo) {
              },
            // This callback is fired when all files are uploaded.
            'onUploadEnd':function(uploadInfo){
               }
          });
        ```

    2.  Select the method to initialize the upload instance as needed.

        -   Use the upload URL and credential

            **Note:** We recommend that you use the upload URL and credential to initialize the upload instance.

            You do not need to specify the obtained upload URL and credential during initialization. Instead, specify them in the SDK by calling the `setUploadAuthAndAddress(uploadFileInfo, uploadAuth, uploadAddress,videoId)` method in the `onUploadStarted` callback that is fired when the upload starts.

            When the upload credential expires, the `onUploadTokenExpired` callback is fired. Call the `resumeUploadWithAuth(uploadAuth)` method to resume the upload by using a new upload credential.

            ```
            var uploader = new AliyunUpload.Vod({
                   // Required. The ID of your Alibaba Cloud account.
                   userId:"122",
                   // The size of each part in multipart upload. The default size is 1 MB. The size cannot be smaller than 100 KB.
                   partSize: 1048576,
                 // The maximum number of parts that can be uploaded in parallel. Default value: 5.
                   parallel: 5,
                 // The maximum number of attempts to retry the upload upon a network exception. Default value: 3.
                 retryCount: 3,
                 // The intervals at which the system retries the upload upon a network exception. Default value: 2. Unit: seconds.
                 retryDuration: 2,
                 // Specify whether to report the upload logs to ApsaraVideo VOD. Default value: true.
                 enableUploadProgress: true,
                  // This callback is fired when the upload starts.
                  'onUploadstarted': function (uploadInfo) {
                    log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                // Use upload mode 1. In this mode, you must call different operations to obtain the values of the uploadAuth and uploadAddress parameters, depending on whether the uploadInfo.videoId parameter has a value.
                if (uploadInfo.videoId) {
                        // If the uploadInfo.videoId parameter has a value, call the RefreshUploadVideo operation.
                     }
                 else{
                        // If the uploadInfo.videoId parameter does not have a value, call the CreateUploadVideo operation.
                  // Specify the values of the uploadAuth, uploadAddress, and videoId parameters obtained from ApsaraVideo VOD in the SDK.
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
                  // During implementation, call the RefreshUploadVideo operation to obtain a new value of the uploadAuth parameter based on the uploadInfo.videoId parameter.
                  // Specify the new value of the uploadAuth parameter obtained from ApsaraVideo VOD in the SDK.
            
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
            var uploader = new AliyunUpload.Vod({
                     // The size of each part in multipart upload. The default size is 1 MB. The size cannot be smaller than 100 KB.
                   partSize: 1048576,
                 // The maximum number of parts that can be uploaded in parallel. Default value: 5.
                   parallel: 5,
                 // The maximum number of attempts to retry the upload upon a network exception. Default value: 3.
                 retryCount: 3,
                 // The intervals at which the system retries the upload upon a network exception. Default value: 2. Unit: seconds.
                 retryDuration: 2,
                 // Specify whether to report the upload logs to ApsaraVideo VOD. Default value: true.
                 enableUploadProgress: true,
                  // This callback is fired when the upload starts.
                  'onUploadstarted': function (uploadInfo) {
                    log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                  // Obtain the STS token and specify it in the SDK.
                     uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret, secretToken);
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
                  // This callback is fired when the STS token expires.
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

4.  Manage the upload list.

    -   Add a file to be uploaded

        Use the standard HTML input type to select a file. The size of the file to be uploaded cannot exceed 10 GB.

        ```
         <form action="">
           <input type="file" name="file" id="files" multiple/>
         </form>
         userData = '';
         document.getElementById("files")
          .addEventListener('change', function (event) {
            for(var i=0; i<event.target.files.length; i++) {
              // The logic code.
            }
          });
        ```

        Obtain the selected file and add it to the upload list.

        ```
         uploader.addFile(event.target.files[i], null, null, null, paramData);
        ```

        If you use STS tokens to upload media files, you can specify whether to enable the watermark and job priority features. The value of the paramData parameter is a JSON object in string format. In this JSON object, you must set the first Vod parameter, as shown in the following sample code. You can specify attributes in the Vod parameter. For more information about attributes supported by the paramData parameter, see [CreateUploadVideo](https://help.aliyun.com/document_detail/55407.html?spm=a2c4g.11186623.6.680.7dda6bd1kRRwXO).

        ```
         var paramData = '{"Vod":{"Title":"test","CateId":"234"}"}';
        ```

        **Note:** You must set the paramData parameter in the SDK only when you use the STS token to upload a file. If you use the upload URL and credential to upload a file, you can set the paramData parameter in the request of the CreateUploadVideo operation rather than the SDK.

    -   Remove a file to be uploaded

        The index parameter indicates the index of a file in the list returned by the listFiles\(\) method.

        ```
         uploader.deleteFile(index);
        ```

    -   Cancel the upload of a single file

        ```
         uploader.cancelFile(index);
        ```

    -   Resume the upload of a single file

        ```
         uploader.resumeFile(index);
        ```

    -   Query the upload list

        ```
         uploader.listFiles();
         var list = uploader.listFiles();
        for (var i=0; i<list.length; i++) {
            log("file:" + list[i].file.name + ", status:" +       list[i].state + ", endpoint:" + list[i].endpoint + ", bucket:" + list[i].bucket + ", object:" + list[i].object);
        }
        ```

    -   Clear the upload list

        ```
         uploader.cleanList();
        ```

5.  Control the upload.

    -   Start the upload

        ```
          uploader.startUpload();
        ```

    -   Stop the upload

        ```
         uploader.stopUpload();
        ```

    -   Resume the upload after the upload credential expires

        ```
         uploader.resumeUploadWithAuth(uploadAuth);
        ```

    -   Specify the upload URL and credential

        Specify the upload URL and credential in the `onUploadstarted` callback. The callback parameters include the `uploadInfo` parameter.

        ```
         uploader.setUploadAuthAndAddress(uploadInfo,uploadAuth, uploadAddress, videoId);
        ```

    -   Specify the STS token

        Specify the STS token in the `onUploadstarted` callback. The callback parameters include the `uploadInfo` parameter.

        ```
        uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret,secretToken);
        ```

    -   Resume the upload after the STS token expires

        ```
        uploader.resumeUploadWithSTSToken(accessKeyId, accessKeySecret, secretToken, expireTime);
        ```


## Resumable upload

If the upload of a file fails halfway due to a specific reason and you upload the file again later, the SDK resumes the upload from the last breakpoint. The SDK obtains the upload credential from the `onUploadstarted` callback. If you use upload mode 1, you must call different ApsaraVideo VOD API operations based on the value of the videoId parameter returned by the callback.

```
onUploadstarted': function (uploadInfo) {
if (Upload mode 1) {
  if(! uploadInfo.videoId)// No exception occurs when you upload the file.
  {
    // Call the CreateUploadVideo operation in your environment.
    uploader.setUploadAuthAndAddress(uploadInfo, uploadAuth, uploadAddress,videoId);
  }
  else// If the videoId parameter has a value, update the upload credential based on the value.
  {
    // Call the RefreshUploadVideo operation in your environment to update the upload credential.
    uploader.setUploadAuthAndAddress(uploadInfo, uploadAuth, uploadAddress);
  }
}
else(Upload mode 2)
{
   // Call the operation for obtaining the STS token in your environment.
   uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret,secretToken);
}
}
```

Obtain the breakpoint information

```
 uploader.getCheckpoint(file);
```

