# FAQ about the short video SDK for iOS

This topic provides answers to some frequently asked questions when you use the short video SDK for iOS.

## What can I do if the console displays a message indicating that the Category method cannot be found when I import the short video SDK for iOS?

In Xcode, click your target in the project. On the page that appears, click the Build Setting tab and add the `-ObjC` flag to Other Linker Flags.

## What are the differences between the Debug folder and Release folder?

The Debug folder contains frameworks for both emulators and devices, whereas the Release folder contains frameworks only for devices. To submit an application to App Store, strip the frameworks for emulators from dynamic frameworks. Otherwise, your application will be rejected.

## Why does the console display a message indicating duplicate symbols when I import the short video SDK for iOS?

This message may be returned if you integrate the upload SDK that is contained in the short video SDK. You can ignore the message because it does not affect the functionality.

## What can I do if my project fails and the "Image not found" message appears after I import the short video SDK to the project?

The short video SDK contains dynamic libraries. To import dynamic libraries to a project, add the frameworks that contain these dynamic libraries to Embedded Binaries in Xcode.

## Does the short video SDK support bitcode?

No, the short video SDK does not support bitcode. You must set the Enable Bitcode parameter to No. If the "Failed to verify bitcode" error occurs when you package the SDK, you must clear Rebuild from Bitcode.

## Why is the "\[NSDictionary oss\_dictionaryWithXMLData:\]: unrecognized selector sent to class" error returned?

This error occurs because the upload SDK is not imported to your project. The short video SDK depends on the `AliyunOSSiOS.framework` file of the upload SDK.

## Why am I unable to obtain the recorded video after the recording is complete?

To obtain the recorded video, call the `- (void)recorderDidFinishRecording;` callback function when the recording is complete.

## How do I record a video in landscape mode?

Call the `cameraRotate` operation to set the rotation angle for recording. If a recorded video contains multiple clips, the rotation angle follows that of the first clip.

## Why am I unable to switch music when I record a video?

The short video SDK does not allow you to switch music when you record a video.

## How do I record a video in full screen mode?

The aspect ratio of recordings is 9:16. To record videos in full screen mode, you can add black borders at the top and bottom of the recording image, the same with the demo project. You can also display the recording image to fulfill the height of the iPhone screen and hide part of the image on the left and right sides.

## What can I do if error code 1008 is returned when I crop a video?

Set `shouldOptimize` to false.

## What can I do if error code 700004 is returned when I crop a video?

You must set the output path.

## How do I obtain a cropped video without black borders?

You can crop videos without changing the aspect ratio. Make sure that resolutions of cropped videos are even integer numbers.

## How do I crop a piece of music?

You can set the parameters in the same way as cropping a video. You do not need to set the `videoSize` or `outputSize` parameter.

## What can I do if the "\[null length\]" error is returned when I produce a video after I finish editing it?

Make sure that you specify a valid path to the watermark image file.

## Why is the sound distorted when I call the volume control operation to set the volume?

The default volume value is 100, indicating the original volume. If the volume value is greater than 100, the sound may be distorted. We recommend that you set the volume value in the range from 0 to 100.

## What can I do if I fail to obtain resources such as filters and music videos \(MVs\)?

You can copy entire folders of the required resources to your project to maintain the file structure of the resources. Note that real resource folders of your application are referenced to your project in Xcode as blue folders.

## What can I do if the "Operation not permitted" message appears when I import a video?

To import videos from Photos, call the system operation to obtain the access permissions on Photos. Make sure that the AVAsset class is not destroyed.

## What can I do if I am unable to adjust the volume or add or delete sound effects for imported audio files?

Make sure that the imported files are audio files, such as PCM files and MP3 files. Do not import video files to add BGM.

## What can I do if an upload error is returned indicating that I am not authorized?

Perform the following steps to obtain a security token that Security Token Service \(STS\) issues:

1.  Create a RAM user by using your Alibaba Cloud account and grant the AliyunSTSAssumeRoleAccess permission to the RAM user.
2.  Use the RAM user to create a role and grant the AliyunVODFullAccess permission to the role.
3.  Call the STS SDK to obtain the security token. For more information, see [STS SDK for Java](/intl.en-US/SDK Reference/STS SDK Reference/STS SDK for Java.md).

    **Note:** Use the AccessKey pair of the RAM user to call the STS SDK.

4.  Modify the policy so that the RAM user has all permissions on ApsaraVideo VOD.

```
  String policy = "{\n" +
           "    \"Version\": \"1\", \n" +                
           "    \"Statement\": [\n" +                
           "        {\n" +                
           "            \"Action\": [\n" +                
           "                \"vod:*\"\n" +                
           "            ], \n" +                
           "            \"Resource\": [\n" +                
           "                \"*\" \n" +                
           "            ], \n" +                
           "            \"Effect\": \"Allow\"\n" +                
           "        }\n" +                
           "    ]\n" +                
           "}"
```

## The network is disconnected when I upload a video. Why is no callback notification returned?

If the network is disconnected when you upload a video, the system automatically retries the upload process. If you do not want the system to retry the upload, you can manually call an operation to cancel the upload.

## I use the server SDK to download a video that is uploaded to ApsaraVideo VOD. Why is the downloaded video in the M3U8 format?

If you enable HTTP Live Streaming \(HLS\) Encryption in transcoding settings, videos are generated in the M3U8 format.

