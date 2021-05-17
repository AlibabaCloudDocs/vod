VOD CDN 
============================

This topic provides examples on how to use the API operations of the VOD CDN module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to preload and refresh caches, query the refresh and preload statuses, query traffic data and network bandwidth, and query the logs of domain names. You can also query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Preload caches {#h2--div-id-preloadvodobjectcaches-div-2}
---------------------------------------------------------

You can call the PreloadVodObjectCaches operation to preload caches.
For more information about the request and response parameters of this operation, see [PreloadVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/PreloadVodObjectCaches.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.PreloadVodObjectCachesRequest;
    import com.aliyuncs.vod.model.v20170321.PreloadVodObjectCachesResponse;
    
        /**
         * Preload caches.
         * @param client The client that is used to send requests.
         * @return PreloadVodObjectCachesResponse
         * @throws Exception
         */
        public static PreloadVodObjectCachesResponse preloadVodObjectCaches(DefaultAcsClient client) throws Exception {
            PreloadVodObjectCachesRequest request = new PreloadVodObjectCachesRequest();
            // The URL of files that you want to preload.
            request.setObjectPath("http://test.com/fd.mp4");
            return client.getAcsResponse(request);
        }
    
        /**
         * Call example
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                PreloadVodObjectCachesResponse response = preloadVodObjectCaches(client);
                // The ID of the preload task.
                System.out.println("PreloadTaskId = " + response.getPreloadTaskId());
                // The ID of the request.
                System.out.println("RequestId = " + response.getRequestId());
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



Refresh caches {#h2--div-id-refreshvodobjectcaches-div-3}
---------------------------------------------------------

You can call the RefreshVodObjectCaches operation to refresh caches.

For more information about the request and response parameters of this operation, see [RefreshVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/RefreshVodObjectCaches.md). Example:

    import com.aliyuncs.vod.model.v20170321.RefreshVodObjectCachesRequest;
    import com.aliyuncs.vod.model.v20170321.RefreshVodObjectCachesResponse;
    
        /**
         * Refresh caches.
         * @param client The client that is used to send requests.
         * @return RefreshVodObjectCachesResponse
         * @throws Exception
         */
        public static RefreshVodObjectCachesResponse refreshVodObjectCaches(DefaultAcsClient client) throws Exception {
            RefreshVodObjectCachesRequest request = new RefreshVodObjectCachesRequest();
            // The URL or directory of files that you want to refresh.
            request.setObjectPath("http://test.com/fd.mp4");
            // The type of refresh.
            request.setObjectType("File");
            return client.getAcsResponse(request);
        }
    
        /**
         * Call example
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                RefreshVodObjectCachesResponse response = refreshVodObjectCaches(client);
                // The ID of the refresh task.
                System.out.println("PreloadTaskId = " + response.getRefreshTaskId());
                // The ID of the request.
                System.out.println("RequestId = " + response.getRequestId());
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



Query the refresh and preload statuses {#h2--div-id-describevodrefreshtasks-div-4}
----------------------------------------------------------------------------------

You can call the DescribeVodRefreshTasks operation to query the refresh and preload statuses.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshTasks](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshTasks.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshTasksRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshTasksResponse;
    
        /**
         * Query the refresh and preload statuses.
         * @param client The client that is used to send requests.
         * @return DescribeVodRefreshTasksResponse
         * @throws Exception
         */
        public static DescribeVodRefreshTasksResponse describeVodRefreshTasks(DefaultAcsClient client) throws Exception {
            DescribeVodRefreshTasksRequest request = new DescribeVodRefreshTasksRequest();
            // The domain name that you want to query.
            request.setDomainName("test.com");
            // The task type.
            request.setObjectType("file");
            return client.getAcsResponse(request);
        }
    
        /**
         * Call example
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                DescribeVodRefreshTasksResponse response = describeVodRefreshTasks(client);
                // The number of entries to return on each page.
                System.out.println("PageSize = " + response.getPageSize());
                // The number of the page to return.
                System.out.println("PageNumber = " + response.getPageNumber());
                // The total number of entries.
                System.out.println("TotalCount = " + response.getTotalCount());
                // The ID of the request.
                System.out.println("RequestId = " + response.getRequestId());
                if (response.getTasks() ! = null && response.getTasks().size() > 0) {
                    for (DescribeVodRefreshTasksResponse.Task task : response.getTasks()) {
                        System.out.println("-----------------------------");
                        // The task ID.
                        System.out.println("TaskId = " + task.getTaskId());
                        // The URL or directory of files that you want to refresh.
                        System.out.println("ObjectPath = " + task.getObjectPath());
                        // The task status.
                        System.out.println("Status = " + task.getStatus());
                        // The task progress, in percent.
                        System.out.println("Process = " + task.getProcess());
                        // The task type.
                        System.out.println("ObjectType = " + task.getObjectType());
                        // The creation time of the task, in UTC.
                        System.out.println("CreationTime = " + task.getCreationTime());
                        // The error information returned if the refresh or preload operation fails.
                        System.out.println("Description = " + task.getDescription());
                    }
                }
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



Query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations {#h2--div-id-describevodrefreshquota-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------

You can call the DescribeVodRefreshQuota operation to query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshQuota](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshQuota.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshQuotaRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodRefreshQuotaResponse;
    
        /**
         * Query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.
         * @param client The client that is used to send requests.
         * @return DescribeVodRefreshQuotaResponse
         * @throws Exception
         */
        public static DescribeVodRefreshQuotaResponse describeVodRefreshQuota(DefaultAcsClient client) throws Exception {
            DescribeVodRefreshQuotaRequest request = new DescribeVodRefreshQuotaRequest();
            return client.getAcsResponse(request);
        }
    
        /**
         * Call example
         * @param argv
         */
        public static void main(String[] argv) {
            try {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                DescribeVodRefreshQuotaResponse response = describeVodRefreshQuota(client);
                // The maximum allowed number of URLs for the refresh operation per day.
                System.out.println("UrlQuota = " + response.getUrlQuota());
                // The maximum allowed number of directories for the refresh operation per day.
                System.out.println("DirQuota = " + response.getDirQuota());
                // The currently allowed number of URLs for the refresh operation per day.
                System.out.println("UrlRemain = " + response.getUrlRemain());
                // The currently allowed number of directories for the refresh operation per day.
                System.out.println("DirRemain = " + response.getDirRemain());
                // The maximum allowed number of URLs for the preload operation per day.
                System.out.println("PreloadQuota = " + response.getPreloadQuota());
                // The currently allowed number of URLs for the preload operation per day.
                System.out.println("PreloadRemain = " + response.getPreloadRemain());
                // The ID of the request.
                System.out.println("RequestId = " + response.getRequestId());
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getMessage());
            }
        }



Query traffic data {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------------------

You can call the DescribeVodDomainTrafficData operation to query traffic data.
For more information about the request and response parameters of this operation, see [DescribeVodDomainTrafficData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainTrafficData.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainTrafficDataRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainTrafficDataResponse;
    
    /**
     * Query traffic data.
     */
    public static DescribeVodDomainTrafficDataResponse describeVodDomainTrafficData(DefaultAcsClient client) throws Exception {
            DescribeVodDomainTrafficDataRequest request = new DescribeVodDomainTrafficDataRequest();
            // Specify the domain name.
            request.setDomainName("example.test.com");
            // Specify the beginning of the time range to query, in UTC.
            request.setStartTime("2019-01-15T15:59:59Z");
            // Specify the end of the time range to query, in UTC.
            request.setEndTime("2019-01-20T15:59:58Z");
    
            // List the results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List the results.
                DescribeVodDomainTrafficDataResponse response = describeVodDomainTrafficData(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the domain name.
                System.out.println("DomainName:" + response.getDomainName());
                // List the beginning of the time range to query.
                System.out.println("StartTime:" + response.getStartTime());
                // List the end of the time range to query.
                System.out.println("EndTime:" + response.getEndTime());
                // List the query intervals.
                System.out.println("DataInterval:" + response.getDataInterval());
                // List the traffic data.
                if (response.getTrafficDataPerInterval() ! = null && response.getTrafficDataPerInterval().size() ! = 0) {
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



Query network bandwidth {#h2--div-id-describevoddomainbpsdata-div-7}
--------------------------------------------------------------------

You can call the DescribeVodDomainBpsData operation to query network bandwidth.
For more information about the request and response parameters of this operation, see [DescribeVodDomainBpsData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainBpsData.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainBpsDataRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainBpsDataResponse;
    import java.util.List;
    
    /**
     * Query network bandwidth.
     */
    public static DescribeVodDomainBpsDataResponse describeVodDomainBpsData(DefaultAcsClient client) throws Exception {
            DescribeVodDomainBpsDataRequest request = new DescribeVodDomainBpsDataRequest();
            // Specify the domain name.
            request.setDomainName("example.test.com");
            // Specify the beginning of the time range to query, in UTC.
            request.setStartTime("2019-01-15T15:59:59Z");
            // Specify the end of the time range to query, in UTC.
            request.setEndTime("2019-01-20T15:59:58Z");
    
            // List the results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
            try {
                // List the results.
                DescribeVodDomainBpsDataResponse response = describeVodDomainBpsData(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the domain name.
                System.out.println("DomainName:" + response.getDomainName());
                // List the beginning of the time range to query.
                System.out.println("StartTime:" + response.getStartTime());
                // List the end of the time range to query.
                System.out.println("EndTime:" + response.getEndTime());
                // List the query intervals.
                System.out.println("DataInterval:" + response.getDataInterval());
                // List the network bandwidth data.
                if (response.getBpsDataPerInterval() ! = null && response.getBpsDataPerInterval().size() ! = 0) {
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



Query the logs of a domain name {#h2--div-id-describevoddomainlog-div-8}
------------------------------------------------------------------------

You can call the DescribeVodDomainLog operation to query the logs of a domain name.
For more information about the request and response parameters of this operation, see [DescribeVodDomainLog](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Log management/DescribeVodDomainLog.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainLogRequest;
    import com.aliyuncs.vod.model.v20170321.DescribeVodDomainLogResponse;
    import java.util.List;
    
    /**
     * Query the logs of a domain name.
     */
    public static DescribeVodDomainLogResponse describeVodDomainLog(DefaultAcsClient client) throws Exception {
            DescribeVodDomainLogRequest request = new DescribeVodDomainLogRequest();
            // Specify the domain name.
            request.setDomainName("zhptest.alicdn.com");
            // Specify the beginning of the time range to query, in UTC.
            request.setStartTime("2019-01-15T15:59:59Z");
            // Specify the end of the time range to query, in UTC.
            request.setEndTime("2019-01-20T15:59:58Z");
            // Specify the number of entries to return on each page.
            //request.setPageSize(300L);
            // Specify the number of the page to return.
            //request.setPageNumber(1L);
    
            // List the results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
            try {
                // List the results.
                DescribeVodDomainLogResponse response = describeVodDomainLog(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
    
                // List the details about CDN logs.
                if (response.getDomainLogDetails() ! = null && response.getDomainLogDetails().size() ! = 0) {
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
                        if (logInfos ! = null && logInfos.size() ! = 0) {
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


