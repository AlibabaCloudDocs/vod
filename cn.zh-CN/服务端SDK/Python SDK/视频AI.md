视频AI 
=========================

本篇文档提供了Python SDK视频AI模块相关功能的API调用示例。包含提交AI作业、查询AI作业、添加AI模板、修改AI模板、删除AI模板、查询AI模板、查询设置默认AI模板等。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/Python SDK/初始化.md)接口。

提交AI作业 {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交AI作业功能。

接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/提交AI作业.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import SubmitAIJobRequest
    def submit_ai_job(clt):
        request = SubmitAIJobRequest.SubmitAIJobRequest()
        request.set_MediaId('<videoId>')  # 视频ID
        request.set_Types('AIVideoCover')  # AI类型，请确保已开通该类型AI服务
    
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



查询AI作业 {#h2--ai-div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询AI作业功能。

接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/查询AI作业.md)。调用示例如下：

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



添加AI模板 {#h2--ai-div-id-addaitemplate-div-4}
-------------------------------------------

调用AddAITemplate接口，完成添加AI模板功能。

接口参数和返回字段请参见[AddAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/添加AI模板.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import AddAITemplateRequest
    def add_ai_template(clt):
        request = AddAITemplateRequest.AddAITemplateRequest()
    
        # 设置模板类型，以智能审核模板为例
        request.set_TemplateType('AIMediaAudit')
        # 设置模板名称
        request.set_TemplateName('My AI Template')
        # 设置模板详细配置
        auditItem = ['terrorism', 'porn']
        auditRange = ['video', 'image-cover', 'text-title']
        auditContent = ['screen']
        templateConfig = {'AuditItem': auditItem, 'AuditRange': auditRange, 'AuditContent': auditContent,
                          'AuditAutoBlock': 'no'}
        request.set_TemplateConfig(json.dumps(templateConfig))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = add_ai_template(clt)
        print(res['TemplateId'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



删除AI模板 {#h2--ai-div-id-deleteaitemplate-div-5}
----------------------------------------------

调用DeleteAITemplate接口，完成删除AI模板功能。

接口参数和返回字段请参见[DeleteAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/删除AI模板.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import DeleteAITemplateRequest
    def delete_ai_template(clt):
        request = DeleteAITemplateRequest.DeleteAITemplateRequest()
        request.set_TemplateId('<TemplateId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = delete_ai_template(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



修改AI模板 {#h2--ai-div-id-updateaitemplate-div-6}
----------------------------------------------

调用UpdateAITemplate接口，完成修改AI模板功能。

接口参数和返回字段请参见[UpdateAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/修改AI模板.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import UpdateAITemplateRequest
    def update_ai_template(clt):
        request = UpdateAITemplateRequest.UpdateAITemplateRequest()
        # 设置模板ID
        request.set_TemplateId('<TemplateId>')
        # 设置模板名称
        request.set_TemplateName('New AI Template Name')
        # 设置模板详细配置
        auditItem = ['terrorism', 'porn']
        auditRange = ['video', 'image-cover']
        auditContent = ['screen']
        templateConfig = {'AuditItem': auditItem, 'AuditRange': auditRange, 'AuditContent': auditContent,
                          'AuditAutoBlock': 'yes'}
        request.set_TemplateConfig(json.dumps(templateConfig))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = update_ai_template(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



查询AI模板 {#h2--ai-div-id-getaitemplate-div-7}
-------------------------------------------

调用GetAITemplate接口，完成查询AI模板功能。

接口参数和返回字段请参见[GetAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import GetAITemplateRequest
    def get_ai_template(clt):
        request = GetAITemplateRequest.GetAITemplateRequest()
        request.set_TemplateId('<TemplateId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        template = get_ai_template(clt)
        print(template['TemplateInfo'])
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



查询AI模板列表 {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------

调用ListAITemplate接口，完成查询AI模板列表功能。

接口参数和返回字段请参见[ListAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板列表.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import ListAITemplateRequest
    def list_ai_template(clt):
        request = ListAITemplateRequest.ListAITemplateRequest()
        request.set_TemplateType('AIMediaAudit')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        templates = list_ai_template(clt)
        print(templates['TemplateInfoList'])
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



设置默认AI模板 {#h2--ai-div-id-setdefaultaitemplate-div-9}
----------------------------------------------------

调用SetDefaultAITemplate接口，完成设置默认AI模板功能。

接口参数和返回字段请参见[SetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/设置默认AI模板.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import SetDefaultAITemplateRequest
    def set_default_ai_template(clt):
        request = SetDefaultAITemplateRequest.SetDefaultAITemplateRequest()
        request.set_TemplateId('<TemplateId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = set_default_ai_template(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



查询默认AI模板 {#h2--ai-div-id-getdefaultaitemplate-div-10}
-----------------------------------------------------

调用GetDefaultAITemplate接口，完成查询默认AI模板功能。

接口参数和返回字段请参见[GetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询默认AI模板.md)。调用示例如下：

    from aliyunsdkvod.request.v20170321 import GetDefaultAITemplateRequest
    def get_default_ai_template(clt):
        request = GetDefaultAITemplateRequest.GetDefaultAITemplateRequest()
        request.set_TemplateType('AIMediaAudit')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        template = get_default_ai_template(clt)
        print(template['TemplateInfo'])
        print(json.dumps(template, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


