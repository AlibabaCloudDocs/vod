# FAQ

## What is the difference between the multi-application and RAM services?

-   The RAM service isolates and manages permissions on resources at the account level, whereas the multi-application service physically isolates resources and data for multiple users in the same Alibaba Cloud account.
-   The multi-application service does not provide logon or authentication for Alibaba Cloud accounts. It provides fine-grained permission control over applications after the AliyunVODFullAccess permission for ApsaraVideo VOD is granted in the RAM console. The multi-application service must be used together with RAM to implement role-based access control.

No, existing services are not affected if you activate the multi-application service. ApsaraVideo VOD is backward compatible. By default, data is placed in the system default application. In addition, if a RAM user or RAM role in your Alibaba Cloud account is granted the permissions to access ApsaraVideo VOD, the RAM user or RAM role has the permissions on the system default application.

Yes, you can use a RAM role to authorize other accounts to access resources within an application. For more information, see [Use a RAM role to grant permissions across Alibaba Cloud accounts](/intl.en-US/Tutorials/Use a RAM role to grant permissions across Alibaba Cloud accounts.md).

No, applications cannot be billed separately. Resources such as storage resources and domain names are not physically isolated for applications. After all usage-based resources such as storage resources, domain names, transcoding resources, and AI processing resources are isolated for applications, the usage and data statistics for each application can be calculated or collected separately. However, the bills are generated for your Alibaba Cloud account.

