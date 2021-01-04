Media review 
=================================

This topic provides examples on how to use the API operations of the media review module. The API operations are encapsulated in ApsaraVideo VOD SDK for SDK. You can call the API operations to submit and query automated review jobs. You can also query automated review results and create manual reviews.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Submit an automated review job {#h2--div-id-submitaimediaauditjob-div-2}
------------------------------------------------------------------------

You can call the SubmitAIMediaAuditJob operation to submit an automated review job.

For more information about the request and response parameters of this operation, see [SubmitAIMediaAuditJob](). Example:

    import com.aliyuncs.vod.model.v20170321.SubmitAIMediaAuditJobRequest;
    import com.aliyuncs.vod.model.v20170321.SubmitAIMediaAuditJobResponse;
    
    /**
     * Submit an automated review job.
     */
    public static SubmitAIMediaAuditJobResponse submitAIMediaAuditJob(DefaultAcsClient client) throws Exception {
            SubmitAIMediaAuditJobRequest request = new SubmitAIMediaAuditJobRequest();
            // The ID of the video.
            request.setMediaId("dc063078c1d845139e2a5bd8ff****");
    
            // The returned results.
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
                // List execution results.
                SubmitAIMediaAuditJobResponse response = submitAIMediaAuditJob(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the ID of the video.
                System.out.println("MediaId:" + response.getMediaId());
                // List the ID of the job.
                System.out.println("JobId:" + response.getJobId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Query an automated review job {#h2--div-id-getaimediaauditjob-div-3}
--------------------------------------------------------------------

You can call GetAIMediaAuditJob operation to query details about an automated review job.
For more information about the request and response parameters of this operation, see [GetAIMediaAuditJob](). Example: {#h2--div-id-getaimediaauditjob-div-3}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetAIMediaAuditJobRequest;
    import com.aliyuncs.vod.model.v20170321.GetAIMediaAuditJobResponse;
    
    /**
     * Query an automated review job.
     */
    public static GetAIMediaAuditJobResponse getAIMediaAuditJob(DefaultAcsClient client) throws Exception {
            GetAIMediaAuditJobRequest request = new GetAIMediaAuditJobRequest();
            // The ID of the job.
            request.setJobId("7dc69b893c8b4f13b47aae8de0df****");
    
            // The returned results.
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
                // List execution results.
                GetAIMediaAuditJobResponse response = getAIMediaAuditJob(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
    
                // List the results.
                System.out.println("MediaId:" + response.getMediaAuditJob().getMediaId());
                System.out.println("JobId:" + response.getMediaAuditJob().getJobId());
                System.out.println("Type:" + response.getMediaAuditJob().getType());
                System.out.println("Status:" + response.getMediaAuditJob().getStatus());
                System.out.println("Code:" + response.getMediaAuditJob().getCode());
                System.out.println("Message:" + response.getMediaAuditJob().getMessage());
                System.out.println("Data AbnormalModules:" + response.getMediaAuditJob().getData().getAbnormalModules());
                System.out.println("Data Label:" + response.getMediaAuditJob().getData().getLabel());
                System.out.println("Data Suggestion:" + response.getMediaAuditJob().getData().getSuggestion());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Query the summary of automated review results {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------

You can call the GetMediaAuditResult operation to query the summary of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResult](). Example: {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetMediaAuditResultRequest;
    import com.aliyuncs.vod.model.v20170321.GetMediaAuditResultResponse;
    
    /**
     * Query the summary of automated review results.
     */
    public static GetMediaAuditResultResponse getMediaAuditResult(DefaultAcsClient client) throws Exception {
            GetMediaAuditResultRequest request = new GetMediaAuditResultRequest();
            // The ID of the video.
            request.setMediaId("dc063078c1d845139e2a5bd8f58****");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     */
    // Call example
        public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List execution results.
                GetMediaAuditResultResponse response = getMediaAuditResult(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
    
                // List job results.
                System.out.println("Data AbnormalModules:" + response.getMediaAuditResult().getAbnormalModules());
                System.out.println("Data Label:" + response.getMediaAuditResult().getLabel());
                System.out.println("Data Suggestion:" + response.getMediaAuditResult().getSuggestion());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Query details about automated review results {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultDetail operation to query details about automated review results.

For more information about the request and response parameters of this operation, see [GetMediaAuditResultDetail](). Example:

    import com.aliyuncs.vod.model.v20170321.GetMediaAuditResultDetailRequest;
    import com.aliyuncs.vod.model.v20170321.GetMediaAuditResultDetailResponse;
    
    /**
     * Query details about automated review results.
     */
    public static GetMediaAuditResultDetailResponse getMediaAuditResultDetail(DefaultAcsClient client) throws Exception {
            GetMediaAuditResultDetailRequest request = new GetMediaAuditResultDetailRequest();
            // The ID of the video.
            request.setMediaId("dc063078c1d845139e2a5bd8f69****");
            // The number of the page to return.
            request.setPageNo(1);
    
            // The returned results.
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
                // List execution results.
                GetMediaAuditResultDetailResponse response = getMediaAuditResultDetail(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
    
                // List the results.
                System.out.println("Data Total:" + response.getMediaAuditResultDetail().getTotal());
                System.out.println("Data List Size:" + response.getMediaAuditResultDetail().getList().size());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Query the timeline of automated review results {#h2--div-id-getmediaauditresulttimeline-div-6}
----------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultTimeline operation to query the timeline of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultTimeline](). Example: {#h2--div-id-getmediaauditresulttimeline-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetMediaAuditResultTimelineRequest;
    import com.aliyuncs.vod.model.v20170321.GetMediaAuditResultTimelineResponse;
    
    /**
     * Query the timeline of automated review results.
     */
    public static GetMediaAuditResultTimelineResponse getMediaAuditResultTimeline(DefaultAcsClient client) throws Exception {
            GetMediaAuditResultTimelineRequest request = new GetMediaAuditResultTimelineRequest();
            // The ID of the video.
            request.setMediaId("dc063078c1d845139e2a5bd8f55****");
    
            // The returned results.
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
                // List execution results.
                GetMediaAuditResultTimelineResponse response = getMediaAuditResultTimeline(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
    
                // List the results.
                System.out.println(response.getMediaAuditResultTimeline().getTerrorism());
                System.out.println(response.getMediaAuditResultTimeline().getPorn());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Create a manual review {#h2--div-id-createaudit-div-7}
------------------------------------------------------

You can call the CreateAuditRequest operation to create a manual review.
For more information about the request and response parameters of this operation, see [CreateAuditRequest](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md). Example: {#h2--div-id-createaudit-div-7}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.CreateAuditRequest;
    import com.aliyuncs.vod.model.v20170321.CreateAuditResponse;
    import com.alibaba.fastjson.JSONObject;
    
    /**
     * Build parameters for a review.
     */
    public static String buildAuditContent() throws Exception {
            List<JSONObject> auditContents = new ArrayList<>();
    
            JSONObject auditContent = new JSONObject();
            auditContent.put("VideoId", "3ebc10160bda481ca9b6858a0b58****"); // The video ID.
            auditContent.put("Status", "Blocked"); // The review status.
            auditContent.put("Reason", "Including porn"); // If the review status is Blocked, a reason must be provided. The reason can contain a maximum of 128 bytes.
            auditContents.add(auditContent);
    
            return auditContents.toString();
    }
    
    /**
     * Create a manual review.
     */
    public static CreateAuditResponse createAudit(DefaultAcsClient client) throws Exception {
            CreateAuditRequest request = new CreateAuditRequest();
            // The review content.
            request.setAuditContent(buildAuditContent());
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // Submit manual review results.
            CreateAuditResponse response = createAudit(client);
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



Query the historical records of manual reviews {#h2--div-id-getaudithistory-div-8}
----------------------------------------------------------------------------------

You can call the GetAuditHistory operation to query the historical records of manual reviews.
For more information about the request and response parameters of this operation, see [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md). Example: {#h2--div-id-getaudithistory-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetAuditHistoryRequest;
    import com.aliyuncs.vod.model.v20170321.GetAuditHistoryResponse;
    
    /**
     * Query the historical records of manual reviews.
     */
    public static GetAuditHistoryResponse getAuditHistory(DefaultAcsClient client) throws Exception {
            GetAuditHistoryRequest request = new GetAuditHistoryRequest();
    
            // The video ID.
            request.setVideoId("3ebc10160bda481ca9b6858a0b25****");
            // The number of the page to return.
            request.setPageNo(1L);
            // The number of entries to return on each page.
            request.setPageSize(10L);
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // Query the historical records of manual reviews.
            GetAuditHistoryResponse response = getAuditHistory(client);
    
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
            // List the total number of historical records.
            System.out.println("Total:" + response.getTotal());
            // List the result of the current review.
            System.out.println("Status:" + response.getStatus());
            // List historical records.
            System.out.println("Histories:" + response.getHistories().toString());
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



Set an IP address whitelist for reviews {#h2--ip-div-id-setauditsecurityip-div-9}
---------------------------------------------------------------------------------

You can call the SetAuditSecurityIp operation to set an IP address whitelist for reviews.
For more information about the request and response parameters of this operation, see [SetAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/SetAuditSecurityIp.md). Example: {#h2--ip-div-id-setauditsecurityip-div-9}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SetAuditSecurityIpRequest;
    import com.aliyuncs.vod.model.v20170321.SetAuditSecurityIpResponse;
    
    /**
     * Set an IP address whitelist for reviews.
     */
    public static SetAuditSecurityIpResponse setAuditSecurityIp(DefaultAcsClient client) throws Exception {
            SetAuditSecurityIpRequest request = new SetAuditSecurityIpRequest();
    
            // The name of the IP address whitelist for reviews. The default value is Default.
            request.setSecurityGroupName("MyGroupName");
            // The operation type. The default value is Append, which indicates that IP addresses are added to the whitelist.
            request.setOperateMode("Cover");
            // The IP addresses that are added to the whitelist.
            request.setIps("10.23.12.20,10.23.12.21,10.23.12.22");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // Set an IP address whitelist for reviews.
            SetAuditSecurityIpResponse response = setAuditSecurityIp(client);
    
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



Query the IP addresses in a whitelist {#h2--ip-div-id-listauditsecurityip-div-10}
---------------------------------------------------------------------------------

You can call the ListAuditSecurityIp operation to query the IP addresses in a whitelist.
For more information about the request and response parameters of this operation, see [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md). Example: {#h2--ip-div-id-listauditsecurityip-div-10}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListAuditSecurityIpRequest;
    import com.aliyuncs.vod.model.v20170321.ListAuditSecurityIpResponse;
    
    /**
     * Query the IP addresses in a whitelist.
     */
    public static ListAuditSecurityIpResponse listAuditSecurityIp(DefaultAcsClient client) throws Exception {
            ListAuditSecurityIpRequest request = new ListAuditSecurityIpRequest();
    
            // The name of the whitelist.
            request.setSecurityGroupName("MyGroupName");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    
    /**
     * Call example
     * @param args
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // Query the IP addresses in a whitelist.
            ListAuditSecurityIpResponse response = listAuditSecurityIp(client);
    
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
            // List the IP addresses.
            System.out.println("SecurityIpList:" + response.getSecurityIpList().toString());
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }


