Video editing 
==================================

This topic provides examples on how to use the API operations of the video editing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to create, modify, and delete online editing projects. You can also query details about an online editing project and create a video assembly task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Create a video assembly task based on a timeline {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on a timeline.
The timeline method is most commonly used to assemble videos. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Video editing/ProduceEditingProjectVideo.md). Example:
**Note**
For more examples on how to assemble videos based on timelines, see [Video assembly](/intl.en-US/Developer Guide/Online editing/Overview.md). {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ProduceEditingProjectVideoRequest;
    import com.aliyuncs.vod.model.v20170321.ProduceEditingProjectVideoResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            ProduceEditingProjectVideoRequest request = new ProduceEditingProjectVideoRequest();
            // Build Editing Project Timeline
            request.setTimeline(buildTimeline());
            // Set Produce Media Metadata
            request.setMediaMetadata(buildMediaMetadata());
            // Set Produce Configuration
            request.setProduceConfig(buildProduceConfig());
    
            ProduceEditingProjectVideoResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    // Produce Media ID
                    System.out.println("MediaId:" + response.getMediaId());
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }
    
        public static String buildMediaMetadata(){
            JSONObject mediaMetadata = new JSONObject();
            // Produce Media Title
            mediaMetadata.put("Title", "Title");
            // Produce Media Description
            mediaMetadata.put("Description", "Description");
            // Produce Media UserDefined Cover URL
            mediaMetadata.put("CoverURL", "http://192.168.0.0/16/media/cover/mediaid.jpg");
            // Produce Media Category ID
            mediaMetadata.put("CateId", null);
            // Produce Media Category Name
            mediaMetadata.put("Tags", "Tag1,Tag2,Test");
            return mediaMetadata.toString();
        }
    
        public static String buildProduceConfig(){
            JSONObject produceConfig = new JSONObject();
            /*
             The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
             1. Not required 
             2. Use default transcode template group id when empty
             */
            produceConfig.put("TemplateGroupId", null);
            return produceConfig.toString();
        }
    
        /**
         * This Sample shows how to merge two videos
         */
        public static String buildTimeline(){
            JSONObject timeline = new JSONObject();
    
            // Video Track
            JSONArray videoTracks = new JSONArray();
            JSONObject videoTrack = new JSONObject();
    
            // Video Track Clips
            JSONArray videoTrackClips = new JSONArray();
            JSONObject videoTrackClip1 = new JSONObject();
            videoTrackClip1.put("MediaId", "11119b4d7cf14dc7b83b0e801cbe****");
            videoTrackClips.add(videoTrackClip1);
            JSONObject videoTrackClip2 = new JSONObject();
            videoTrackClip2.put("MediaId", "22229b4d7cf14dc7b83b0e801cbe****");
            videoTrackClips.add(videoTrackClip2);
    
            videoTrack.put("VideoTrackClips", videoTrackClips);
            videoTracks.add(videoTrack);
    
            timeline.put("VideoTracks", videoTracks);
    
            return timeline.toString();
        }



