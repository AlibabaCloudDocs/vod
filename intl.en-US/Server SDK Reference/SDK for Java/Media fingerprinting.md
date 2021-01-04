Media fingerprinting 
=========================================

This topic provides examples on how to use the API operations of the media fingerprinting module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to submit media fingerprinting jobs, query media fingerprinting jobs, and query media fingerprinting results.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Submit a media fingerprinting job {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------------------------------

You can call the SubmitAIJob operation to submit a media fingerprinting job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--dna-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SubmitAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.SubmitAIJobResponse;
    
    /**
     * Submit a job.
     */
    public static SubmitAIJobResponse submitAIJob(DefaultAcsClient client) throws Exception {
        SubmitAIJobRequest request = new SubmitAIJobRequest();
        // The video ID.
        request.setMediaId(" 
    3eb19a4585bc475e995bdd4d9a**** 
    ");
        // The AI type. Set the value to AIMediaDNA.
        request.setTypes("AIMediaDNA");
        // The returned results.
        return client.getAcsResponse(request);
    }
    
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // Submit a job.
            SubmitAIJobResponse response = submitAIJob(client);
    
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
            // List the results.
            if (response.getAIJobList() ! = null && response.getAIJobList().size() ! = 0) {
                for (SubmitAIJobResponse.AIJob aiJob : response.getAIJobList()) {
                  // The video ID.
                  System.out.println("MediaId:" + aiJob.getMediaId());
                  // The job ID.
                  System.out.println("JobId:" + aiJob.getJobId());
                  // The AI type.
                  System.out.println("Type:" + aiJob.getType());
                }
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



Query media fingerprinting jobs {#h2--dna-div-id-listaijob-div-3}
-----------------------------------------------------------------

You can call the ListAIJob operation to query media fingerprinting jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--dna-div-id-listaijob-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.ListAIJobResponse;
    
    /**
     * Query media fingerprinting jobs.
     */
    public static ListAIJobResponse listAIJob(DefaultAcsClient client) throws Exception {
        ListAIJobRequest request = new ListAIJobRequest();
        // The job ID.
        request.setJobIds("979d4d7a36ae41b1a945a257****,3eb19a4585bc475e995bddea57****");
        // The returned results.
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // Query media fingerprinting jobs.
            ListAIJobResponse response = listAIJob(client);
    
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
    
            // List media fingerprinting jobs.
            System.out.println("============ AIJobList:");
            if (response.getAIJobList() ! = null && response.getAIJobList().size() ! = 0) {
                for (ListAIJobResponse.AIJob aiJob: response.getAIJobList()) {
                    // The video ID.
                    System.out.println("MediaId:" + aiJob.getMediaId());
                    // The job ID.
                    System.out.println("JobId:" + aiJob.getJobId());
                    // The AI type. Set the value to AIMediaDNA.
                    System.out.println("Type:" + aiJob.getType());
                    // The job status.
                    System.out.println("Status:" + aiJob.getStatus());
                    // The job result.
                    System.out.println("Data:" + aiJob.getData());
                }
            }
    
            // List the IDs of jobs that do not exist.
            System.out.println("============ NonExistAIJobIds:");
            if (response.getNonExistAIJobIds() ! = null && response.getNonExistAIJobIds().size() ! = 0) {
                for (String jobId: response.getNonExistAIJobIds()) {
                    // The job ID.
                    System.out.println("NonExistAIJobId:" + jobId);
                }
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



Query media fingerprinting results {#h2--dna-div-id-getmediadnaresult-div-4}
----------------------------------------------------------------------------

You can call the GetMediaDNAResult operation to query media fingerprinting results.
For more information about the request and response parameters of this operation, see [GetMediaDNAResult](). Example: {#h2--dna-div-id-getmediadnaresult-div-4}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetMediaDNAResultRequest;
    import com.aliyuncs.vod.model.v20170321.GetMediaDNAResultResponse;
    
    /**
     * Query media fingerprinting results.
     */
    public static GetMediaDNAResultResponse getMediaDNAResult(DefaultAcsClient client) throws Exception {
        GetMediaDNAResultRequest request = new GetMediaDNAResultRequest();
        // The video ID.
        request.setMediaId("3eb19a4585bc475e995bdd57****");
        // The returned results.
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // List the results.
            GetMediaDNAResultResponse response = getMediaDNAResult(client);
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
            // List media fingerprinting results.
            System.out.println("DNAResult:" + response.getDNAResult().toString());
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }


