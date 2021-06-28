Configure CORS 
===================================

This topic describes how to configure cross-origin resource sharing (CORS) for playbacks that are performed by using the HTML5 player, Flash player, and Object Storage Service (OSS). 

Configure CORS for using the HTML5 player to play FLV and M3U8 videos 
------------------------------------------------------------------------------------------

If the following error message is returned, you need to enable CORS for the domain name for playback. 

    No 'Access-Control-Allow-Origin' header is present on the requested resource. 
    Origin 'http://localhost:9030' is therefore not allowed access. 



Add HTTP headers to enable CORS. For more information, see [Configure an HTTP header](/intl.en-US/User Guide/Domain management/Cache configuration/Configure an HTTP header.md). 

* Access-Control-Allow-Origin: specifies the domain name from which cross-origin requests are allowed. Set the value of the HTTP header to the domain name of the website on which videos are played. For example, if videos are played on the [https://www.aliyun.com](https://www.aliyun.com/) website, set the value to [https://www.aliyun.com](https://www.aliyun.com/). The following figure shows how to configure the Access-Control-Allow-Origin header.![Configure the Access-Control-Allow-Origin header](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2364784261/p271224.png)

  




<!-- -->

* Access-Control-Allow-Methods: specifies the allowed methods of the cross-origin requests. Valid values: POST and GET. If both POST and GET need to be allowed, separate them with a comma (,). The following figure shows how to configure the Access-Control-Allow-Methods header.![Configure the Access-Control-Allow-Methods header](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7132442261/p271225.png)

  



**Note**

If the URL of a media segment file and the URL of the M3U8 video belongs to different domain names, you need to configure the preceding HTTP headers for the domain name of the media segment file.

Configure CORS for the Flash player 
--------------------------------------------------------

If the error message in the following figure is returned, you need to first check whether an Internet content provider (ICP) filing is obtained and whether a CNAME is mapped to the domain name for playback. For more information, see [Domain verification](/intl.en-US/User Guide/Domain management/Domain verification.md) and [Configure a CNAME record in Alibaba Cloud DNS](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record in Alibaba Cloud DNS.md). 

![Error message of the Flash player](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7132442261/p271226.png)

If the domain name has an ICP filing and is mapped to a CNAME, you need to configure CORS. You can configure CORS by adding a cross-origin policy file named crossdomain.xml for the player. 

Add the file to the root directory of the domain name to which the video URL belongs. If the video to be played is stored in an OSS bucket, add the file to the root directory of the OSS bucket. 

If you are using ApsaraVideo VOD, ApsaraVideo VOD automatically adds the crossdomain.xml file after you activate the service. 

The following sample code shows the content of the crossdomain.xml file: 

    <?xml version="1.0" encoding="UTF-8"?>
    <cross-domain-policy>
        <allow-access-from domain="*"/>
        <allow-http-request-headers-from domain="*" headers="*" secure="false"/>
    </cross-domain-policy>


**Note**

If the URL of the thumbnail and the URL of the video belongs to different domain names, you need to add the crossdomain.xml file for the domain name of the thumbnail.

Configure CORS for playing videos that are stored in OSS 
-----------------------------------------------------------------------------

If you want the player to access the OSS bucket where videos are stored, you need to configure CORS for the OSS bucket. For more information, see [Configure CORS rules](/intl.en-US/Console User Guide/Manage buckets/Access control/Configure CORS rules.md) and [Configure CORS](/intl.en-US/Developer Guide/Buckets/Configure CORS.md). 

Set the following parameters to create a CORS rule: 

* **Sources** : Set the parameter to an asterisk (\*).

  

* **Allow Methods** : Valid values: GET, POST, PUT, DELETE, and HEAD.

  

* **Allowed Headers** : Set the parameter to an asterisk (\*).

  

* **Exposed Headers** : Set the parameter to ETag.

  





**Notice**

Specify this rule as the first of all CORS rules.

The following figure shows how to set the parameters to create a CORS rule.![Create a CORS rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7132442261/p271235.png)
