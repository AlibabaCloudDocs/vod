点播CDN 
==========================

本篇文档提供了Node.js SDK点播CDN模块相关功能的API调用示例。包含预热缓存、刷新缓存、查询刷新和预热状态、查询刷新预热次数限制和余量、查询流量数据、查询网络带宽、下载域名日志。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/Node.js SDK/初始化.md)。

预热缓存 {#h2-u9884u70EDu7F13u5B582}
--------------------------------

调用PreloadVodObjectCaches接口，完成预热缓存功能。

接口参数和返回字段请参见[PreloadVodObjectCaches](/intl.zh-CN/服务端API/点播CDN/刷新预热/预热缓存.md)。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("PreloadVodObjectCaches", {
        ObjectPath: 'http://192.168.0.0/16/video/789123x-1688e7fd1ca-0005-36ec-adb-83212.mp4'   // 需要预热的文件路径
    }, {}).then(function (response) {
        // 预热返回的任务ID
        console.log('PreloadTaskId = ' + response.PreloadTaskId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



刷新缓存 {#h2-u5237u65B0u7F13u5B583}
--------------------------------

调用RefreshVodObjectCaches接口，完成刷新缓存功能。

接口参数和返回字段请参见[RefreshVodObjectCaches](/intl.zh-CN/服务端API/点播CDN/刷新预热/刷新缓存.md)。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("RefreshVodObjectCaches", {
        ObjectPath: 'http://192.168.0.0/16/video/83213214-1688e7fd1ca-0005-36ec-adb-8512.mp4',  // 需要刷新的文件或者目录路径
        ObjectType: 'File'  // 刷新的类型
    }, {}).then(function (response) {
        // 刷新返回的任务ID
        console.log('RefreshTaskId = ' + response.RefreshTaskId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



查询刷新和预热状态 {#h2-u67E5u8BE2u5237u65B0u548Cu9884u70EDu72B6u60014}
--------------------------------------------------------------

调用DescribeVodRefreshTasks接口，完成查询刷新和预热状态功能。

接口参数和返回字段请参见[DescribeVodRefreshTasks](/intl.zh-CN/服务端API/点播CDN/刷新预热/查询刷新和预热状态.md)。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodRefreshTasks", {
        DomainName: '192.168.0.0/16.com',  // 需要查询的域名
        ObjectType: 'File'  // 任务类型
    }, {}).then(function (response) {
        console.log(response);
        // 整页大小
        console.log('PageSize = ' + response.PageSize);
        // 页码
        console.log('PageNumber = ' + response.PageNumber);
        // 总条数
        console.log('TotalCount = ' + response.TotalCount);
        // 任务信息
        if (response.Tasks && response.Tasks.Task && response.Tasks.Task.length > 0){
            for (var i=0; i<response.Tasks.Task.length; i++){
                console.log('The ' + i + ' Task.');
                var task = response.Tasks.Task[i];
                // 任务ID
                console.log('TaskId = ' + task.TaskId);
                // 刷新对象路径
                console.log('ObjectPath = ' + task.ObjectPath);
                // 状态
                console.log('Status = ' + task.Status);
                // 进度百分比
                console.log('Process = ' + task.Process);
                // 任务类型
                console.log('ObjectType = ' + task.ObjectType);
                // 任务对象创建时间，使用UTC时间
                console.log('CreationTime = ' + task.CreationTime);
                // 刷新预热失败返回的错误描述
                console.log('Description = ' + task.Description);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



查询刷新预热次数限制和余量 {#h2-u67E5u8BE2u5237u65B0u9884u70EDu6B21u6570u9650u5236u548Cu4F59u91CF5}
--------------------------------------------------------------------------------------

调用DescribeVodRefreshQuota接口，完成查询刷新预热次数限制和余量功能。

接口参数和返回字段请参见[DescribeVodRefreshQuota](/intl.zh-CN/服务端API/点播CDN/刷新预热/查询刷新预热次数限制和余量.md)。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodRefreshQuota", {}, {}).then(function (response) {
        // 当日URL刷新数量上限
        console.log('UrlQuota = ' + response.UrlQuota);
        // 当日目录刷新数量上限
        console.log('DirQuota = ' + response.DirQuota);
        // 当日剩余URL刷新数量
        console.log('UrlRemain = ' + response.UrlRemain);
        // 当日剩余目录刷新数量
        console.log('DirRemain = ' + response.DirRemain);
        // 当天预热数量上限
        console.log('PreloadQuota = ' + response.PreloadQuota);
        // 当天剩余预热数量
        console.log('PreloadRemain = ' + response.PreloadRemain);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



查询流量数据 {#h2-u67E5u8BE2u6D41u91CFu6570u636E6}
--------------------------------------------

调用DescribeVodDomainTrafficData接口，完成查询流量数据功能。

接口参数和返回字段请参见[DescribeVodDomainTrafficData](/intl.zh-CN/服务端API/点播CDN/数据监控/查询流量数据.md)。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodDomainTrafficData", {
        DomainName: '192.168.0.0/16.com',    // 域名
        StartTime: '2019-01-15T15:59:59Z',  // 开始时间，请使用UTC格式
        EndTime: '2019-01-20T15:59:59Z'     // 结束时间，请使用UTC格式
    }, {}).then(function (response) {
        // 域名
        console.log('DomainName = ' + response.DomainName);
        // 开始时间
        console.log('StartTime = ' + response.StartTime);
        // 结束时间
        console.log('EndTime = ' + response.EndTime);
        // 时间间隔
        console.log('DataInterval = ' + response.DataInterval);
        // 流量数据
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



查询网络带宽 {#h2-u67E5u8BE2u7F51u7EDCu5E26u5BBD7}
--------------------------------------------

调用DescribeVodDomainBpsData接口，完成查询网络带宽功能。

接口参数和返回字段请参见[DescribeVodDomainBpsData](/intl.zh-CN/服务端API/点播CDN/数据监控/查询网络带宽.md)。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodDomainBpsData", {
        DomainName: '192.168.0.0/16.com',    // 域名
        StartTime: '2019-01-15T15:59:59Z',  // 开始时间，请使用UTC格式
        EndTime: '2019-01-20T15:59:59Z'     // 结束时间，请使用UTC格式
    }, {}).then(function (response) {
        // 域名
        console.log('DomainName = ' + response.DomainName);
        // 开始时间
        console.log('StartTime = ' + response.StartTime);
        // 结束时间
        console.log('EndTime = ' + response.EndTime);
        // 时间间隔
        console.log('DataInterval = ' + response.DataInterval);
        // 带宽数据
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



下载域名日志 {#h2-u4E0Bu8F7Du57DFu540Du65E5u5FD78}
--------------------------------------------

调用DescribeVodDomainLog接口，完成下载域名日志功能。

接口参数和返回字段请参见[DescribeVodDomainLog](/intl.zh-CN/服务端API/点播CDN/日志管理/下载域名日志.md)。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DescribeVodDomainLog", {
        DomainName: '192.168.0.0/16.com',    // 域名
        // PageSize: 300,  // 分页大小
        // PageNumber: 1,  // 分页页号
        StartTime: '2019-01-15T15:59:59Z',  // 开始时间，请使用UTC格式
        EndTime: '2019-01-20T15:59:59Z'     // 结束时间，请使用UTC格式
    }, {}).then(function (response) {
        // CDN日志详细数据
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


