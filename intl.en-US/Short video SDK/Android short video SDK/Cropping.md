# Cropping

The short video SDK provides a cropping module that allows you to crop videos by duration and aspect ratio, crop audio by duration, and crop images by aspect ratio.

## Related class

|Class|Description|
|-----|-----------|
|AliyunCrop|The core cropping class.|

**Note:** All cropping features are supported in Professional Edition, Standard Edition, and Basic Edition.

## Cropping process

|Action|Sample code|
|------|-----------|
|Create a cropping instance.|```
AliyunCropCreator.createCropInstance(context);
``` |
|Set cropping parameters.|```
AliyunICrop.setCropParam(param);
``` |
|Set cropping callbacks.|```
AliyunICrop.setCropCallback();
``` |
|Start cropping.|```
AliyunICrop.startCrop();
``` |
|Release resources.|```
AliyunICrop.dispose();
``` |

**Note:** You must set the OutputWidth, OutputHeight, OutputPath, and InputPath parameters for video cropping.

## Sample code

```
//1. Create a cropping instance.
AliyunICrop aliyunICrop = AliyunCropCreator.createCropInstance(context);
CropParam cropParam = new CropParam();
//2. Set cropping parameters.
// You must specify the width and height of the cropped video, in pixels. In addition, you must specify the path of the mezzanine file to be cropped and the path of the cropped video file.
int outputWidth = 720;
int outputHeight = 1080;
cropParam.setOutputWidth(outputWidth);
cropParam.setOutputHeight(outputHeight);
cropParam.setOutputPath("/storage/emulated/0/DCIM/Camera/test.mp4");
cropParam.setInputPath("/storage/emulated/0/DCIM/Camera/VID_20210111_134419.mp4");
// You can set the following parameters as needed:
// The type of the media file. Default value: ANY_VIDEO_TYPE.
cropParam.setMediaType(MediaType.ANY_VIDEO_TYPE);
// The cropping area.
int startCropPosX = 0;
int startCropPoxY = 0;
Rect cropRect = new Rect(startCropPosX, startCropPoxY, startCropPosX + outputWidth,
    startCropPoxY + outputHeight);
cropParam.setCropRect(cropRect);
// Set the ScaleMode parameter. A value of VideoDisplayMode.SCALE indicates the cropping mode. A value of VideoDisplayMode.FILL indicates the padding mode.
cropParam.setScaleMode(VideoDisplayMode.SCALE);
// The frame rate.
cropParam.setFrameRate(30);
//gop
cropParam.setGop(5);
// The video quality.
cropParam.setQuality(VideoQuality.HD);
// The video codec format.
cropParam.setVideoCodec(VideoCodecs.H264_HARDWARE);
// The fill color.
cropParam.setFillColor(Color.BLACK);
aliyunICrop.setCropParam(cropParam);
//3. Set cropping callbacks.
aliyunICrop.setCropCallback(new CropCallback() {
    @Override
    public void onProgress(int i) {
    }

    @Override
    public void onError(int i) {
        Log.i("TestCrop", "testCrop,onError:" + i);
    }

    @Override
    public void onComplete(long l) {
        Log.i("TestCrop", "onComplete:" + l);
        Toast.makeText(context, "The cropping process is complete. Consumed time:" + l, Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onCancelComplete() {
    }
});
//4. Start cropping.
aliyunICrop.startCrop();
```

## Error codes

|Error code|Description|Solution|
|----------|-----------|--------|
|20010002|-   The error message returned because the mezzanine file does not exist.
-   The error message returned because you do not have the read and write permissions on the mezzanine file.
-   The error message returned because the sandbox restraints take effect. The sandbox restraints take effect only when the API level equals to 30.

|Make sure that the mezzanine file exists and you have the read and write permissions on the mezzanine file. Make sure that the API level is lower than 30.|

