点播CDN 
==========================

本篇文档提供了Python SDK点播CDN模块相关功能的API调用示例。包含预热缓存、刷新缓存、查询刷新和预热状态、查询刷新预热次数限制和余量、查询流量数据、查询网络带宽、下载域名日志。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/Python SDK/初始化.md)。

预热缓存 {#h2--div-id-preloadvodobjectcaches-div-2}
-----------------------------------------------

调用PreloadVodObjectCaches接口，完成预热缓存功能。

接口参数和返回字段请参见[PreloadVodObjectCaches](/intl.zh-CN/服务端API/点播CDN/刷新预热/预热缓存.md)。调用示例如下：

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



刷新缓存 {#h2--div-id-refreshvodobjectcaches-div-3}
-----------------------------------------------

调用RefreshVodObjectCaches接口，完成刷新缓存功能。
接口参数和返回字段请参见[RefreshVodObjectCaches](/intl.zh-CN/服务端API/点播CDN/刷新预热/刷新缓存.md)。调用示例如下： 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



查询刷新和预热状态 {#h2--div-id-describevodrefreshtasks-div-4}
-----------------------------------------------------

调用DescribeVodRefreshTasks接口，完成查询刷新和预热状态功能。
接口参数和返回字段请参见[DescribeVodRefreshTasks](/intl.zh-CN/服务端API/点播CDN/刷新预热/查询刷新和预热状态.md)。调用示例如下： 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



查询刷新预热次数限制和余量 {#h2--div-id-describevodrefreshquota-div-5}
---------------------------------------------------------

调用DescribeVodRefreshQuota接口，完成查询刷新预热次数限制和余量功能。
接口参数和返回字段请参见[DescribeVodRefreshQuota](/intl.zh-CN/服务端API/点播CDN/刷新预热/查询刷新预热次数限制和余量.md)。调用示例如下： 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



查询流量数据 {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------

调用DescribeVodDomainTrafficData接口，完成查询流量数据功能。
接口参数和返回字段请参见[DescribeVodDomainTrafficData](/intl.zh-CN/服务端API/点播CDN/数据监控/查询流量数据.md)。调用示例如下： 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



查询网络带宽 {#h2--div-id-describevoddomainbpsdata-div-7}
---------------------------------------------------

调用DescribeVodDomainBpsData接口，完成查询网络带宽功能。
接口参数和返回字段请参见[DescribeVodDomainBpsData](/intl.zh-CN/服务端API/点播CDN/数据监控/查询网络带宽.md)。调用示例如下： 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



下载域名日志 {#h2--div-id-describevoddomainlog-div-8}
-----------------------------------------------

调用DescribeVodDomainLog接口，完成下载域名日志功能。
接口参数和返回字段请参见[DescribeVodDomainLog](/intl.zh-CN/服务端API/点播CDN/日志管理/下载域名日志.md)。调用示例如下： 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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


