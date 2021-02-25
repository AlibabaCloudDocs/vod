# 使用JavaScript上传SDK

通过阅读本文，您可以了解JavaScript上传SDK的方式和基本流程。

## 操作步骤

1.  在页面上引入下面的JavaScript脚本，更多信息，请参见[SDK下载](/cn.zh-CN/SDK下载/SDK下载.md)。

    ```
    <!--  IE需要es6-promise -->
      <script src="../lib/es6-promise.min.js"></script>
      <script src="../lib/aliyun-oss-sdk6.10.0.min.js"></script>
      <script src="../aliyun-vod-upload-sdk1.5.2.min.js"></script>
    ```

2.  请求上传地址和凭证、STS。

    -   请求上传地址和凭证

        上传图片和上传视频获取上传地址和凭证所请求的API不同，如下所示：

        上传视频：客户端向AppServer发送请求，AppServer通过OpenAPI向阿里云视频点播服务发送`CreateUploadVideo`请求。请求成功将返回上传地址、上传凭证以及VideoId，AppServer将结果返回给客户端。

        上传图片：客户端向AppServer发送请求，AppServer通过OpenAPI向阿里云视频点播服务发送`CreateUploadImage`请求。请求成功将返回上传地址、上传凭证以及ImageURL，AppServer将结果返回给客户端。

    -   请求STS

        通过STS方式，客户端向AppServer发送请求，AppServer向阿里云STS服务请求临时STS凭证。请求成功将返回STS凭证，AppServer将结果返回给客户端。

3.  初始化上传实例。

    1.  声明`AliyunUpload.Vod`初始化回调。

        ```
        var uploader = new AliyunUpload.Vod({
               //阿里账号ID，必须有值
               userId:"122",
             //上传到视频点播的地域，默认值为'cn-shanghai'，//eu-central-1，ap-southeast-1
             region:"",
               //分片大小默认1 MB，不能小于100 KB
               partSize: 1048576,
             //并行上传分片个数，默认5
               parallel: 5,
             //网络原因失败时，重新上传次数，默认为3
             retryCount: 3,
             //网络原因失败时，重新上传间隔时间，默认为2秒
             retryDuration: 2,
              //开始上传
              'onUploadstarted': function (uploadInfo) {
              },
              //文件上传成功
              'onUploadSucceed': function (uploadInfo) {
              },
              //文件上传失败
              'onUploadFailed': function (uploadInfo, code, message) {
              },
              //文件上传进度，单位：字节
              'onUploadProgress': function (uploadInfo, totalSize, loadedPercent) {
              },
              //上传凭证或STS token超时
              'onUploadTokenExpired': function (uploadInfo) {
              },
            //全部文件上传结束
            'onUploadEnd':function(uploadInfo){
               }
          });
        ```

    2.  根据实际情况，选择初始化上传实例的方法。

        -   上传地址和凭证方式

            **说明：** 推荐使用上传地址和凭证方式进行初始化。

            请求获取的上传地址和凭证初始化时无需设置，在上传开始后触发的`onUploadStarted`回调中调用`setUploadAuthAndAddress(uploadFileInfo, uploadAuth, uploadAddress,videoId)`方法进行设置。

            当token超时，会触发`onUploadTokenExpired`回调，需要调用`resumeUploadWithAuth(uploadAuth)`方法，设置新的上传凭证继续上传。

            ```
            var uploader = new AliyunUpload.Vod({
                   //阿里账号ID，必须有值
                   userId:"122",
                   //分片大小默认1 MB，不能小于100 KB
                   partSize: 1048576,
                 //并行上传分片个数，默认5
                   parallel: 5,
                 //网络原因失败时，重新上传次数，默认为3
                 retryCount: 3,
                 //网络原因失败时，重新上传间隔时间，默认为2秒
                 retryDuration: 2,
                 //是否上报上传日志到视频点播，默认为true
                 enableUploadProgress: true,
                  //开始上传
                  'onUploadstarted': function (uploadInfo) {
                    log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                //上传方式1，需要根据uploadInfo.videoId是否有值，调用视频点播的不同接口获取uploadauth和uploadAddress，如果videoId有值，调用刷新视频上传凭证接口，否则调用创建视频上传凭证接口
                if (uploadInfo.videoId) {
                        //如果uploadInfo.videoId存在，调用刷新视频上传凭证接口
                     }
                 else{
                        //如果uploadInfo.videoId不存在，调用获取视频上传地址和凭证接口
                  //从视频点播服务获取的uploadAuth、uploadAddress和videoId，设置到SDK里
                     uploader.setUploadAuthAndAddress(uploadInfo, uploadAuth, uploadAddress,videoId);
                  },
                  //文件上传成功
                  'onUploadSucceed': function (uploadInfo) {
                    log("onUploadSucceed: " + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                  },
                  //文件上传失败
                  'onUploadFailed': function (uploadInfo, code, message) {
                    log("onUploadFailed: file:" + uploadInfo.file.name + ",code:" + code + ", message:" + message);
                  },
                  //文件上传进度，单位：字节
                  'onUploadProgress': function (uploadInfo, totalSize, loadedPercent) {
                      log("onUploadProgress:file:" + uploadInfo.file.name + ", fileSize:" + totalSize + ", percent:" + Math.ceil(loadedPercent * 100) + "%");
                  },
                  //上传凭证超时
                  'onUploadTokenExpired': function (uploadInfo) {
                      console.log("onUploadTokenExpired");
                  //实现时，根据uploadInfo.videoId调用刷新视频上传凭证接口重新获取UploadAuth
                  //从点播服务刷新的uploadAuth，设置到SDK里
            
                  uploader.resumeUploadWithAuth(uploadAuth);
                  },
                //全部文件上传结束
                'onUploadEnd':function(uploadInfo){
                       console.log("onUploadEnd: uploaded all the files");
                   }
            });
            ```

        -   STS方式

            请求获取的STS初始化时无需设置，而是在上传开始后触发的`onUploadStarted`回调中调用`setSTSToken(uploadInfo, accessKeyId, accessKeySecret, secretToken);`方法进行设置。

            当token超时，会触发`onUploadTokenExpired`回调，需要调用`resumeUploadWithSTSToken(accessKeyId, accessKeySecret, secretToken)`方法，设置新的STS继续上传。

            ```
            var uploader = new AliyunUpload.Vod({
                     //分片大小默认1 MB，不能小于100 KB
                   partSize: 1048576,
                 //并行上传分片个数，默认5
                   parallel: 5,
                 //网络原因失败时，重新上传次数，默认为3
                 retryCount: 3,
                 //网络原因失败时，重新上传间隔时间，默认为2秒
                 retryDuration: 2,
                 //是否上报上传日志到视频点播，默认为true
                 enableUploadProgress: true,
                  //开始上传
                  'onUploadstarted': function (uploadInfo) {
                    log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                  //获取STS Token，设置到SDK
                     uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret, secretToken);
                  },
                  //文件上传成功
                  'onUploadSucceed': function (uploadInfo) {
                    log("onUploadSucceed: " + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
                  },
                  //文件上传失败
                  'onUploadFailed': function (uploadInfo, code, message) {
                    log("onUploadFailed: file:" + uploadInfo.file.name + ",code:" + code + ", message:" + message);
                  },
                  //文件上传进度，单位：字节
                  'onUploadProgress': function (uploadInfo, totalSize, loadedPercent) {
                      log("onUploadProgress:file:" + uploadInfo.file.name + ", fileSize:" + totalSize + ", percent:" + Math.ceil(loadedPercent * 100) + "%");
                  },
                  //STS token超时
                  'onUploadTokenExpired': function (uploadInfo) {
                      console.log("onUploadTokenExpired");
                      //重新获取STS token，恢复上传
                  uploader.resumeUploadWithSTSToken(accessKeyId, accessKeySecret, secretToken);
                  },
                //全部文件上传结束
                'onUploadEnd':function(uploadInfo){
                       console.log("onUploadEnd: uploaded all the files");
                   }
              });
            ```

