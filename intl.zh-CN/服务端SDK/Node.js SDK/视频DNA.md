视频DNA 
==========================

本篇文档提供了Node.js SDK视频DNA模块相关功能的API调用示例。包含提交视频DNA作业、查询视频DNA作业、获取视频DNA结果。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/Node.js SDK/初始化.md)。

提交视频DNA作业 {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------

调用SubmitAIJob接口，完成提交视频DNA作业功能。

接口参数和返回字段请参见[SubmitAIJob]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SubmitAIJob", {
        MediaId: '584625a507a44d0eaa7424afd56****',
        Types: 'AIMediaDNA'
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



查询视频DNA作业 {#h2--dna-div-id-listaijob-div-3}
-------------------------------------------

调用ListAIJob接口，完成查询视频DNA作业功能。

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
                // AI类型，注意校验类型是否为AIMediaDNA
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



获取视频DNA结果 {#h2--dna-div-id-getmediadnaresult-div-4}
---------------------------------------------------

调用GetMediaDNAResult接口，完成获取视频DNA结果功能。

接口参数和返回字段请参见[GetMediaDNAResult]()。调用示例如下：

    // 调用样例
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetMediaDNAResult", {
        MediaId: '584625a507a44d0eaa7424afd56****'
    }, {}).then(function (response) {
        // 打印DNA结果
        console.log("DNAResult = ");
        console.log(response.DNAResult);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