Create a video assembly task based on an online editing project {#h2--div-id-produceeditingprojectvideoprojectid-div-3}
-----------------------------------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on an online editing project.
If you have high requirements for online editing and management, we recommend that you use this method. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Video editing/ProduceEditingProjectVideo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ProduceEditingProjectVideoRequest;
    import com.aliyuncs.vod.model.v20170321.ProduceEditingProjectVideoResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            ProduceEditingProjectVideoRequest request = new ProduceEditingProjectVideoRequest();
            // Set Editing Project ID need to produce
            request.setProjectId("ProjectId");
            // Set Produce Media Metadata
            request.setMediaMetadata(buildMediaMetadata());
            // Set Produce Configuration
            request.setProduceConfig(buildProduceConfig());
    
            ProduceEditingProjectVideoResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    // Produce Media ID
                    System.out.println("MediaId:" + response.getMediaId());
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }
    
        public static String buildMediaMetadata(){
            JSONObject mediaMetadata = new JSONObject();
            // Produce Media Title
            mediaMetadata.put("Title", "Title");
            // Produce Media Description
            mediaMetadata.put("Description", "Description");
            // Produce Media UserDefined Cover URL
            mediaMetadata.put("CoverURL", "http://192.168.0.0/16/media/cover/mediaid.jpg");
            // Produce Media Category ID
            mediaMetadata.put("CateId", null);
            // Produce Media Category Name
            mediaMetadata.put("Tags", "Tag1,Tag2,Test");
            return mediaMetadata.toString();
        }
    
        public static String buildProduceConfig(){
            JSONObject produceConfig = new JSONObject();
            /*
             The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
             1. Not required 
             2. Use default transcode template group id when empty
             */
            produceConfig.put("TemplateGroupId", null);
            return produceConfig.toString();
        }



