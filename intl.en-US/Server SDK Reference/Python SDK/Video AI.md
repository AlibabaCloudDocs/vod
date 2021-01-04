Video AI 
=============================

This topic provides examples on how to use the API operations of the video AI module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to submit or query AI jobs, specify an AI template as the default one, and query the default AI template. You can also create, delete, modify, and query AI templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Submit an AI job {#h2--ai-div-id-submitaijob-div-2}
---------------------------------------------------

You can call the SubmitAIJob operation to submit an AI job.

For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example:

    from aliyunsdkvod.request.v20170321 import SubmitAIJobRequest
    def submit_ai_job(clt):
        request = SubmitAIJobRequest.SubmitAIJobRequest()
        request.set_MediaId ('<videoId>')# The video ID.
        request.set_Types('AIVideoCover')  # The AI type. Make sure that this AI type is enabled.
    
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



Query AI jobs {#h2--ai-div-id-listaijob-div-3}
----------------------------------------------

You can call the ListAIJob operation to query AI jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--ai-div-id-listaijob-div-3}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



Create an AI template {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------

You can call the AddAITemplate operation to create an AI template.
For more information about the request and response parameters of this operation, see [AddAITemplate](). Example: {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import AddAITemplateRequest
    def add_ai_template(clt):
        request = AddAITemplateRequest.AddAITemplateRequest()
    
        # The template type. For this example, specify an automated review template.
        request.set_TemplateType('AIMediaAudit')
        # The template name.
        request.set_TemplateName('My AI Template')
        # The detailed configurations of the template.
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



Delete an AI template {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------

You can call the DeleteAITemplate operation to delete an AI template.
For more information about the request and response parameters of this operation, see [DeleteAITemplate](). Example: {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



Modify an AI template {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------

You can call the UpdateAITemplate operation to modify an AI template.
For more information about the request and response parameters of this operation, see [UpdateAITemplate](). Example: {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateAITemplateRequest
    def update_ai_template(clt):
        request = UpdateAITemplateRequest.UpdateAITemplateRequest()
        # The template ID.
        request.set_TemplateId('<TemplateId>')
        # The template name.
        request.set_TemplateName('New AI Template Name')
        # The detailed configurations of the template.
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



Query an AI template {#h2--ai-div-id-getaitemplate-div-7}
---------------------------------------------------------

You can call the GetAITemplate operation to query details about an AI template.
For more information about the request and response parameters of this operation, see [GetAITemplate](). Example: {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



Query AI templates {#h2--ai-div-id-listaitemplate-div-8}
--------------------------------------------------------

You can call the ListAITemplate operation to query AI templates.
For more information about the request and response parameters of this operation, see [ListAITemplate](). Example: {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



Specify an AI template as the default one {#h2--ai-div-id-setdefaultaitemplate-div-9}
-------------------------------------------------------------------------------------

You can call the SetDefaultAITemplate operation to specify an AI template as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultAITemplate](). Example: {#h2--ai-div-id-setdefaultaitemplate-div-9}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



Query the default AI template {#h2--ai-div-id-getdefaultaitemplate-div-10}
--------------------------------------------------------------------------

You can call the GetDefaultAITemplate operation to query details about the default AI template.
For more information about the request and response parameters of this operation, see [GetDefaultAITemplate](). Example: {#h2--ai-div-id-getdefaultaitemplate-div-10}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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


