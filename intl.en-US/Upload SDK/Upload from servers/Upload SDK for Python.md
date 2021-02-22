# Upload SDK for Python

You can use the upload SDKs of ApsaraVideo VOD to upload media files with efficiency. This topic provides an example to describe how to use the upload SDK for Python.

## Features

The upload SDK provides the following major features:

-   Allows you to upload various types of media files to ApsaraVideo VOD, including video and audio files, images, and auxiliary media assets such as watermarks and subtitle files.
-   Allows you to upload on-premises media files: By default, multipart upload is used. A single file to upload can be up to 48.8 TB in size. Resumable upload is supported.
-   Allows you to upload online media files to ApsaraVideo VOD: A single file to upload can be up to 48.8 TB in size. Online media files are downloaded to on-premises temporary directories and then uploaded to ApsaraVideo VOD. Resumable upload is not supported.
-   Allows you to upload M3U8 video files: ApsaraVideo VOD provides an operation to parse the M3U8 index files to obtain the lists of part URLs. You can also specify the URLs of part files as needed.

The upload SDK provides the following additional features:

-   Provides an upload progress bar and supports the callbacks for default and custom upload progress.
-   Allows you to specify the region of an Elastic Compute Service \(ECS\) instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the specified file is automatically uploaded by using an internal network. This can accelerate the upload speed and save the public network traffic.
-   Allows you to specify the VOD center and storage region to facilitate upload outside China. The default VOD center is in the China \(Shanghai\) region.
-   Allows you to set the metadata, such as the title, storage locations, user data, and transcoding templates for the upload.

For more information about the file formats that are supported by ApsaraVideo VOD, see the "Supported file formats" section of [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

## Prerequisites

-   Python 2.7 or later is installed. For more information, visit the [Python official website](https://www.python.org/).
-   pip is installed. For more information, see [Installation](https://pip.pypa.io/en/stable/installing).

## Install the SDK

1.  Run the following commands to install dependencies:

    pip install aliyun-python-sdk-core

    pip install aliyun-python-sdk-vod

    pip install oss2

    **Note:** If you are using Python 3.x, replace pip install aliyun-python-sdk-core with pip install aliyun-python-sdk-core-v3. If you have installed different versions, you can run the pip3 command.

2.  Download the VodUploadSDK-Python\_1.3.1.zip package, which contains the upload SDK for Python and sample code. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

    **Note:** In this topic, the SDK V1.3.1 is used as an example. You can use other versions based on your business requirements.

3.  Decompress the VodUploadSDK-Python\_1.3.1.zip package and copy voduploadsdk in the VodUploadSDK-Python\_1.3.1 directory to your on-premises installation directory.


## Update the SDK

If new operations or new features of existing operations are unavailable in the current SDK, update the SDK to the latest version.

1.  Run the following commands to install dependencies:

    pip install --upgrade aliyun-python-sdk-vod

    pip install --upgrade oss2

2.  Download the latest version of the upload SDK for Python. Extract files and save them by replacing existing ones. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

    **Note:** You can check the version number and release date of the current SDK in the first line of the ChangeLog.txt file in the voduploadsdk directory.


## Description of directories

-   voduploadsdk directory
    -   AliyunVodUtils.py
        -   AliyunVodLog: the log class of the upload SDK. It is implemented based on logging.
        -   AliyunVodUtils: the utility class of the upload SDK.
        -   AliyunVodException: the exception class of the upload SDK. It supports unified exception handling. You only need to detect AliyunVodException exceptions for external calls.
    -   UploadVideoRequest.py

        UploadVideoRequest: the request class for uploading videos. For more information about the parameters, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md).

    -   UploadImageRequest.py

        UploadImageRequest: the request class for uploading images. For more information about the parameters, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md).

    -   UploadAttachedMediaRequest.py

        UploadAttachedMediaRequest: the request class for uploading auxiliary media assets. For more information about the parameters, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).

    -   AliyunVodUploader.py includes methods of the AliyunVodUploader class.
        -   uploadLocalVideo: a method used to upload on-premises videos.
        -   uploadWebVideo: a method used to upload online videos.
        -   uploadLocalM3u8: a method used to upload on-premises M3U8 videos.
        -   uploadWebM3u8: a method used to upload online M3U8 videos.
        -   uploadImage: a method used to upload on-premises or online images.
        -   uploadAttachedMedia: a method used to upload on-premises or online auxiliary media assets.
        -   parseWebM3u8: a method used to parse the part information of online M3U8 videos.
        -   parseLocalM3u8: a method used to parse the part information of on-premises M3U8 videos.
        -   setApiRegion: a method used to specify the access region of the ApsaraVideo VOD API. The default region is the China \(Shanghai\) region. You can also specify a region outside China, such as the Singapore \(Singapore\) region. For more information, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md).
        -   setMultipartUpload: a method used to set the threshold of the file size based on which multipart upload starts and the size of each part in multipart upload.
        -   uploadProgressCallback: a method used to set the callback for upload progress. This method can be overridden.
        -   setEnableCrc: a method for specifying whether to enable cyclic redundancy check \(CRC\) for the upload. By default, CRC is enabled.
    -   ChangeLog.txt: provides version history. You can obtain the version number and release date of the current SDK in the first line.
