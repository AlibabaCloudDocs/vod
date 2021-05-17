Transcoding task 
=====================================

This topic provides examples on how to use the API operations of the transcoding task module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to query the transcoding summary of a video, transcoding tasks, and details about a transcoding task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Query the transcoding summary of a video {#h2--div-id-gettranscodesummary-div-2}
--------------------------------------------------------------------------------

You can call the GetTranscodeSummary operation to query the transcoding summary of a video.
For more information about the request and response parameters of this operation, see [GetTranscodeSummary](/intl.en-US/API Reference/Media processing/Transcoding task/GetTranscodeSummary.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetTranscodeSummaryRequest;
    import com.aliyuncs.vod.model.v20170321.GetTranscodeSummaryResponse;
    
    /**
     * Query the transcoding summary of a video.
     */
    public static GetTranscodeSummaryResponse getTranscodeSummary(DefaultAcsClient client) throws Exception {
        GetTranscodeSummaryRequest request = new GetTranscodeSummaryRequest();
        request.setVideoIds("14f35e2c5ca348831c2d2ae1d5b****,1dd4516420d247c777538c9aaa****");
        return client.getAcsResponse(request);
    }
    
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        GetTranscodeSummaryResponse response = new GetTranscodeSummaryResponse();
        try {
            response = getTranscodeSummary(client);
            for (GetTranscodeSummaryResponse.TranscodeSummary summary : response.getTranscodeSummaryList()) {
                // The transcoding status.
                System.out.println("TranscodeStatus = " + summary.getTranscodeStatus());
                for (GetTranscodeSummaryResponse.TranscodeSummary.TranscodeJobInfoSummary jobInfoSummary : summary.getTranscodeJobInfoSummaryList()) {
                    // The transcoding progress.
                    System.out.println("TranscodeProgress = " + jobInfoSummary.getTranscodeProgress());
                    // The status of the transcoding job.
                    System.out.println("TranscodeJobStatus = " + jobInfoSummary.getTranscodeJobStatus());
                    // The time when the transcoding job was completed.
                    System.out.println("CompleteTime = " + jobInfoSummary.getCompleteTime());
                }
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Query transcoding tasks {#h2--div-id-listtranscodetask-div-3}
-------------------------------------------------------------

You can call the ListTranscodeTask operation to query transcoding tasks.
For more information about the request and response parameters of this operation, see [ListTranscodeTask](/intl.en-US/API Reference/Media processing/Transcoding task/ListTranscodeTask.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListTranscodeTaskRequest;
    import com.aliyuncs.vod.model.v20170321.ListTranscodeTaskResponse;
    
    /**
     * Query transcoding tasks.
     */
    public static ListTranscodeTaskResponse listTranscodeTask(DefaultAcsClient client) throws Exception {
        ListTranscodeTaskRequest request = new ListTranscodeTaskRequest();
        request.setVideoId("14f35e2c5ca345cb88de1d5b2801");
        return client.getAcsResponse(request);
    }
    
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        ListTranscodeTaskResponse response = new ListTranscodeTaskResponse();
        try {
            response = listTranscodeTask(client);
            for (ListTranscodeTaskResponse.TranscodeTask transcodeTask : response.getTranscodeTaskList()) {
                // The ID of the transcoding task.
                System.out.println("TranscodeTaskId = " + transcodeTask.getTranscodeTaskId());
                // The status of the transcoding task.
                System.out.println("TaskStatus = " + transcodeTask.getTaskStatus());
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Query details about a transcoding task {#h2--div-id-gettranscodetask-div-4}
---------------------------------------------------------------------------

You can call the GetTranscodeTask operation to query details about a transcoding task.
For more information about the request and response parameters of this operation, see [GetTranscodeTask](/intl.en-US/API Reference/Media processing/Transcoding task/GetTranscodeTask.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetTranscodeTaskRequest;
    import com.aliyuncs.vod.model.v20170321.GetTranscodeTaskResponse;
    
    /**
     * Query details about a transcoding task.
     */
    public static GetTranscodeTaskResponse getTranscodeTask(DefaultAcsClient client) throws Exception {
        GetTranscodeTaskRequest request = new GetTranscodeTaskRequest();
        request.setTranscodeTaskId("eab6f992b5f9436e6f425****");
        return client.getAcsResponse(request);
    }
    
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        GetTranscodeTaskResponse response = new GetTranscodeTaskResponse();
        try {
            response = getTranscodeTask(client);
            // The ID of the transcoding task.
            System.out.println("TranscodeTaskId = " + response.getTranscodeTask().getTranscodeTaskId());
            // The status of the transcoding task.
            System.out.println("TaskStatus = " + response.getTranscodeTask().getTaskStatus());
            for (GetTranscodeTaskResponse.TranscodeTask.TranscodeJobInfo jobInfo : response.getTranscodeTask().getTranscodeJobInfoList()) {
                // The ID of the transcoding job.
                System.out.println("TranscodeJobId = " + jobInfo.getTranscodeJobId());
                // The status of the transcoding job.
                System.out.println("TranscodeJobStatus = " + jobInfo.getTranscodeJobStatus());
                // The transcoding progress.
                System.out.println("TranscodeProgress = " + jobInfo.getTranscodeProgress());
                // The time when the transcoding job was completed.
                System.out.println("CompleteTime = " + jobInfo.getCompleteTime());
    
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }


