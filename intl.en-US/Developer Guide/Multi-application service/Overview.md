Overview 
=============================

The multi-application service allows you to isolate the resources, configurations, and data of different users within the same account. You can call API operations to manage applications and grant permissions to identity entities. This topic describes the scenarios and usage limits of the multi-application service, as well as how to manage applications and grant permissions to identity entities.

Introduction 
---------------------------------

When you use ApsaraVideo VOD, you may need to isolate the resources, configurations, and data of multiple users within the same account. Multiple users include multiple environments, business lines, or channels.

ApsaraVideo VOD provides the multi-application service to implement isolation between multiple users. By default, the multi-application service is disabled. You can apply to activate the service and complete the related configurations. You can also use [Resource Access Management](https://www.aliyun.com/product/ram?spm=a2c4g.11186623.2.17.ddffaa32IhbDVd) to manage permissions. For more information, see [Use the multi-application service](/intl.en-US/Developer Guide/Multi-application service/Use the multi-application service.md).

Scenarios 
------------------------------

* Isolation of multiple environments:

  In testing and online environments, resources such as videos and images, configurations, and data must be isolated. You can use the multi-application service to create different applications for each environment, associate different RAM users with these applications, and grant permissions to the RAM users. This can avoid impacts from applications under test or development on online applications.
  

* Isolation of multiple business lines:

  When your company has multiple business lines or multiple departments that all need to use ApsaraVideo VOD, you can use the multi-application service to create an application for each business line or department for isolation.
  

* Isolation of multiple channels:

  If you want to build platform services based on the capabilities of ApsaraVideo VOD for multiple channels or customers, you can use the multi-application service.
  




Limits 
---------------------------

* You can create up to 10 applications in the same account. You can submit a ticket to apply for an increase in this quota.

  

* Currently, the multi-application service supports only **media upload, audio and video playback, media management, and callbacks** .

  

* The multi-application service implements isolation only at the metadata level, not at the physical storage level. Therefore, separate billing for each application is not supported. Physical isolation such as domain name isolation and storage isolation will be supported in the future.

  




Application management 
-------------------------------------------

* Application types

  After you activate the multi-application service, you can create custom applications. To ensure that the multi-application service is compatible with both new and existing resources, ApsaraVideo VOD provides the system default application. The default application cannot be deleted. The following table describes the two types of applications.
  

  | Application type |        Description         |                                                                                         Related resource                                                                                         |                                                                                      Permission                                                                                       |
  |------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | System           | System default application | All existing resources are in the system default application. If you do not specify an application when you create new resources, the new resources are also created in the default application. | To avoid impacts on your existing business, all the identity entities (RAM users or RAM roles) in your Alibaba cloud account have full permissions on the system default application. |
  | Custom           | Custom application         | Initially, no resources exist in custom applications. You can create new resources in custom applications. You can also migrate existing resources to custom applications.                       | Identity entities in your Alibaba Cloud account can access the resources in an application only after the identity entities are granted the access permissions.                       |

  

* Application IDs

  * The ID of the system default application is `app-1000000`.

    
  
  * The IDs of custom applications are in the `app-xxxxxxx` format.

    
  

  
  **Note**

  You can call the [ListAppInfo](/intl.en-US/API Reference/Multi-application service/Application management/ListAppInfo.md) operation to query the IDs of applications that you are authorized to access.
  

* Management

  You can call API operations of the multi-application service to create, query, update, and delete applications. For more information, see the "Multi-application service" section in [List of operations by function](/intl.en-US/API Reference/List of operations by function.md). The multi-application service will be available in the ApsaraVideo VOD console.
  




Accounts and permissions 
---------------------------------------------

Accounts in Alibaba Cloud include Alibaba Cloud accounts, RAM users, and RAM roles. You can grant the access permissions on an application to a specified identity entity (RAM user or RAM role).

* Policies

  ApsaraVideo VOD provides the following policies to grant permissions to identity entities.
  

  |          Policy           |                               Description                                |       Scope        |                                                              Operation permission                                                              |
  |---------------------------|--------------------------------------------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
  | VODAppAdministratorAccess | Grants all permissions of the application administrator                  | All applications   | Permissions to manage all applications in the Alibaba Cloud account and all resources in the applications                                      |
  | VODAppFullAccess          | Grants permissions to manage all resources in a specified application    | Single application | Permissions to manage all resources in a specified application                                                                                 |
  | VODAppReadOnlyAccess      | Grants read-only permissions on all resources in a specified application | Single application | Permissions on read operations on all resources in a specified application, such as operations that start with Get, Describe, Search, and List |

  

* Permissions of Alibaba Cloud accounts

  An Alibaba Cloud account has all the permissions of the application administrator (VODAppAdministratorAccess). The permissions of an Alibaba Cloud account cannot be changed. For example, you cannot revoke the permissions of the Alibaba Cloud account on an application. The application administrator has the following permissions:
  * Create, delete, modify, and query all applications in the Alibaba Cloud account.

    
  
  * Create, delete, modify, and query all resources, configurations, and data in each application.

    
  
  * Grant permissions to identity entities (RAM users or RAM roles) in the Alibaba Cloud account or revoke these permissions. However, the application administrator cannot revoke its own permissions.

    
  

  

* Permissions of RAM users or RAM roles

  Before a RAM user or role can use the multi-application service, the Alibaba Cloud account of the RAM user or role must grant the **VODFullAccess** permission to the RAM user or role in the [RAM](https://ram.console.aliyun.com/users) console. To grant finer-grained permissions on resources in ApsaraVideo VOD, you must use the multi-application service. The permissions of an identity entity are an **intersection** of RAM permissions and the permissions granted by the multi-application service in ApsaraVideo VOD.
  

*
  * To ensure that the multi-application service is compatible with both new and existing resources, all RAM users and RAM roles have the VODAppFullAccess permission on the system default application. The application administrator can revoke or re-grant the permission.

    
  
  * A RAM user or role can query the applications that the RAM user or role is authorized to access. After the RAM user or role is granted permissions on an application, the RAM user or role can perform related operations on resources such as media and callbacks in this application.

    
  
  * If a RAM user or role is granted the VODAppAdministratorAccess permission of the application administrator, the RAM user or role can manage all applications and resources in the Alibaba Cloud account.

    
  
  * To migrate resources between two applications, a RAM user or role must have the read and write permissions on both applications.

    
  

  

* Authorization method

  You can call API operations to grant permissions on applications to identity entities or revoke the permissions. For more information, see the "Multi-application service" section in [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).
  



