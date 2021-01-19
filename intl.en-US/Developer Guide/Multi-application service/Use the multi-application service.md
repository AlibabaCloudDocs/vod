# Use the multi-application service

Before you can use the multi-application service, you must activate ApsaraVideo VOD. This topic describes the steps, notes, and FAQ for using the multi-application service.

If you have already activated [ApsaraVideo VOD](https://www.aliyun.com/product/vod?spm=a2c4g.11186623.2.20.67e51a9e8NkYq1), you can perform the following steps to use the multi-application service:

1.  Apply for activation
2.  Create an application
3.  Grant permissions to the identity entity
4.  Upload media
5.  Manage media for each application separately

Or

1.  Apply for activation
2.  Create an application
3.  Grant permissions to the identity entity
4.  Configure callbacks
5.  Configure callbacks for each application separately

## Apply for activation

-   Prerequisites

    The multi-application service is currently in public preview and not available in the ApsaraVideo VOD console. Before you apply to activate the multi-application service, make sure that following requirement is met:

    The peak bandwidth for accelerated traffic in the last seven days is 500 Mbit/s or higher. To view the peak bandwidth, see the [Resource Consumption](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.22.67e51a9e8NkYq1#/usage/flow) page in the ApsaraVideo VOD console.

-   Impacts

    -   You cannot disable the default application. Otherwise, normal online services may be affected.
    -   You cannot manage or query resources in applications other than the default application in the ApsaraVideo VOD console. Such resources include media assets, reviews, and media processing configurations.
    -   For new applications, you must call API operations to re-configure transcoding and callbacks.
    **Note:**

    -   If you want to test the callback feature, you can specify callback URLs in different environments when you upload media files.
    -   If you want to isolate media files, you can use the media category module.
-   Activation method

    If you meet the requirements to activate the multi-application service and accept the preceding impacts, go to the [request page](https://page.aliyun.com/form/act1652018117/index.htm) and [submit a ticket](https://selfservice.console.aliyun.com/ticket/category/vod/recommend/561) to activate the service.

    **Note:** In the ticket, you must provide the **UID of your Alibaba Cloud account** and declare that you acknowledge and accept the impacts in applying to activate the multi-application service.


## Create an application

You can call the [CreateAppInfo]() operation to create applications. Up to 10 applications can be created in a single account. Application names must be unique.

**Note:** When you create an application for the first time, you must use the AccessKey pair of your Alibaba Cloud account to create the application. Later, you can grant administrator permissions to RAM users to manage the application.

## Grant permissions to the identity entity

You can call the [t1235660.md\#]() operation to grant permissions to an identity entity \(RAM user or role\) before the identity entity can manage resources in applications. For more information about policies, see the "Policies" section in [Overview](/intl.en-US/Developer Guide/Multi-application service/Overview.md).

## Use the multi-application service

The `AppId` parameter is added for services that support the multi-application service. You can specify this parameter when you create resources or make settings. When you query data, only resources in the applications that you are authorized to access are returned. When you modify or delete data, permissions must be verified before you can proceed.

Only the **callback** and **media services \(including media upload, playback, and media management\)** support the multi-application service. Support from other services will be available soon.

-   Callbacks

    You can set a separate callback method and URL for each application. You can use the AppId parameter in the following operation:

    [t1235667.md\#](/intl.en-US/API Reference/Global Config/Event notification/SetMessageCallback.md): If the AppId parameter is specified, you can configure callbacks for the application. If the AppId parameter is not specified, the system default application is used.

    -       -       After the settings are complete, callbacks are performed for event notifications for video and image uploads in different applications based on the settings. You can also call the [t1235668.md\#](/intl.en-US/API Reference/Global Config/Event notification/GetMessageCallback.md) operation to query related configurations.

    **Note:** After you activate the multi-application service, you can manage callback configurations for only the default application in the ApsaraVideo VOD console. The ApsaraVideo VOD console will be upgraded to support the management of other applications.

-   Media services

    -   Media upload: You can specify the AppId parameter in upload operations such as CreateUploadVideo and CreateUploadImage to upload media files to the specified application, provided that you have the required permissions on this application. If you do not have the permissions on the specified application, the upload fails. If you do not specify the AppId parameter, media files are uploaded to the system default application.
    -   Audio and video playback: You can obtain playback information such as playback credentials and URLs only from applications that you are authorized to access.
    -   Media modification and deletion: You can modify and delete media resources only in applications that you are authorized to access.
    -   Media query: When you call API operations to query the details of media resources, you can obtain information about media resources only in applications that you are authorized to access. Batch queries return the data of media resources only in applications that you are authorized to access. The IDs \(MediaId\) of media resources in applications that you are not authorized to access are included in the NonExistMediaIds field \(the field name may vary\).
    -   Media search: Media search operations return the data of media resources only in applications that you are authorized to access. You can specify one or more application IDs \(AppId\) in the search criteria.
    **Note:** After you activate the multi-application service, you can manage media resources only in applications that you are authorized to access in the ApsaraVideo VOD console. The ApsaraVideo VOD console will be upgraded to support the management of other applications.


