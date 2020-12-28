Parameter pass-through for HLS encryption 
==============================================================

If you want to implement encrypted playback, you can enable parameter pass-through for HTTP Live Streaming (HLS) encryption. This topic introduces the parameter pass-through for HLS encryption feature and describes how to enable this feature.

Overview 
-----------------------------

**Parameter pass-through for HLS encryption** allows you to enable HLS encryption and rewrite M3U8 files. After you enable HLS encryption, you can add a custom parameter name to the M3U8 file. The custom parameter name must be the same as that in client requests. If you do not customize a parameter name, the parameter name `MtsHlsUriToken` is used by default.

To rewrite the M3U8 file for HLS encryption, Alibaba Cloud CDN rewrites the `#EXT-X-KEY` tag in the M3U8 file. After the `#EXT-X-KEY` tag is rewritten, the specified parameter name and value are added to the end of the URI attribute in the tag. Client requests contain the parameter name and value.

Procedure 
------------------------------

1. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

   

2. In the left-side navigation pane of the ApsaraVideo VOD console, find **Configuration Management** .

   

3. Choose **CDN Configuration \> Domain Names** to go to the Domain Names page.

   

4. Find the required domain and click **Configure** .

   ![Select a domain](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7583888061/p181835.png)
   

5. Click **Video Related** and turn on **Parameter Pass-through for HLS Encryption** **.** 

   ![HLS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1939319061/p181836.png)
   **Note**

   After you enable parameter pass-through for HLS encryption, the `MtsHlsUriToken` parameter will be overwritten in decryption requests when users attempt to play HLS-encrypted videos **.**

   




Example 
----------------------------

After you enable **parameter pass-through for HLS encryption** in the ApsaraVideo VOD console, the parameter name `MtsHlsUriToken` is used by default.

A client request contains the `MtsHlsUriToken` parameter. The value of this parameter is `test`. To decrypt the M3U8 file, Alibaba Cloud CDN adds `MtsHlsUriToken=test` to the end of the URI attribute in the `#EXT-X-KEY` tag.
**Notice**

Alibaba Cloud Gov Cloud does not support parameter pass-through for HLS encryption.
