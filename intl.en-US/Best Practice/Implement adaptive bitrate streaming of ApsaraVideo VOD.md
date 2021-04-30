# Implement adaptive bitrate streaming of ApsaraVideo VOD

You can package video streams in different bitrates with a file that contains the bitrate and resolution information of these video streams. This way, players can switch to the most appropriate video stream for playback based on the current network bandwidth condition. This process is called adaptive bitrate streaming.

**Note:** Two most widely used output formats of adaptive bitrate streaming are HTTP Live Streaming \(HLS\) and Dynamic Adaptive Streaming over HTTP \(DASH\). ApsaraVideo VOD supports only HLS adaptive bitrate streaming. For more information, see [Adaptive bitrate streaming](https://help.aliyun.com/document_detail/153422.html).

The following table describes the differences between an adaptive bitrate streaming template and a common transcoding template.

|Item|Adaptive bitrate streaming template|Common transcoding template|
|----|-----------------------------------|---------------------------|
|Configuration|Packaging parameters are required to specify the packaging type and bandwidth threshold.|Packaging parameters are not required.|
|Subtitling|Burnt subtitles and external subtitles are supported.|Only burnt subtitles are supported.|
|Playback|The most appropriate bitrate can be selected to play a video based on the network bandwidth condition.|Only the specified video stream can be played.|

## Notes

-   Adaptive bitrate streaming templates do not support HLS encryption.
-   The subtitle file and video mezzanine file must be stored in the same bucket in the same region.
-   Adaptive bitrate streaming templates support only subtitle files in the .vtt format. The Language parameter is used only to search for the subtitle file to be overridden. The subtitle language is not changed during the overriding. The overriding fails if the specified subtitle language does not exist.

## Procedure

1.  **Use the ApsaraVideo VOD API to create an adaptive bitrate streaming template.**

    This following sample code provides examples on how to configure a common transcoding template, an adaptive bitrate streaming template, and a subtitle package template. You can use the sample code as needed.

    ```
        /**
         * Sample code
         */
        public static void main(String[] args) throws ClientException {
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
            AddTranscodeTemplateGroupResponse response = new AddTranscodeTemplateGroupResponse();
            try {
                response = addTranscodeTemplateGroup(client);
                System.out.println("TranscodeTemplateGroupId = " + response.getTranscodeTemplateGroupId());
            } catch (Exception e) {
                System.out.println("ErrorMessage = " + e.getLocalizedMessage());
            }
            System.out.println("RequestId = " + response.getRequestId());
        }
    
        /**
         * Configure a transcoding template group.
         */
        public static AddTranscodeTemplateGroupResponse addTranscodeTemplateGroup(DefaultAcsClient client) throws Exception {
            AddTranscodeTemplateGroupRequest request = new AddTranscodeTemplateGroupRequest();
            request.setName("grouptest2");
            JSONArray transcodeTemplateList = new JSONArray();
            // Configure a common transcoding template.
            transcodeTemplateList.add(buildNormalTranscodeConfig());
            // Configure an adaptive bitrate streaming template.
            transcodeTemplateList.add(buildVideoPackageConfig());
            // Configure a subtitle package template.
            transcodeTemplateList.add(buildSubtitlePackageConfig());
            request.setTranscodeTemplateList(transcodeTemplateList.toJSONString());
            System.out.println("request = " + JSONObject.toJSONString(request));
            return client.getAcsResponse(request);
        }
    
        /**
         * Build configuration parameters for the transcoding templates that you want to add.
         *
         * @return
         */
        public static JSONObject buildNormalTranscodeConfig() {
            JSONObject transcodeTemplate = new JSONObject();
            // The type of the template. <Normal: common transcoding template; VideoPackage: adaptive bitrate streaming template; SubtitlePackage: subtitle package template>
            transcodeTemplate.put("Type","Normal");
            // The name of the template.
            transcodeTemplate.put("TemplateName", "Common transcoding template for MP4");
            // The resolution.
            transcodeTemplate.put("Definition", "HD");
            // The transcoding configuration for video streams.
            JSONObject video = new JSONObject();
            video.put("Width", 1280);
            //video.put("Height", 720);
            video.put("Bitrate", 1500);
            video.put("Fps", 25);
            //video.put("Remove", false);
            video.put("Codec", "H.264");
            video.put("Gop", "250");
            video.put("LongShortMode", false);
            transcodeTemplate.put("Video", video);
            // The transcoding configuration for audio streams.
            JSONObject audio = new JSONObject();
            audio.put("Codec", "AAC");
            audio.put("Bitrate", "64");
            audio.put("Channels", "2");
            audio.put("Samplerate", "32000");
            transcodeTemplate.put("Audio", audio);
            // The container.
            JSONObject container = new JSONObject();
            container.put("Format", "mp4");
            transcodeTemplate.put("Container", container);
            // The subtitle override configuration.
            JSONObject subtitleSetting = new JSONObject();
            JSONArray subtitleList = new JSONArray();
            JSONObject subtitle = new JSONObject();
            // The Object Storage Service (OSS) URL of the subtitle file. HTTPS URLs are not supported.
            subtitle.put("SubtitleUrl", "http://outin-8db8d2****3e1c9256.oss-cn-shanghai.aliyuncs.com/subtitle/3215879C9F724A43BC84C63BE2AA19AF****.srt");
            // The encoding format of the subtitle content. Valid values: auto, UTF-8, GBK, and BIG5. The value auto indicates automatic detection.
            subtitle.put("CharEncode", "UTF-8");
            subtitleList.add(subtitle);
            transcodeTemplate.put("SubtitleList", subtitleList);
            return transcodeTemplate;
        }
    
        /**
         * Configure video packaging parameters.
         *
         * @return
         */
        private static JSONObject buildVideoPackageConfig() {
            JSONObject transcodeTemplate = new JSONObject();
            // The type of the template. <Normal: common transcoding template; VideoPackage: adaptive bitrate streaming template; SubtitlePackage: subtitle package template>
            transcodeTemplate.put("Type","VideoPackage");
            // The name of the template.
            transcodeTemplate.put("TemplateName", "HLS LD package");
            // The resolution.
            transcodeTemplate.put("Definition", "LD");
            // The transcoding configuration for video streams.
            JSONObject video = new JSONObject();
            video.put("Width", 1280);
            //video.put("Height", 720);
            video.put("Bitrate", 1500);
            video.put("Fps", 25);
            //video.put("Remove", false);
            video.put("Codec", "H.264");
            video.put("Gop", "250");
            video.put("LongShortMode", false);
            transcodeTemplate.put("Video", video);
            // The transcoding configuration for audio streams.
            JSONObject audio = new JSONObject();
            audio.put("Codec", "AAC");
            audio.put("Bitrate", "64");
            audio.put("Channels", "2");
            audio.put("Samplerate", "32000");
            transcodeTemplate.put("Audio", audio);
            // The container.
            JSONObject container = new JSONObject();
            container.put("Format", "m3u8");
            transcodeTemplate.put("Container", container);
            // Set the container format to M3U8. The MuxConfig parameter is required.
            JSONObject muxConfig = new JSONObject();
            JSONObject segment = new JSONObject();
            segment.put("Duration", "10");// The unit is seconds.
            muxConfig.put("Segment", segment);
            transcodeTemplate.put("MuxConfig",muxConfig);
    
            // The package configuration.
            JSONObject packageSetting = new JSONObject();
            // The package type. Set the value to HLSPackage.
            packageSetting.put("PackageType","HLSPackage");
            JSONObject packageConfig = new JSONObject();
            packageConfig.put("BandWidth","500000");
            packageSetting.put("PackageConfig",packageConfig);
            transcodeTemplate.put("PackageSetting",packageSetting);
            return transcodeTemplate;
        }
    
        /**
         * Configure subtitle packaging parameters.
         *
         * @return
         */
        private static JSONObject buildSubtitlePackageConfig() {
            JSONObject transcodeTemplate = new JSONObject();
            // The type of the template. <Normal: common transcoding template; VideoPackage: adaptive bitrate streaming template; SubtitlePackage: subtitle package template>
            transcodeTemplate.put("Type","SubtitlePackage");
            // The name of the template.
            transcodeTemplate.put("TemplateName", "Multi-subtitle packaging");
            // The resolution.
            transcodeTemplate.put("Definition", "HD");
            // The transcoding configuration for video streams.
            JSONObject video = new JSONObject();
            video.put("Width", 1280);
            //video.put("Height", 720);
            video.put("Bitrate", 1500);
            video.put("Fps", 25);
            //video.put("Remove", false);
            video.put("Codec", "H.264");
            video.put("Gop", "250");
            video.put("LongShortMode", false);
            transcodeTemplate.put("Video", video);
            // The transcoding configuration for audio streams.
            JSONObject audio = new JSONObject();
            audio.put("Codec", "AAC");
            audio.put("Bitrate", "64");
            audio.put("Channels", "2");
            audio.put("Samplerate", "32000");
            transcodeTemplate.put("Audio", audio);
            // The container.
            JSONObject container = new JSONObject();
            container.put("Format", "m3u8");
            transcodeTemplate.put("Container", container);
            // Set the container format to M3U8. The MuxConfig parameter is required.
            JSONObject muxConfig = new JSONObject();
            JSONObject segment = new JSONObject();
            segment.put("Duration", "10");// The unit is seconds.
            muxConfig.put("Segment", segment);
            transcodeTemplate.put("MuxConfig",muxConfig);
    
            /*
            The OSS endpoint of the subtitle file. HTTPS URLs and domain names for CDN are not supported.
            Note: The subtitle file and video mezzanine file must be stored in the same bucket in the same region, such as cn-shanghai.
             */
            // The subtitle package template.
            JSONObject subtitlePackageConfig = new JSONObject();
            subtitlePackageConfig.put("Type","SubtitlePackage");
            // The configuration of subtitle packaging.
            JSONObject subtitlePackageSetting = new JSONObject();
            // The package type. Set the value to HLSPackage.
            subtitlePackageSetting.put("PackageType","HLSPackage");
            JSONArray subtitleExtractConfigs = new JSONArray();
            // Subtitle 1
            JSONObject subtitleExtractConfig = new JSONObject();
            JSONArray subtitleUrlList = new JSONArray();
            subtitleUrlList.add("http://outin-bfefbb9****e1c7426.oss-cn-shanghai.aliyuncs.com/subtitle/260447BA31D24F9E9E7752BF73F1319B****.vtt");
            subtitleExtractConfig.put("SubtitleUrlList",subtitleUrlList);
            subtitleExtractConfig.put("Language","cn");
            subtitleExtractConfig.put("Format","vtt");
            subtitleExtractConfig.put("Name","Chinese-test");
            // Subtitle 2
            JSONObject subtitleExtractConfig2 = new JSONObject();
            JSONArray subtitleUrlList2 = new JSONArray();
            subtitleUrlList2.add("http://outin-bfefbb9****3e1c7426.oss-cn-shanghai.aliyuncs.com/subtitle/661C67325E0543F0BB8CA7AAB756E6D8****.vtt");
            subtitleExtractConfig2.put("SubtitleUrlList",subtitleUrlList2);
            subtitleExtractConfig2.put("Language","en-US");
            subtitleExtractConfig2.put("Format","vtt");
            subtitleExtractConfig 2.put( "Name","English-test");
    
            subtitleExtractConfigs.add(subtitleExtractConfig);
            subtitleExtractConfigs.add(subtitleExtractConfig2);
            subtitlePackageSetting.put("SubtitleExtractConfigList",subtitleExtractConfigs);
            transcodeTemplate.put("PackageSetting",subtitlePackageSetting);
            return transcodeTemplate;
        }
    
        public static DefaultAcsClient initVodClient(String accessKeyId, String accessKeySecret) throws ClientException {
            // The access region of ApsaraVideo VOD.
            String regionId = "cn-shanghai";
            DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
            DefaultAcsClient client = new DefaultAcsClient(profile);
            return client;
        }
    ```

    **Note:**

    -   If you require only an adaptive bitrate streaming template, you do not need to create a common transcoding template.
    -   Adaptive bitrate streaming templates do not support HLS encryption. If you require HLS encryption, use a common transcoding template.
2.  **Use the ApsaraVideo VOD API to transcode a video into streams in multiple bitrates.**

    **Note:** Before you transcode a video, you must create an adaptive bitrate streaming template. For more information, see Step 1.

    ```
         public static void main(String[] args) {
           // Set the regionId parameter to the access region of ApsaraVideo VOD, such as cn-shanghai.
           String regionId = "cn-shanghai";
            DefaultProfile profile = DefaultProfile.getProfile(regionId, "<accessKeyId>", "<accessSecret>");
            IAcsClient client = new DefaultAcsClient(profile);
            String videoId = "76913816d****8e57e8c2952";
            String templateId = "4733b3a5****ae36ac22d34";
            try {
                SubmitTranscodeJobsResponse response = submitTranscodeJobs(client,videoId,templateId);
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
        }
        
        /**
         * Start a transcoding job.
         * Pass the video ID and transcoding group ID.
         *
         * @param client
         * @param videoId
         * @param templateGroupId
         * @return
         * @throws Exception
         */
        public static SubmitTranscodeJobsResponse submitTranscodeJobs(DefaultAcsClient client, String videoId, String templateGroupId) throws Exception {
            SubmitTranscodeJobsRequest request = new SubmitTranscodeJobsRequest();
            // Set the ID of the video to be transcoded.
            request.setVideoId(videoId);
            // Set the ID of the transcoding template group.
            request.setTemplateGroupId(templateGroupId);
            // Set the transcoding priority. The default value is 6. A larger value indicates a higher priority. The value ranges from 1 to 10.
            request.setPriority("8");
            JSONObject overrideParams = buildOverrideParams();
            // Set the overrideParams parameter.
            request.setOverrideParams(overrideParams.toJSONString());
            return client.getAcsResponse(request);
        }
    
        // The following code provides an example on how to build the overrideParams parameter.
        public static JSONObject buildOverrideParams() {
            JSONObject overrideParams = new JSONObject();
            // Configure subtitle overriding.
            JSONObject packageSubtitleSetting = new JSONObject();
            JSONArray packageSubtitleList = new JSONArray();
            JSONObject packageSubtitle = new JSONObject();
          // The ID of the subtitle template in the template group that is used for subtitle overriding.
            packageSubtitle.put("SubtitlePackageTemplateId", "69fa6ee58****e8492c76168****");
          // The Language parameter is only used to search for the subtitle file to be overridden. The subtitle language is not changed during the overriding. The overriding fails if the specified subtitle language does not exist.
            packageSubtitle.put("Language", "cn");
            // The OSS endpoint of the subtitle file. HTTPS URLs are not supported. The subtitle file and video mezzanine file must be stored in the same region.
            packageSubtitle.put("SubtitleUrl", "http://outin-bfefbb9****3e1c7426.oss-cn-shanghai.aliyuncs.com/subtitle/043956117D0C475EAB0CE8C4F7294221****.vtt");
            packageSubtitleList.add(packageSubtitle);
            packageSubtitleSetting.put("PackageSubtitleList", packageSubtitleList);
            overrideParams.put("PackageSubtitleSetting", packageSubtitleSetting);
            return overrideParams;
        }
    ```

3.  **View the processing effects.**
    -   The following figure shows the video streams that are generated after adaptive bitrate streaming is implemented. In this example, three transcoded streams and one adaptive bitrate stream are generated.

        ![Effect display 1](../images/p180161.png)

    -   The following figure shows the effect of playing the adaptive bitrate stream.

        ![Effect display 2](../images/p180162.png)


