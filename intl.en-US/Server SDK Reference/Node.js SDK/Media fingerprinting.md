Media fingerprinting 
=========================================

This topic provides examples on how to use the API operations of the media fingerprinting module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to submit media fingerprinting jobs, query media fingerprinting jobs, and query media fingerprinting results.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Submit a media fingerprinting job {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------------------------------

You can call the SubmitAIJob operation to submit a media fingerprinting job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--dna-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SubmitAIJob", {
        MediaId: '584625a507a44d0eaa7424afd56****',
        Types: 'AIMediaDNA'
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



Query media fingerprinting jobs {#h2--dna-div-id-listaijob-div-3}
-----------------------------------------------------------------

You can call the ListAIJob operation to query media fingerprinting jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--dna-div-id-listaijob-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
                // The AI type. Set the value to AIMediaDNA.
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



Query media fingerprinting results {#h2--dna-div-id-getmediadnaresult-div-4}
----------------------------------------------------------------------------

You can call the GetMediaDNAResult operation to query media fingerprinting results.
For more information about the request and response parameters of this operation, see [GetMediaDNAResult](). Example: {#h2--dna-div-id-getmediadnaresult-div-4}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetMediaDNAResult", {
        MediaId: '584625a507a44d0eaa7424afd56****'
    }, {}).then(function (response) {
        // List media fingerprinting results.
        console.log("DNAResult = ");
        console.log(response.DNAResult);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


