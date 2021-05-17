Video editing 
==================================

This topic provides examples on how to use the API operations of the video editing module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to create, modify, and delete online editing projects. You can also query details about an online editing project, configure materials for an online project, and create a video assembly task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Create a video assembly task based on a timeline {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on a timeline.

The timeline method is most commonly used to assemble videos. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:
**Note**

For more examples on how to assemble videos based on timelines, see [Video assembly](/intl.en-US/Developer Guide/Online editing/Overview.md).

    function buildMediaMetadata() {
        $mediaMetadata = array();
        // Produce Media Title
        $mediaMetadata['Title'] = 'Title';
        // Produce Media Description
        $mediaMetadata['Description'] = 'Description';
        // Produce Media UserDefined Cover URL
        $mediaMetadata['CoverURL'] = 'http://192.168.0.0/16/media/cover/mediaid.jpg';
        // Produce Media Category ID
        $mediaMetadata['CateId'] = null;
        // Produce Media Category Name
        $mediaMetadata['Tags'] = 'Tag1,Tag2,Test';
    
        return json_encode($mediaMetadata);
    }
    
    function buildProduceConfig() {
        $produceConfig = array();
        /*
         The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
         1. Not required
         2. Use default transcode template group id when empty
         */
        $produceConfig['TemplateGroupId'] = null;
        return json_encode($produceConfig);
    }
    
    function buildTimeline() {
        $timeline = array();
    
        // Video Track
        $videoTracks = array();
        $videoTrack = array();
    
        // Video Track Clicps
        $videoTrackClips = array();
        $videoTrackClip1 = array();
        $videoTrackClip1['MediaId'] = '6893fca9814640c8821efa52352****';
        $videoTrackClips[] = $videoTrackClip1;
    
        $videoTrackClip2 = array();
        $videoTrackClip2['MediaId'] = '070bbc13d8294e35b36c3e7ab52****';
        $videoTrackClips[] = $videoTrackClip2;
    
        $videoTrack['VideoTrackClips'] = $videoTrackClips;
        $videoTracks[] = $videoTrack;
        $timeline['VideoTracks'] = $videoTracks;
    
        return json_encode($timeline);
    }
    
    try {
         $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\ProduceEditingProjectVideoRequest();
        // Set Produce Media Metadata
        $request->setMediaMetadata(buildMediaMetadata());
        // Set Produce Configuration
        $request->setProduceConfig(buildProduceConfig());
        // Build Editing Project Timeline
        $request->setTimeline(buildTimeline());
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Create a video assembly task based on an online editing project {#h2--div-id-produceeditingprojectvideoprojectid-div-3}
-----------------------------------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on an online editing project.

If you have high requirements for online editing and management, we recommend that you use this method. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:

    function buildMediaMetadata() {
        $mediaMetadata = array();
        // Produce Media Title
        $mediaMetadata['Title'] = 'Title';
        // Produce Media Description
        $mediaMetadata['Description'] = 'Description';
        // Produce Media UserDefined Cover URL
        $mediaMetadata['CoverURL'] = 'http://192.168.0.0/16/media/cover/mediaid.jpg';
        // Produce Media Category ID
        $mediaMetadata['CateId'] = null;
        // Produce Media Category Name
        $mediaMetadata['Tags'] = 'Tag1,Tag2,Test';
    
        return json_encode($mediaMetadata);
    }
    
    function buildProduceConfig() {
        $produceConfig = array();
        /*
         The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
         1. Not required
         2. Use default transcode template group id when empty
         */
        $produceConfig['TemplateGroupId'] = null;
        return json_encode($produceConfig);
    }
    
    try {
         $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\ProduceEditingProjectVideoRequest();
        // Set Editing Project ID need to produce
        $request->setProjectId('7794d3757fe548e0abacb5dd1052****');
        // Set Produce Media Metadata
        $request->setMediaMetadata(buildMediaMetadata());
        // Set Produce Configuration
        $request->setProduceConfig(buildProduceConfig());
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Create an online editing project {#h2--div-id-addeditingproject-div-4}
----------------------------------------------------------------------

You can call the AddEditingProject operation to create an online editing project.

For more information about the request and response parameters of this operation, see [AddEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/AddEditingProject.md). Example:

    function buildTimeline() {
        $timeline = array();
    
        // Video Track
        $videoTracks = array();
        $videoTrack = array();
    
        // Video Track Clicps
        $videoTrackClips = array();
        $videoTrackClip1 = array();
        $videoTrackClip1['MediaId'] = '6893fca9814640c8821efa52352****';
        $videoTrackClips[] = $videoTrackClip1;
    
        $videoTrackClip2 = array();
        $videoTrackClip2['MediaId'] = '070bbc13d8294e35b36c3e7ab52****';
        $videoTrackClips[] = $videoTrackClip2;
    
        $videoTrack['VideoTrackClips'] = $videoTrackClips;
        $videoTracks[] = $videoTrack;
        $timeline['VideoTracks'] = $videoTracks;
    
        return json_encode($timeline);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\AddEditingProjectRequest();
        // Build Editing Project Timeline
        $request->setTimeline(buildTimeline());
       // Set Editing Project Title
        $request->setTitle('Editing Project Title');
        // Set Editing Project Description
        $request->setDescription('Editing Project Description');
        // Set Editing Project Cover URL
        $request->setCoverURL('http://192.168.0.0/16/editingproject/cover/projectid.jpg');
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify an online editing project {#h2--div-id-updateeditingproject-div-5}
-------------------------------------------------------------------------

You can call the UpdateEditingProject operation to modify an online editing project.

For more information about the request and response parameters of this operation, see [UpdateEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/UpdateEditingProject.md). Example:

    function buildTimeline() {
        $timeline = array();
    
        // Video Track
        $videoTracks = array();
        $videoTrack = array();
    
        // Video Track Clicps
        $videoTrackClips = array();
        $videoTrackClip1 = array();
        $videoTrackClip1['MediaId'] = '6893fca9814640c8821efa523xxxxxx';
        $videoTrackClips[] = $videoTrackClip1;
    
        $videoTrackClip2 = array();
        $videoTrackClip2['MediaId'] = '070bbc13d8294e35b36c3e7ab52****';
        $videoTrackClips[] = $videoTrackClip2;
    
        $videoTrack['VideoTrackClips'] = $videoTrackClips;
        $videoTracks[] = $videoTrack;
        $timeline['VideoTracks'] = $videoTracks;
    
        return json_encode($timeline);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\UpdateEditingProjectRequest();
        // Set Editing Project ID
        $request->setProjectId('e7c5d44105d3487db23703be152****');
        // Build Editing Project Timeline
        $request->setTimeline(buildTimeline());
        // Set Editing Project Title
        $request->setTitle('Editing Project Title2');
        // Set Editing Project Description
        $request->setDescription('Editing Project Description2');
        // Set Editing Project Cover URL
        $request->setCoverURL('http://192.168.0.0/16/editingproject/cover/projectid.jpg');
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete an online editing project {#h2--div-id-deleteeditingproject-div-6}
-------------------------------------------------------------------------

You can call the DeleteEditingProject operation to delete an online editing project.

For more information about the request and response parameters of this operation, see [DeleteEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/DeleteEditingProject.md). Example:

    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\DeleteEditingProjectRequest();
        // Use comma to split Multi Editing Project IDs
        $request->setProjectIds('e7c5d44105d3487db23703be1352****,12c5d44105d3487db23703be1352****');
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query an online editing project {#h2--div-id-geteditingproject-div-7}
---------------------------------------------------------------------

You can call the GetEditingProject operation to query details about an online editing project.

For more information about the request and response parameters of this operation, see [GetEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProject.md). Example:

    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\GetEditingProjectRequest();
        // Set Editing Project ID
        $request->setProjectId('7794d3757fe548e0abacb5dd152****');
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Search for online editing projects {#h2--div-id-searcheditingproject-div-8}
---------------------------------------------------------------------------

You can call the SearchEditingProject operation to search for online editing projects.

For more information about the request and response parameters of this operation, see [SearchEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/SearchEditingProject.md). Example:

    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\SearchEditingProjectRequest();
        $request->setTitle('Title Keywords');
        $request->setStartTime('2017-01-11T12:00:00Z');
        $request->setEndTime('2017-01-12T12:00:00Z');
        $request->setPageSize(10);
        $request->setPageNo(1);
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Configure materials for an online editing project {#h2--div-id-seteditingprojectmaterials-div-9}
------------------------------------------------------------------------------------------------

You can call the SetEditingProjectMaterials operation to configure materials for an online editing project.

For more information about the request and response parameters of this operation, see [SetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/SetEditingProjectMaterials.md). Example:

    // Configure materials for an online editing project.
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\SetEditingProjectMaterialsRequest();
        // Set Editing Project ID    
        $request->setProjectId('7794d3757fe548e0abacb5dd1052****');
        // Set Editing Project Material IDs, use comma to split
        $request->setMaterialIds('materialId1,materialId2');
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query the materials of an online editing project {#h2--div-id-geteditingprojectmaterials-div-10}
------------------------------------------------------------------------------------------------

You can call the GetEditingProjectMaterials operation to query the materials of an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProjectMaterials.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $request = new vod\GetEditingProjectMaterialsRequest();
        // Set Editing Project ID
        $request->setProjectId('7794d3757fe548e0abacb5dd1052****');
        // Set Editing Project Type
        $request->setType('video');
    
        // Get result
        $result = $client->getAcsResponse($request);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


