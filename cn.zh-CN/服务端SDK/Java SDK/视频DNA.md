视频DNA 
==========================

本篇文档提供了Java SDK视频DNA模块相关功能的API调用示例。包含提交视频DNA作业、查询视频DNA作业、获取视频DNA结果。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/Java SDK/初始化.md)。

提交视频DNA作业 {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------

调用SubmitAIJob接口，完成提交视频DNA作业功能。

接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/提交视频DNA作业.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.SubmitAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.SubmitAIJobResponse;
    
    /**
     * 提交作业
     */
    public static SubmitAIJobResponse submitAIJob(DefaultAcsClient client) throws Exception {
        SubmitAIJobRequest request = new SubmitAIJobRequest();
        // 设置视频ID
        request.setMediaId("3eb19a4585bc475e995bdd4d9a****");
        // 设置AI类型，类型为AIMediaDNA
        request.setTypes("AIMediaDNA");
        // 返回结果
        return client.getAcsResponse(request);
    }
    
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // 提交作业
            SubmitAIJobResponse response = submitAIJob(client);
    
            // 打印请求ID
            System.out.println("ResquestId:" + response.getRequestId());
            // 打印结果信息
            if (response.getAIJobList() != null && response.getAIJobList().size() != 0) {
                for (SubmitAIJobResponse.AIJob aiJob : response.getAIJobList()) {
                  // 视频ID
                  System.out.println("MediaId:" + aiJob.getMediaId());
                  // 作业ID
                  System.out.println("JobId:" + aiJob.getJobId());
                  // AI类型
                  System.out.println("Type:" + aiJob.getType());
                }
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



查询视频DNA作业 {#h2--dna-div-id-listaijob-div-3}
-------------------------------------------

调用ListAIJob接口，完成查询视频DNA作业功能。

接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/查询视频DNA作业.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.ListAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.ListAIJobResponse;
    
    /**
     * 查询作业
     */
    public static ListAIJobResponse listAIJob(DefaultAcsClient client) throws Exception {
        ListAIJobRequest request = new ListAIJobRequest();
        // 设置作业ID
        request.setJobIds("979d4d7a36ae41b1a945a257****,3eb19a4585bc475e995bddea57****");
        // 返回结果
        return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // 查询作业
            ListAIJobResponse response = listAIJob(client);
    
            // 打印请求ID
            System.out.println("ResquestId:" + response.getRequestId());
    
            // 打印作业列表
            System.out.println("============ AIJobList:");
            if (response.getAIJobList() != null && response.getAIJobList().size() != 0) {
                for (ListAIJobResponse.AIJob aiJob: response.getAIJobList()) {
                    // 视频ID
                    System.out.println("MediaId:" + aiJob.getMediaId());
                    // 作业ID
                    System.out.println("JobId:" + aiJob.getJobId());
                    // AI类型，注意校验类型是否为AIMediaDNA
                    System.out.println("Type:" + aiJob.getType());
                    // 作业状态
                    System.out.println("Status:" + aiJob.getStatus());
                    // 作业结果
                    System.out.println("Data:" + aiJob.getData());
                }
            }
    
            // 打印不存在的作业ID
            System.out.println("============ NonExistAIJobIds:");
            if (response.getNonExistAIJobIds() != null && response.getNonExistAIJobIds().size() != 0) {
                for (String jobId: response.getNonExistAIJobIds()) {
                    // 作业ID
                    System.out.println("NonExistAIJobId:" + jobId);
                }
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



获取视频DNA结果 {#h2--dna-div-id-getmediadnaresult-div-4}
---------------------------------------------------

调用GetMediaDNAResult接口，完成获取视频DNA结果功能。

接口参数和返回字段请参见[GetMediaDNAResult](/cn.zh-CN/服务端API/视频AI/视频DNA/获取视频DNA结果.md)。调用示例如下：

    import com.aliyuncs.vod.model.v20170321.GetMediaDNAResultRequest;
    import com.aliyuncs.vod.model.v20170321.GetMediaDNAResultResponse;
    
    /**
     * 查询结果
     */
    public static GetMediaDNAResultResponse getMediaDNAResult(DefaultAcsClient client) throws Exception {
        GetMediaDNAResultRequest request = new GetMediaDNAResultRequest();
        // 设置视频ID
        request.setMediaId("3eb19a4585bc475e995bdd57****");
        // 返回结果
        return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // 查询结果
            GetMediaDNAResultResponse response = getMediaDNAResult(client);
            // 打印请求ID
            System.out.println("ResquestId:" + response.getRequestId());
            // 打印DNA结果
            System.out.println("DNAResult:" + response.getDNAResult().toString());
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }


