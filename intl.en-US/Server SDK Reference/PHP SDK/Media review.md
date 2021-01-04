Media review 
=================================

This topic provides examples on how to use the API operations of the media review module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to submit and query automated review jobs. You can also query automated review results, create manual reviews, and set an IP address whitelist for reviews.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Submit an automated review job {#h2--div-id-submitaimediaauditjob-div-2}
------------------------------------------------------------------------

You can call the SubmitAIMediaAuditJob operation to submit an automated review job.

For more information about the request and response parameters of this operation, see [SubmitAIMediaAuditJob](). Example:

    /**
     * Submit an automated review job.
     */
    function submitAIMediaAuditJob($client) {
        $request = new vod\SubmitAIMediaAuditJobRequest();
        // The video ID.
        $request->setMediaId("dc063078c1d845139e2a5bd8f52****");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = submitAIMediaAuditJob($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query an automated review job {#h2--div-id-getaimediaauditjob-div-3}
--------------------------------------------------------------------

You can call the GetAIMediaAuditJob operation to query details about an automated review job.
For more information about the request and response parameters of this operation, see [GetAIMediaAuditJob](). Example: {#h2--div-id-getaimediaauditjob-div-3}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query an automated review job.
     */
    function getAIMediaAuditJob($client) {
        $request = new vod\GetAIMediaAuditJobRequest();
        // The job ID.
        $request->setJobId("f980db7d82e644478206a4a52152****");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = getAIMediaAuditJob($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query the summary of automated review results {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------

You can call the GetMediaAuditResult operation to query the summary of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResult](). Example: {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query the summary of automated review results.
     */
    function getMediaAuditResult($client) {
        $request = new vod\GetMediaAuditResultRequest();
        // The video ID.
        $request->setMediaId("dc063078c1d845139e2a5bd8ff52****");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = getMediaAuditResult($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query details about automated review results {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultDetail operation to query details about automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultDetail](). Example: {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query details about automated review results
     */
    function getMediaAuditResultDetail($client) {
        $request = new vod\GetMediaAuditResultDetailRequest();
        // The video ID.
        $request->setMediaId("dc063078c1d845139e2a5bd8ff52****");
        // The page number.
        $request->setPageNo(1);
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = getMediaAuditResultDetail($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query the timeline of automated review results {#h2--div-id-getmediaauditresulttimeline-div-6}
----------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultTimeline operation to query the timeline of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultTimeline](). Example: {#h2--div-id-getmediaauditresulttimeline-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query the timeline of automated review results.
     */
    function getMediaAuditResultTimeline($client) {
        $request = new vod\GetMediaAuditResultTimelineRequest();
        // The video ID.
        $request->setMediaId("dc063078c1d845139e2a5bd8ff52****");
    
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = getMediaAuditResultTimeline($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Create a manual review {#h2--div-id-createaudit-div-7}
------------------------------------------------------

You can call the CreateAudit operation to create a manual review.
For more information about the request and response parameters of this operation, see [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md). Example: {#h2--div-id-createaudit-div-7}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Create a manual review.
     */
    function buildAuditContent() {
        $auditContent = array();
    
        $auditContent1 = array();
        $auditContent1["VideoId"] = "070bbc13d8294e35b36c3e7ab452****"; // The video ID.
        $auditContent1["Status"] = "Blocked"; // The review status.
        $auditContent1["Reason"] = "Reason"; // If the review status is Blocked, a reason must be provided. The reason can contain a maximum of 128 bytes.
        $auditContent[] = $auditContent1;
    
        return json_encode($auditContent);
    }
    
    /**
     * Manual review
     */
    function createAudit($client) {
        $request = new vod\CreateAuditRequest();
        // The content to review.
        $request->setAuditContent(buildAuditContent());
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = createAudit($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query the historical records of manual reviews {#h2--div-id-getaudithistory-div-8}
----------------------------------------------------------------------------------

You can call the GetAuditHistory operation to query the historical records of manual reviews.
For more information about the request and response parameters of this operation, see [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md). Example: {#h2--div-id-getaudithistory-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query the historical records of manual reviews.
     */
    function getAuditHistory($client) {
        $request = new vod\GetAuditHistoryRequest();
        // The video ID.
        $request->setVideoId("070bbc13d8294e35b36c3e7ab452****");
        // The page number.
        $request->setPageNo("1");
        // The page size.
        $request->setPageSize("10");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = getAuditHistory($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Set an IP address whitelist for reviews {#h2--ip-div-id-setauditsecurityip-div-9}
---------------------------------------------------------------------------------

You can call the SetAuditSecurityIp operation to set an IP address whitelist for reviews.
For more information about the request and response parameters of this operation, see [SetAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/SetAuditSecurityIp.md). Example: {#h2--ip-div-id-setauditsecurityip-div-9}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Set an IP address whitelist for reviews.
     */
    function setAuditSecurityIp($client) {
        $request = new vod\SetAuditSecurityIpRequest();
        /// The name of the IP address whitelist for reviews. The default value is Default.
        $request->setSecurityGroupName("MyGroupName");
        // The operation type. The default value is Append, which indicates that IP addresses are added to the whitelist.
        $request->setOperateMode("Cover");
        // The IP addresses that are added to the whitelist. You can add multiple IP addresses to a whitelist. Separate multiple IP addresses with commas (,).
        $request->setIps("10.23.12.20,10.23.12.21,10.23.12.22");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = setAuditSecurityIp($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query the IP addresses in a whitelist {#h2--ip-div-id-listauditsecurityip-div-10}
---------------------------------------------------------------------------------

You can call the ListAuditSecurityIp operation to query the IP addresses in a whitelist.
For more information about the request and response parameters of this operation, see [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md). Example: {#h2--ip-div-id-listauditsecurityip-div-10}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query the IP addresses in a whitelist.
     */
    function listAuditSecurityIp($client) {
        $request = new vod\ListAuditSecurityIpRequest();
        /// The name of the IP address whitelist for reviews. The default value is Default.
        $request->setSecurityGroupName("MyGroupName");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = listAuditSecurityIp($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


