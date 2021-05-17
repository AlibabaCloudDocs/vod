VOD CDN 
============================

This topic provides examples on how to use the API operations of the VOD CDN module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to preload and refresh caches, query the refresh and preload statuses, query traffic data and network bandwidth, and query the logs of domain names. You can also query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Preload caches {#h2--div-id-preloadvodobjectcaches-div-2}
---------------------------------------------------------

You can call the PreloadVodObjectCaches operation to preload caches.
For more information about the request and response parameters of this operation, see [PreloadVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/PreloadVodObjectCaches.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function preloadVodObjectCaches($client) {
        $request = new vod\PreloadVodObjectCachesRequest();
        // The URL of files that you want to preload.
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



Refresh caches {#h2--div-id-refreshvodobjectcaches-div-3}
---------------------------------------------------------

You can call the RefreshVodObjectCaches operation to refresh caches.
For more information about the request and response parameters of this operation, see [RefreshVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/RefreshVodObjectCaches.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function refreshVodObjectCaches($client) {
        $request = new vod\RefreshVodObjectCachesRequest();
        // The URL or directory of files that you want to refresh.
        $request->setObjectPath("http://test.com/fd.mp4");
        // The type of refresh.
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



Query the refresh and preload statuses {#h2--div-id-describevodrefreshtasks-div-4}
----------------------------------------------------------------------------------

You can call the DescribeVodRefreshTasks operation to query the refresh and preload statuses.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshTasks](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshTasks.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function describeVodRefreshTasks($client) {
        $request = new vod\DescribeVodRefreshTasksRequest();
        // The domain name that you want to query.
        $request->setDomainName("test.com");
        // The type of the task.
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



Query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations {#h2--div-id-describevodrefreshquota-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------

You can call the DescribeVodRefreshQuota operation to query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshQuota](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshQuota.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



Query traffic data {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------------------

You can call the DescribeVodDomainTrafficData operation to query traffic data.
For more information about the request and response parameters of this operation, see [DescribeVodDomainTrafficData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainTrafficData.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function describeVodDomainTrafficData($client) {
        $request = new vod\DescribeVodDomainTrafficDataRequest();
        // The domain name.
        $request->setDomainName("example.test.com");
        // The beginning of the time range to query, in UTC.
        $request->setStartTime("2019-01-15T15:59:59Z");
        // The end of the time range to query, in UTC.
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



Query network bandwidth {#h2--div-id-describevoddomainbpsdata-div-7}
--------------------------------------------------------------------

You can call the DescribeVodDomainBpsData operation to query network bandwidth.
For more information about the request and response parameters of this operation, see [DescribeVodDomainBpsData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainBpsData.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function describeVodDomainBpsData($client) {
        $request = new vod\DescribeVodDomainBpsDataRequest();
        // The domain name.
        $request->setDomainName("example.test.com");
        // The beginning of the time range to query, in UTC.
        $request->setStartTime("2019-01-15T15:59:59Z");
        // The end of the time range to query, in UTC.
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



Query the logs of a domain name {#h2--div-id-describevoddomainlog-div-8}
------------------------------------------------------------------------

You can call the DescribeVodDomainLog operation to query the logs of a domain name.
For more information about the request and response parameters of this operation, see [DescribeVodDomainLog](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Log management/DescribeVodDomainLog.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function describeVodDomainLog($client) {
        $request = new vod\DescribeVodDomainLogRequest();
        // The domain name.
        $request->setDomainName("zhptest.alicdn.com");
        // The beginning of the time range to query, in UTC.
        $request->setStartTime("2019-01-15T21:00:00Z");
        // The end of the time range to query, in UTC.
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


