Snapshot template 
======================================

This topic provides examples on how to use the API operations of the snapshot template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to create, delete, modify, and query snapshot templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Create a snapshot template {#h2--div-id-addvodtemplate-div-2}
-------------------------------------------------------------

You can call the AddVodTemplate operation to create a snapshot template.
For more information about the request and response parameters of this operation, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var templateConfig = {
        // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        SnapshotType: 'SpriteSnapshot',
        // The configurations of common snapshots. The configurations are also used by image sprites.
        SnapshotConfig:{
            Count: '50',
            Interval: '1',
            SpecifiedOffsetTime: '0',
            Width: '200',
            Height: '200',
            FrameType: 'normal',
            // The configurations of image sprites. The configurations must be based on those of common snapshots.
            SpriteSnapshotConfig:{
                CellWidth: '120',
                CellHeight: '68',
                Columns: '3',
                Lines: '10',
                Padding: '20',
                Margin: '50',
                KeepCellPic: 'keep',
                Color: 'tomato'
            }
        }
    };
    client.request("AddVodTemplate", {
        Name: 'Test to add a snapshot template',     // The template name.
        TemplateType: 'Snapshot',   // The template type. Set the value to Snapshot.
        TemplateConfig: JSON.stringify(templateConfig)   // The template configurations.
    }, {}).then(function (response) {
        // The template ID.
        console.log('SnapshotVodTemplateId = ' + response.VodTemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify a snapshot template {#h2--div-id-updatevodtemplate-div-3}
----------------------------------------------------------------

You can call the UpdateVodTemplate operation to modify a snapshot template.
For more information about the request and response parameters of this operation, see [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/UpdateVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var templateConfig = {
        // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        SnapshotType: 'SpriteSnapshot',
        // The configurations of common snapshots. The configurations are also used by image sprites.
        SnapshotConfig:{
            Count: '50',
            Interval: '1',
            SpecifiedOffsetTime: '0',
            Width: '200',
            Height: '200',
            FrameType: 'normal',
            // The configurations of image sprites. The configurations must be based on those of common snapshots.
            SpriteSnapshotConfig:{
                CellWidth: '120',
                CellHeight: '68',
                Columns: '3',
                Lines: '10',
                Padding: '20',
                Margin: '50',
                KeepCellPic: 'keep',
                Color: 'tomato'
            }
        }
    };
    client.request("UpdateVodTemplate", {
        VodTemplateId: 'VodTemplateId',   // The ID of the template that you want to modify.
        Name: 'Test to modify a snapshot template',     // The template name.
        TemplateConfig: JSON.stringify(templateConfig)   // The template configurations.
    }, {}).then(function (response) {
        // The template ID.
        console.log('SnapshotVodTemplateId = ' + response.VodTemplateId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete a snapshot template {#h2--div-id-deletevodtemplate-div-4}
----------------------------------------------------------------

You can call the DeleteVodTemplate operation to delete a snapshot template.
For more information about the request and response parameters of this operation, see [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/DeleteVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DeleteVodTemplate", {
        VodTemplateId: 'VodTemplateId',   // The ID of the template that you want to delete.
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query snapshot templates {#h2--div-id-listvodtemplate-div-5}
------------------------------------------------------------

You can call the ListVodTemplate operation to query snapshot templates.
For more information about the request and response parameters of this operation, see [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/ListVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListVodTemplate", {
        TemplateType: 'Snapshot'   // The template type. Set the value to Snapshot.
    }, {}).then(function (response) {
        // List the number of snapshot templates.
        console.log('SnapshotVodTemplate Count = ' + response.VodTemplateInfoList.length);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query a snapshot template {#h2--div-id-getvodtemplate-div-6}
------------------------------------------------------------

You can call the GetVodTemplate operation to query details about a snapshot template.
For more information about the request and response parameters of this operation, see [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/GetVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetVodTemplate", {
        VodTemplateId: 'VodTemplateId',   // The ID of the template that you want to query.
    }, {}).then(function (response) {
        // List the ID of the snapshot template.
        if (response.VodTemplateInfo){
            console.log('SnapshotVodTemplateId = ' + response.VodTemplateInfo.VodTemplateId);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


