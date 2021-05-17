VOD CDN 
============================

This topic provides examples on how to use the API operations of the VOD CDN module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to preload and refresh caches, query the refresh and preload statuses, query traffic data and network bandwidth, and query the logs of domain names. You can also query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Preload caches {#h2--div-id-preloadvodobjectcaches-div-2}
---------------------------------------------------------

You can call the PreloadVodObjectCaches operation to preload caches.

For more information about the request and response parameters of this operation, see [PreloadVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/PreloadVodObjectCaches.md). Example:

    from aliyunsdkvod.request.v20170321 import PreloadVodObjectCachesRequest
    def preload_object_caches(clt):
        request = PreloadVodObjectCachesRequest.PreloadVodObjectCachesRequest()
        objectPath = ['http://192.168.0.0/16/fd.mp4',
                      'http://192.168.0.0/16/ld.mp4']
        request.set_ObjectPath("\n".join(objectPath))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = preload_object_caches(clt)
        print(res['PreloadTaskId'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Refresh caches {#h2--div-id-refreshvodobjectcaches-div-3}
---------------------------------------------------------

You can call the RefreshVodObjectCaches operation to refresh caches.
For more information about the request and response parameters of this operation, see [RefreshVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/RefreshVodObjectCaches.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import RefreshVodObjectCachesRequest
    def refresh_object_caches(clt):
        request = RefreshVodObjectCachesRequest.RefreshVodObjectCachesRequest()
        objectPath = ['http://192.168.0.0/16/fd.mp4',
                      'http://192.168.0.0/16/ld.mp4']
        request.set_ObjectPath("\n".join(objectPath))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = refresh_object_caches(clt)
        print(res['RefreshTaskId'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the refresh and preload statuses {#h2--div-id-describevodrefreshtasks-div-4}
----------------------------------------------------------------------------------

You can call the DescribeVodRefreshTasks operation to query the refresh and preload statuses.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshTasks](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshTasks.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DescribeVodRefreshTasksRequest
    def describe_refresh_task(clt):
        request = DescribeVodRefreshTasksRequest.DescribeVodRefreshTasksRequest()
        request.set_DomainName('test.com')
        request.set_ObjectType('preload')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = describe_refresh_task(clt)
        print(res['Tasks']['Task'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations {#h2--div-id-describevodrefreshquota-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------

You can call the DescribeVodRefreshQuota operation to query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshQuota](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshQuota.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DescribeVodRefreshQuotaRequest
    def describe_refresh_quota(clt):
        request = DescribeVodRefreshQuotaRequest.DescribeVodRefreshQuotaRequest()
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = describe_refresh_quota(clt)
        print(res['PreloadRemain'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query traffic data {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------------------

You can call the DescribeVodDomainTrafficData operation to query traffic data.
For more information about the request and response parameters of this operation, see [DescribeVodDomainTrafficData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainTrafficData.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DescribeVodDomainTrafficDataRequest
    def describe_domain_traffic_data(clt):
        request = DescribeVodDomainTrafficDataRequest.DescribeVodDomainTrafficDataRequest()
        request.set_DomainName("example.test.com")
        request.set_StartTime("2019-01-15T15:59:59Z")
        request.set_EndTime("2019-01-20T15:59:58Z")
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = describe_domain_traffic_data(clt)
        print(res['TrafficDataPerInterval']['DataModule'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query network bandwidth {#h2--div-id-describevoddomainbpsdata-div-7}
--------------------------------------------------------------------

You can call the DescribeVodDomainBpsData operation to query network bandwidth.
For more information about the request and response parameters of this operation, see [DescribeVodDomainBpsData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainBpsData.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DescribeVodDomainBpsDataRequest
    def describe_domain_bps_data(clt):
        request = DescribeVodDomainBpsDataRequest.DescribeVodDomainBpsDataRequest()
        request.set_DomainName("example.test.com")
        request.set_StartTime("2019-01-15T15:59:59Z")
        request.set_EndTime("2019-01-20T15:59:58Z")
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = describe_domain_bps_data(clt)
        print(res['BpsDataPerInterval']['DataModule'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the logs of a domain name {#h2--div-id-describevoddomainlog-div-8}
------------------------------------------------------------------------

You can call the DescribeVodDomainLog operation to query the logs of a domain name.
For more information about the request and response parameters of this operation, see [DescribeVodDomainLog](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Log management/DescribeVodDomainLog.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DescribeVodDomainLogRequest
    def describe_domain_log(clt):
        request = DescribeVodDomainLogRequest.DescribeVodDomainLogRequest()
        request.set_DomainName("example.test.com")
        request.set_StartTime("2019-01-15T15:59:59Z")
        request.set_EndTime("2019-01-20T15:59:58Z")
        request.set_PageNumber(1)
        request.set_PageSize(300)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = describe_domain_log(clt)
        logDetail = res['DomainLogDetails']['DomainLogDetail'][0]
        print("TotalLogCount: %s" % (logDetail['PageInfos']['Total']))
        print(logDetail['LogInfos']['LogInfoDetail'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


