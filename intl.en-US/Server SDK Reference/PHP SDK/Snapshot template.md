Snapshot template 
======================================

This topic provides examples on how to use the API operations of the snapshot template module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to create, delete, modify, and query snapshot templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Create a snapshot template {#h2--div-id-addvodtemplate-div-2}
-------------------------------------------------------------

You can call the AddVodTemplate operation to create a snapshot template.

For more information about the request and response parameters of this operation, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md). Example:

    /**
     * Create a snapshot template. Configure the parameters as required.
     * (The following sample code shows the complete configuration of image sprites.)
     * @return
     */
    function buildSnapshotTemplateConfig() {
        $templateConfig = array();
    
        // The configurations of common snapshots. The configurations are also used by image sprites.
        $snapshotConfig = array();
        $snapshotConfig["Count"] = "50";
        $snapshotConfig["Interval"] = "1";
        $snapshotConfig["SpecifiedOffsetTime"] = "0";
        $snapshotConfig["Width"] = "200";
        $snapshotConfig["Height"] = "200";
        $snapshotConfig["FrameType"] = "normal";
        $templateConfig["SnapshotConfig"] = $snapshotConfig;
    
        // The configurations of image sprites. The configurations must be based on those of common snapshots.
        $spriteSnapshotConfig = array();
        $spriteSnapshotConfig["CellWidth"] = "120";
        $spriteSnapshotConfig["CellHeight"] = "68";
        $spriteSnapshotConfig["Columns"] = "3";
        $spriteSnapshotConfig["Lines"] = "10";
        $spriteSnapshotConfig["Padding"] = "20";
        $spriteSnapshotConfig["Margin"] = "50";
        $spriteSnapshotConfig["KeepCellPic"] = "keep";
        $spriteSnapshotConfig["Color"] = "tomato";
        $templateConfig["SpriteSnapshotConfig"] = $spriteSnapshotConfig;
    
        // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        $templateConfig["SnapshotType"] = "SpriteSnapshot";
    
        return json_encode($templateConfig);
    }
    
    /**
     * Add a snapshot template.
     */
    function addSnapshotVodTemplate($client) {
        $request = new vod\AddVodTemplateRequest();
        // The name of the template.
        $request->setName("Test to add a snapshot template");
        // The template type. Set the value to Snapshot.
        $request->setTemplateType("Snapshot");
        // The template configurations.
        $request->setTemplateConfig(buildSnapshotTemplateConfig());
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = addSnapshotVodTemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify a snapshot template {#h2--div-id-updatevodtemplate-div-3}
----------------------------------------------------------------

You can call the UpdateVodTemplate operation to modify a snapshot template.
For more information about the request and response parameters of this operation, see [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/UpdateVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Create a snapshot template. Configure the parameters as required.
     * (The following code shows the complete configurations of common snapshots.)
     * @return
     */
    function buildSnapshotTemplateConfig() {
        $templateConfig = array();
    
        // The configurations of common snapshots. The configurations are also used by image sprites.
        $snapshotConfig = array();
        $snapshotConfig["Count"] = "50";
        $snapshotConfig["Interval"] = "1";
        $snapshotConfig["SpecifiedOffsetTime"] = "0";
        $snapshotConfig["Width"] = "200";
        $snapshotConfig["Height"] = "200";
        $snapshotConfig["FrameType"] = "normal";
        $templateConfig["SnapshotConfig"] = $snapshotConfig;
    
        // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        $templateConfig["SnapshotType"] = "NormalSnapshot";
    
        return json_encode($templateConfig);
    }
    
    /**
     * Modify a snapshot template.
     */
    function updateSnapshotVodTemplate($client) {
        $request = new vod\UpdateVodTemplateRequest();
        // The ID of the template that you want to modify.
        $request->setVodTemplateId("6e9835ce8896aa3ace027c048352****");
        // The name of the template.
        $request->setName("Test to modify a snapshot template");
        // The template configurations.
        $request->setTemplateConfig(buildSnapshotTemplateConfig());
    
        return $client->getAcsResponse($request);
    }
    
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = updateSnapshotVodTemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete a snapshot template {#h2--div-id-deletevodtemplate-div-4}
----------------------------------------------------------------

You can call the DeleteVodTemplate operation to delete a snapshot template.

For more information about the request and response parameters of this operation, see [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/DeleteVodTemplate.md). Example:

    /**
     * Delete a snapshot template.
     */
    function deleteSnapshotVodTemplate($client) {
        $request = new vod\DeleteVodTemplateRequest();
        // The ID of the template that you want to delete.
        $request->setVodTemplateId("6e9835ce8896aa3ace027c048352****");
    
        return $client->getAcsResponse($request);
    }
    
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = deleteSnapshotVodTemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query snapshot templates {#h2--div-id-listvodtemplate-div-5}
------------------------------------------------------------

You can call the ListVodTemplate operation to query snapshot templates.

For more information about the request and response parameters of this operation, see [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/ListVodTemplate.md). Example:

    /**
     * Query snapshot templates.
     */
    function listSnapshotVodTemplate($client) {
        $request = new vod\ListVodTemplateRequest();
        // The template type. Set the value to Snapshot.
        $request->setTemplateType("Snapshot");
    
        return $client->getAcsResponse($request);
    }
    
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = listSnapshotVodTemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query a snapshot template {#h2--div-id-getvodtemplate-div-6}
------------------------------------------------------------

You can call the GetVodTemplate operation to query a snapshot template.

For more information about the request and response parameters of this operation, see [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/GetVodTemplate.md). Example:

    /**
     * Query a snapshot template.
     */
    function getSnapshotVodTemplate($client) {
        $request = new vod\GetVodTemplateRequest();
        // The ID of the template that you want to query.
        $request->setVodTemplateId("6e9835ce8896aa3ace027c048352****");
    
        return $client->getAcsResponse($request);
    }
    
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = getSnapshotVodTemplate($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