Create an online editing project {#h2--div-id-addeditingproject-div-4}
----------------------------------------------------------------------

You can call the AddEditingProject operation to create an online editing project.
For more information about the request and response parameters of this operation, see [AddEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/AddEditingProject.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.AddEditingProjectRequest;
    import com.aliyuncs.vod.model.v20170321.AddEditingProjectResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            AddEditingProjectRequest request = new AddEditingProjectRequest();
            // Build Editing Project Timeline
            request.setTimeline(buildTimeline());
            // Set Editing Project Title
            request.setTitle("Editing Project Title");
            // Set Editing Project Description
            request.setDescription("Editing Project Description");
            // Set Editing Project Cover URL
            request.setCoverURL("http://192.168.0.0/16/editingproject/cover/projectid.jpg");
    
            AddEditingProjectResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    if (response.getProject() ! = null){
                        System.out.println("Editing Project ID:" + response.getProject().getProjectId());
                        System.out.println("Editing Project Title:" + response.getProject().getTitle());
                        System.out.println("Editing Project Create Time:" + response.getProject().getCreationTime());
                        System.out.println("Editing Project Description:" + response.getProject().getDescription());
                        System.out.println("Editing Project Status:" + response.getProject().getStatus());
                    }
    
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }
    
        /**
         * This Sample shows how to merge two videos
         */
        public static String buildTimeline(){
            JSONObject timeline = new JSONObject();
    
            // Video Track
            JSONArray videoTracks = new JSONArray();
            JSONObject videoTrack = new JSONObject();
    
            // Video Track Clips
            JSONArray videoTrackClips = new JSONArray();
            JSONObject videoTrackClip1 = new JSONObject();
            videoTrackClip1.put("MediaId", "11119b4d7cf14dc7b83b0e801cbe****");
            videoTrackClips.add(videoTrackClip1);
            JSONObject videoTrackClip2 = new JSONObject();
            videoTrackClip2.put("MediaId", "22229b4d7cf14dc7b83b0e801cbe****");
            videoTrackClips.add(videoTrackClip2);
    
            videoTrack.put("VideoTrackClips", videoTrackClips);
            videoTracks.add(videoTrack);
    
            timeline.put("VideoTracks", videoTracks);
    
            return timeline.toString();
        }



Modify an online editing project {#h2--div-id-updateeditingproject-div-5}
-------------------------------------------------------------------------

You can call the UpdateEditingProject operation to modify an online editing project.

For more information about the request and response parameters of this operation, see [UpdateEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/UpdateEditingProject.md). Example:

    import com.aliyuncs.vod.model.v20170321.UpdateEditingProjectRequest;
    import com.aliyuncs.vod.model.v20170321.UpdateEditingProjectResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            UpdateEditingProjectRequest request = new UpdateEditingProjectRequest();
            request.setProjectId("YourProjectId");
            // Set Editing Project Timeline
            request.setTimeline(buildTimeline());
            // Set Editing Project Title
            request.setTitle("Editing Project Title");
            // Set Editing Project Description
            request.setDescription("Editing Project Description");
            // Set Editing Project Cover URL
            request.setCoverURL("http://192.168.0.0/16/editingproject/cover/projectid.jpg");
    
            UpdateEditingProjectResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }
    
        /**
         * This Sample shows how to merge two videos
         */
        public static String buildTimeline(){
            JSONObject timeline = new JSONObject();
    
            // Video Track
            JSONArray videoTracks = new JSONArray();
            JSONObject videoTrack = new JSONObject();
    
            // Video Track
            JSONArray videoTrackClips = new JSONArray();
            JSONObject videoTrackClip1 = new JSONObject();
            videoTrackClip1.put("MediaId", "11119b4d7cf14dc7b83b0e801cbe****");
            videoTrackClips.add(videoTrackClip1);
            JSONObject videoTrackClip2 = new JSONObject();
            videoTrackClip2.put("MediaId", "22229b4d7cf14dc7b83b0e801cbe****");
            videoTrackClips.add(videoTrackClip2);
    
            videoTrack.put("VideoTrackClips", videoTrackClips);
            videoTracks.add(videoTrack);
    
            timeline.put("VideoTracks", videoTracks);
    
            return timeline.toString();
        }



Delete an online editing project {#h2--div-id-deleteeditingproject-div-6}
-------------------------------------------------------------------------

You can call the DeleteEditingProject operation to delete an online editing project.
For more information about the request and response parameters of this operation, see [DeleteEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/DeleteEditingProject.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DeleteEditingProjectRequest;
    import com.aliyuncs.vod.model.v20170321.DeleteEditingProjectResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            DeleteEditingProjectRequest request = new DeleteEditingProjectRequest();
            // Use comma to split Multi Editing Project IDs
            request.setProjectIds("projectid1,projectid2");
            DeleteEditingProjectResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }



Query an online editing project {#h2--div-id-geteditingproject-div-7}
---------------------------------------------------------------------

You can call the GetEditingProject operation to query details about an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/GetEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetEditingProjectRequest;
    import com.aliyuncs.vod.model.v20170321.GetEditingProjectResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            GetEditingProjectRequest request = new GetEditingProjectRequest();
            request.setProjectId("projectId");
    
            GetEditingProjectResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    if (response.getProject() ! = null){
                        System.out.println("Editing Project ID:" + response.getProject().getProjectId());
                        System.out.println("Editing Project Timeline:" + response.getProject().getTimeline());
                        System.out.println("Editing Project Title:" + response.getProject().getTitle());
                        System.out.println("Editing Project Description:" + response.getProject().getDescription());
                        System.out.println("Editing Project Cover URL:" + response.getProject().getCoverURL());
                        System.out.println("Editing Project Create Time:" + response.getProject().getCreationTime());
                        System.out.println("Editing Project Last Modified Time:" + response.getProject().getModifiedTime());
                        System.out.println("Editing Project Status:" + response.getProject().getStatus());
                    }
    
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }



Search for online editing projects {#h2--div-id-searcheditingproject-div-8}
---------------------------------------------------------------------------

You can call the SearchEditingProject operation to search for online editing projects.
For more information about the request and response parameters of this operation, see [SearchEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/SearchEditingProject.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SearchEditingProjectRequest;
    import com.aliyuncs.vod.model.v20170321.SearchEditingProjectResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            SearchEditingProjectRequest request = new SearchEditingProjectRequest();
            request.setTitle("Title Keywords");
            request.setStartTime("2017-01-11T12:00:00Z");
            request.setEndTime("2017-01-12T12:00:00Z");
            request.setPageSize(10);
            request.setPageNo(1);
    
            SearchEditingProjectResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    if (response.getProjectList() ! = null && response.getProjectList().size() > 0){
                        System.out.println("Total Size:" + response.getProjectList().size());
                        for (int i=0; i<response.getProjectList().size(); i++){
                            System.out.println("No " + i + " Editing Project");
    
                            SearchEditingProjectResponse.Project editingProject = response.getProjectList().get(i);
                            System.out.println("Editing Project ID:" + editingProject.getProjectId());
                            System.out.println("Editing Project Title:" + editingProject.getTitle());
                            System.out.println("Editing Project Description:" + editingProject.getDescription());
                            System.out.println("Editing Project Cover URL:" + editingProject.getCoverURL());
                            System.out.println("Editing Project Create Time:" + editingProject.getCreationTime());
                            System.out.println("Editing Project Last Modified Time:" + editingProject.getModifiedTime());
                            System.out.println("Editing Project Status:" + editingProject.getStatus());
                        }
                    }
    
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }



Configure materials for an online editing project {#h2--div-id-seteditingprojectmaterials-div-9}
------------------------------------------------------------------------------------------------

You can call the SetEditingProjectMaterials operation to configure materials for an online editing project.
For more information about the request and response parameters of this operation, see [SetEditingProjectMaterials](/intl.en-US/API Reference/Video editing/Editing Projects/SetEditingProjectMaterials.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SetEditingProjectMaterialsRequest;
    import com.aliyuncs.vod.model.v20170321.SetEditingProjectMaterialsResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKey ID>", "<Your AccessKey secret>");
    
            SetEditingProjectMaterialsRequest request = new SetEditingProjectMaterialsRequest();
            // Editing Project ID
            request.setProjectId("projectid");
            // Set Editing Project Material IDs, use comma to split
            request.setMaterialIds("materialId1,materialId2");
    
            SetEditingProjectMaterialsResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }



Query the materials of an online editing project {#h2--div-id-geteditingprojectmaterials-div-10}
------------------------------------------------------------------------------------------------

You can call the GetEditingProjectMaterials operation to query the materials of an online editing project.

For more information about the request and response parameters of this operation, see [GetEditingProjectMaterials](/intl.en-US/API Reference/Video editing/Editing Projects/GetEditingProject.md). Example:

    import com.aliyuncs.vod.model.v20170321.GetEditingProjectMaterialsRequest;
    import com.aliyuncs.vod.model.v20170321.GetEditingProjectMaterialsResponse;
    
        /**
         * Sample Code
         */
        public static void main(String[] args) throws Exception {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            GetEditingProjectMaterialsRequest request = new GetEditingProjectMaterialsRequest();
            request.setProjectId("projectid");
            request.setType("video");
    
            GetEditingProjectMaterialsResponse response = null;
            try {
                response = client.getAcsResponse(request);
                if (response ! = null){
                    if (response.getMaterialList() ! = null && response.getMaterialList().size() > 0){
                        for (int i=0; i<response.getMaterialList().size(); i++){
                            System.out.println("No " + i + " Material");
    
                            GetEditingProjectMaterialsResponse.Material material = response.getMaterialList().get(i);
                            System.out.println("Editing Project Material ID:" + material.getMaterialId());
                            System.out.println("Editing Project Material Title:" + material.getTitle());
                            System.out.println("Editing Project Material Category ID:" + material.getCateId());
                            System.out.println("Editing Project Material Category Name:" + material.getCateName());
                            System.out.println("Editing Project Material Tags:" + material.getTags());
                            System.out.println("Editing Project Material Cover URL:" + material.getCoverURL());
                            System.out.println("Editing Project Material Create Time:" + material.getCreationTime());
                            System.out.println("Editing Project Material Last Modified Time:" + material.getModifiedTime());
                        }
                    }
    
                    // Request ID
                    System.out.println("RequestId:" + response.getRequestId());
                }
            } catch (ServerException e){
                System.out.println("ServerError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (ClientException e){
                System.out.println("ClientError code:" + e.getErrCode() + ", message:" + e.getErrMsg());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
        }


