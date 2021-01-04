Media review 
=================================

This topic provides examples on how to use the API operations of the media review module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to submit and query automated review jobs. You can also query automated review results, create manual reviews, and set an IP address whitelist for reviews.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Submit an automated review job {#h2--div-id-submitaimediaauditjob-div-2}
------------------------------------------------------------------------

You can call the SubmitAIMediaAuditJob operation to submit an automated review job.

For more information about the request and response parameters of this operation, see [SubmitAIMediaAuditJob](). Example:

    from aliyunsdkvod.request.v20170321 import SubmitAIMediaAuditJobRequest
    def submit_ai_media_audit_job(clt):
        request = SubmitAIMediaAuditJobRequest.SubmitAIMediaAuditJobRequest()
        request.set_MediaId('<VideoId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = submit_ai_media_audit_job(clt)
        print(res['JobId'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query an automated review job {#h2--div-id-getaimediaauditjob-div-3}
--------------------------------------------------------------------

You can call the GetAIMediaAuditJob operation to query details about an automated review job.

For more information about the request and response parameters of this operation, see [GetAIMediaAuditJob](). Example:

    from aliyunsdkvod.request.v20170321 import GetAIMediaAuditJobRequest
    def get_ai_media_audit_job(clt):
        request = GetAIMediaAuditJobRequest.GetAIMediaAuditJobRequest()
        request.set_JobId('<JobId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = get_ai_media_audit_job(clt)
        print(res['MediaAuditJob'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the summary of automated review results {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------

You can call the GetMediaAuditResult operation to query the summary of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResult](). Example: {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetMediaAuditResultRequest
    def get_media_audit_result(clt):
        request = GetMediaAuditResultRequest.GetMediaAuditResultRequest()
        request.set_MediaId('<VideoId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = get_media_audit_result(clt)
        print(res['MediaAuditResult'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query details about automated review results {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultDetail operation to query details about automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultDetail](). Example: {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetMediaAuditResultDetailRequest
    def get_media_audit_result_detail(clt):
        request = GetMediaAuditResultDetailRequest.GetMediaAuditResultDetailRequest()
        request.set_MediaId('<VideoId>')
        request.set_PageNo(1)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = get_media_audit_result_detail(clt)
        print(res['MediaAuditResultDetail']['Total'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the timeline of automated review results {#h2--div-id-getmediaauditresulttimeline-div-6}
----------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultTimeline operation to query the timeline of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultTimeline](). Example: {#h2--div-id-getmediaauditresulttimeline-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetMediaAuditResultTimelineRequest
    def get_media_audit_result_timeline(clt):
        request = GetMediaAuditResultTimelineRequest.GetMediaAuditResultTimelineRequest()
        request.set_MediaId('<VideoId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = get_media_audit_result_timeline(clt)
        print(res['MediaAuditResultTimeline']['Porn'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Create a manual review {#h2--div-id-createaudit-div-7}
------------------------------------------------------

You can call the CreateAudit operation to create a manual review.
For more information about the request and response parameters of this operation, see [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md). Example: {#h2--div-id-createaudit-div-7}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import CreateAuditRequest
    def create_audit(clt):
        request = CreateAuditRequest.CreateAuditRequest()
    
        auditContent = []
        # Specify the video ID and review status. Specify the reason for blocking the video if the Status parameter is set to Blocked.
        auditItem = {'VideoId': '<videoId>', 'Status': 'Blocked', 'Reason': 'porn video'}
        auditContent.append(auditItem)
        request.set_AuditContent(json.dumps(auditContent))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = create_audit(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the historical records of manual reviews {#h2--div-id-getaudithistory-div-8}
----------------------------------------------------------------------------------

You can call the GetAuditHistory operation to query the historical records of manual reviews.
For more information about the request and response parameters of this operation, see [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md). Example: {#h2--div-id-getaudithistory-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetAuditHistoryRequest
    def get_audit_history(clt):
        request = GetAuditHistoryRequest.GetAuditHistoryRequest()
    
        request.set_VideoId('<videoId>')
        request.set_PageNo(1)
        request.set_PageSize(10)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        history = get_audit_history(clt)
        print(history['Histories'])
        print(json.dumps(history, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Set an IP address whitelist for reviews {#h2--ip-div-id-setauditsecurityip-div-9}
---------------------------------------------------------------------------------

You can call the SetAuditSecurityIp operation to set an IP address whitelist for reviews.
For more information about the request and response parameters of this operation, see [SetAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/SetAuditSecurityIp.md). Example: {#h2--ip-div-id-setauditsecurityip-div-9}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import SetAuditSecurityIpRequest
    def set_audit_security_ip(clt):
        request = SetAuditSecurityIpRequest.SetAuditSecurityIpRequest()
    
        # The name of the IP address whitelist for reviews. The default value is Default.
        request.set_SecurityGroupName('MyGroupName')
        # The operation type. The default value is Append, which indicates that IP addresses are added to the whitelist.
        request.set_OperateMode('Cover')
        # The IP addresses that are added to the whitelist. You can add a maximum of 100 IP addresses to a whitelist. Separate multiple IP addresses with commas (,).
        request.set_Ips('10.23.12.20,10.23.12.21,10.23.12.22')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = set_audit_security_ip(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the IP addresses in a whitelist {#h2--ip-div-id-listauditsecurityip-div-10}
---------------------------------------------------------------------------------

You can call the ListAuditSecurityIp operation to query the IP addresses in a whitelist.
For more information about the request and response parameters of this operation, see [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md). Example: {#h2--ip-div-id-listauditsecurityip-div-10}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import ListAuditSecurityIpRequest
    def list_audit_security_ip(clt):
        request = ListAuditSecurityIpRequest.ListAuditSecurityIpRequest()
    
        # The name of the whitelist.
        request.set_SecurityGroupName('MyGroupName')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        ips = list_audit_security_ip(clt)
        print(ips['SecurityIpList'])
        print(json.dumps(ips, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


