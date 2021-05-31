Initialization 
===================================

This topic describes how to initialize ApsaraVideo VOD SDK for PHP by using an AccessKey pair or a Security Token Service (STS) token.

Prerequisites 
----------------------------------

* An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.13.6f2f12574nF4oY&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). Real-name verification is completed. [ApsaraVideo VOD](https://www.alibabacloud.com/product/apsaravideo-for-vod?spm=a3c0i.7911826.6791778070.dnavproductmedia3.441914b3psWeWQ) is activated.

  

* An AccessKey pair is created to call ApsaraVideo VOD operations. You can create the AccessKey pair of your Alibaba Cloud account in the [User Management console](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Fak-console.aliyun.com%2F%3Fspm%3Da2c4g.11186623.2.16.6f2f12574nF4oY#/accesskey). Alternatively, you can create a RAM user in the [RAM console](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Fram.console.aliyun.com%2F%3Fspm%3Da2c4g.11186623.2.17.6f2f12574nF4oY#/user/list) and grant the RAM user the permissions on ApsaraVideo VOD. For more information, see [Create a RAM user and perform authorization](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

  




Initialize the SDK 
---------------------------------------

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and endpoints.md). For example, if you want to call the operations in the China (Shanghai) region, use `cn-shanghai`. 

* Use the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md) to initialize the SDK. Example: 

      require_once './aliyun-php-sdk/aliyun-php-sdk-core/Config.php';   // Assume that your source code file is stored in the same directory as aliyun-php-sdk.
      use vod\Request\V20170321 as vod;
      
      function initVodClient($accessKeyId, $accessKeySecret) {
          $regionId = 'cn-shanghai';  // The region where you want to call ApsaraVideo VOD operations.
          $profile = DefaultProfile::getProfile($regionId, $accessKeyId, $accessKeySecret);
          return new DefaultAcsClient($profile);
      }
                              

  

* Use an [STS token](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md) to initialize the SDK. Example:

      require_once './aliyun-php-sdk/aliyun-php-sdk-core/Config.php';   // Assume that your source code file is stored in the same directory as aliyun-php-sdk.
      use vod\Request\V20170321 as vod;
      
      function initVodClient($accessKeyId, $accessKeySecret, $securityToken) {
          $regionId = 'cn-shanghai';  // The region where you want to call ApsaraVideo VOD operations.
          $profile = DefaultProfile::getProfile($regionId, $accessKeyId, $accessKeySecret, $securityToken);
          return new DefaultAcsClient($profile);
      }
                              

  



**Notice**

If you fail to call ApsaraVideo VOD operations in other regions, update the aliyun-php-sdk-core SDK to version 1.3.8 or later, and the aliyun-php-sdk-vod SDK to version 2.15.1 or later.
