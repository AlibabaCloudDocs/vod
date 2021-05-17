Video editing 
==================================

This topic provides examples on how to use the API operations of the video editing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to create, modify, and delete online editing projects. You can also query details about an online editing project, configure materials for an online project, and create a video assembly task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Create a video assembly task based on a timeline {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on a timeline.

The timeline method is most commonly used to assemble videos. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:
**Note**

For more examples on how to assemble videos based on timelines, see [Video assembly](/intl.en-US/Developer Guide/Online editing/Overview.md).

    from aliyunsdkvod.request.v20170321 import ProduceEditingProjectVideoRequest
    def produce_editing_video(clt):
        request = ProduceEditingProjectVideoRequest.ProduceEditingProjectVideoRequest()
    
        # set timeline, this sample shows how to merge two videos
        videoTrackClips = []
        videoTracks = []
        timeline = {}
        videoTrackClip1 = {'MediaId': '<videoId1>'}
        videoTrackClips.append(videoTrackClip1)
        videoTrackClip2 = {'MediaId': '<videoId2>'}
        videoTrackClips.append(videoTrackClip2)
        videoTrack = {'VideoTrackClips': videoTrackClips}
        videoTracks.append(videoTrack)
        timeline['VideoTracks'] = videoTracks
        request.set_Timeline(json.dumps(timeline))
    
        # set media metadata
        mediaMetadata = {'Title': 'editing sample title', 'Description': 'editing sample description', 'Tags': 'Tag1,Tag2,Test',
                         'CoverURL': 'http://test.testvod123.com/media/cover/mediaid.jpg'}
        request.set_MediaMetadata(json.dumps(mediaMetadata))
    
        # set produce config
        produceConfig = {'TemplateGroupId': '<templateGroupId>'}
        #request.set_ProduceConfig(json.dumps(produceConfig))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        produce = produce_editing_video(clt)
        print(produce['MediaId'])
        print(json.dumps(produce, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Create a video assembly task based on an online editing project {#h2--div-id-produceeditingprojectvideoprojectid-div-3}
-----------------------------------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on an online editing project.

If you have high requirements for online editing and management, we recommend that you use this method. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:

    from aliyunsdkvod.request.v20170321 import ProduceEditingProjectVideoRequest
    def produce_editing_video_by_id(clt):
        request = ProduceEditingProjectVideoRequest.ProduceEditingProjectVideoRequest()
    
        # set ProjectId
        request.set_ProjectId('<ProjectId>')
    
        # set media metadata
        mediaMetadata = {'Title': 'editing sample title by ProjectId', 'Description': 'editing sample description by ProjectId',
                         'Tags': 'Tag1,Tag2,Test'}
        request.set_MediaMetadata(json.dumps(mediaMetadata))
    
        # set produce config
        produceConfig = {'TemplateGroupId': '<templateGroupId>'}
        #request.set_ProduceConfig(json.dumps(produceConfig))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        produce = produce_editing_video_by_id(clt)
        print(produce['MediaId'])
        print(json.dumps(produce, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Create an online editing project {#h2--div-id-addeditingproject-div-4}
----------------------------------------------------------------------

You can call the AddEditingProject operation to create an online editing project.

For more information about the request and response parameters of this operation, see [AddEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/AddEditingProject.md). Example:

    from aliyunsdkvod.request.v20170321 import AddEditingProjectRequest
    def add_editing_project(clt):
        request = AddEditingProjectRequest.AddEditingProjectRequest()
    
        # set timeline, this sample shows how to merge two videos
        videoTrackClips = []
        videoTracks = []
        timeline = {}
        videoTrackClip1 = {'MediaId': '<videoId1>'}
        videoTrackClips.append(videoTrackClip1)
        videoTrackClip2 = {'MediaId': '<videoId2>'}
        videoTrackClips.append(videoTrackClip2)
        videoTrack = {'VideoTrackClips': videoTrackClips}
        videoTracks.append(videoTrack)
        timeline['VideoTracks'] = videoTracks
        request.set_Timeline(json.dumps(timeline))
    
        # set project metadata
        request.set_Title('editing project title')
        request.set_Description('editing project description')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        project = add_editing_project(clt)
        print(project['Project'])
        print(json.dumps(project, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify an online editing project {#h2--div-id-updateeditingproject-div-5}
-------------------------------------------------------------------------

You can call the UpdateEditingProject operation to modify an online editing project.
For more information about the request and response parameters of this operation, see [UpdateEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/UpdateEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateEditingProjectRequest
    def update_editing_project(clt):
        request = UpdateEditingProjectRequest.UpdateEditingProjectRequest()
    
        # set projectId
        request.set_ProjectId('<projectId>')
    
        # set timeline, this sample shows how to merge two videos
        videoTrackClips = []
        videoTracks = []
        timeline = {}
        videoTrackClip1 = {'MediaId': '<videoId1>'}
        videoTrackClips.append(videoTrackClip1)
        videoTrackClip2 = {'MediaId': '<videoId2>'}
        videoTrackClips.append(videoTrackClip2)
        videoTrack = {'VideoTrackClips': videoTrackClips}
        videoTracks.append(videoTrack)
        timeline['VideoTracks'] = videoTracks
        request.set_Timeline(json.dumps(timeline))
    
        # set project metadata
        request.set_Title('new editing project title')
        request.set_Description('new editing project description')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = update_editing_project(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete an online editing project {#h2--div-id-deleteeditingproject-div-6}
-------------------------------------------------------------------------

You can call the DeleteEditingProject operation to delete an online editing project.
For more information about the request and response parameters of this operation, see [DeleteEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/DeleteEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteEditingProjectRequest
    def delete_editing_project(clt):
        request = DeleteEditingProjectRequest.DeleteEditingProjectRequest()
    
        # set projectId list
        request.set_ProjectIds('projectId1,projectId2')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = delete_editing_project(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query an online editing project {#h2--div-id-geteditingproject-div-7}
---------------------------------------------------------------------

You can call the GetEditingProject operation to query details about an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProject.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetEditingProjectRequest
    def get_editing_project(clt):
        request = GetEditingProjectRequest.GetEditingProjectRequest()
    
        # set projectId
        request.set_ProjectId('<ProjectId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        project = get_editing_project(clt)
        print(json.dumps(project, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Search for online editing projects {#h2--div-id-searcheditingproject-div-8}
---------------------------------------------------------------------------

You can call the SearchEditingProject operation to search for online editing projects.
For more information about the request and response parameters of this operation, see [SearchEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/SearchEditingProject.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import SearchEditingProjectRequest
    def search_editing_project(clt):
        request = SearchEditingProjectRequest.SearchEditingProjectRequest()
    
        request.set_Title('Title Keywords')
        request.set_StartTime('2018-10-11T12:00:00Z')
        request.set_EndTime('2018-12-25T12:00:00Z')
        request.set_PageSize(10)
        request.set_PageNo(1)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        projects = search_editing_project(clt)
        print(projects['ProjectList']['Project'])
        print(json.dumps(projects, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Configure materials for an online editing project {#h2--div-id-seteditingprojectmaterials-div-9}
------------------------------------------------------------------------------------------------

You can call the SetEditingProjectMaterials operation to configure materials for an online editing project.
For more information about the request and response parameters of this operation, see [SetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/SetEditingProjectMaterials.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import SetEditingProjectMaterialsRequest
    def set_editing_project_materials(clt):
        request = SetEditingProjectMaterialsRequest.SetEditingProjectMaterialsRequest()
    
        request.set_ProjectId('<ProjectId>')
        request.set_MaterialIds('materialId1,materialId2')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = set_editing_project_materials(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the materials of an online editing project {#h2--div-id-geteditingprojectmaterials-div-10}
------------------------------------------------------------------------------------------------

You can call the GetEditingProjectMaterials operation to query the materials of an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProjectMaterials.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetEditingProjectMaterialsRequest
    def get_editing_project_materials(clt):
        request = GetEditingProjectMaterialsRequest.GetEditingProjectMaterialsRequest()
    
        request.set_ProjectId('<ProjectId>')
        request.set_Type('video')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = get_editing_project_materials(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


