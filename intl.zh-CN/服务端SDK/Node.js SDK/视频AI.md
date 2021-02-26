视频AI 
=========================

本篇文档提供了Node.js SDK视频AI模块相关功能的API调用示例。包含提交AI作业、查询AI作业、添加AI模板、修改AI模板、删除AI模板、查询AI模板、查询设置默认AI模板等。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/Node.js SDK/初始化.md)接口。

提交AI作业 {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交AI作业功能。

接口参数和返回字段请参见[SubmitAIJob]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SubmitAIJob", {
        MediaId: '584625a507a44d0eaa7424afd56****',
        Types: 'AIVideoCover'
    }, {}).then(function (response) {
        if (response.AIJobList && response.AIJobList.AIJob && response.AIJobList.AIJob.length > 0){
            for(var i=0; i<response.AIJobList.AIJob.length; i++){
                var job = response.AIJobList.AIJob[i];
                // 视频ID
                console.log('MediaId = ' + job.MediaId);
                // 作业ID
                console.log('JobId = ' + job.JobId);
                // AI类型
                console.log('Type = ' + job.Type);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



查询AI作业 {#h2--ai-div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询AI作业功能。

接口参数和返回字段请参见[ListAIJob]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListAIJob", {
        JobIds: 'JobId1,JobId2'
    }, {}).then(function (response) {
        // 打印作业列表
        console.log("============ AIJobList ============");
        if (response.AIJobList && response.AIJobList.AIJob && response.AIJobList.AIJob.length > 0){
            for(var i=0; i<response.AIJobList.AIJob.length; i++){
                var job = response.AIJobList.AIJob[i];
                // 视频ID
                console.log('MediaId = ' + job.MediaId);
                // 作业ID
                console.log('JobId = ' + job.JobId);
                // AI类型
                console.log('Type = ' + job.Type);
                // 作业状态
                console.log('Status = ' + job.Status);
                // 作业结果
                console.log('Data = ' + job.Data);
            }
        }
        // 打印不存在的作业ID
        console.log("============ NonExistAIJobIds ============");
        if (response.NonExistAIJobIds && response.NonExistAIJobIds.String && response.NonExistAIJobIds.String.length > 0) {
            for (var i=0; i<response.NonExistAIJobIds.String.length; i++) {
                // 作业ID
                console.log('NonExistAIJobId = ' + response.NonExistAIJobIds.String[i]);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



添加AI模板 {#h2--ai-div-id-addaitemplate-div-4}
-------------------------------------------

调用AddAITemplate接口，完成添加AI模板功能。

接口参数和返回字段请参见[AddAITemplate]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // 模板详细配置, 以审核模版为例
    var templateConfig = {
        AuditAutoBlock: "no",
        AuditContent: ["screen"],
        AuditRange:["video", "image-cover", "text-title"],
        AuditItem: ["terrorism", "porn"]
    };
    client.request("AddAITemplate", {
        TemplateType: 'AIMediaAudit',   // 设置模板类型，以智能审核模板为例
        TemplateName: 'myaitemplate',   // 设置模板名称
        TemplateConfig: JSON.stringify(templateConfig)   // 设置模板详细配置
    }, {}).then(function (response) {
        console.log(response);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



删除AI模板 {#h2--ai-div-id-deleteaitemplate-div-5}
----------------------------------------------

调用DeleteAITemplate接口，完成删除AI模板功能。

接口参数和返回字段请参见[DeleteAITemplate]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DeleteAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****' // 设置模板ID
    }, {}).then(function (response) {
        console.log('TemplateId = ' + response.TemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



修改AI模板 {#h2--ai-div-id-updateaitemplate-div-6}
----------------------------------------------

调用UpdateAITemplate接口，完成修改AI模板功能。

接口参数和返回字段请参见[UpdateAITemplate]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // 模板详细配置, 以审核模版为例
    var templateConfig = {
        AuditAutoBlock: "no",
        AuditContent: ["screen"],
        AuditRange:["video", "image-cover"],
        AuditItem: ["terrorism", "porn"]
    };
    client.request("UpdateAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****',  // 模板ID
        TemplateName: 'myaitemplatemodify',              // 模板名称
        TemplateConfig: JSON.stringify(templateConfig)   // 模板详细配置
    }, {}).then(function (response) {
        console.log('TemplateId = ' + response.TemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



查询AI模板 {#h2--ai-div-id-getaitemplate-div-7}
-------------------------------------------

调用GetAITemplate接口，完成查询AI模板功能。

接口参数和返回字段请参见[GetAITemplate]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****'  // 模板ID
    }, {}).then(function (response) {
        console.log(response);
        // 模板信息
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



查询AI模板列表 {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------

调用ListAITemplate接口，完成查询AI模板列表功能。

接口参数和返回字段请参见[ListAITemplate]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListAITemplate", {
        TemplateType: 'AIMediaAudit'  // 模板类型
    }, {}).then(function (response) {
        console.log(response);
        // 模板信息列表
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



设置默认AI模板 {#h2--ai-div-id-setdefaultaitemplate-div-9}
----------------------------------------------------

调用SetDefaultAITemplate接口，完成设置默认AI模板功能。

接口参数和返回字段请参见[SetDefaultAITemplate]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SetDefaultAITemplate", {
        TemplateId: '584625a507a44d0eaa7424afd56****' // 模板ID
    }, {}).then(function (response) {
        console.log('TemplateId = ' + response.TemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



查询默认AI模板 {#h2--ai-div-id-getdefaultaitemplate-div-10}
-----------------------------------------------------

调用GetDefaultAITemplate接口，完成查询默认AI模板功能。

接口参数和返回字段请参见[GetDefaultAITemplate]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetDefaultAITemplate", {
        TemplateType: 'AIMediaAudit'   // 模板类型
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


