视频DNA 
==========================

本篇文档提供了PHP SDK视频DNA模块相关功能的API调用示例。包含提交视频DNA作业、查询视频DNA作业、获取视频DNA结果。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/PHP SDK/安装SDK/初始化.md)。

提交视频DNA作业 {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------

调用SubmitAIJob接口，完成提交视频DNA作业功能。

接口参数和返回字段请参见[SubmitAIJob]()。调用示例如下：

    function submitAIJob($client) {
        $request = new vod\SubmitAIJobRequest();
        // 设置视频ID
        $request->setMediaId('3eb19a4585bc475e995bdd52****');
        // 设置AI类型，类型为AIMediaDNA
        $request->setTypes('AIMediaDNA');
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = submitAIJob($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询视频DNA作业 {#h2--dna-div-id-listaijob-div-3}
-------------------------------------------

调用ListAIJob接口，完成查询视频DNA作业功能。

接口参数和返回字段请参见[ListAIJob]()。调用示例如下：

    function listAIJob($client) {
        $request = new vod\ListAIJobRequest();
        // 设置作业ID
        $request->setJobIds("979d4d7a36ae41b1a945a252****,3eb19a4585bc475e995bddea52****");
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = listAIJob($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



获取视频DNA结果 {#h2--dna-div-id-getmediadnaresult-div-4}
---------------------------------------------------

调用GetMediaDNAResult接口，完成获取视频DNA结果功能。

接口参数和返回字段请参见[GetMediaDNAResult]()。调用示例如下：

    function getMediaDNAResult($client) {
        $request = new vod\GetMediaDNAResultRequest();
        // 设置视频ID
        $request->setMediaId("3eb19a4585bc475e995bdd52****");
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = getMediaDNAResult($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


