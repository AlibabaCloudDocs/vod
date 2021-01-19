Overview 
=============================

ApsaraVideo VOD authenticates the identities of users who initiate requests and determines whether the users have the required permissions based on AccessKey pairs. ApsaraVideo VOD supports authorization by using AccessKey pairs of Alibaba Cloud accounts, AccessKey pairs of RAM users, and STS temporary AccessKey pairs. This topic compares these three authorization methods and describes the system policies provided by Alibaba Cloud.

Authentication of account permissions 
----------------------------------------------------------

You can access ApsaraVideo VOD by using the [RESTful APIs](/intl.en-US/API Reference/API overview.md) or [SDKs](/intl.en-US/SDK Downloads/SDK download.md) (including the APIs and upload, playback, and short video SDKs) provided by ApsaraVideo VOD.

For each request, ApsaraVideo VOD authenticates the identity of the user based on the current operation to check whether the user has the required permissions. AccessKey pairs are used in user identity authentication.

Terms 
--------------------------

* RAM

  Resource Access Management (RAM) is a service provided by Alibaba Cloud that allows you to manage user identities and control access to your resources. For more information, see [What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md)
  **Note**

  The RAM service isolates and manages permissions rather than resources. RAM users are subordinate to Alibaba Cloud accounts and do not own actual resources. All resources belong only to Alibaba Cloud accounts. To implement resource isolation, you can use the multi-application service in ApsaraVideo VOD. For more information, see [Overview]().
  

* Alibaba Cloud account

  Alibaba Cloud accounts are owners of Alibaba Cloud resources. Alibaba Cloud accounts are charged for all of the resources that they own and have full control over the resources.
  

* RAM user

  RAM users are created under Alibaba Cloud accounts. Each RAM user under an Alibaba Cloud account has its own AccessKey pair and can perform authorized operations in the same way as the Alibaba Cloud account. A RAM user can be considered as a user who has specific operation permissions.
  

* role

  Roles are identities to which permission policies are attached. Roles do not have logon passwords or AccessKey pairs. A RAM user can assume roles. When a RAM user assumes a role, permissions of the role are granted to the RAM user.
  **Note**

  The relationship between RAM users and their roles is similar to the relationship between individuals and their identities. For example, the roles of a person may be an employee at work and a father at home. A person may play different roles in different scenarios. When a person plays a specific role, the person has the permissions of that role. A role is not an operational entity. It is a complete operational entity only after it is assumed by a user.

  Furthermore, a role can be assumed by multiple users at the same time. The user who assumes a role is automatically assigned all of the permissions of the role.
  

* RAM policy

  A RAM policy is a set of permissions that are described based on the policy structure and syntax. You can use policies to describe the authorized resource sets, authorized operation sets, and authorization conditions. You can configure RAM policies and grant specific permissions to users or user groups to control their access to resources or services in your account. For example, you can limit the permissions of users to only upload, play, or audit permissions.
  




For more terms about access control, see [Terms](/intl.en-US/Product Introduction/Terms.md).

AccessKey pairs 
------------------------------------

An AccessKey pair consists of an AccessKey ID and an AccessKey secret. The AccessKey pair is used to authenticate access identities. ApsaraVideo VOD uses AccessKey pairs to implement symmetric encryption and identity authentication.

* AccessKey ID: used to identify users.

  

* AccessKey secret: used to encrypt and verify signature strings. You must keep your AccessKey secret confidential.

  

* AccessKey pair: consists of an AccessKey ID and an AccessKey secret.

  




The following three types of AccessKey pairs are available for use in ApsaraVideo VOD:

* AccessKey pairs of Alibaba Cloud accounts

  AccessKey pairs of Alibaba Cloud accounts are AccessKey pairs of accounts that activate the ApsaraVideo VOD service or accounts registered with Alibaba Cloud. The AccessKey pair of each Alibaba Cloud account has all of the permissions on resources owned by the account. Each Alibaba Cloud account can have up to five enabled or disabled AccessKey pairs.

  You can apply to add or delete your AccessKey pairs in the [Alibaba Cloud Management Console](https://ak-console.aliyun.com/?#/accesskey). Each AccessKey pair may be in the enabled or disabled state. Only enabled AccessKey pairs can be used for identity authentication.
  **Warning**

  AccessKey pairs of Alibaba Cloud accounts have full permissions and carry high risks for data leaks if it is disclosed. Therefore, we recommend that you do not use AccessKey pairs of Alibaba Cloud accounts to access ApsaraVideo VOD.
  

* AccessKey pairs of RAM users

  RAM is a resource access control service provided by Alibaba Cloud. AccessKey pairs of RAM users are authorized in RAM. They can be used to access ApsaraVideo VOD resources only based on the rules defined by RAM. You can use RAM to manage users such as employees, systems, and applications, and control the permissions of users to access your resources. For example, you can use RAM to grant only the video playback permission to the users. A RAM user belongs to the Alibaba Cloud account under which it was created and does not actually own any resources. All resources belong to the corresponding Alibaba Cloud account.

  You can log on to the [RAM console](https://ram.console.aliyun.com/#/user/list) to create RAM users, obtain AccessKey pairs, and grant permissions to the RAM users.
  




<!-- -->

* STS temporary AccessKey pairs

  Security Token Service (STS) is an Alibaba Cloud service that provides temporary access credentials. An STS temporary AccessKey pair is an AccessKey pair that is issued by STS temporarily for the duration of a validity period. STS temporary AccessKey pairs can be used to access ApsaraVideo VOD resources only based on the rules defined by STS and expire after the specified validity period ends.
  




Comparison of the authentication methods 
-------------------------------------------------------------



|           Authentication method           |   Risk    |                        Permission                        |                Validity                |                                                                                                                                             Scenario                                                                                                                                              |
|-------------------------------------------|-----------|----------------------------------------------------------|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AccessKey pairs of Alibaba Cloud accounts | Very high | Permissions on managing all resources in ApsaraVideo VOD | Always valid after being enabled       | AccessKey pairs of Alibaba Cloud accounts can be used by the super administrator to perform operations. We do not recommend that you use these AccessKey pairs in programs, especially on clients.                                                                                                |
| AccessKey pairs of RAM users              | High      | Permissions granted based on policies                    | Always valid after being enabled       | The AccessKey pairs of RAM users are used to authorize specific upload, playback, and management operations. You can create multiple spare RAM users in case of AccessKey pair leaks (for example, when the RAM user resigns). We recommend that you use AccessKey pairs of RAM users on servers. |
| STS temporary AccessKey pairs             | Secure    | Permissions granted based on policies                    | Valid until the custom expiration time | STS temporary AccessKey pairs can be used on mobile or web terminals. You must deploy servers to generate STS temporary AccessKey pairs.                                                                                                                                                          |



In addition to the preceding authentication methods, you can also use upload credentials and playback credentials to handle authorization and security issues during media upload and playback. For a comparison between credentials and STS, see [Comparison between upload (playback) credentials and STS](/intl.en-US/Developer Guide/Access authorization/Comparison between upload (playback) credentials and STS.md).

System policies 
------------------------------------

ApsaraVideo VOD provides four system policies to authorize RAM users or STS accounts.


|         Policy          |                                                     Description                                                     |                                                                                                                                                                                                                              Operation permission                                                                                                                                                                                                                               |
|-------------------------|---------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AliyunVODFullAccess     | Grants permissions to manage all resources in ApsaraVideo VOD                                                       | All operations in ApsaraVideo VOD                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| AliyunVODReadOnlyAccess | Grants read-only permissions on all resources in ApsaraVideo VOD                                                    | All read operations in ApsaraVideo VOD, such as those starting with Get, Describe, Search, and List                                                                                                                                                                                                                                                                                                                                                                             |
| AliyunVODPlayAuth       | Grants permissions to play videos in ApsaraVideo VOD by using playback SDKs or calling playback-related operations  | Playback operations: * [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md)   * [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md)   * [GetVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md)    |
| AliyunVODUploadAuth     | Grants permissions to upload resources in ApsaraVideo VOD by using upload SDKs or calling upload-related operations | Upload operations: * [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md)   * [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md)   * [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md)           |


