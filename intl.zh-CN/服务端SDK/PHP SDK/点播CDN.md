点播CDN 
==========================

本篇文档提供了PHP SDK点播CDN模块相关功能的API调用示例。包含预热缓存、刷新缓存、查询刷新和预热状态、查询刷新预热次数限制和余量、查询流量数据、查询网络带宽、下载域名日志。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/PHP SDK/安装SDK/初始化.md)。

预热缓存 {#h2--div-id-preloadvodobjectcaches-div-2}
-----------------------------------------------

调用PreloadVodObjectCaches接口，完成预热缓存功能。

接口参数和返回字段请参见[PreloadVodObjectCaches](/intl.zh-CN/服务端API/点播CDN/刷新预热/预热缓存.md)。调用示例如下：

    function preloadVodObjectCaches($client) {
        $request = new vod\PreloadVodObjectCachesRequest();
        // 需要预热的文件路径
        $request->setObjectPath("http://test.com/fd.mp4");
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = preloadVodObjectCaches($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



刷新缓存 {#h2--div-id-refreshvodobjectcaches-div-3}
-----------------------------------------------

调用RefreshVodObjectCaches接口，完成刷新缓存功能。

接口参数和返回字段请参见[RefreshVodObjectCaches](/intl.zh-CN/服务端API/点播CDN/刷新预热/刷新缓存.md)。调用示例如下：

    function refreshVodObjectCaches($client) {
        $request = new vod\RefreshVodObjectCachesRequest();
        // 需要刷新的文件或者目录路径
        $request->setObjectPath("http://test.com/fd.mp4");
        // 刷新的类型
        $request->setObjectType("File");
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = refreshVodObjectCaches($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询刷新和预热状态 {#h2--div-id-describevodrefreshtasks-div-4}
-----------------------------------------------------

调用DescribeVodRefreshTasks接口，完成查询刷新和预热状态功能。

接口参数和返回字段请参见[DescribeVodRefreshTasks](/intl.zh-CN/服务端API/点播CDN/刷新预热/查询刷新和预热状态.md)。调用示例如下：

    function describeVodRefreshTasks($client) {
        $request = new vod\DescribeVodRefreshTasksRequest();
        // 需要查询的域名
        $request->setDomainName("test.com");
        // 任务类型
        $request->setObjectType("file");
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = describeVodRefreshTasks($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询刷新预热次数限制和余量 {#h2--div-id-describevodrefreshquota-div-5}
---------------------------------------------------------

调用DescribeVodRefreshQuota接口，完成查询刷新预热次数限制和余量功能。

接口参数和返回字段请参见[DescribeVodRefreshQuota](/intl.zh-CN/服务端API/点播CDN/刷新预热/查询刷新预热次数限制和余量.md)。调用示例如下：

    function describeVodRefreshQuota($client) {
        $request = new vod\DescribeVodRefreshQuotaRequest();
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = describeVodRefreshQuota($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询流量数据 {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------

调用DescribeVodDomainTrafficData接口，完成查询流量数据功能。

接口参数和返回字段请参见[DescribeVodDomainTrafficData](/intl.zh-CN/服务端API/点播CDN/数据监控/查询加速域名的流量数据.md)。调用示例如下：

    function describeVodDomainTrafficData($client) {
        $request = new vod\DescribeVodDomainTrafficDataRequest();
        // 设置域名
        $request->setDomainName("example.test.com");
        // 设置开始时间，请使用UTC格式
        $request->setStartTime("2019-01-15T15:59:59Z");
        // 设置结束时间，请使用UTC格式
        $request->setEndTime("2019-01-20T15:59:58Z");
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = describeVodDomainTrafficData($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询网络带宽 {#h2--div-id-describevoddomainbpsdata-div-7}
---------------------------------------------------

调用DescribeVodDomainBpsData接口，完成查询网络带宽功能。

接口参数和返回字段请参见[DescribeVodDomainBpsData](/intl.zh-CN/服务端API/点播CDN/数据监控/查询加速域名的网络带宽.md)。调用示例如下：

    function describeVodDomainBpsData($client) {
        $request = new vod\DescribeVodDomainBpsDataRequest();
        // 设置域名
        $request->setDomainName("example.test.com");
        // 设置开始时间，请使用UTC格式
        $request->setStartTime("2019-01-15T15:59:59Z");
        // 设置结束时间，请使用UTC格式
        $request->setEndTime("2019-01-20T15:59:58Z");
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = describeVodDomainBpsData($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



下载域名日志 {#h2--div-id-describevoddomainlog-div-8}
-----------------------------------------------

调用DescribeVodDomainLog接口，完成下载域名日志功能。

接口参数和返回字段请参见[DescribeVodDomainLog](/intl.zh-CN/服务端API/点播CDN/日志管理/查询域名日志.md)。调用示例如下：

    function describeVodDomainLog($client) {
        $request = new vod\DescribeVodDomainLogRequest();
        // 设置域名
        $request->setDomainName("zhptest.alicdn.com");
        // 设置开始时间，请使用UTC格式
        $request->setStartTime("2019-01-15T21:00:00Z");
        // 设置结束时间，请使用UTC格式
        $request->setEndTime("2019-01-15T22:00:00Z");
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = describeVodDomainLog($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


