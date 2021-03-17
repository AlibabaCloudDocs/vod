Request syntax 
===================================

This topic describes the request syntax of the ApsaraVideo VOD API.

Endpoints 
------------------------------

The endpoint for the ApsaraVideo VOD API is `vod.{ApiRegion}.aliyuncs.com.`
**Note**

Replace {ApiRegion} with the ID of the region where the ApsaraVideo VOD API is used. For example, if the region is China (Shanghai), set the ID to `cn-shanghai`. In this case, the endpoint is `vod.cn-shanghai.aliyuncs.com`. If the region is Singapore, set the ID to `ap-southeast-1`. In this case, the endpoint is `vod.ap-southeast-1.aliyuncs.com`. For more information, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md).

Communication protocols 
--------------------------------------------

You can send requests by using the HTTP or HTTPS protocol. For a higher level of security, we recommend that you send requests by using the HTTPS protocol.

Request methods 
------------------------------------

You can use the HTTP GET method to send requests. If the HTTP GET method is applied, you must include request parameters in each request URL.

Request parameters 
---------------------------------------

In each request, you must set the Action parameter that specifies the operation that you want to perform, common parameters, and operation-specific parameters.

Character encoding 
---------------------------------------

Requests and responses are encoded in UTF-8.
