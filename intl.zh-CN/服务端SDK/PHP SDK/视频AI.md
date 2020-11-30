视频AI 
=========================

本篇文档提供了PHP SDK视频AI模块相关功能的API调用示例。包含提交AI作业、查询AI作业、添加AI模板、修改AI模板、删除AI模板、查询AI模板、查询设置默认AI模板等。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/PHP SDK/安装SDK/初始化.md)。

提交AI作业 {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交AI作业功能。

接口参数和返回字段请参见[SubmitAIJob]()。调用示例如下：

    function submitAIJob($client) {
        $request = new vod\SubmitAIJobRequest();
        // 设置视频ID
        $request->setMediaId('04df94402a5342928de6d6a2652****');
        // 设置AI类型，请确保已开通该类型AI
        $request->setTypes('AIVideoCover');
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



查询AI作业 {#h2--ai-div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询AI作业功能。

接口参数和返回字段请参见[ListAIJob]()。调用示例如下：

    function listAIJob($client) {
        $request = new vod\ListAIJobRequest();
        // 设置作业ID
        $request->setJobIds("7664bb4f06c44f0a84ccb49f452****,1234b4f06c44f0a84ccb49f452****");
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



添加AI模板 {#h2--ai-div-id-addaitemplate-div-4}
-------------------------------------------

调用AddAITemplate接口，完成添加AI模板功能。

接口参数和返回字段请参见[AddAITemplate]()。调用示例如下：

    function addAITemplate($client) {
        $request = new vod\AddAITemplateRequest();
        // 设置模板类型，以智能审核模板为例
        $request->setTemplateType("AIMediaAudit");
        // 设置模板名称
        $request->setTemplateName("myaitemplate");
        // 设置模板详细配置
        $templateConfigrray = array();
        $auditItem = array();
        $auditItem[] = "terrorism";
        $auditItem[] = "porn";
        $templateConfig["AuditItem"] = $auditItem;
    
        $auditRange = array();
        $auditRange[] = "video";
        $auditRange[] = "image-cover";
        $auditRange[] = "text-title";
        $templateConfig["AuditRange"] = $auditRange;
    
        $auditContent = array();
        $auditContent[] = "screen";
        $templateConfig["AuditContent"] = $auditContent;
    
        $templateConfig["AuditAutoBlock"] = "no";
        $request->setTemplateConfig(json_encode($templateConfig));
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = addAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



删除AI模板 {#h2--ai-div-id-deleteaitemplate-div-5}
----------------------------------------------

调用DeleteAITemplate接口，完成删除AI模板功能。

接口参数和返回字段请参见[DeleteAITemplate]()。调用示例如下：

    function deleteAITemplate($client) {
        $request = new vod\DeleteAITemplateRequest();
        // 设置模板ID
        $request->setTemplateId("3e539dfefc651c6796fea2549a****");
    
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = deleteAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



修改AI模板 {#h2--ai-div-id-updateaitemplate-div-6}
----------------------------------------------

调用UpdateAITemplate接口，完成修改AI模板功能。

接口参数和返回字段请参见[UpdateAITemplate]()。调用示例如下：

    function updateAITemplate($client) {
        $request = new vod\UpdateAITemplateRequest();
        // 设置模板ID
        $request->setTemplateId("3e539dfefc651c6796fea2549a****");
        // 设置模板名称
        $request->setTemplateName("myaitempalte1");
        // 设置模板详细配置
        $templateConfigrray = array();
        $auditItem = array();
        $auditItem[] = "terrorism";
        //$auditItem[] = "porn";
        $templateConfig["AuditItem"] = $auditItem;
    
        $auditRange = array();
        $auditRange[] = "video";
        $auditRange[] = "image-cover";
        //$auditRange[] = "text-title";
        $templateConfig["AuditRange"] = $auditRange;
    
        $auditContent = array();
        $auditContent[] = "screen";
        $templateConfig["AuditContent"] = $auditContent;
    
        $templateConfig["AuditAutoBlock"] = "no";
        $request->setTemplateConfig(json_encode($templateConfig));
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = updateAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询AI模板 {#h2--ai-div-id-getaitemplate-div-7}
-------------------------------------------

调用GetAITemplate接口，完成查询AI模板功能。

接口参数和返回字段请参见[GetAITemplate]()。调用示例如下：

    function getAITemplate($client) {
        $request = new vod\GetAITemplateRequest();
        // 设置模板ID
        $request->setTemplateId("3e539dfefc651c6796fea25452****");
    
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = getAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询AI模板列表 {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------

调用ListAITemplate接口，完成查询AI模板列表功能。

接口参数和返回字段请参见[ListAITemplate]()。调用示例如下：

    function listAITemplate($client) {
        $request = new vod\ListAITemplateRequest();
        // 设置模板类型，以智能审核模板为例
        $request->setTemplateType("AIMediaAudit");
    
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = listAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



设置默认AI模板 {#h2--ai-div-id-setdefaultaitemplate-div-9}
----------------------------------------------------

调用SetDefaultAITemplate接口，完成设置默认AI模板功能。

接口参数和返回字段请参见[SetDefaultAITemplate]()。调用示例如下：

    function setDefaultAITemplate($client) {
        $request = new vod\SetDefaultAITemplateRequest();
        // 设置模板ID
        $request->setTemplateId("3e539dfefc651c6796fea25492****");
    
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = setDefaultAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



查询默认AI模板 {#h2--ai-div-id-getdefaultaitemplate-div-10}
-----------------------------------------------------

调用GetDefaultAITemplate接口，完成查询默认AI模板功能。

接口参数和返回字段请参见[GetDefaultAITemplate]()。调用示例如下：

    function getDefaultAITemplate($client) {
        $request = new vod\GetDefaultAITemplateRequest();
        // 设置模板类型，以智能审核模板为例
        $request->setTemplateType("AIMediaAudit");
    
        // 返回结果
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = getDefaultAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


