# Installation

This topic describes the prerequisites for installing ApsaraVideo VOD SDK for .NET. It also describes how to install ApsaraVideo VOD SDK for .NET by using the GitHub.

## Prerequisites

-   .NET 2.0 or later is installed.
-   Visual Studio 2017 or later is installed.
-   Mono 3.12 or later is installed.

## Install the SDK

1.  Download SDK source code from the GitHub
    1.  Install [git](https://git-scm.com/downloads?spm=a2c4g.11186623.2.13.521b4923vV5V58). If it is already installed, skip this step.
    2.  Run the **git clone** command to download the latest source code for the SDKs [aliyun-net-sdk-core](https://github.com/aliyun/aliyun-openapi-net-sdk/tree/master/aliyun-net-sdk-core?spm=a2c4g.11186623.2.14.521b4923GJdKhf) and [aliyun-net-sdk-vod](https://github.com/aliyun/aliyun-openapi-net-sdk/tree/master/aliyun-net-sdk-vod?spm=a2c4g.11186623.2.15.521b4923Q0fRxN).
    3.  After the source code is downloaded, go to the next step to add project references.
2.  Start the Visual Studio and add project references.
    1.  Choose **View** \> **Solution Explorer**.
    2.  In the right-side pane of the window, right-click **Solution** and choose **Add** \> **Existing Project**.
    3.  In the dialog box that appears, select the **aliyun-net-sdk-core.csproj** and **aliyun-net-sdk-vod.csproj** files, and click **Open**.
    4.  Right-click **Project** and select **Reference**. Then, select **Add Reference**. In the dialog box that appears, click the **Project** tab.
    5.  Select **aliyun-net-sdk-core** and **aliyun-net-sdk-vod**. Then, click **OK**.

