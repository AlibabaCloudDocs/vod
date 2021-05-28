Access control 
===================================

ApsaraVideo VOD allows you to configure the blacklists or whitelists of Referer, IP address, and User-Agent. ApsaraVideo VOD also limits the number of URL access and unique IP addresses. This topic describes access control in detail.

Overview 
-----------------------------

The access control service allows you to configure access policies in the cloud to provide basic protection for video resources. The access control service has a low threshold and takes effect in a short period of time. Only cloud configurations do not require additional development. The common access control policies include:

* Referer: the [Referer blacklist or whitelist](#section-nyj-pri-0pv).

  

* User-Agent: the [User-Agent blacklist or whitelist](#section-xkt-yqz-a0e).

  

* IP address: the [IP address blacklist or whitelist](#section-kc9-uzf-smn).

  

* Limits on the number of access times: the [maximum number of times that a video URL can be accessed in a specific period and the maximum number of unique IP addresses that are granted access to the video URL after deduplication](#section-cxj-uj2-rod).

  



**Note**

**User-Agent** and **Limits on the number of access times** are complicated and prone to misoperations. You cannot configure these access control policies in the ApsaraVideo VOD console. If you want to configure these policies,submit [a ticket](https://workorder.console.aliyun.com/console.htm#/ticket/add?productCode=vod&commonQuestionId=561&isSmart=true&iatraceid=1606446020666-2b842b67ddd84da10488b6&channel=selfservice) or contact the Alibaba Cloud technical support.

Referer blacklist or whitelist 
---------------------------------------------------

* Overview

  * Referer is used to track and identify where requests come from based on the HTTP Referer mechanism. You can configure a Referer blacklist or whitelist to identify and filter users. This mechanism limits access to CDN resources and improves CDN security.

    
  
  * A Referer whitelist or a Referer blacklist is supported. After a user sends a request to a CDN node, the node authenticates the user identity based on the preset Referer whitelist or blacklist. If a request meets the rules, video data is returned. If a request does not meet the rules, the request is denied and HTTP status code 403 is returned.

    
  
  * After you configure a Referer blacklist or whitelist, wildcard domain names are automatically supported. For example, if you enter a.com, the actual configuration \*.a.com takes effect. This means that all subdomains take effect.

    
  
  * Typically, mobile terminals cannot obtain the Referer header. By default, access requests that exclude the Referer header are allowed. You can choose to disable the access from requests that exclude the Referer header.

    
  

  

  For more information, see [Hotlink protection](/intl.en-US/User Guide/Domain management/Access control/Hotlink protection.md).
  

* Examples

  Set the Referer whitelist of the vod-test1.cn-shanghai.aliyuncs.com domain name in ApsaraVideo VOD to aliyun.com. Disable the access from requests that exclude the Referer header. Construct the following request:

      curl -i 'http://vod-test1.cn-shanghai.aliyuncs.com/sv/5101d1f8-1643f9ab241/5101d1f8-1643f9ab241.mp4'

  

* Responses

  ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3230401161/p178325.png)

  After you add the Referer that matches the whitelist to the request,Rthe access is allowed.

      curl -i 'http://vod-test1.cn-shanghai.aliyuncs.com/sv/5101d1f8-1643f9ab241/5101d1f8-1643f9ab241.mp4' \
      -H 'Referer: http://www.aliyun.com' 

  




User-Agent blacklist or whitelist 
------------------------------------------------------

* Overview

  User-Agent is a special string header. It helps the server identify the operating system type and version, CPU type, browser type and version, browser rendering engine, language, and plug-in that are used by users. You can configure a User-Agent blacklist or whitelist to control access from specific browsers or terminals.
  




<!-- -->

* Examples

  * User-Agent header for Internet Explorer 9.0 on a Windows PC:

        User-Agent:Mozilla/5.0(compatible;MSIE9.0;WindowsNT6.1;Trident/5.0;

    
  
  * Simulate the following HTTP request for verification:

        curl -i 'http://vod-test1.cn-shanghai.aliyuncs.com/sv/5101d1f8-1643f9ab241/5101d1f8-1643f9ab241.mp4' \
        -H 'User-Agent: iPhone OS;MI 5'

    
  

  




IP address blacklist or whitelist 
------------------------------------------------------

ApsaraVideo VOD allows you to configure an IP address blacklist or whitelist to deny or allow access only from specific IP addresses.

* You can add a list of IP addresses or a CIDR block

  such as `127.0.0.1/24` to the IP address blacklist or whitelist. 24 indicates that the first 24 bits are the mask to represent the part of the network portion of the address. The remaining ^8^ bits are host bits. The subnet can accommodate 254 hosts. Therefore, the IP address is from 127.0.0.1 to 127.0.0.255.
  

* You can choose whether to preferentially use remote_addr or X-Forwarded-For to determine the IP address of origin for requests. You can also use both remote_addr and X-Forwarded-For (XFF).

  




For more information, see [IP address blacklist or whitelist](/intl.en-US/User Guide/Domain management/Access control/IP address blacklist or whitelist.md).

Limits on the number of access times and the number of unique IP addresses 
-----------------------------------------------------------------------------------------------

ApsaraVideo VOD allows you to configure the maximum number of times that media resources can be accessed in a specific period such as one day and the maximum number of unique IP addresses that are granted access to media resources. The core principle is that all requests are sent to the centralized access count service for verification. The access count service checks whether the specified threshold is exceeded. If the specified threshold is exceeded, the access count service rejects a request and returns HTTP status code 403.

* The limits are imposed on access to a URL that contains the file URL and signature information. The limits are not imposed on access to a file. However, you can configure the system to ignore some parameters in URLs. The limit on threshold values can be separately specified for each domain name.

  

* The access count service is a centralized service deployed across multiple regions. Access requests to a URL are dispatched to only one of the regions to ensure centralized counting.

  

* After a CDN edge node receives a request, the CDN edge node accesses the centralized access count service for counting and verification.

  




Summary 
----------------------------

* The access control service requires only simple configuration, which makes it easy to use. The access control service can provide basic protection, especially for access from web browsers.

  

* Referer and User-Agent are common HTTP headers, which are prone to forgery and have low security.

  

* IP address access control and limits on the number of access times hinder the distribution of content to a large number of consumers. Therefore, IP address access control and limits on the number of access times are unsuitable for widespread content consumption. Additionally, illegal access may still occur even when the limit on threshold values are not exceeded.

  



