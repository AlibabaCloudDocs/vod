Media review 
=================================

This topic provides examples on how to use the API operations of the media review module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to submit and query automated review jobs. You can also query automated review results, create manual reviews, and set an IP address whitelist for reviews.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Submit an automated review job {#h2--div-id-submitaimediaauditjob-div-2}
------------------------------------------------------------------------

You can call the SubmitAIMediaAuditJob operation to submit an automated review job.
For more information about the request and response parameters of this operation, see [SubmitAIMediaAuditJob](). Example: {#h2--div-id-submitaimediaauditjob-div-2}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SubmitAIMediaAuditJob", {
        MediaId: '584625a507a44d0eaa7424afd56****'  // The media resource ID.
    }, {}).then(function (response) {
        console.log('JobId = ' + response.JobId);       // The job ID.
        console.log('MediaId = ' + response.MediaId);   // The video ID.
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query an automated review job {#h2--div-id-getaimediaauditjob-div-3}
--------------------------------------------------------------------

You can call GetAIMediaAuditJob operation to query details about an automated review job.
For more information about the request and response parameters of this operation, see [GetAIMediaAuditJob](). Example: {#h2--div-id-getaimediaauditjob-div-3}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetAIMediaAuditJob", {
        JobId: '584625a507a44d0eaa7424afd56****'  // The job ID.
    }, {}).then(function (response) {
        if (response.MediaAuditJob){
            // The job results.
            console.log('MediaId = ' + response.MediaAuditJob.MediaId);
            console.log('JobId = ' + response.MediaAuditJob.JobId);
            console.log('Type = ' + response.MediaAuditJob.Type);
            console.log('Status = ' + response.MediaAuditJob.Status);
            if (response.MediaAuditJob.Code){
                console.log('Code = ' + response.MediaAuditJob.Code);
            }
            if (response.MediaAuditJob.Message){
                console.log('Message = ' + response.MediaAuditJob.Message);
            }
            if (response.MediaAuditJob.Data){
                console.log('Data Label = ' + response.MediaAuditJob.Data.Label);
                console.log('Data Suggestion = ' + response.MediaAuditJob.Data.Suggestion);
                console.log('Data AbnormalModules = ' + response.MediaAuditJob.Data.AbnormalModules);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the summary of automated review results {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------

You can call the GetMediaAuditResult operation to query the summary of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResult](). Example: {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetMediaAuditResult", {
        MediaId: '584625a507a44d0eaa7424afd56****'  // The media resource ID.
    }, {}).then(function (response) {
        console.log(response);
        if (response.MediaAuditResult){
            // The automated review results.
            console.log('Data Label = ' + response.MediaAuditResult.Label);
            console.log('Data Suggestion = ' + response.MediaAuditResult.Suggestion);
            console.log('Data AbnormalModules = ' + response.MediaAuditResult.AbnormalModules);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query details about automated review results {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultDetail operation to query details about automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultDetail](). Example: {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetMediaAuditResultDetail", {
        MediaId: '584625a507a44d0eaa7424afd56****',  // The media resource ID.
        PageNo: 1
    }, {}).then(function (response) {
        if (response.MediaAuditResultDetail){
            // The automated review results.
            console.log('Data Total = ' + response.MediaAuditResultDetail.Total);
            console.log('Data List Size = ' + response.MediaAuditResultDetail.List.length);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the timeline of automated review results {#h2--div-id-getmediaauditresulttimeline-div-6}
----------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultTimeline operation to query the timeline of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultTimeline](). Example: {#h2--div-id-getmediaauditresulttimeline-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetMediaAuditResultTimeline", {
        MediaId: '584625a507a44d0eaa7424afd56****'  // The media resource ID.
    }, {}).then(function (response) {
        if (response.MediaAuditResultTimeline){
            // The timeline of automated review results.
            if (response.MediaAuditResultTimeline.Terrorism){
                console.log('Terrorism = ' + response.MediaAuditResultTimeline.Terrorism);
            }
            if (response.MediaAuditResultTimeline.Porn){
                console.log('Porn = ' + response.MediaAuditResultTimeline.Porn);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Create a manual review {#h2--div-id-createaudit-div-7}
------------------------------------------------------

You can call the CreateAudit operation to create a manual review.
For more information about the request and response parameters of this operation, see [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md). Example: {#h2--div-id-createaudit-div-7}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var auditContent = [{
        VideoId: 'VideoId',  // The video ID.
        Status: 'Blocked',   // The review status.
        Reason: 'Including porn'  // If the review status is Blocked, a reason must be provided. The reason can contain a maximum of 128 bytes.
    }];
    client.request("CreateAudit", {
        AuditContent: JSON.stringify(auditContent)
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the historical records of manual reviews {#h2--div-id-getaudithistory-div-8}
----------------------------------------------------------------------------------

You can call the GetAuditHistory operation to query the historical records of manual reviews.
For more information about the request and response parameters of this operation, see [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md). Example: {#h2--div-id-getaudithistory-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetAuditHistory", {
        VideoId: 'VideoId',
        PageNo: 1,
        PageSize: 10
    }, {}).then(function (response) {
        // List the total number of historical records.
        console.log('Total = ' + response.Total);
        // List the result of the current review.
        console.log('Status = ' + response.Status);
        // List historical records.
        console.log('Histories = ');
        console.log(response.Histories);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Set an IP address whitelist for reviews {#h2--ip-div-id-setauditsecurityip-div-9}
---------------------------------------------------------------------------------

You can call the SetAuditSecurityIp operation to set an IP address whitelist for reviews.
For more information about the request and response parameters of this operation, see [SetAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/SetAuditSecurityIp.md). Example: {#h2--ip-div-id-setauditsecurityip-div-9}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SetAuditSecurityIp", {
        SecurityGroupName: 'MyGroupName',  // The name of the IP address whitelist for reviews. The default value is Default.
        OperateMode: 'Cover',   // The operation type. The default value is Append, which indicates that IP addresses are added to the whitelist.
        Ips: '10.23.12.20,10.23.12.21,10.23.12.22'    // The IP addresses that are added to the whitelist. You can add a maximum of 100 IP addresses to a whitelist. Separate multiple IP addresses with commas (,).
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the IP addresses in a whitelist {#h2--ip-div-id-listauditsecurityip-div-10}
---------------------------------------------------------------------------------

You can call the ListAuditSecurityIp operation to query the IP addresses in a whitelist.
For more information about the request and response parameters of this operation, see [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md). Example: {#h2--ip-div-id-listauditsecurityip-div-10}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListAuditSecurityIp", {
        SecurityGroupName: 'MyGroupName'  // The name of the whitelist.
    }, {}).then(function (response) {
        // List the IP addresses in the whitelist.
        console.log('SecurityIpList = ');
        console.log(response.SecurityIpList);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


