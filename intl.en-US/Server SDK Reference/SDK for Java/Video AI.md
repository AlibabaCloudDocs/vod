Video AI 
=============================

This topic provides examples on how to use the API operations of the video AI module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to submit or query AI jobs, specify an AI template as the default one, and query the default AI template. You can also create, delete, modify, and query AI templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Submit an AI job {#h2--ai-div-id-submitaijob-div-2}
---------------------------------------------------

You can call the SubmitAIJob operation to submit an AI job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SubmitAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.SubmitAIJobResponse;
    
    /**
     * Submit a job.
     */
    public static SubmitAIJobResponse submitAIJob(DefaultAcsClient client) throws Exception {
        SubmitAIJobRequest request = new SubmitAIJobRequest();
        // The video ID.
        request.setMediaId("3eb19a4585bc475e995bdd4a5c****");
        // The AI type. Make sure that the AI type is enabled.
        request.setTypes("AIVideoCover");
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



Query AI jobs {#h2--ai-div-id-listaijob-div-3}
----------------------------------------------

You can call the ListAIJob operation to query AI jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--ai-div-id-listaijob-div-3}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.ListAIJobResponse;
    
    /**
     * Query AI jobs.
     */
    public static ListAIJobResponse listAIJob(DefaultAcsClient client) throws Exception {
        ListAIJobRequest request = new ListAIJobRequest();
        // The job ID.
        request.setJobIds("979d4d7a36ae41b1a945a2xxxxx,3eb19a4585bc475e995bddea****");
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
            // Query AI jobs.
            ListAIJobResponse response = listAIJob(client);
    
            // List the ID of the request.
            System.out.println("ResquestId:" + response.getRequestId());
    
            // List AI jobs.
            System.out.println("============ AIJobList:");
            if (response.getAIJobList() ! = null && response.getAIJobList().size() ! = 0) {
                for (ListAIJobResponse.AIJob aiJob: response.getAIJobList()) {
                    // The video ID.
                    System.out.println("MediaId:" + aiJob.getMediaId());
                    // The job ID.
                    System.out.println("JobId:" + aiJob.getJobId());
                    // The AI type.
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



Create an AI template {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------

You can call the AddAITemplate operation to create an AI template.
For more information about the request and response parameters of this operation, see [AddAITemplate](). Example: {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.alibaba.fastjson.JSONArray;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.vod.model.v20170321.AddAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.AddAITemplateResponse;
    
    /**
     * Create an AI template.
     */
    public static AddAITemplateResponse addAITemplate(DefaultAcsClient client) throws Exception {
            AddAITemplateRequest request = new AddAITemplateRequest();
            // The template type. For this example, specify an automated review template.
            request.setTemplateType("AIMediaAudit");
            // The template name.
            request.setTemplateName("myaitemplate");
            // The detailed configurations of the template.
            JSONObject templateConfig = new JSONObject();
            JSONArray auditItem = new JSONArray();
            auditItem.add("terrorism");
            auditItem.add("porn");
            templateConfig.put("AuditItem", auditItem);
    
            JSONArray auditRange = new JSONArray();
            auditRange.add("video");
            auditRange.add("image-cover");
            auditRange.add("text-title");
            templateConfig.put("AuditRange", auditRange);
    
            JSONArray auditContent = new JSONArray();
            auditContent.add("screen");
            templateConfig.put("AuditContent", auditContent);
    
            templateConfig.put("AuditAutoBlock", "no");
            request.setTemplateConfig(templateConfig.toString());
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List execution results.
                AddAITemplateResponse response = addAITemplate(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the ID of the template.
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Delete an AI template {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------

You can call the DeleteAITemplate operation to delete an AI template.
For more information about the request and response parameters of this operation, see [DeleteAITemplate](). Example: {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DeleteAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.DeleteAITemplateResponse;
    
    /**
     * Delete an AI template.
     */
    public static DeleteAITemplateResponse deleteAITemplate(DefaultAcsClient client) throws Exception {
            DeleteAITemplateRequest request = new DeleteAITemplateRequest();
            // The template ID.
            request.setTemplateId("1d763dd8987a122ab8596eb7d57****");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List execution results.
                DeleteAITemplateResponse response = deleteAITemplate(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the ID of the template.
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Modify an AI template {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------

You can call the UpdateAITemplate operation to modify an AI template.

For more information about the request and response parameters of this operation, see [UpdateAITemplate](). Example:

    import com.alibaba.fastjson.JSONArray;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.vod.model.v20170321.UpdateAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.UpdateAITemplateResponse;
    
    /**
     * Modify an AI template.
     */
    public static UpdateAITemplateResponse updateAITemplate(DefaultAcsClient client) throws Exception {
            UpdateAITemplateRequest request = new UpdateAITemplateRequest();
            // The template ID.
            request.setTemplateId("1d763dd8987a122ab8596eb7d257****");
            // The template name.
            request.setTemplateName("myaitemplate1");
            // The detailed configurations of the template.
            JSONObject templateConfig = new JSONObject();
            JSONArray auditItem = new JSONArray();
            //auditItem.add("terrorism");
            auditItem.add("porn");
            templateConfig.put("AuditItem", auditItem);
    
            JSONArray auditRange = new JSONArray();
            auditRange.add("video");
            auditRange.add("image-cover");
            //auditRange.add("text-title");
            templateConfig.put("AuditRange", auditRange);
    
            JSONArray auditContent = new JSONArray();
            auditContent.add("screen");
            templateConfig.put("AuditContent", auditContent);
    
            templateConfig.put("AuditAutoBlock", "no");
            request.setTemplateConfig(templateConfig.toString());
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List execution results.
                UpdateAITemplateResponse response = updateAITemplate(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the ID of the template.
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Query an AI template {#h2--ai-div-id-getaitemplate-div-7}
---------------------------------------------------------

You can call the GetAITemplate operation to query details about an AI template.
For more information about the request and response parameters of this operation, see [GetAITemplate](). Example: {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.GetAITemplateResponse;
    
    /**
     * Query an AI template.
     */
    public static GetAITemplateResponse getAITemplate(DefaultAcsClient client) throws Exception {
            GetAITemplateRequest request = new GetAITemplateRequest();
            // The template ID.
            request.setTemplateId("1d763dd8987a122ab8596eb7d257****");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List execution results.
                GetAITemplateResponse response = getAITemplate(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the information about the template.
                System.out.println("TemplateId:" + response.getTemplateInfo().getTemplateId());
                System.out.println("TemplateType:" + response.getTemplateInfo().getTemplateType());
                System.out.println("TemplateName:" + response.getTemplateInfo().getTemplateName());
                System.out.println("TemplateConfig:" + response.getTemplateInfo().getTemplateConfig());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Query AI templates {#h2--ai-div-id-listaitemplate-div-8}
--------------------------------------------------------

You can call the ListAITemplate operation to query AI templates.
For more information about the request and response parameters of this operation, see [ListAITemplate](). Example: {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.ListAITemplateResponse;
    
    /**
     * Query AI templates.
     */
    public static ListAITemplateResponse listAITemplate(DefaultAcsClient client) throws Exception {
            ListAITemplateRequest request = new ListAITemplateRequest();
            // The template type. For this example, specify an automated review template.
            request.setTemplateType("AIMediaAudit");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List the results.
                ListAITemplateResponse response = listAITemplate(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the information about the template.
                if (response.getTemplateInfoList() ! = null) {
                    for (ListAITemplateResponse.TemplateInfoListItem templateInfo : response.getTemplateInfoList()) {
                        System.out.println("================");
                        System.out.println("TemplateId:" + templateInfo.getTemplateId());
                        System.out.println("TemplateType:" + templateInfo.getTemplateType());
                        System.out.println("TemplateName:" + templateInfo.getTemplateName());
                        System.out.println("TemplateConfig:" + templateInfo.getTemplateConfig());
                    }
                }
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Specify an AI template as the default one {#h2--ai-div-id-setdefaultaitemplate-div-9}
-------------------------------------------------------------------------------------

You can call the SetDefaultAITemplate operation to specify an AI template as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultAITemplate](). Example: {#h2--ai-div-id-setdefaultaitemplate-div-9}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SetDefaultAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.SetDefaultAITemplateResponse;
    
    /**
     * Specify an AI template as the default one.
     */
    public static SetDefaultAITemplateResponse setDefaultAITemplate(DefaultAcsClient client) throws Exception {
            SetDefaultAITemplateRequest request = new SetDefaultAITemplateRequest();
            // The template ID.
            request.setTemplateId("1d763dd8987a122ab8596eb757****");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List execution results.
                SetDefaultAITemplateResponse response = setDefaultAITemplate(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the ID of the template.
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



Query the default AI template {#h2--ai-div-id-getdefaultaitemplate-div-10}
--------------------------------------------------------------------------

You can call the GetDefaultAITemplate operation to query details about the default AI template.
For more information about the request and response parameters of this operation, see [GetDefaultAITemplate](). Example: {#h2--ai-div-id-getdefaultaitemplate-div-10}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetDefaultAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.GetDefaultAITemplateResponse;
    
    /**
     * Query the default AI template.
     */
    public static GetDefaultAITemplateResponse getDefaultAITemplate(DefaultAcsClient client) throws Exception {
            GetDefaultAITemplateRequest request = new GetDefaultAITemplateRequest();
            // The template type. For this example, specify an automated review template.
            request.setTemplateType("AIMediaAudit");
    
            // The returned results.
            return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // Initialize the client.
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // List execution results.
                GetDefaultAITemplateResponse response = getDefaultAITemplate(client);
    
                // List the ID of the request.
                System.out.println("ResquestId:" + response.getRequestId());
                // List the information about the template.
                System.out.println("TemplateId:" + response.getTemplateInfo().getTemplateId());
                System.out.println("TemplateType:" + response.getTemplateInfo().getTemplateType());
                System.out.println("TemplateName:" + response.getTemplateInfo().getTemplateName());
                System.out.println("IsDefault:" + response.getTemplateInfo().getIsDefault());
                System.out.println("TemplateConfig:" + response.getTemplateInfo().getTemplateConfig());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }


