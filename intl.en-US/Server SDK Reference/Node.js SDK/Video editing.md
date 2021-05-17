Video editing 
==================================

This topic provides examples on how to use the API operations of the video editing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to create, modify, and delete online editing projects. You can also query details about an online editing project, configure materials for an online project, and create a video assembly task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Create a video assembly task based on a timeline {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on a timeline.
The timeline method is most commonly used to assemble videos. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:
**Note**
For more examples on how to assemble videos based on timelines, see [Video assembly](/intl.en-US/Developer Guide/Online editing/Overview.md). {#h2--div-id-produceeditingprojectvideo-div-2}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // Build Editing Project Timeline
    var timeline = {
        // Video Track
        VideoTracks: [{
            // Video Track Clips
            VideoTrackClips: [{
                MediaId: 'MediaId1'
            },{
                MediaId: 'MediaId2'
            }]
        }]
    };
    // Set Produce Media Metadata
    var mediaMetadata = {
        Title: 'Title',  // Produce Media Title
        Description: 'Description',  // Produce Media Description
        CoverURL: 'http://test.testvod123.com/media/cover/mediaid.jpg',  // Produce Media UserDefined Cover URL
        CateId: null,   // Produce Media Category ID
        Tags: 'Tag1,Tag2'   // Produce Media Category Name
    };
    // Set Produce Configuration
    var produceConfig = {
        /*
         The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
         1. Not required
         2. Use default transcode template group id when empty
         */
        TemplateGroupId: null
    };
    client.request("ProduceEditingProjectVideo", {
        Timeline: JSON.stringify(timeline),
        MediaMetadata: JSON.stringify(mediaMetadata),
        ProduceConfig: JSON.stringify(produceConfig)
    }, {}).then(function (response) {
        // Produce Media ID
        console.log('MediaId = '+ response.MediaId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Also, you can call the ProduceEditingProjectVideo operation to create a video assembly task based on an online editing project.
If you have high requirements for online editing and management, we recommend that you use this method. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // Set Produce Media Metadata
    var mediaMetadata = {
        Title: 'Title',  // Produce Media Title
        Description: 'Description',  // Produce Media Description
        CoverURL: 'http://test.testvod123.com/media/cover/mediaid.jpg',  // Produce Media UserDefined Cover URL
        CateId: null,   // Produce Media Category ID
        Tags: 'Tag1,Tag2'   // Produce Media Category Name
    };
    // Set Produce Configuration
    var produceConfig = {
        /*
         The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
         1. Not required
         2. Use default transcode template group id when empty
         */
        TemplateGroupId: null
    };
    client.request("ProduceEditingProjectVideo", {
        ProjectId: 'ProjectId',    // Set Editing Project ID need to produce
        MediaMetadata: JSON.stringify(mediaMetadata),
        ProduceConfig: JSON.stringify(produceConfig)
    }, {}).then(function (response) {
        // Produce Media ID
        console.log('MediaId = '+ response.MediaId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Create an online editing project {#h2--div-id-addeditingproject-div-4}
----------------------------------------------------------------------

You can call the AddEditingProject operation to create an online editing project.
For more information about the request and response parameters of this operation, see [AddEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/AddEditingProject.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // Build Editing Project Timeline
    var timeline = {
        // Video Track
        VideoTracks: [{
            // Video Track Clips
            VideoTrackClips: [{
                MediaId: 'MediaId1'
            },{
                MediaId: 'MediaId2'
            }]
        }]
    };
    client.request("AddEditingProject", {
        Timeline: JSON.stringify(timeline),
        Title: 'Editing Project Title',   // Set Editing Project Title
        Description: 'Editing Project Description',   // Set Editing Project Description
        CoverURL: 'http://test.testvod123.com/editingproject/cover/projectid.jpg'  // Set Editing Project Cover URL
    }, {}).then(function (response) {
        if (response.Project){
            console.log('Editing Project Id = '+ response.Project.ProjectId);
            console.log('Editing Project Title = '+ response.Project.Title);
            console.log('Editing Project Description = '+ response.Project.Description);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify an online editing project {#h2--div-id-updateeditingproject-div-5}
-------------------------------------------------------------------------

You can call the UpdateEditingProject operation to modify an online editing project.
For more information about the request and response parameters of this operation, see [UpdateEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/UpdateEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // Build Editing Project Timeline
    var timeline = {
        // Video Track
        VideoTracks: [{
            // Video Track Clips
            VideoTrackClips: [{
                MediaId: 'MediaId1'
            },{
                MediaId: 'MediaId2'
            }]
        }]
    };
    client.request("UpdateEditingProject", {
        ProjectId: 'ProjectId',
        Timeline: JSON.stringify(timeline),
        Title: 'Editing Project Title',   // Set Editing Project Title
        Description: 'Editing Project Description',   // Set Editing Project Description
        CoverURL: 'http://test.testvod123.com/editingproject/cover/projectid.jpg'  // Set Editing Project Cover URL
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete an online editing project {#h2--div-id-deleteeditingproject-div-6}
-------------------------------------------------------------------------

You can call the DeleteEditingProject operation to delete an online editing project.
For more information about the request and response parameters of this operation, see [DeleteEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/DeleteEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DeleteEditingProject", {
        ProjectIds: 'ProjectId1,projectid2'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query an online editing project {#h2--div-id-geteditingproject-div-7}
---------------------------------------------------------------------

You can call the GetEditingProject operation to query details about an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProject.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetEditingProject", {
        ProjectId: 'ProjectId'
    }, {}).then(function (response) {
        if (response.Project){
            console.log('Editing Project Id = '+ response.Project.ProjectId);
            console.log('Editing Project Timeline = '+ response.Project.Timeline);
            console.log('Editing Project Title = '+ response.Project.Title);
            console.log('Editing Project Description = '+ response.Project.Description);
            console.log('Editing Project CoverURL = '+ response.Project.CoverURL);
            console.log('Editing Project CreationTime = '+ response.Project.CreationTime);
            console.log('Editing Project ModifiedTime = '+ response.Project.ModifiedTime);
            console.log('Editing Project Status = '+ response.Project.Status);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Search for online editing projects {#h2--div-id-searcheditingproject-div-8}
---------------------------------------------------------------------------

You can call the SearchEditingProject operation to search for online editing projects.
For more information about the request and response parameters of this operation, see [SearchEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/SearchEditingProject.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SearchEditingProject", {
        Title: 'TitleKeywords',
        StartTime: '2018-12-28T14:42:18Z',
        EndTime: '2018-12-30T14:42:18Z',
        PageSize: 10,
        PageNo: 1
    }, {}).then(function (response) {
        if (response.ProjectList && response.ProjectList.Project && response.ProjectList.Project.length > 0){
            console.log('Total Size = ' + response.Total);
            for(var i=0; i<response.ProjectList.Project.length; i++){
                var project = response.ProjectList.Project[i];
                console.log('No ' + i + ' Editing Project');
                console.log('Editing Project Id = '+ project.ProjectId);
                console.log('Editing Project Title = '+ project.Title);
                console.log('Editing Project Description = '+ project.Description);
                console.log('Editing Project CoverURL = '+ project.CoverURL);
                console.log('Editing Project CreationTime = '+ project.CreationTime);
                console.log('Editing Project ModifiedTime = '+ project.ModifiedTime);
                console.log('Editing Project Status = '+ project.Status);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Configure materials for an online editing project {#h2--div-id-seteditingprojectmaterials-div-9}
------------------------------------------------------------------------------------------------

You can call the SetEditingProjectMaterials operation to configure materials for an online editing project.
For more information about the request and response parameters of this operation, see [SetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/SetEditingProjectMaterials.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SetEditingProjectMaterials", {
        ProjectId: 'ProjectId',
        MaterialIds: 'MaterialId1,MaterialId2'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query the materials of an online editing project {#h2--div-id-geteditingprojectmaterials-div-10}
------------------------------------------------------------------------------------------------

You can call the GetEditingProjectMaterials operation to query the materials of an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProjectMaterials.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetEditingProjectMaterials", {
        ProjectId: 'ProjectId',
        Type: 'video'
    }, {}).then(function (response) {
        if (response.MaterialList && response.MaterialList.Material && response.MaterialList.Material.length > 0){
            for(var i=0; i<response.MaterialList.Material.length; i++){
                var material = response.MaterialList.Material[i];
                console.log('No ' + i + ' Editing Project');
                console.log('Editing Project Material Id = '+ material.MaterialId);
                console.log('Editing Project Material Title = '+ material.Title);
                console.log('Editing Project Material Category ID = '+ material.CateId);
                console.log('Editing Project Material Category Name = '+ material.CateName);
                console.log('Editing Project Material Tags = '+ material.Tags);
                console.log('Editing Project Material CoverURL = '+ material.CoverURL);
                console.log('Editing Project Material Create Time = '+ material.CreationTime);
                console.log('Editing Project Material Last ModifiedTime = '+ material.ModifiedTime);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


