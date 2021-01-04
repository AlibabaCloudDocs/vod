VOD CDN 
============================

This topic provides examples on how to use the API operations of the VOD CDN module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to preload and refresh caches, query the refresh and preload statuses, query traffic data and network bandwidth, and query the logs of domain names. You can also query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Preload caches {#h2-u9884u70EDu7F13u5B582}
------------------------------------------

You can call the PreloadVodObjectCaches operation to preload caches.

For more information about the request and response parameters of this operation, see [PreloadVodObjectCaches](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/PreloadVodObjectCaches.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("PreloadVodObjectCaches", {
        ObjectPath: 'http://192.168.0.0/16/video/789123x-1688e7fd1ca-0005-36ec-adb-83212.mp4'   // The URL of files that you want to preload.
    }, {}).then(function (response) {
        // The ID of the preload task.
        console.log('PreloadTaskId = ' + response.PreloadTaskId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Refresh caches {#h2-u5237u65B0u7F13u5B583}
------------------------------------------

You can call the RefreshVodObjectCaches operation to refresh caches.

For more information about the request and response parameters of this operation, see [RefreshVodObjectCaches](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/RefreshVodObjectCaches.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("RefreshVodObjectCaches", {
        ObjectPath: 'http://192.168.0.0/16/video/83213214-1688e7fd1ca-0005-36ec-adb-8512.mp4',  // The URL or directory of files that you want to refresh.
        ObjectType: 'File'  // The type of refresh.
    }, {}).then(function (response) {
        // The ID of the refresh task.
        console.log('RefreshTaskId = ' + response.RefreshTaskId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the refresh and preload statuses {#h2-u67E5u8BE2u5237u65B0u548Cu9884u70EDu72B6u60014}
-------------------------------------------------------------------------------------------

You can call the DescribeVodRefreshTasks operation to query the refresh and preload statuses.

For more information about the request and response parameters of this operation, see [DescribeVodRefreshTasks](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/DescribeRefreshTasks.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodRefreshTasks", {
        DomainName: '192.168.0.0/16.com',  // The domain name that you want to query.
        ObjectType: 'File'  // The type of the task.
    }, {}).then(function (response) {
        console.log(response);
        // The number of entries to return on each page.
        console.log('PageSize = ' + response.PageSize);
        // The number of the page to return.
        console.log('PageNumber = ' + response.PageNumber);
        // The total number of entries.
        console.log('TotalCount = ' + response.TotalCount);
        // The task information.
        if (response.Tasks && response.Tasks.Task && response.Tasks.Task.length > 0){
            for (var i=0; i<response.Tasks.Task.length; i++){
                console.log('The ' + i + ' Task.');
                var task = response.Tasks.Task[i];
                // The task ID.
                console.log('TaskId = ' + task.TaskId);
                // The URL or directory of files that you want to refresh.
                console.log('ObjectPath = ' + task.ObjectPath);
                // The task status.
                console.log('Status = ' + task.Status);
                // The task progress, in percent.
                console.log('Process = ' + task.Process);
                // The task type.
                console.log('ObjectType = ' + task.ObjectType);
                // The creation time of the task, in UTC.
                console.log('CreationTime = ' + task.CreationTime);
                // The error information returned if the refresh or preload operation fails.
                console.log('Description = ' + task.Description);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations {#h2-u67E5u8BE2u5237u65B0u9884u70EDu6B21u6570u9650u5236u548Cu4F59u91CF5}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

You can call the DescribeVodRefreshQuota operation to query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.

For more information about the request and response parameters of this operation, see [DescribeVodRefreshQuota](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/DescribeVodRefreshQuota.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodRefreshQuota", {}, {}).then(function (response) {
        // The maximum allowed number of URLs for the refresh operation per day.
        console.log('UrlQuota = ' + response.UrlQuota);
        // The maximum allowed number of directories for the refresh operation per day.
        console.log('DirQuota = ' + response.DirQuota);
        // The currently allowed number of URLs for the refresh operation per day.
        console.log('UrlRemain = ' + response.UrlRemain);
        // The currently allowed number of directories for the refresh operation per day.
        console.log('DirRemain = ' + response.DirRemain);
        // The maximum allowed number of URLs for the preload operation per day.
        console.log('PreloadQuota = ' + response.PreloadQuota);
        // The currently allowed number of URLs for the preload operation per day.
        console.log('PreloadRemain = ' + response.PreloadRemain);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query traffic data {#h2-u67E5u8BE2u6D41u91CFu6570u636E6}
--------------------------------------------------------

You can call the DescribeVodDomainTrafficData operation to query traffic data.

For more information about the request and response parameters of this operation, see [DescribeVodDomainTrafficData](/intl.en-US/API Reference/VoD CDN/Data Monitoring/DescribeVodDomainTrafficData.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodDomainTrafficData", {
        DomainName: '192.168.0.0/16.com',    // The domain name.
        StartTime: '2019-01-15T15:59:59Z',  // The beginning of the time range to query, in UTC.
        EndTime: '2019-01-20T15:59:59Z'     // The end of the time range to query, in UTC.
    }, {}).then(function (response) {
        // The domain name.
        console.log('DomainName = ' + response.DomainName);
        // The beginning of the time range to query.
        console.log('StartTime = ' + response.StartTime);
        // The end of the time range to query.
        console.log('EndTime = ' + response.EndTime);
        // The time interval.
        console.log('DataInterval = ' + response.DataInterval);
        // The traffic data.
        if (response.TrafficDataPerInterval && response.TrafficDataPerInterval.DataModule && response.TrafficDataPerInterval.DataModule.length > 0){
            for(var i=0; i<response.TrafficDataPerInterval.DataModule.length; i++){
                var trafficData = response.TrafficDataPerInterval.DataModule[i];
                console.log("The " + i + " TrafficData.");
                console.log('TimeStamp = ' + trafficData.TimeStamp);
                console.log('Value = ' + trafficData.Value);
                console.log('DomesticValue = ' + trafficData.DomesticValue);
                console.log('OverseasValue = ' + trafficData.OverseasValue);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query network bandwidth {#h2-u67E5u8BE2u7F51u7EDCu5E26u5BBD7}
-------------------------------------------------------------

You can call the DescribeVodDomainBpsData operation to query network bandwidth.

For more information about the request and response parameters of this operation, see [DescribeVodDomainBpsData](/intl.en-US/API Reference/VoD CDN/Data Monitoring/DescribeVodDomainBpsData.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodDomainBpsData", {
        DomainName: '192.168.0.0/16.com',    // The domain name.
        StartTime: '2019-01-15T15:59:59Z',  // The beginning of the time range to query, in UTC.
        EndTime: '2019-01-20T15:59:59Z'     // The end of the time range to query, in UTC.
    }, {}).then(function (response) {
        // The domain name.
        console.log('DomainName = ' + response.DomainName);
        // The beginning of the time range to query.
        console.log('StartTime = ' + response.StartTime);
        // The end of the time range to query.
        console.log('EndTime = ' + response.EndTime);
        // The time interval.
        console.log('DataInterval = ' + response.DataInterval);
        // The network bandwidth data.
        if (response.BpsDataPerInterval && response.BpsDataPerInterval.DataModule && response.BpsDataPerInterval.DataModule.length > 0){
            for(var i=0; i<response.BpsDataPerInterval.DataModule.length; i++){
                var bpsData = response.BpsDataPerInterval.DataModule[i];
                console.log("The " + i + " BpsData.");
                console.log('TimeStamp = ' + bpsData.TimeStamp);
                console.log('Value = ' + bpsData.Value);
                console.log('DomesticValue = ' + bpsData.DomesticValue);
                console.log('OverseasValue = ' + bpsData.OverseasValue);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the logs of a domain name {#h2-u4E0Bu8F7Du57DFu540Du65E5u5FD78}
---------------------------------------------------------------------

You can call the DescribeVodDomainLog operation to query the logs of a domain name.

For more information about the request and response parameters of this operation, see [DescribeVodDomainLog](/intl.en-US/API Reference/VoD CDN/Log Management/DescribeVodDomainLog.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodDomainLog", {
        DomainName: '192.168.0.0/16.com',    // The domain name.
        // PageSize: 300,  // The number of entries to return on each page.
        // PageNumber: 1,  // The number of the page to return.
        StartTime: '2019-01-15T15:59:59Z',  // The beginning of the time range to query, in UTC.
        EndTime: '2019-01-20T15:59:59Z'     // The end of the time range to query, in UTC.
    }, {}).then(function (response) {
        // The details about CDN logs.
        console.log(response.DomainLogDetails);
        if (response.DomainLogDetails && response.DomainLogDetails.DomainLogDetail && response.DomainLogDetails.DomainLogDetail.length > 0){
            for(var i=0; i<response.DomainLogDetails.DomainLogDetail.length; i++){
                var logData = response.DomainLogDetails.DomainLogDetail[i];
                console.log("The " + i + " LogData.");
                console.log('DomainName = ' + logData.DomainName);
                console.log('LogCount = ' + logData.LogCount);
                console.log('=== PageInfoDetail Data ===');
                console.log('PageNumber = ' + logData.PageInfos.PageNumber);
                console.log('PageSize = ' + logData.PageInfos.PageSize);
                console.log('Total = ' + logData.PageInfos.Total);
                console.log('=== LogInfoDetail Data ===');
                if (logData.LogInfos && logData.LogInfos.LogInfoDetail && logData.LogInfos.LogInfoDetail.length > 0){
                    for (var j=0; j<logData.LogInfos.LogInfoDetail.length; j++){
                        var logInfoDetail = logData.LogInfos.LogInfoDetail[j]
                        console.log('LogName = ' + logInfoDetail.LogName);
                        console.log('LogPath = ' + logInfoDetail.LogPath);
                        console.log('LogSize = ' + logInfoDetail.LogSize);
                        console.log('StartTime = ' + logInfoDetail.StartTime);
                        console.log('EndTime = ' + logInfoDetail.EndTime);
                    }
                }
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


