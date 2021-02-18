视频DNA 
==========================

本篇文档提供了Python SDK视频DNA模块相关功能的API调用示例。包含提交视频DNA作业、查询视频DNA作业、获取视频DNA结果。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/Python SDK/初始化.md)。

提交视频DNA作业 {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------

调用SubmitAIJob接口，完成提交视频DNA作业功能。

接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/提交视频DNA作业.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import SubmitAIJobRequest
    def submit_ai_job(clt):
        request = SubmitAIJobRequest.SubmitAIJobRequest()
        request.set_MediaId('<videoId>')  # 视频ID
        request.set_Types('AIMediaDNA')  # 设置AI类型，类型为AIMediaDNA
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        job = submit_ai_job(clt)
        print(json.dumps(job, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



查询视频DNA作业 {#h2--dna-div-id-listaijob-div-3}
-------------------------------------------

调用ListAIJob接口，完成查询视频DNA作业功能。

接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/查询视频DNA作业.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import ListAIJobRequest
    def list_ai_job(clt):
        request = ListAIJobRequest.ListAIJobRequest()
        jobIds = ['jobId1', 'jobId2']
        request.set_JobIds(','.join(jobIds))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        jobs = list_ai_job(clt)
        print(json.dumps(jobs, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



获取视频DNA结果 {#h2--dna-div-id-getmediadnaresult-div-4}
---------------------------------------------------

调用GetMediaDNAResult接口，完成获取视频DNA结果功能。

接口参数和返回字段请参见[GetMediaDNAResult](/cn.zh-CN/服务端API/视频AI/视频DNA/获取视频DNA结果.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import GetMediaDNAResultRequest
    def get_media_dna_result(clt):
        request = GetMediaDNAResultRequest.GetMediaDNAResultRequest()
        request.set_MediaId('<videoId>')  # 视频ID
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        dna = get_media_dna_result(clt)
        print(json.dumps(dna, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


