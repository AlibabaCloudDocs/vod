Media fingerprinting 
=========================================

This topic provides examples on how to use the API operations of the media fingerprinting module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to submit media fingerprinting jobs, query media fingerprinting jobs, and query media fingerprinting results.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Submit a media fingerprinting job {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------------------------------

You can call the SubmitAIJob operation to submit a media fingerprinting job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--dna-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function submitAIJob($client) {
        $request = new vod\SubmitAIJobRequest();
        // The video ID.
        $request->setMediaId('3eb19a4585bc475e995bdd52****');
        // The AI type. The value is set to AIMediaDNA.
        $request->setTypes('AIMediaDNA');
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



Query media fingerprinting jobs {#h2--dna-div-id-listaijob-div-3}
-----------------------------------------------------------------

You can call the ListAIJob operation to query media fingerprinting jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--dna-div-id-listaijob-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function listAIJob($client) {
        $request = new vod\ListAIJobRequest();
        // The job ID.
        $request->setJobIds("979d4d7a36ae41b1a945a252****,3eb19a4585bc475e995bddea52****");
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



Query media fingerprinting results {#h2--dna-div-id-getmediadnaresult-div-4}
----------------------------------------------------------------------------

You can call the GetMediaDNAResult operation to query media fingerprinting results.
For more information about the request and response parameters of this operation, see [GetMediaDNAResult](). Example: {#h2--dna-div-id-getmediadnaresult-div-4}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function getMediaDNAResult($client) {
        $request = new vod\GetMediaDNAResultRequest();
        // The video ID.
        $request->setMediaId("3eb19a4585bc475e995bdd52****");
        // Returned results.
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = getMediaDNAResult($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


