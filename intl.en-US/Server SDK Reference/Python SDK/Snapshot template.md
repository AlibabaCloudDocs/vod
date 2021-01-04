Snapshot template 
======================================

This topic provides examples on how to use the API operations of the snapshot template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to create, delete, modify, and query snapshot templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Create a snapshot template {#h2--div-id-addvodtemplate-div-2}
-------------------------------------------------------------

You can call the AddVodTemplate operation to create a snapshot template.
For more information about the request and response parameters of this operation, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import AddVodTemplateRequest
    def add_vod_template(clt):
        request = AddVodTemplateRequest.AddVodTemplateRequest()
        # The template name.
        request.set_Name('Sample Snapshot Template')
        # The template type. Set the value to Snapshot.
        request.set_TemplateType('Snapshot')
    
        # The template configurations.
        snapshotConfig = {'Count': 50, 'Interval': 1, 'SpecifiedOffsetTime': 0, 'Width': 200, 'Height': 200,
                          'FrameType': 'normal'}
        templateConfig = {'SnapshotConfig': snapshotConfig, 'SnapshotType': 'NormalSnapshot'}
    
        """
        # Optional: The configurations of image sprites. The configurations must be based on those of common snapshots.
        spriteSnapshotConfig = {'CellWidth': 120, 'CellHeight': 68, 'Columns': 3, 'Lines': 10, 'Padding': 20,
                                'Margin': 50, 'KeepCellPic': 'keep', 'Color': 'tomato'}
        snapshotConfig['SpriteSnapshotConfig'] = spriteSnapshotConfig
        templateConfig['SnapshotType'] = 'SpriteSnapshot'
        """
    
        request.set_TemplateConfig(json.dumps(templateConfig))
    
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        template = add_vod_template(clt)
        print(template['VodTemplateId'])
        print(json.dumps(template, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify a snapshot template {#h2--div-id-updatevodtemplate-div-3}
----------------------------------------------------------------

You can call the UpdateVodTemplate operation to modify a snapshot template.
For more information about the request and response parameters of this operation, see [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/UpdateVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateVodTemplateRequest
    def update_vod_template(clt):
        request = UpdateVodTemplateRequest.UpdateVodTemplateRequest()
        request.set_VodTemplateId('<templateId>')
        # Modify the template name.
        request.set_Name('New Snapshot Template Name')
        # Modify the configurations of the snapshot template .
        snapshotConfig = {'Count': 50, 'Interval': 1, 'SpecifiedOffsetTime': 0, 'Width': 200, 'Height': 200,
                          'FrameType': 'normal'}
        templateConfig = {'SnapshotConfig': snapshotConfig, 'SnapshotType': 'NormalSnapshot'}
        request.set_TemplateConfig(json.dumps(templateConfig))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        template = update_vod_template(clt)
        print(json.dumps(template, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete a snapshot template {#h2--div-id-deletevodtemplate-div-4}
----------------------------------------------------------------

You can call the DeleteteVodTemplate operation to delete a snapshot template.
For more information about the request and response parameters of this operation, see [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/DeleteVodTemplate.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteVodTemplateRequest
    def delete_vod_template(clt):
        request = DeleteVodTemplateRequest.DeleteVodTemplateRequest()
        request.set_VodTemplateId('<templateId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = delete_vod_template(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query snapshot templates {#h2--div-id-listvodtemplate-div-5}
------------------------------------------------------------

You can call the ListVodTemplate operation to query snapshot templates.
For more information about the request and response parameters of this operation, see [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/ListVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import ListVodTemplateRequest
    def list_vod_template(clt):
        request = ListVodTemplateRequest.ListVodTemplateRequest()
        # The template type. Set the value to Snapshot.
        request.set_TemplateType('Snapshot')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        templates = list_vod_template(clt)
        print(templates['VodTemplateInfoList'])
        print(json.dumps(templates, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query a snapshot template {#h2--div-id-getvodtemplate-div-6}
------------------------------------------------------------

You can call the GetVodTemplate operation to query a snapshot template.
For more information about the request and response parameters of this operation, see [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/GetVodTemplate.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetVodTemplateRequest
    def get_vod_template(clt):
        request = GetVodTemplateRequest.GetVodTemplateRequest()
        request.set_VodTemplateId('<templateId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        template = get_vod_template(clt)
        print(template['VodTemplateInfo'])
        print(json.dumps(template, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


