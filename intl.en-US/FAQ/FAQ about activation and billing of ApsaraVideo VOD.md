# FAQ about activation and billing of ApsaraVideo VOD

This topic provides answers to some frequently asked questions when you purchase an ApsaraVideo VOD package and use Alibaba Cloud CDN and Object Storage Service \(OSS\).

## Can I use the resource plans in my purchased ApsaraVideo VOD package to pay for Alibaba Cloud CDN and OSS?

No, you cannot use the resource plans in your ApsaraVideo VOD package to pay for the resources consumed in other services, such as Alibaba Cloud CDN and OSS. ApsaraVideo VOD is independently charged from other services. When you use ApsaraVideo VOD, you are charged for the storage, transcoding, traffic, or bandwidth resources consumed. An ApsaraVideo VOD package contains resource plans such as a data transfer plan, a storage plan, and a transcoding plan. You can use the resource plans to pay only for the resources consumed in ApsaraVideo VOD.

## Are OSS and Alibaba Cloud CDN automatically activated when I activate ApsaraVideo VOD?

No, OSS and Alibaba Cloud CDN are not activated. When you use ApsaraVideo VOD, you may need to use the storage, transcoding, and CDN acceleration services. These services require different resources. As an independently charged service, ApsaraVideo VOD provides a private OSS bucket to store your videos, and automatically initiates and completes video transcoding. In addition, ApsaraVideo VOD accelerates content delivery based on the domain name for CDN that you provide. You do not need to activate other services such as OSS, ApsaraVideo for Media Processing, and Alibaba Cloud CDN. By default, these services are not automatically activated when you activate ApsaraVideo VOD.

## What can I do if I cannot renew the ApsaraVideo VOD package that I purchased before March 2017?

If you purchased an ApsaraVideo VOD package of an earlier version before March 2017, the package contains the following items: a CDN data transfer plan, an OSS storage plan, an OSS resource plan about the number of OSS access requests, and an ApsaraVideo for Media Processing voucher. In this case, you can separately purchase the CDN data transfer plan and OSS resource plan.

**Note:** The ApsaraVideo VOD console of the earlier version is integrated into the ApsaraVideo for Media Processing console, where you can retrieve your ApsaraVideo VOD data.

In March 2017, a new version of ApsaraVideo VOD was released, which includes significant updates to features and usage. In addition, ApsaraVideo VOD has become an independently charged service. A subscription plan that matches the new version of ApsaraVideo VOD was launched in May 2017.

## What are the differences between ApsaraVideo VOD and OSS?

In terms of definition:

-   ApsaraVideo VOD is an all-in-one solution for on-demand audio and video streaming. It provides features such as audio and video collection, editing, uploading, automated transcoding, media resource management, and CDN acceleration.
-   OSS is a secure, cost-effective, and highly reliable service that stores large amounts of data.

In terms of functionality:

-   ApsaraVideo VOD stores videos. It will support audio storage in the future to enhance the capabilities of the media library.
-   OSS stores various types of files, such as video files, audio files, images, DOC files, and PDF files. OSS can be considered as a disk in the cloud.

In terms of connection:

-   OSS can be used as an independent storage service or connected to CDN to accelerate delivery of files that are stored in OSS. ApsaraVideo VOD serves as a hosting service for the audio and video files that you store in ApsaraVideo VOD to meet business requirements for online on-demand audio and video streaming. ApsaraVideo VOD also provides various capabilities to address all aspects of on-demand video streaming. Such capabilities include media asset management, online video editing, video moderation and publishing, data statistics, short video SDK, and video security.
-   ApsaraVideo VOD stores data in OSS buckets. However, the private bucket that ApsaraVideo VOD provides does not consume OSS resources. This means that you do not need to activate OSS. If you have activated OSS, the private bucket is invisible in your OSS service and is independently charged.

