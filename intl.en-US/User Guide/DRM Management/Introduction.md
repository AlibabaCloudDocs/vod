# Introduction

ApsaraVideo VOD supports mainstream digital rights management \(DRM\) encryption technologies in the industry. You can add and manage DRM certificates and enable DRM encryption in the ApsaraVideo VOD console to protect the security of your copyrighted video content.

## Limits

|DRM encryption technology|Mobile client|Supported browser|
|-------------------------|-------------|-----------------|
|Widevine|Android|Chrome, Firefox 47 and later, Microsoft Edge, and Opera|
|FairPlay|iOS|Safari|

**Note:** You can enable DRM encryption only in the ApsaraVideo VOD console. For more information, see [DRM encryption](/intl.en-US/User Guide/DRM Management/DRM encryption.md).

## Features

-   DRM encryption: ApsaraVideo VOD supports Widevine and FairPlay DRM encryption.
-   Certificate management: You can add and manage FairPlay Streaming certificates in the ApsaraVideo VOD console.
-   DRM-based playback: You can use ApsaraVideo Player to decrypt and play DRM-encrypted videos.

## Benefits

-   Comprehensive features: ApsaraVideo VOD allows you to manage DRM certificates, issue DRM licenses, encrypt videos based on DRM, and decrypt and play DRM-encrypted videos. You can use the features without the need to understand the architecture and implementation of DRM.
-   Cost efficiency: ApsaraVideo VOD generates only one output file that supports Widevine and FairPlay DRM encryption in each transcoding task. This reduces the transcoding and storage costs. Your use of DRM encryption is charged in the pay-as-you-go billing method without minimum fees.
-   High security, stability, and concurrency: ApsaraVideo VOD ensures secure storage of your copyrighted video content by using refined permission management and system security settings. In addition, the distributed service architecture meets high-concurrency requirements of your business.

## Architecture diagram

![Architecture diagram](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5535794061/p177190.jpg)

## Billing

DRM encryption is implemented based on transcoding. The fee for using DRM encryption is included in the transcoding fee. You are charged an extra fee each time when a device requests a license to play a DRM-encrypted video. The following table describes the billing rule.

|Region|Pricing|
|------|-------|
|Mainland China|USD 0.0012 per request|
|Singapore, Japan \(Tokyo\), Germany \(Frankfurt\), India \(Mumbai\), and Indonesia \(Jakarta\)|USD 0.0015 per request|

