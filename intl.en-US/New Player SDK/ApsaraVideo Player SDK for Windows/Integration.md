# Integration

This topic shows you how to integrate ApsaraVideo Player SDK for Windows by using on-premises files. This topic also provides the links for you to download relevant installation packages.

## Supported systems

Windows 7 and later are supported.

## Prepare the environment

We recommend that you use Visual Studio 2017 as the development tool. This topic is based on the Visual Studio 2017 development environment.

## Integrate the SDK by using on-premises files

-   SDK download

    Download the latest version of ApsaraVideo Player SDK for Windows. For more information, see [Release notes of ApsaraVideo Player SDK for Windows](/intl.en-US/SDK Downloads/player-sdk-new-history/Player SDK for Windows.md).

-   SDK structure

    ![Folder](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5380401161/p184069.png)

    -   sdk folder: contains the SDK files, including header files, .lib files, .dll files, and .pdb files.
        -   sdk\_headers folder
        -   bin folder
    -   doc folder: contains help documentation, including .js files and .html files.
        -   en folder
        -   cn folder
    -   demo folder: contains a demo of the SDK, including the source code and an .exe file.
        -   src folder
        -   bin folder
-   Demo compilation
    1.  Install Visual Studio 2017. Click [here](https://download.visualstudio.microsoft.com/download/pr/6a433d5c-4604-4a3e-8b78-707ba18a9ba0/acd74a4a755fb6272d68cb3ab678ea020faf0078a89099ce352dfabc623a1db7/vs_Community.exe) to download the installation package of Visual Studio 2017.
    2.  Install Qt 5.12.9. Click [here](https://iso.mirrors.ustc.edu.cn/qtproject/archive/qt/5.12/5.12.9/qt-opensource-windows-x86-5.12.9.exe) to download the installation package of Qt 5.12.9.
    3.  Install the Qt plug-in. Click [here](http://download.qt.io/official_releases/vsaddin/2.5.2/qt-vsaddin-msvc2017-2.5.2-rev.01.vsix) to download the installation package of the Qt plug-in.
    4.  Open the SDK. Go to the demo directory and choose **src** \> **AliyunPlayerTest** \> **AliyunPlayerTest.sln**.
    5.  Add a Qt version: Open Qt in Visual Studio 2017 and choose **Qt VS Tools** \> **Qt Options**. In the Qt Options dialog box, click **Add** on the **Qt Versions** tab. Set the following parameters:
        -   Version name: Set the parameter to 5.12.9.
        -   Path: Set the parameter to C:\\Qt\\Qt5.12.9\\5.12.9\\msvc2017.
    6.  Set Qt dependencies: Open Qt in Visual Studio 2017 and choose **Qt VS Tools** \> **Qt Project Settings**. In the Qt Project Settings dialog box, click the **Qt Modules** tab, select the following options, and then click OK.
        -   core
        -   gui
        -   network
        -   widget
-   Integration procedure

    Copy the sdk\_headers and bin folders in the sdk folder to your Qt project directory and set dependencies for your project. For example, copy the sdk\_headers and bin folders to the third\_party/aliplayer directory of your project.

    1.  Copy files in the sdk/sdk\_headers directory to the third\_party/aliplayer directory.
    2.  Copy the AliPlayer.lib and artpSource.lib files in the sdk/bin directory to the third\_party/aliplayer/lib directory.
    3.  Configure the add-on package in the third\_party/aliplayer/sdk\_headers directory of your project in Visual Studio 2017.
    4.  After the project is compiled, copy all the .dll files in the sdk/bin directory to the directory of the same level as the .exe file.

