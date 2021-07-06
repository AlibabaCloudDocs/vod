Verify the ownership of a domain name 
==========================================================

When you add a domain name to the ApsaraVideo VOD console for the first time, you must verify the ownership of the domain name. This ensures that the domain name is added only by the owner. If a domain name that belongs to User A is added to the ApsaraVideo VOD console by User B, conflicts and security issues may occur. If you pass the verification, ApsaraVideo VOD identifies you as the owner of the domain name.In this case, if you add the domain name to the ApsaraVideo VOD console again or add its subdomain names to the ApsaraVideo VOD console, no ownership verification is required. 

Verification methods 
-----------------------------------------

1. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/#/domain/list).

   

2. In the left-side navigation pane, choose **Configuration Management \> CDN Configuration \> Domain Names** . On the Domain Names page, click Add Domain Name.

   

3. After you set the parameters that are required for adding a domain name, click **Submit** . The following page on which you can verify the ownership of the domain name appears. 

   ApsaraVideo VOD allows you to use a Domain Name System (DNS) record or a verification file to verify the ownership of a domain name. You can choose one of the methods to complete ownership verification. After you pass the verification, the domain name is successfully added.![Verification page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9704655261/p275334.png)
   




Method 1: Use a DNS record to verify the ownership (Recommended) 
-------------------------------------------------------------------------------------

In the following examples, `a.com` is used to show how to verify the ownership of a domain name. 

1. On the verification page, click the **Method 1: DNS Settings** tab. 

   The system automatically recognizes the record type, host, and record value. Do not close the verification page before the verification is complete. 
   **Note**

   You can also call the [AddVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/AddVodDomain.md) operation to add a domain name. Before that, you must call the [DescribeVodVerifyContent](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name verification/DescribeVodVerifyContent.md) operation to obtain the record value and then perform the operations in Step 2 to add a DNS record in the TXT format.[AddVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/AddVodDomain.md)

   ![Method 1: DNS Settings tab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9704655261/p275382.png)
   

2. In the system of your DNS service provider, add a DNS record in the TXT format for the domain name. 

   In this example, the Alibaba Cloud DNS console is used to show how to add a DNS record in the TXT format. You can add a DNS record in the TXT format at other DNS service providers such as DNSPod of Tencent Cloud and Xinnet in a similar way. 
   1. Log on to the [Alibaba Cloud DNS console](https://dns.console.aliyun.com/#/dns/domainList).

      
   
   2. On the **Manage DNS** page, find the `a.com` domain name and click **Configure** in the Actions column.

      
   
   3. Click **Add Record** .

      
   
   4. Specify the record type, host, and record value that are automatically generated in [Step 1](#p-o7x-m8r-xys). Click **Confirm** . 

      ![Add Record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9704655261/p275367.png)
      
   

   

3. After the DNS record in the TXT format takes effect, log on to the ApsaraVideo VOD console. Click **Verify** to complete the verification. 

   If the system prompts that the domain name fails the verification, check whether the DNS record in the TXT format is valid. Wait for the DNS record to take effect and try again.
   




Method 2: Upload a verification file to verify the ownership 
---------------------------------------------------------------------------------

In the following examples, `a.com` is used to show how to verify the ownership of a domain name. 

1. On the verification page, click the **Method 2: Verification File** tab. 

   Do not close the verification page before the verification is complete.![Method 2: Verification File tab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9704655261/p275385.png)
   

2. Click **verification.html** to download the verification file of the domain name. 

   **Note**

   You can call the [DescribeVodVerifyContent](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name verification/DescribeVodVerifyContent.md) operation to generate verification strings in the verification.html file. You can also call the [AddVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/AddVodDomain.md) operation to add a domain name. Before that, you must call the [DescribeVodVerifyContent](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name verification/DescribeVodVerifyContent.md) operation to obtain verification strings, create a `verification.html` file that contains the verification strings, and then perform the operations in Step 3 to upload the verification.html file.[AddVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/AddVodDomain.md)
   

3. Upload the verification file to the root directory on the origin server of the domain name. The origin server can be an Elastic Compute Service (ECS) instance, an Object Storage Service (OSS) bucket, a Cloud Virtual Machine (CVM) instance, a Container-Optimized OS (COS) instance, or an Elastic Compute Cloud (EC2) instance. 

   After you upload the verification file, Alibaba Cloud CDN visits the origin server at `http://a.com/verification.html` to obtain the verification file. Then, Alibaba Cloud CDN determines whether you have uploaded the verification file as required. Make sure that the verification file is accessible.
   

4. Click **Verify** to complete the verification.

   






FAQ 
------------------------

The following issues may occur when you add a domain name to the ApsaraVideo VOD console:

* Q: Why does ApsaraVideo VOD verify the ownership of domain names?
  

  A: The ownership verification is required to ensure that a domain name is added only by its owner. If a domain name of User A is added to the ApsaraVideo VOD console by User B, conflicts and security issues may occur.
  

* Q: I have multiple Alibaba Cloud accounts. Do I need to pass ownership verification for each account that I use to add a domain name to the ApsaraVideo VOD console for the first time?
  

  A: Yes. Each Alibaba Cloud account is identified as an independent user. When you use an account to add a domain name to the ApsaraVideo VOD for the first time, the account must pass ownership verification.
  

* Q: After a domain name passes ownership verification by adding a DNS record or uploading a verification file, can I delete the record or file?
  

  A: Yes. The required DNS record or verification file is only used for ownership verification. After you pass ownership verification, you can delete the record or file.
  

* Q: Do I need to verify the ownership of a domain name that has been added to Alibaba Cloud CDN?
  

  A: No. For example, you have added the b.a.com domain name to Alibaba Cloud CDN and the canonical domain name that is assigned to the domain name works as expected. In this case, you are deemed to own the a.com domain name. When you add the subdomain names of a.com, such as xx.a.com and xxx.a.com, you do not need to perform ownership verification.
  

* Q: Do I need to verify the ownership of a domain name if I call the AddVodDomain operation to add the domain name to the ApsaraVideo VOD console?
  

  A: Yes, you must verify the ownership of the domain name in this case. You can choose to use a DNS record or a verification file to complete the ownership verification, which is similar to the ownership verification in the ApsaraVideo VOD console. You can add a DNS record or upload the required verification file to the root directory of the origin server of your domain name. Then, you can call the AddVodDomain operation to add the domain name.
  

* Q: What can I do if I am unable to verify the ownership of a domain name by adding a DNS record or uploading the verification file to the origin server?
  

  A: To address this issue, you can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex). In the ticket, provide the reason why you are unable to verify the ownership of a domain name by using the given methods, and include the information that can be used to identify you as the owner of the domain name. Then, wait for Alibaba Cloud to perform manual verification.
  




Related API operations 
-------------------------------------------

* [VerifyVodDomainOwner](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name verification/VerifyVodDomainOwner.md): verifies the ownership of a specified domain name.

  

* [DescribeVodVerifyContent](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name verification/DescribeVodVerifyContent.md): queries the ownership verification content.

  



