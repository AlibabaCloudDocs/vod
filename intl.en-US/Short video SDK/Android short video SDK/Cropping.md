# Cropping

## Overview

The short video SDK allows you to crop videos by duration and frame size, crop audio by duration, and crop images by frame size. The core cropping operation is AliyunICrop.

**Note:** All cropping features are supported in Professional Edition, Standard Edition, and Basic Edition.

## Cropping process

-   **Set parameters**

    |Action|Sample code|
    |------|-----------|
    |Create a cropping instance.|    ```
AliyunCropCreator#createCropInstance(Context context);
    ``` |
    |Destroy the cropping instance.|    ```
AliyunICrop#dispose(); // Release resources.
    ``` |
    |Set the cropping parameters.|    ```
AliyunICrop#setCropParam(CropParam param);
    ``` |
    |Set a callback.|    ```
AliyunICrop#setCropCallback(CropCallback callback);
    ``` |

-   **Start cropping**

    |Action|Sample code|
    |------|-----------|
    |Start cropping.|    ```
AliyunICrop#startCrop();
    ``` |
    |Cancel cropping.|    ```
AliyunICrop#cancel();
    ``` |

-   **Complete cropping**

    |Action|Sample code|
    |------|-----------|
    |Release resources.|    ```
AliyunICrop#dispose();
    ``` |


