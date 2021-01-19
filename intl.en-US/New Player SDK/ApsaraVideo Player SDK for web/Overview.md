# Overview

ApsaraVideo Player SDK is an important part of ApsaraVideo. It supports interactions between clients and Alibaba Cloud. It also supports features such as encrypted playback, resolution switching, and time shifting. This topic describes online settings and features of ApsaraVideo Player SDK for web. This topic also provides a demo that illustrates how to play videos from ApsaraVideo VOD in a WeChat mini program. ApsaraVideo Player SDK provides you with simple, fast, secure, and stable video playback services.

## Online settings

ApsaraVideo Player SDK allows you to configure settings online. When you configure the settings on the [Online Settings](https://player.alicdn.com/aliplayer/setting/setting.html?spm=a2c4g.11186623.2.17.52686782JpdzLD) page, executable code is also generated so that you can integrate ApsaraVideo Player SDK with ease.

![Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6180401161/p208950.png)

## Features

ApsaraVideo Player SDK displays its features on the [Functions](https://player.alicdn.com/aliplayer/presentation/index.html?type=cover) page. It uses components to provide features such as last position, marquee, playlist, and ad. It also provides feature code so that you can customize features as required.

![Features](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6180401161/p208952.png)

**Note:** On an Android mobile phone, the internal browsers in WeChat and QQ may modify the settings of ApsaraVideo Player SDK without your permission or knowledge. In this case, specific features of ApsaraVideo Player SDK may fail.

## WeChat mini program

A WeChat mini program lacks relevant DOM API and BOM API. In this case, specific libraries that are commonly used in frontend development, such as jQuery and Zepto, cannot be loaded in the WeChat mini program. Similarly, ApsaraVideo Player SDK for web, which relies on the support of browsers, cannot be run in the WeChat mini program. Therefore, you must use the default video component that is provided by the WeChat mini program to play videos. For more information, visit [Demo of WeChat applet that integrates ApsaraVideo for VOD](https://github.com/aliyunvideo/AliyunPlayer_Web/tree/master/vod-mini-program?spm=a2c4g.11186623.2.21.52686782OXIoWp).

## QR code for demos

Use DingTalk to scan the following QR code to use the demos of ApsaraVideo Player SDK.

![QR code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6180401161/p208954.png)

