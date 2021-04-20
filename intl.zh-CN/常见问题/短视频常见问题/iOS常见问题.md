# iOS常见问题

本文主要介绍短视频在iOS端的使用问题。

## 导入SDK时,控制台提示category方法没找到，该如何解决？

在工程target中选择Build Setting\>other linker flags，添加`-ObjC`。

## debug包和release包有什么区别？

debug包包含模拟器和真机版本，可以保证模拟器编译通过；在提交app store时使用release包，因为apple要求动态库提交不能包含模拟器版本。

## 导入SDK时，控制台提示重复符号duplicate symbol的警告，是什么原因？

短视频内部包含的上传SDK，如果集成了上传SDK会报警告，对功能没有影响，可以忽略。

## 导入SDK后运行crash，提示image not found，该如何解决？

短视频sdk使用了动态库，导入动态库需要在Embedded Binaries中添加对应的framework，参考集成文档。

## 短视频SDK支持bitcode吗？

短视频SDK不支持bitcode，需要在设置中把Enable Bitcode设为NO。打包如果出现”failed to verify bitcode”错误，需要取消勾选rebuild for bitcode选项。

## 提示\[NSDictionary oss\_dictionaryWithXMLData:\]: unrecognized selector sent to class，是什么原因？

没有导入上传SDK，短视频SDK需要依赖上传SDK`AliyunOSSiOS.framework`。

## 录制完成后，获取不到视频，该如何解决？

需要在录制完成回调函数`- (void)recorderDidFinishRecording;`里才能获取到视频。

## 如何实现横屏录制？

录制时候设置`cameraRotate`角度值，录制的视频方向会以第一段视频的角度值为准。

## 录制过程中切换音乐，没有生效，是什么原因？

录制过程中不支持更换音乐。

## 如何实现全屏录制方案？

录制分辨率9：16，显示有两种方案，一种和demo一样iphone x上下留黑边，另一种可以调整view布局上下撑，满左右一部分内容不显示。

## 裁剪提示1008错误，该如何解决？

关闭`shouldOptimize`选项。

## 裁剪提示700004错误，该如何解决？

输出路径没有设置。

## 如何实现没有黑边的裁剪？

根据原始分辨率，做一个缩放，缩放后的分辨率保证是偶数。

## 如何裁剪一段音乐？

裁剪参数`videoSize`和`ouptutSize`都无需设置，其他操作和裁剪视频保持一致。

## 编辑完成后，合成crash，出现报错提示\[null length\]，该如何解决？

检查水印路径有没有正确设置。

## 调用音量接口出现破音，是什么原因？

默认值100代表原声，大于100可能会破音，建议0-100。

## 滤镜mv等资源找不到，该如何解决？

资源拷贝到项目中需要用folder方式导入才能保证层级关系，注意在xcode中显示的文件夹是蓝色的。

## 导入视频，提示operation not permit，该如何解决？

从系统相册导入的视频，需要调用系统接口获取相册访问权限，同时保证对应的AVAseset没有被销毁。

## 加入音频后，无法调节音量和添加、删除音效，该如何解决？

注意加的音频需要为pcm、mp3等音频文件，不能为视频文件。

## 上传报错，提示没有授权，该如何解决？

获取STS流程简单介绍：

1.  阿里云主账户创建子账户 —- 给子账户授权AliyunSTSAssumeRoleAccess。
2.  使用子账户—-创建角色 —- 给角色授权VODFULL。
3.  通过调用STS的SDK，获取STS，参考：[Java示例](/intl.zh-CN/SDK参考/SDK参考（STS）/Java示例.md)。

    **说明：** 调用STS的SDK中的ak必须要是子账户的ak。

4.  修改policy为点播的全量权限。

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
           “}”
```

## 上传过程中断网，为什么没有失败回调？

上传过程中断网，会自动重试，如果不想走重试接口，可以手动调用取消上传。

## 上传后的视频，通过服务端SDK下载的视频格式为什么是m3u8？

转码配置里面，如果勾选了hls选项，会生成m3u8格式视频。

