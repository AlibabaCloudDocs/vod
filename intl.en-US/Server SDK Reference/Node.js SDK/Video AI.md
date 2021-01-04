Video AI 
=============================

This topic provides examples on how to use the API operations of the video AI module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to submit or query AI jobs, specify an AI template as the default one, and query the default AI template. You can also create, delete, modify, and query AI templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Submit an AI job {#h2--ai-div-id-submitaijob-div-2}
---------------------------------------------------

You can call the SubmitAIJob operation to submit an AI job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SubmitAIJob", {
        MediaId: '584625a507a44d0eaa7424afd56****',
        Types: 'AIVideoCover'
    }, {}).then(function (response) {
        if (response.AIJobList && response.AIJobList.AIJob && response.AIJobList.AIJob.length > 0){
            for(var i=0; i<response.AIJobList.AIJob.length; i++){
                var job = response.AIJobList.AIJob[i];
                // The video ID.
                console.log('MediaId = ' + job.MediaId);
                // The job ID.
                console.log('JobId = ' + job.JobId);
                // The AI type.
                console.log('Type = ' + job.Type);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query AI jobs {#h2--ai-div-id-listaijob-div-3}
----------------------------------------------

You can call the ListAIJob operation to query AI jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--ai-div-id-listaijob-div-3}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListAIJob", {
        JobIds: 'JobId1,JobId2'
    }, {}).then(function (response) {
        // List details about jobs.
        console.log("============ AIJobList ============");
        if (response.AIJobList && response.AIJobList.AIJob && response.AIJobList.AIJob.length > 0){
            for(var i=0; i<response.AIJobList.AIJob.length; i++){
                var job = response.AIJobList.AIJob[i];
                // The video ID.
                console.log('MediaId = ' + job.MediaId);
                // The job ID.
                console.log('JobId = ' + job.JobId);
                // The AI type.
                console.log('Type = ' + job.Type);
                // The job status.
                console.log('Status = ' + job.Status);
                // The job result.
                console.log('Data = ' + job.Data);
            }
        }
        // List the IDs of jobs that do not exist.
        console.log("============ NonExistAIJobIds ============");
        if (response.NonExistAIJobIds && response.NonExistAIJobIds.String && response.NonExistAIJobIds.String.length > 0) {
            for (var i=0; i<response.NonExistAIJobIds.String.length; i++) {
                // The job ID.
                console.log('NonExistAIJobId = ' + response.NonExistAIJobIds.String[i]);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Create an AI template {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------

You can call the AddAITemplate operation to create an AI template.
For more information about the request and response parameters of this operation, see [AddAITemplate](). Example: {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // The detailed configurations of the template. For this example, use a review template.
    var templateConfig = {
        AuditAutoBlock: "no",
        AuditContent: ["screen"],
        AuditRange:["video", "image-cover", "text-title"],
        AuditItem: ["terrorism", "porn"]
    };
    client.request("AddAITemplate", {
        TemplateType: 'AIMediaAudit',   // The template type. For this example, specify an automated review template.
        TemplateName: 'myaitemplate',   // The template name.
        TemplateConfig: JSON.stringify(templateConfig)   // The detailed configurations of the template.
    }, {}).then(function (response) {
        console.log(response);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete an AI template {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------

You can call the DeleteAITemplate operation to delete an AI template.
For more information about the request and response parameters of this operation, see [DeleteAITemplate](). Example: {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DeleteAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****' // The template ID.
    }, {}).then(function (response) {
        console.log('TemplateId = ' + response.TemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify an AI template {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------

You can call the UpdateAITemplate operation to modify an AI template.
For more information about the request and response parameters of this operation, see [UpdateAITemplate](). Example: {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // The detailed configurations of the template. For this example, use a review template.
    var templateConfig = {
        AuditAutoBlock: "no",
        AuditContent: ["screen"],
        AuditRange:["video", "image-cover"],
        AuditItem: ["terrorism", "porn"]
    };
    client.request("UpdateAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****',  // The template ID.
        TemplateName: 'myaitemplatemodify',              // The template name.
        TemplateConfig: JSON.stringify(templateConfig)   // The detailed configurations of the template.
    }, {}).then(function (response) {
        console.log('TemplateId = ' + response.TemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query an AI template {#h2--ai-div-id-getaitemplate-div-7}
---------------------------------------------------------

You can call the GetAITemplate operation to query details about an AI template.
For more information about the request and response parameters of this operation, see [GetAITemplate](). Example: {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****'  // The template ID.
    }, {}).then(function (response) {
        console.log(response);
        // The template information.
        if (response.TemplateInfo){
            console.log('TemplateId = ' + response.TemplateInfo.TemplateId);
            console.log('TemplateType = ' + response.TemplateInfo.TemplateType);
            console.log('TemplateName = ' + response.TemplateInfo.TemplateName);
            console.log('TemplateConfig = ' + response.TemplateInfo.TemplateConfig);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query AI templates {#h2--ai-div-id-listaitemplate-div-8}
--------------------------------------------------------

You can call the ListAITemplate operation to query AI templates.
For more information about the request and response parameters of this operation, see [ListAITemplate](). Example: {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListAITemplate", {
        TemplateType: 'AIMediaAudit'  // The template type.
    }, {}).then(function (response) {
        console.log(response);
        // The template information.
        if (response.TemplateInfoList && response.TemplateInfoList.length > 0){
            for (var i=0; i<response.TemplateInfoList.length; i++){
                console.log("The " + i + " Template.");
                console.log('TemplateId = ' + response.TemplateInfoList[i].TemplateId);
                console.log('TemplateType = ' + response.TemplateInfoList[i].TemplateType);
                console.log('TemplateName = ' + response.TemplateInfoList[i].TemplateName);
                console.log('TemplateConfig = ' + response.TemplateInfoList[i].TemplateConfig);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Specify an AI template as the default one {#h2--ai-div-id-setdefaultaitemplate-div-9}
-------------------------------------------------------------------------------------

You can call the SetDefaultAITemplate operation to specify an AI template as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultAITemplate](). Example: {#h2--ai-div-id-setdefaultaitemplate-div-9}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SetDefaultAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****' // The template ID.
    }, {}).then(function (response) {
        console.log('TemplateId = ' + response.TemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the default AI template {#h2--ai-div-id-getdefaultaitemplate-div-10}
--------------------------------------------------------------------------

You can call the GetDefaultAITemplate operation to query details about the default AI template.
For more information about the request and response parameters of this operation, see [GetDefaultAITemplate](). Example: {#h2--ai-div-id-getdefaultaitemplate-div-10}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetDefaultAITemplate", {
        TemplateType: 'AIMediaAudit'   // The template type.
    }, {}).then(function (response) {
        if (response.TemplateInfo){
            console.log('TemplateId = ' + response.TemplateInfo.TemplateId);
            console.log('TemplateType = ' + response.TemplateInfo.TemplateType);
            console.log('TemplateName = ' + response.TemplateInfo.TemplateName);
            console.log('IsDefault = ' + response.TemplateInfo.IsDefault);
            console.log('TemplateConfig = ' + response.TemplateInfo.TemplateConfig);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


