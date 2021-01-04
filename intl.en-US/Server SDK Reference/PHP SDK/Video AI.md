Video AI 
=============================

This topic provides examples on how to use the API operations of the video AI module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to submit or query AI jobs, specify an AI template as the default one, and query the default AI template. You can also create, delete, modify, and query AI templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Submit an AI job {#h2--ai-div-id-submitaijob-div-2}
---------------------------------------------------

You can call the SubmitAIJob operation to submit an AI job.

For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example:

    function submitAIJob($client) {
        $request = new vod\SubmitAIJobRequest();
        // The video ID.
        $request->setMediaId('04df94402a5342928de6d6a2652****');
        // The AI type. Make sure that the AI type is enabled.
        $request->setTypes('AIVideoCover');
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = submitAIJob($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query AI jobs {#h2--ai-div-id-listaijob-div-3}
----------------------------------------------

You can call the ListAIJob operation to query AI jobs.

For more information about the request and response parameters of this operation, see [ListAIJob](). Example:

    function listAIJob($client) {
        $request = new vod\ListAIJobRequest();
        // The job ID.
        $request->setJobIds("7664bb4f06c44f0a84ccb49f452****,1234b4f06c44f0a84ccb49f452****");
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = listAIJob($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Create an AI template {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------

You can call the AddAITemplate operation to create an AI template.

For more information about the request and response parameters of this operation, see [AddAITemplate](). Example:

    function addAITemplate($client) {
        $request = new vod\AddAITemplateRequest();
        // The template type. For this example, specify an automated review template.
        $request->setTemplateType("AIMediaAudit");
        // The template name.
        $request->setTemplateName("myaitemplate");
        // The detailed configurations of the template.
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
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = addAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete an AI template {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------

You can call the DeleteAITemplate operation to delete an AI template.

For more information about the request and response parameters of this operation, see [DeleteAITemplate](). Example:

    function deleteAITemplate($client) {
        $request = new vod\DeleteAITemplateRequest();
        // The template ID.
        $request->setTemplateId("3e539dfefc651c6796fea2549a****");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = deleteAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify an AI template {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------

You can call the UpdateAITemplate operation to modify an AI template.

For more information about the request and response parameters of this operation, see [UpdateAITemplate](). Example:

    function updateAITemplate($client) {
        $request = new vod\UpdateAITemplateRequest();
        // The template ID.
        $request->setTemplateId("3e539dfefc651c6796fea2549a****");
        // The template name.
        $request->setTemplateName("myaitempalte1");
        // The detailed configurations of the template.
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
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = updateAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query an AI template {#h2--ai-div-id-getaitemplate-div-7}
---------------------------------------------------------

You can call the GetAITemplate operation to query details about an AI template.

For more information about the request and response parameters of this operation, see [GetAITemplate](). Example:

    function getAITemplate($client) {
        $request = new vod\GetAITemplateRequest();
        // The template ID.
        $request->setTemplateId("3e539dfefc651c6796fea25452****");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = getAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query AI templates {#h2--ai-div-id-listaitemplate-div-8}
--------------------------------------------------------

You can call the ListAITemplate operation to query AI templates.

For more information about the request and response parameters of this operation, see [ListAITemplate](). Example:

    function listAITemplate($client) {
        $request = new vod\ListAITemplateRequest();
        // The template type. For this example, specify an automated review template.
        $request->setTemplateType("AIMediaAudit");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = listAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Specify an AI template as the default one {#h2--ai-div-id-setdefaultaitemplate-div-9}
-------------------------------------------------------------------------------------

You can call the SetDefaultAITemplate operation to specify an AI template as the default one.

For more information about the request and response parameters of this operation, see [SetDefaultAITemplate](). Example:

    function setDefaultAITemplate($client) {
        $request = new vod\SetDefaultAITemplateRequest();
        // The template ID.
        $request->setTemplateId("3e539dfefc651c6796fea25492****");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = setDefaultAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query the default AI template {#h2--ai-div-id-getdefaultaitemplate-div-10}
--------------------------------------------------------------------------

You can call the GetDefaultAITemplate operation to query details about the default AI template.

For more information about the request and response parameters of this operation, see [GetDefaultAITemplate](). Example:

    function getDefaultAITemplate($client) {
        $request = new vod\GetDefaultAITemplateRequest();
        // The template type. For this example, specify an automated review template.
        $request->setTemplateType("AIMediaAudit");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = getDefaultAITemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


