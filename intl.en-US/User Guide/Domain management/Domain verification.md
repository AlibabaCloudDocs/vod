# Domain verification

ApsaraVideo VOD allows you to accelerate website content delivery by using Alibaba Cloud CDN. This topic describes the verification procedure for domain names and related limits. Before you add a domain name to Alibaba Cloud CDN, you must ensure that the domain name meets the relevant compliance requirements. This prevents losses that can be caused by noncompliance.

## Verification procedure

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0026319061/p172505.png)

1.  Log on to the [Alibaba Cloud official website](https://account.console.aliyun.com/?spm=a2c4g.11186623.2.11.252241abqbKiGM#/auth/home). In the left-side navigation pane of the Account Management console, click **Real-name Verification**. On the Real-name Verification page, complete the real-name verification as prompted.

2.  Apply for an Internet content provider \(ICP\) license from the Ministry of Industry and Information Technology \(MIIT\) of China. We recommend that you use the [Alibaba Cloud ICP Filing system](https://beian.aliyun.com/?spm=5176.8142029.388261.3.a0SCC3).

3.  Review the content saved on the origin server of the domain name for CDN. To be exempt from content review, you can specify an Object Storage Service \(OSS\) bucket or a bucket provided by ApsaraVideo VOD as the origin server. If your origin server is not deployed on Alibaba Cloud, submit a [ticket](https://selfservice.console.aliyun.com/ticket/createIndex).

4.  Add a canonical name \(CNAME\) record for your domain name at the DNS service provider. This ensures that your domain name is mapped to the CNAME that is allocated by CDN. For more information, see [Configure a CNAME record]().


**Note:**

-   If your origin server is deployed on ECS, we recommend that you reserve at least 20% of your overall workloads for the server.
-   Make sure that the security software settings of the origin server allow the CDN cache nodes to access the origin server.
-   Make sure that all requests destined for an accelerated domain are sent back to the origin if the CDN service is stopped.
-   After a domain name is added to Alibaba Cloud CDN, you cannot use the domain name to access its resources until you add a CNAME record.

## Content moderation

All the content of domain names added to Alibaba Cloud must be reviewed. Domain names that cannot be added to Alibaba Cloud CDN include but are not limited to:

-   Content that is inaccessible or does not include valid information
-   Servers that host pirated games
-   Websites that provide multiplayer games and card games
-   Websites that provide downloads of pirated software
-   Websites that run P2P lending
-   Lottery websites
-   Websites of unlicensed hospitals and pharmaceuticals
-   Websites that contain content of pornography, drugs, or gambling

**Note:**

-   If the preceding content is detected from your domain name for CDN, you must bear all risks that may arise. Alibaba Cloud CDN regularly reviews the content of accelerated domain names. If illicit content is detected from a domain name, Alibaba Cloud CDN immediately disables or blocks the domain name. If the violation is severe, Alibaba Cloud CDN may even permanently block all domain names of the Alibaba Cloud account.
-   If you add a wildcard domain name, for example, `*.example.com`, to Alibaba Cloud CDN and a specific domain name, for example, `a.example.com` contains illicit content, Alibaba Cloud CDN disables the wildcard domain name \(`*.example.com`\).
-   If a domain name is rejected after the review, you can check the reason for the rejection on the Domain Names page in the Alibaba Cloud CDN console. You can modify the content based on the rejection details, and submit the domain name for review again.

## Quantity limits

|Item|Limit|
|:---|:----|
|Domain names|You can add a maximum of 50 domain names to Alibaba Cloud CDN for each Alibaba Cloud account. If the average daily peak bandwidth of your domain names exceeds 50 Mbit/s, you can [submit a ticket](https://workorder.console.aliyun.com/console.htm?lang=&accounttraceid=3c62958a-b7f1-4439-b87b-5f59ed3e9704#/ticket/add?productCode=cdn) to increase the quota of domain names. Make sure that the quota increase does not incur business risks.|
|IP addresses of origin servers|If the origin server of a domain name for CDN uses IP addresses, you can add a maximum of 10 IP addresses for each domain name for CDN.|
|Cache and refresh operations|-   URL refresh: 2,000 URLs per day for each Alibaba Cloud account.
-   Directory refresh: 100 directories per day for each Alibaba Cloud account. |

## Recycling rules of domain names

|Scenario|Action|Solution|
|:-------|:-----|:-------|
|An accelerated domain name has not been visited for more than 90 days. The domain name may run as expected during this period.|Alibaba Cloud CDN automatically disables the domain name but retains the related records.|Enable the domain name.|
|An accelerated domain name remains disabled for more than 120 days, including the days during which the domain name fails the content review.|Alibaba Cloud CDN automatically deletes the records of the domain name.|Add the domain name to Alibaba Cloud CDN again.|