4.  列表管理。

    -   添加上传文件

        需要使用标准的input方式选择文件，文件大小不大于10 GB。

        ```
         <form action="">
           <input type="file" name="file" id="files" multiple/>
         </form>
         userData = '';
         document.getElementById("files")
          .addEventListener('change', function (event) {
            for(var i=0; i<event.target.files.length; i++) {
              //逻辑代码
            }
          });
        ```

        获取到用户选择的文件后，添加到上传列表中。

        ```
         uploader.addFile(event.target.files[i], null, null, null, paramData);
        ```

        STS方式上传时，可以选择是否启用水印和优先级，paramData是一个json对象字符串，第一级的Vod是必须的，Vod下面添加属性，paramData支持的属性请参见视频点播服务的接口[createUploadVideo](https://help.aliyun.com/document_detail/55407.html?spm=a2c4g.11186623.6.680.7dda6bd1kRRwXO)，接口示例如下：

        ```
         var paramData = '{"Vod":{"Title":"test","CateId":"234"}"}';
        ```

        **说明：** paramData只有在STS方式上传时需要在SDK指定， 如果是上传地址和凭证方式，则在获取上传凭证createUploadVideo接口的参数里指定，无需在SDK里指定paramData参数。

    -   删除上传文件

        index对应listFiles接口返回列表中元素的索引。

        ```
         uploader.deleteFile(index);
        ```

    -   取消单个文件上传

        ```
         uploader.cancelFile(index);
        ```

    -   恢复单个文件上传

        ```
         uploader.resumeFile(index);
        ```

    -   获取上传文件列表

        ```
         uploader.listFiles();
         var list = uploader.listFiles();
        for (var i=0; i<list.length; i++) {
            log("file:" + list[i].file.name + ", status:" +       list[i].state + ", endpoint:" + list[i].endpoint + ", bucket:" + list[i].bucket + ", object:" + list[i].object);
        }
        ```

    -   清理上传文件列表

        ```
         uploader.cleanList();
        ```

5.  上传控制。

    -   开始上传

        ```
          uploader.startUpload();
        ```

    -   停止上传

        ```
         uploader.stopUpload();
        ```

    -   上传凭证失效后恢复上传

        ```
         uploader.resumeUploadWithAuth(uploadAuth);
        ```

    -   设置上传地址和上传凭证

        设置上传地址和上传凭证方法在`onUploadstarted`回调里调用，此回调的参数包含`uploadInfo`的值。

        ```
         uploader.setUploadAuthAndAddress(uploadInfo,uploadAuth, uploadAddress, videoId);
        ```

    -   设置STS Token

        设置STS Token方法在`onUploadstarted`回调里调用，此回调的参数包含`uploadInfo`的值。

        ```
        uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret,secretToken);
        ```

    -   上传STS Token失效后恢复上传

        ```
        uploader.resumeUploadWithSTSToken(accessKeyId, accessKeySecret, secretToken, expireTime);
        ```


## 断点续传

在上传过程中，由于某种原因没有上传完成，下次选择同一个文件上传时， SDK会从上次完成的位置继续上传，并在`onUploadstarted`回调中获取上传凭证， 如果使用的是上传方式1（上传地址和凭证）上传时，用户需要根据回调返回的videoId的值，调用视频点播的不同接口。

```
onUploadstarted': function (uploadInfo) {
if (上传方式1) {
  if(!uploadInfo.videoId)//这个文件没有上传异常
  {
    //实际环境中调用调用视频点播的获取上传凭证接口
    uploader.setUploadAuthAndAddress(uploadInfo, uploadAuth, uploadAddress,videoId);
  }
  else//如果videoId有值，根据videoId刷新上传凭证
  {
    //实际环境中调用视频点播的刷新上传凭证接口，获取凭证
    uploader.setUploadAuthAndAddress(uploadInfo, uploadAuth, uploadAddress);
  }
}
else(上传方式2)
{
   //实际环境中调用获取STS接口，获取STS的值
   uploader.setSTSToken(uploadInfo, accessKeyId, accessKeySecret,secretToken);
}
}
```

获取断点信息

```
 uploader.getCheckpoint(file);
```

