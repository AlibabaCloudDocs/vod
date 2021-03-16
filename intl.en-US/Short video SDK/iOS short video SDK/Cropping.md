# Cropping

The short video SDK provides a cropping module that allows you to crop videos by duration and aspect ratio, crop audio by duration, and crop images by aspect ratio.

## Related class

|Name|Description|
|----|-----------|
|AliyunCrop|The core cropping class.|

**Note:**

-   An instance object of the AliyunCrop class must be a property instead of a local variable.
-   All cropping features are supported in Professional Edition, Standard Edition, and Basic Edition.

## Crop a video file or an audio file

-   Initialize an object

    |Action|Sample code|
    |------|-----------|
    |Call the initialization method to create a cropping object.|    ```
/**
@param error The error code.
*/ 
- (instancetype)initWithDelegate:(id<AliyunCropDelegate>)delegate;
    ``` |
    |Set the path of the input video or audio file.|    ```
@property (nonatomic, copy) NSString *inputPath;
    ``` |
    |Set the path of the output video or audio file.|    ```
@property (nonatomic, copy) NSString *outputPath;
    ``` |

    **Note:** If the path of the output file contains folders in multiple levels, make sure that the folders have been created.

-   Set parameters

    |Action|Sample code|
    |------|-----------|
    |Set the resolution of the output video.|    ```
@property (nonatomic, assign) CGSize outputSize;
    ``` |
    |Set the time when the cropping starts, in seconds.|    ```
@property (nonatomic, assign) float startTime;
    ``` |
    |Set the time when the cropping ends, in seconds.|    ```
@property (nonatomic, assign) float endTime;
    ``` |
    |Set the cropping mode.|    ```
/**
This method is not required for audio cropping.
*/
@property (nonatomic, assign) AliyunCropCutMode cropMode;
    ``` |
    |Set an effective area for video cropping.|Calculate the x, y, w, and h values within the cropping area in the following manner: Define the upper-left corner of the video as the origin O \(0,0\). Define the horizontal direction as the x-axis and the vertical direction as the y-axis. Assume that the video cropping area is Z. The x value is the distance along the x-axis between the upper-left vertex of the area Z and the origin O. The y value is the distance along the y-axis between the upper-left vertex of the area Z and the origin O. The w value is the width of the area Z. The h value is the height of the area Z. The x, y, w, and h values are measured in pixels.

    ```
/**
This method is not required for audio cropping.
*/
@property (nonatomic, assign) CGRect rect;
    ``` |
    |Set the video quality.|Default value: AliyunVideoQualityMedium.

    ```
/**
This method is not required for audio cropping.
*/
@property (nonatomic, assign) AliyunVideoQuality videoQuality;
    ``` |
    |Set the encoding mode.|Hardware encoding is faster, whereas software encoding provides a higher resolution.

    ```
/**
A value of 0 indicates the software encoding mode. A value of 1 indicates the hardware encoding mode. Default value: 1.
*/
@property (nonatomic, assign) int encodeMode;
    ``` |
    |Set the frame rate.|Default value: 25.

    ```
/**
This method is not required for audio cropping.
*/
@property (nonatomic, assign) int fps;
    ``` |
    |Set the group of pictures \(GOP\) size.|Default value: 5.

    ```
@property (nonatomic, assign) int gop;
    ``` |
    |Set the bitrate, in bit/s.|    ```
/**
This method is not required for audio cropping.
*/
@property (nonatomic, assign) int bitrate;
    ``` |
    |Set the background color in padding mode.|    ```
/**
This method is not required for audio cropping.
*/
@property (nonatomic, strong) UIColor *fillBackgroundColor;
    ``` |

-   Configure cropping

    |Action|Sample code|
    |------|-----------|
    |Start the cropping.|    ```
- (int)startCrop;
    ``` |
    |Cancel the cropping.|    ```
- (void)cancel;
    ``` |

-   Listen to cropping callbacks

    The delegate object needs to implement the AliyunCropDelegate protocol to listen to cropping callbacks. The AliyunCropDelegate protocol provides the following callbacks.

    |Callback event|Sample code|
    |--------------|-----------|
    |The cropping fails.|    ```
/**
@param progress The current progress is in the range of 0-1.
*/
- (void)cropOnError:(int)error;
    ``` |
    |The cropping progress is monitored.|    ```
- (void)cropTaskOnProgress:(float)progress;
    ``` |
    |The cropping is completed.|    ```
- (void)cropTaskOnComplete;
    ``` |
    |The cropping is canceled or the application is switched to the background.|    ```
- (void)cropTaskOnCancel;
    ``` |


## Crop an image

The short video SDK allows you to crop an image. The core class is AliyunImageCrop.

-   Initialize an object

    Create an AliyunImageCrop object and initialize it.

-   Set parameters

    |Action|Sample code|
    |------|-----------|
    |Specify the image to be cropped.|    ```
@property (nonatomic, strong) UIImage *originImage;
    ``` |
    |Specify the resolution of the output image.|    ```
@property (nonatomic, assign) CGSize outputSize;
    ``` |
    |Specify the image scaling mode. This method is optional.|    ```
/**
A value of 0 indicates the padding mode. A value of 1 indicates the cropping mode.
*/
@property (nonatomic, assign) AliyunImageCropMode cropMode;
    ``` |
    |Specify the cropping area, in pixels. This method is optional.|This method applies only to the cropping mode. Assume that an image has a resolution of 200 × 200 pixels. You can set the cropRect parameter of the image to \(0,0,100,100\), in pixels.

    ```
@property (nonatomic, assign) CGRect cropRect;
    ``` |
    |Set the background color in padding mode. This method is optional.|    ```
@property (nonatomic, strong) UIColor *fillBackgroundColor;
    ``` |

-   Configure cropping

    Generate an image.

    ```
    - (UIImage *)generateImage;
    ```

    **Note:** The cropped image is returned. If the cropping fails, nil is returned.


## Examples

-   Crop a video file

    ```
    self.crop = [[AliyunCrop alloc] initWithDelegate:self];
    self.crop.inputPath = 'The path of the video file to be cropped';
    self.crop.outputPath = 'The path of the output video file';
    self.crop.cropMode = AliyunCropModeScaleAspectCut;
    self.crop.outputSize = CGSizeMake(540, 540);// Set the resolution of the output video to 540 × 540.
    self.crop.rect = CGRectMake(0, 0, 320, 320); // The parameter value indicates that you draw a cropping frame on the current video. To prevent the video image from being cropped, set the width and height of the cropping frame to those of the input video. The aspect ratio of the cropping frame must be the same as that of the output video. Otherwise, distortion may occur.
    self.crop.startTime = 0.0;
    self.crop.endTime = 5.0;
    self.crop.fillBackgroundColor = [UIColor greenColor]; // Specify the background color in padding mode.
    [self.crop startCrop]; // Start video cropping.
    ```

-   Crop an audio file

    ```
    self.crop = [[AliyunCrop alloc] initWithDelegate:self];
    self.crop.inputPath = 'The path of the audio file to be cropped';
    self.crop.outputPath = 'The path of the output audio file';
    self.crop.startTime = 0.0;
    self.crop.endTime = 5.0;[self.crop startCrop]; // Start audio cropping.
    ```


