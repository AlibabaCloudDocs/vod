Naming rules for transcoded files 
======================================================

ApsaraVideo VOD provides default rules for naming transcoded files. The name of a transcoded file can be used as the relative path to the file. This topic describes the default rules for naming transcoded files and how to customize naming rules.

Definition of file names 
---------------------------------------------

Rules for naming transcoded files can contain mutable and immutable strings. Mutable strings are wildcards supported by ApsaraVideo VOD and can be dynamically replaced with corresponding values. Immutable strings cannot be replaced.
**Note**

This naming rule does not apply to output files in **HTTP Live Streaming (HLS)** and **Dynamic Adaptive Streaming over HTTP (DASH)** formats.

* Mutable strings

  Mutable strings are wildcards that can be dynamically replaced with corresponding values. When a transcoded file is generated from a video, ApsaraVideo VOD obtains corresponding values to replace wildcards in the names. ApsaraVideo VOD supports the following wildcards for naming video files:
  * `{MediaId}`: the ID of the video. The ID of each video must be unique, but the names of output files of the same video contain the same video ID. You can generate multiple transcoded streams from a video.

    
  
  * `{JobId}`: the ID of the transcoding job. The job ID must be globally unique to identify a transcoded file.

    
  
  * `{PlayDefinition}`: the resolution of the transcoded file. This parameter does not have to be unique.

    **Note**

    This filed is set to the value of the `Definition` parameter returned by the GetPlayInfo operation in **lower case** . For more information, see [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md).
    
  

  




<!-- -->

* Immutable strings

  Immutable strings indicate detailed business information. For example, the string "watermark" indicates that output files contain watermarks and "encrypt" indicates that source videos are encrypted. By default, ApsaraVideo VOD adds **encrypt-stream** to the names of output files after video encryption. You can also use custom immutable strings to indicate various business features.

  For example, `{MediaId}/{JobId}-watermark-sd` and `{MediaId}/encrypt-hd` contain the "watermark" and "encrypt" strings, which indicate that output files contain watermarks and that the source video is encrypted.
  




Uniqueness of file names 
---------------------------------------------

To prevent overwriting of transcoded files, the name of each transcoded file must be unique.

* For example, `{MediaId}/{JobId}` can ensure the uniqueness of each file name because the {JobId} string ensures global uniqueness.

  

* However, `{MediaId}/test` may lead to duplicated file names because it does not contain a string to ensure global uniqueness. If you apply this naming rule when you transcode a video into two MP4 files with different specifications, ApsaraVideo VOD sets the same name for the two transcoded files. As a result, the transcoded file that is generated later overwrites the transcoded file that is generated earlier.

  




Default rules 
----------------------------------

ApsaraVideo VOD provides the following rules for naming transcoded files.
**Note**

**Custom string** in the following naming rules is used to ensure that the name of each transcoded file is unique.

* Unencrypted output

  Rule:

      {MediaId}/[Custom string]-{PlayDefinition}

  

  Example:

      99f4f18c560c4f35459ef71tr/1b1196c767003c3dba0543055-40023f3f33e648df975f4dfc4c-sd

  




* Encrypted output

  Rule:

      {MediaId}/[Custom string]-{PlayDefinition}-encrypt-stream

  

  Example:

      99f4f18c560c4f35459ef71tr/1b1196c767003c3dba0543055-40023f3f33e648df975f4dfc4c-sd-encrypt-stream

  
  **Note**

  The **encrypt-stream** string indicates that the output file is generated after encryption and transcoding. This rule applies only to Alibaba Cloud proprietary cryptography and HLS encryption.
  




Custom rules 
---------------------------------

To play a video file, the media player must obtain the streaming URL. If you need to shorten the response time for video playback in specific scenarios, you can customize a naming rule that contains the parameters required to generate streaming URLs. For example, if you set a naming rule `{MediaId}/{PlayeDefinition}`, ApsaraVideo VOD generates streaming URLs based on `video IDs and resolutions`. In this case, you do not need to call an operation to query streaming URLs. ApsaraVideo VOD supports custom naming rules for transcoded files. When a transcoded file is generated, ApsaraVideo VOD names the file based on your custom rules.

### **Limits** 

* Custom naming rules for transcoded files support only specific wildcards, letters, digits, hyphens (-), and underscores (_). A rule must not exceed 128 characters in length.

  

* Custom naming rules for transcoded files must start with the wildcard **{MediaId}** to specify the source video. This prevents transcoded files of different videos from using the same name.

  

* ApsaraVideo VOD automatically adds a suffix to the names of transcoded files. If you set a rule to generate MP4 files with names in the **{MediaId}/{JobId}-watermark-{PlayDefinition}** format after transcoding, ApsaraVideo VOD adds the .mp4 suffix to the names of transcoded files.

  Example: `99f4f18c560c4f35459ef71tr/1b1196c767003c3dba0543055-watermark-sd.mp4`
  

* Make sure that your custom rules generate a unique name for each transcoded file to prevent files from being overwritten.

  




### **Configuration methods** 

You can use only the ApsaraVideo VOD API to customize a rule for naming transcoded files. For more information, see [AddTranscodeTemplateGroup](). For information about parameters of this operation, see the `TranscodeFileRegular` parameter of [TranscodeTemplate](/intl.en-US/API Reference/Appendix/Basic data types.md).

### **Configuration example** 

    public static JSONArray buildTranscodeTemplateList() {
            JSONObject transcodeTemplate = new JSONObject();
            // Customize a rule for naming transcoded files.
            transcodeTemplate.put("TranscodeFileRegular", "{MediaId}/{JobId}-{PlayDefinition}-watermark");
            // Specify the template name.
            transcodeTemplate.put("TemplateName", "testtemplate");
            // Specify the definition.
            transcodeTemplate.put("Definition", "LD");
            ......
            // Configure the video transcoding, audio transcoding, and output format settings.
            ......
            JSONArray transcodeTemplateList = new JSONArray();
            transcodeTemplateList.add(transcodeTemplate);
            return transcodeTemplateList;
        }



For more information, see [Transcoding templates](/intl.en-US/Server SDK Reference/SDK for Java/Transcoding template.md).