-   samples directory
    -   uploadVideo.py: provides the sample code for uploading videos.
    -   uploadImage.py: provides the sample code for uploading images.

## Sample code

The following sample code shows you how to upload an on-premises video and an online video:

```
# -*- coding: UTF-8 -*-
from voduploadsdk.AliyunVodUtils import *
from voduploadsdk.AliyunVodUploader import AliyunVodUploader
from voduploadsdk.UploadVideoRequest import UploadVideoRequest 

# Test the upload of an on-premises video.
def testUploadLocalVideo(accessKeyId, accessKeySecret, filePath, storageLocation=None):
    try:
        uploader = AliyunVodUploader(accessKeyId, accessKeySecret)
        uploadVideoRequest = UploadVideoRequest(filePath, 'test upload local video')
        # Specify the video thumbnail. If the video thumbnail is an on-premises or online image, you can call the UploadImageRequest method to upload the image to ApsaraVideo VOD and obtain the value of the ImageURL parameter.
        #uploadVideoRequest.setCoverURL('https://sample.com/sample.jpg')  
        #uploadVideoRequest.setTags('tag1,tag2')
        if storageLocation:
            uploadVideoRequest.setStorageLocation(storageLocation)
        videoId = uploader.uploadLocalVideo(uploadVideoRequest)
        print("file: %s, videoId: %s" % (uploadVideoRequest.filePath, videoId))
        
    except AliyunVodException as e:
        print(e)
 
# Test the upload of an online video.
def testUploadWebVideo(accessKeyId, accessKeySecret, fileUrl, storageLocation=None):
    try:
        uploader = AliyunVodUploader(accessKeyId, accessKeySecret)
        uploadVideoRequest = UploadVideoRequest(fileUrl, 'test upload web video')
        uploadVideoRequest.setTags('tag1,tag2')
        if storageLocation:
            uploadVideoRequest.setStorageLocation(storageLocation)
        videoId = uploader.uploadWebVideo(uploadVideoRequest)
        print("file: %s, videoId: %s" % (uploadVideoRequest.filePath, videoId))
        
    except AliyunVodException as e:
        print(e)

####   Run the test code.   ####   
accessKeyId = '<AccessKeyId>'
accessKeySecret = '<AccessKeySecret>'

localFilePath = '/opt/video/sample.mp4'
testUploadLocalVideo(accessKeyId, accessKeySecret, localFilePath)

fileUrl = 'http://sample.oss.aliyuncs.com/video/sample.mp4'
#testUploadWebVideo(accessKeyId, accessKeySecret, fileUrl)
```

For more sample code, see the files in the samples directory.

