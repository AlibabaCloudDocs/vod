Snapshot template 
======================================

This topic provides examples on how to use the API operations of the snapshot template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to create, delete, modify, and query snapshot templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Create a snapshot template {#h2--div-id-addvodtemplate-div-2}
-------------------------------------------------------------

You can call the AddVodTemplate operation to create a snapshot template.
For more information about the request and response parameters of this operation, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.alibaba.fastjson.JSON;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.vod.model.v20170321.AddVodTemplateRequest;
    import com.aliyuncs.vod.model.v20170321.AddVodTemplateResponse;
    
    /**
     * Build the parameters of a snapshot template. Configure the parameters as required.
     * The following sample code shows the complete configuration of image sprites.
     * @return
     */
    public static JSONObject buildSnapshotTemplateConfig() {
        JSONObject templateConfig = new JSONObject();
        JSONObject snapshotConfig = new JSONObject();
        snapshotConfig.put("Count", "50");
        snapshotConfig.put("Interval", "1");
        snapshotConfig.put("SpecifiedOffsetTime", "0");
        snapshotConfig.put("Width", "200");
        snapshotConfig.put("Height", "200");
        snapshotConfig.put("FrameType", "normal");
        // The configurations of common snapshots. The configurations are also used by image sprites.
        templateConfig.put("SnapshotConfig", snapshotConfig);
    
        // The configurations of image sprites. The configurations must be based on those of common snapshots.
        JSONObject spriteSnapshotConfig = new JSONObject();
        spriteSnapshotConfig.put("CellWidth", "120");
        spriteSnapshotConfig.put("CellHeight", "68");
        spriteSnapshotConfig.put("Columns", "3");
        spriteSnapshotConfig.put("Lines", "10");
        spriteSnapshotConfig.put("Padding", "20");
        spriteSnapshotConfig.put("Margin", "50");
        spriteSnapshotConfig.put("KeepCellPic", "keep");
        spriteSnapshotConfig.put("Color", "tomato");
        snapshotConfig.put("SpriteSnapshotConfig", spriteSnapshotConfig);
    
        // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        templateConfig.put("SnapshotType", "SpriteSnapshot");
        return templateConfig;
    }
    
    /**
     * Create a snapshot template.
     */
    public static AddVodTemplateResponse addSnapshotVodTemplate(DefaultAcsClient client) throws Exception {
        AddVodTemplateRequest request = new AddVodTemplateRequest();
        // The template name.
        request.setName("Test to add a snapshot template");
        // The template type. Set the value to Snapshot.
        request.setTemplateType("Snapshot");
        // The template configurations.
        JSONObject templateConfig = buildSnapshotTemplateConfig();
        request.setTemplateConfig(templateConfig.toJSONString());
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        AddVodTemplateResponse response = new AddVodTemplateResponse();
        try {
            // Create a snapshot template.
            response = addSnapshotVodTemplate(client);
            // The template ID.
            System.out.println("SnapshotVodTemplateId = " + response.getVodTemplateId());
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Modify a snapshot template {#h2--div-id-updatevodtemplate-div-3}
----------------------------------------------------------------

You can call the UpdateVodTemplate operation to modify a snapshot template.
For more information about the request and response parameters of this operation, see [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/UpdateVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.alibaba.fastjson.JSON;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.vod.model.v20170321.UpdateVodTemplateRequest;
    import com.aliyuncs.vod.model.v20170321.UpdateVodTemplateResponse;
    
    /**
     * Build the parameters of a snapshot template. Configure the parameters as required.
     * The following code shows the complete configurations of common snapshots.
     * @return
     */
    public static JSONObject buildSnapshotTemplateConfig() {
        JSONObject templateConfig = new JSONObject();
        JSONObject snapshotConfig = new JSONObject();
        snapshotConfig.put("Count", "50");
        snapshotConfig.put("Interval", "1");
        snapshotConfig.put("SpecifiedOffsetTime", "0");
        snapshotConfig.put("Width", "200");
        snapshotConfig.put("Height", "200");
        snapshotConfig.put("FrameType", "normal");
        // The configurations of common snapshots. The configurations are also used by image sprites.
        templateConfig.put("SnapshotConfig", snapshotConfig);
    
        // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        templateConfig.put("SnapshotType", "NormalSnapshot");
        return templateConfig;
    }
    
    /**
     * Modify a snapshot template.
     */
    public static UpdateVodTemplateResponse updateSnapshotVodTemplate(DefaultAcsClient client) throws Exception {
        UpdateVodTemplateRequest request = new UpdateVodTemplateRequest();
        // The ID of the template that you want to modify.
        request.setVodTemplateId("53azf9d796fad9d7b862b2e****");
        // The template name.
        request.setName("Test to modify a snapshot template");
        // The template configurations.
        JSONObject templateConfig = buildSnapshotTemplateConfig();
        request.setTemplateConfig(templateConfig.toJSONString());
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        UpdateVodTemplateResponse response = new UpdateVodTemplateResponse();
        try {
            // Modify a snapshot template.
            response = updateSnapshotVodTemplate(client);
            // The template ID.
            System.out.println("SnapshotVodTemplateId = " + response.getVodTemplateId());
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Delete a snapshot template {#h2--div-id-deletevodtemplate-div-4}
----------------------------------------------------------------

You can call the DeleteVodTemplate operation to delete a snapshot template.
For more information about the request and response parameters of this operation, see [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/DeleteVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DeleteVodTemplateRequest;
    import com.aliyuncs.vod.model.v20170321.DeleteVodTemplateResponse;
    
    /**
     * Delete a snapshot template.
     */
    public static DeleteVodTemplateResponse deleteSnapshotVodTemplate(DefaultAcsClient client) throws Exception  
        DeleteVodTemplateRequest request = new DeleteVodTemplateRequest();
        // The ID of the template that you want to delete.
        request.setVodTemplateId("53azf9d796fad9d7b862b2e5e5b");
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        DeleteVodTemplateResponse response = new DeleteVodTemplateResponse();
        try {
            // Delete a snapshot template.
            response = deleteSnapshotVodTemplate(client);
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Query snapshot templates {#h2--div-id-listvodtemplate-div-5}
------------------------------------------------------------

You can call the ListVodTemplate operation to query snapshot templates.
For more information about the request and response parameters of this operation, see [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/ListVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListVodTemplateRequest;
    import com.aliyuncs.vod.model.v20170321.ListVodTemplateResponse;
    
    /**
     * Query snapshot templates.
     */
    public static ListVodTemplateResponse listSnapshotVodTemplate(DefaultAcsClient client) throws Exception {
        ListVodTemplateRequest request = new ListVodTemplateRequest();
        // The template type. Set the value to Snapshot.
        request.setTemplateType("Snapshot");
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        ListVodTemplateResponse response = new ListVodTemplateResponse();
        try {
            // Query snapshot templates.
            response = listSnapshotVodTemplate(client);
            // List the number of snapshot templates.
            System.out.println("SnapshotVodTemplateId = " + response.getVodTemplateInfoList().size());
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Query a snapshot template {#h2--div-id-getvodtemplate-div-6}
------------------------------------------------------------

You can call the GetVodTemplate operation to query details about a snapshot template.

For more information about the request and response parameters of this operation, see [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/GetVodTemplate.md). Example:

    import com.aliyuncs.vod.model.v20170321.GetVodTemplateRequest;
    import com.aliyuncs.vod.model.v20170321.GetVodTemplateResponse;
    
    /**
    * Query a snapshot template.
    */
    public static GetVodTemplateResponse getSnapshotVodTemplate(DefaultAcsClient client) throws Exception {
        GetVodTemplateRequest request = new GetVodTemplateRequest();
        // The ID of the template that you want to query.
        request.setVodTemplateId("53azf9d796fad9d7b862b2e****");
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        GetVodTemplateResponse response = new GetVodTemplateResponse();
        try {
            // Query a snapshot template.
            response = getSnapshotVodTemplate(client);
            // List the ID of the snapshot template.
            System.out.println("SnapshotVodTemplateId = " + response.getVodTemplateInfo().getVodTemplateId());
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }


