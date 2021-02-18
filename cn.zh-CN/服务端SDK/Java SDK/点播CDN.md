点播CDN 
==========================

本篇文档提供了Java SDK点播CDN模块相关功能的API调用示例。包含预热缓存、刷新缓存、查询刷新和预热状态、查询刷新预热次数限制和余量、查询流量数据、查询网络带宽、下载域名日志。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/Java SDK/初始化.md)。

预热缓存 {#h2--div-id-preloadvodobjectcaches-div-2}
-----------------------------------------------

调用PreloadVodObjectCaches接口，完成预热缓存功能。

接口参数和返回字段请参见[PreloadVodObjectCaches](/cn.zh-CN/服务端API/点播CDN/刷新预热/预热缓存.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.PreloadVodObjectCachesRequest;
    import com.aliyuncs.vod.model.v20170321.PreloadVodObjectCachesResponse;
    
        /**
         * 预热缓存
         * @param client 发送请求客户端
         * @return PreloadVodObjectCachesResponse
         * @throws Exception
         */
        public static PreloadVodObjectCachesResponse preloadVodObjectCaches(DefaultAcsClient client) throws Exception {
            PreloadVodObjectCachesRequest request = new PreloadVodObjectCachesRequest();
            // 需要预热的文件路径
            request.setObjectPath("http://test.com/fd.mp4");
            return client.getAcsResponse(request);
        }
    
        /**
         * 请求示例
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                PreloadVodObjectCachesResponse response = preloadVodObjectCaches(client);
                // 预热返回的任务ID
                System.out.println("PreloadTaskId = " + response.getPreloadTaskId());
                // 请求ID
                System.out.println("RequestId = " + response.getRequestId());
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



刷新缓存 {#h2--div-id-refreshvodobjectcaches-div-3}
-----------------------------------------------

调用RefreshVodObjectCaches接口，完成刷新缓存功能。

接口参数和返回字段请参见[RefreshVodObjectCaches](/cn.zh-CN/服务端API/点播CDN/刷新预热/刷新缓存.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.RefreshVodObjectCachesRequest;
    import com.aliyuncs.vod.model.v20170321.RefreshVodObjectCachesResponse;
    
        /**
         * 刷新缓存
         * @param client 发送请求客户端
         * @return RefreshVodObjectCachesResponse
         * @throws Exception
         */
        public static RefreshVodObjectCachesResponse refreshVodObjectCaches(DefaultAcsClient client) throws Exception {
            RefreshVodObjectCachesRequest request = new RefreshVodObjectCachesRequest();
            // 需要刷新的文件或者目录路径
            request.setObjectPath("http://test.com/fd.mp4");
            // 刷新的类型
            request.setObjectType("File");
            return client.getAcsResponse(request);
        }
    
        /**
         * 请求示例
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                RefreshVodObjectCachesResponse response = refreshVodObjectCaches(client);
                // 刷新返回的任务ID
                System.out.println("PreloadTaskId = " + response.getRefreshTaskId());
                // 请求ID
                System.out.println("RequestId = " + response.getRequestId());
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



查询刷新和预热状态 {#h2--div-id-describevodrefreshtasks-div-4}
-----------------------------------------------------

调用DescribeVodRefreshTasks接口，完成查询刷新和预热状态功能。

接口参数和返回字段请参见[DescribeVodRefreshTasks](/cn.zh-CN/服务端API/点播CDN/刷新预热/查询刷新和预热状态.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshTasksRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshTasksResponse;
    
        /**
         * 查询刷新和预热状态
         * @param client 发送请求客户端
         * @return DescribeVodRefreshTasksResponse
         * @throws Exception
         */
        public static DescribeVodRefreshTasksResponse describeVodRefreshTasks(DefaultAcsClient client) throws Exception {
            DescribeVodRefreshTasksRequest request = new DescribeVodRefreshTasksRequest();
            // 需要查询的域名
            request.setDomainName("test.com");
            // 任务类型
            request.setObjectType("file");
            return client.getAcsResponse(request);
        }
    
        /**
         * 请求示例
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                DescribeVodRefreshTasksResponse response = describeVodRefreshTasks(client);
                // 整页大小
                System.out.println("PageSize = " + response.getPageSize());
                // 页码
                System.out.println("PageNumber = " + response.getPageNumber());
                // 总条数
                System.out.println("TotalCount = " + response.getTotalCount());
                // 请求ID
                System.out.println("RequestId = " + response.getRequestId());
                if (response.getTasks() != null && response.getTasks().size() > 0) {
                    for (DescribeVodRefreshTasksResponse.Task task : response.getTasks()) {
                        System.out.println("-----------------------------");
                        // 任务ID
                        System.out.println("TaskId = " + task.getTaskId());
                        // 刷新对象路径
                        System.out.println("ObjectPath = " + task.getObjectPath());
                        // 状态
                        System.out.println("Status = " + task.getStatus());
                        // 进度百分比
                        System.out.println("Process = " + task.getProcess());
                        // 任务类型
                        System.out.println("ObjectType = " + task.getObjectType());
                        // 任务对象创建时间，使用UTC时间
                        System.out.println("CreationTime = " + task.getCreationTime());
                        // 刷新预热失败返回的错误描述
                        System.out.println("Description = " + task.getDescription());
                    }
                }
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



查询刷新预热次数限制和余量 {#h2--div-id-describevodrefreshquota-div-5}
---------------------------------------------------------

调用DescribeVodRefreshQuota接口，完成查询刷新预热次数限制和余量功能。

接口参数和返回字段请参见[DescribeVodRefreshQuota](/cn.zh-CN/服务端API/点播CDN/刷新预热/查询刷新预热次数限制和余量.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshQuotaRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshQuotaResponse;
    
        /**
         * 查询刷新预热次数限制和余量
         * @param client 发送请求客户端
         * @return DescribeVodRefreshQuotaResponse
         * @throws Exception
         */
        public static DescribeVodRefreshQuotaResponse describeVodRefreshQuota(DefaultAcsClient client) throws Exception {
            DescribeVodRefreshQuotaRequest request = new DescribeVodRefreshQuotaRequest();
            return client.getAcsResponse(request);
        }
    
        /**
         * 请求示例
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                DescribeVodRefreshQuotaResponse response = describeVodRefreshQuota(client);
                // 当日URL刷新数量上限
                System.out.println("UrlQuota = " + response.getUrlQuota());
                // 当日目录刷新数量上限
                System.out.println("DirQuota = " + response.getDirQuota());
                // 当日剩余URL刷新数量
                System.out.println("UrlRemain = " + response.getUrlRemain());
                // 当日剩余目录刷新数量
                System.out.println("DirRemain = " + response.getDirRemain());
                // 当天预热数量上限
                System.out.println("PreloadQuota = " + response.getPreloadQuota());
                // 当天剩余预热数量
                System.out.println("PreloadRemain = " + response.getPreloadRemain());
                // 请求ID
                System.out.println("RequestId = " + response.getRequestId());
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



查询流量数据 {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------

调用DescribeVodDomainTrafficData接口，完成查询流量数据功能。

接口参数和返回字段请参见[DescribeVodDomainTrafficData](/cn.zh-CN/服务端API/点播CDN/数据监控/查询加速域名的流量数据.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainTrafficDataRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainTrafficDataResponse;
    
    /**
     * 查询流量数据
     */
    public static DescribeVodDomainTrafficDataResponse describeVodDomainTrafficData(DefaultAcsClient client) throws Exception {
            DescribeVodDomainTrafficDataRequest request = new DescribeVodDomainTrafficDataRequest();
            // 设置域名
            request.setDomainName("example.test.com");
            // 设置开始时间，请使用UTC格式
            request.setStartTime("2019-01-15T15:59:59Z");
            // 设置结束时间，请使用UTC格式
            request.setEndTime("2019-01-20T15:59:58Z");
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 获取结果
                DescribeVodDomainTrafficDataResponse response = describeVodDomainTrafficData(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印域名
                System.out.println("DomainName:" + response.getDomainName());
                // 打印开始时间
                System.out.println("StartTime:" + response.getStartTime());
                // 打印结束时间
                System.out.println("EndTime:" + response.getEndTime());
                // 打印时间间隔
                System.out.println("DataInterval:" + response.getDataInterval());
                // 打印流量数据
                if (response.getTrafficDataPerInterval() != null && response.getTrafficDataPerInterval().size() != 0) {
                    List<DescribeVodDomainTrafficDataResponse.DataModule> dataModules = response.getTrafficDataPerInterval();
                    for(int i=0; i<dataModules.size(); i++) {
                        System.out.println("==========================" );
                        System.out.println("TimeStamp:" + dataModules.get(i).getTimeStamp());
                        System.out.println("Value:" + dataModules.get(i).getValue());
                        System.out.println("DomesticValue:" + dataModules.get(i).getDomesticValue());
                        System.out.println("OverseasValue:" + dataModules.get(i).getOverseasValue());
                    }
    
                }
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



查询网络带宽 {#h2--div-id-describevoddomainbpsdata-div-7}
---------------------------------------------------

调用DescribeVodDomainBpsData接口，完成查询网络带宽功能。

接口参数和返回字段请参见[DescribeVodDomainBpsData](/cn.zh-CN/服务端API/点播CDN/数据监控/查询加速域名的网络带宽.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainBpsDataRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainBpsDataResponse;
    import java.util.List;
    
    /**
     * 查询网络带宽
     */
    public static DescribeVodDomainBpsDataResponse describeVodDomainBpsData(DefaultAcsClient client) throws Exception {
            DescribeVodDomainBpsDataRequest request = new DescribeVodDomainBpsDataRequest();
            // 设置域名
            request.setDomainName("example.test.com");
            // 设置开始时间，请使用UTC格式
            request.setStartTime("2019-01-15T15:59:59Z");
            // 设置结束时间，请使用UTC格式
            request.setEndTime("2019-01-20T15:59:58Z");
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
            try {
                // 获取结果
                DescribeVodDomainBpsDataResponse response = describeVodDomainBpsData(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印域名
                System.out.println("DomainName:" + response.getDomainName());
                // 打印开始时间
                System.out.println("StartTime:" + response.getStartTime());
                // 打印结束时间
                System.out.println("EndTime:" + response.getEndTime());
                // 打印时间间隔
                System.out.println("DataInterval:" + response.getDataInterval());
                // 打印带宽数据
                if (response.getBpsDataPerInterval() != null && response.getBpsDataPerInterval().size() != 0) {
                    List<DescribeVodDomainBpsDataResponse.DataModule> dataModules = response.getBpsDataPerInterval();
                    for(int i=0; i<dataModules.size(); i++) {
                        System.out.println("==========================" );
                        System.out.println("TimeStamp:" + dataModules.get(i).getTimeStamp());
                        System.out.println("Value:" + dataModules.get(i).getValue());
                        System.out.println("DomesticValue:" + dataModules.get(i).getDomesticValue());
                        System.out.println("OverseasValue:" + dataModules.get(i).getOverseasValue());
                    }
    
                }
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



下载域名日志 {#h2--div-id-describevoddomainlog-div-8}
-----------------------------------------------

调用DescribeVodDomainLog接口，完成下载域名日志功能。

接口参数和返回字段请参见[DescribeVodDomainLog](/cn.zh-CN/服务端API/点播CDN/日志管理/查询域名日志.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainLogRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainLogResponse;
    import java.util.List;
    
    /**
     * 下载域名日志
     */
    public static DescribeVodDomainLogResponse describeVodDomainLog(DefaultAcsClient client) throws Exception {
            DescribeVodDomainLogRequest request = new DescribeVodDomainLogRequest();
            // 设置域名
            request.setDomainName("zhptest.alicdn.com");
            // 设置开始时间，请使用UTC格式
            request.setStartTime("2019-01-15T15:59:59Z");
            // 设置结束时间，请使用UTC格式
            request.setEndTime("2019-01-20T15:59:58Z");
            // 设置分页大小
            //request.setPageSize(300L);
            // 设置分页页号
            //request.setPageNumber(1L);
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
            try {
                // 获取结果
                DescribeVodDomainLogResponse response = describeVodDomainLog(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
    
                // 打印CDN日志详细数据
                if (response.getDomainLogDetails() != null && response.getDomainLogDetails().size() != 0) {
                    List<DescribeVodDomainLogResponse.DomainLogDetail> domainLogDetails = response.getDomainLogDetails();
                    for(int i=0; i<domainLogDetails.size(); i++) {
                        System.out.println("==========================" );
                        System.out.println("DomainName:" + domainLogDetails.get(i).getDomainName());
                        System.out.println("LogCount:" + domainLogDetails.get(i).getLogCount());
    
                        System.out.println("=== PageInfoDetail Data ===" );
                        System.out.println("PageNumber:" + domainLogDetails.get(i).getPageInfos().getPageNumber());
                        System.out.println("PageSize:" + domainLogDetails.get(i).getPageInfos().getPageSize());
                        System.out.println("Total:" + domainLogDetails.get(i).getPageInfos().getTotal());
    
                        System.out.println("=== LogInfoDetail Data ===" );
                        List<DescribeVodDomainLogResponse.DomainLogDetail.LogInfoDetail> logInfos = domainLogDetails.get(i).getLogInfos();
                        if (logInfos != null && logInfos.size() != 0) {
                            for (int k=0; k<logInfos.size(); k++) {
                                System.out.println("LogName:" + logInfos.get(k).getLogName());
                                System.out.println("LogPath:" + logInfos.get(k).getLogPath());
                                System.out.println("LogSize:" + logInfos.get(k).getLogSize());
                                System.out.println("StartTime:" + logInfos.get(k).getStartTime());
                                System.out.println("EndTime:" + logInfos.get(k).getEndTime());
                            }
                        }
                    }
    
                }
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }


