Video watermark 
====================================

This topic provides examples on how to use the API operations of the video watermark module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to create, modify, delete, and query watermarks. 

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md). 

Create a watermark {#h2--div-id-addwatermark-div-2}
---------------------------------------------------

You can call the AddWatermark operation to create a watermark. 

For more information about the request and response parameters of this operation, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video watermark/AddWatermark.md). Sample code:
**Note**



* For more information about how to query the upload URL and credential, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).

  

* For more information about how to upload a watermark file to an Object Storage Service (OSS) bucket, see [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).

  




    import com.aliyuncs.vod.model.v20170321.AddWatermarkRequest; import com.aliyuncs.vod.model.v20170321.AddWatermarkResponse; /** * Create a watermark. */ public static AddWatermarkResponse addWatermark(DefaultAcsClient client) throws Exception { AddWatermarkRequest request = new AddWatermarkRequest(); // The name of the watermark. request.setName("addwatermark"); // The URL of the watermark file that is stored in an OSS bucket. String fileUrl = "http://test-bucket.oss-cn-shanghai.aliyuncs.com/watermark/test.png"; // If you want to create an image watermark, you must specify the URL of the watermark file. The OSS bucket that stores the watermark file must reside in the same region as the region where the video is stored. For example, if a video is stored in the China (Shanghai) region, the video can use only a watermark file that is stored in the same region. request.setFileUrl(fileUrl); // The configurations of the watermark. JSONObject watermarkConfig = null; // The position configurations of an image watermark. watermarkConfig = buildImageWatermarkConfig(); // The position configurations of a text watermark. //watermarkConfig = buildTextWatermarkConfig(); request.setWatermarkConfig(watermarkConfig.toJSONString()); // The type of the watermark. Set the value to Text for text watermarks and Image for image watermarks. request.setType("Image"); return client.getAcsResponse(request); } /** * Call example * @param args * @throws ClientException */ public static void main(String[] args) throws ClientException { DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); AddWatermarkResponse response = new AddWatermarkResponse(); try { // Create a watermark. response = addWatermark(client); // The ID of the watermark. System.out.println("WatermarkId = " + response.getWatermarkInfo().getWatermarkId()); // The position and effect configurations of the watermark. System.out.println("WatermarkConfig = " + response.getWatermarkInfo().getWatermarkConfig()); // The URL of the watermark file. If you want to create a text watermark, leave this parameter empty. System.out.println("FileUrl = " + response.getWatermarkInfo().getFileUrl()); } catch (Exception e) { System.out.println("ErrorMessage = " + e.getLocalizedMessage()); } System.out.println("RequestId = " + response.getRequestId()); } /** * Build the parameters of an image watermark. Configure the parameters as required. * @return */ public static JSONObject buildImageWatermarkConfig() { JSONObject watermarkConfig = new JSONObject(); // The horizontal offset of the watermark on the output video. watermarkConfig.put("Dx", "8"); // The vertical offset of the watermark on the output video. watermarkConfig.put("Dy", "8"); // The width of the watermark on the output video. watermarkConfig.put("Width", "55"); // The height of the watermark on the output video. watermarkConfig.put("Height", "55"); // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner. watermarkConfig.put("ReferPos", "BottomRight"); // The timeline of the watermark display. You can specify the start time and duration for the watermark display. JSONObject timeline = new JSONObject(); // The start time for the watermark display. timeline.put("Start", "2"); // The duration for the watermark display. timeline.put("Duration", "ToEND"); watermarkConfig.put("Timeline", timeline); return watermarkConfig; } /** * Build the parameters of a text watermark. Configure the parameters as required. * @return */ public static JSONObject buildTextWatermarkConfig() { JSONObject watermarkConfig = new JSONObject(); // The text to use as the watermark. watermarkConfig.put("Content", "testwatermark"); // The font to use for the watermark. watermarkConfig.put("FontName", "SimSun"); // The font size to use for the watermark. watermarkConfig.put("FontSize", 25); // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000. watermarkConfig.put("FontColor", "Black"); // The transparency to use for the watermark. watermarkConfig.put("FontAlpha", "0.2"); // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff. watermarkConfig.put("BorderColor", "White"); // The stroke width to use for the watermark. watermarkConfig.put("BorderWidth", 1); // The distance between the upper-left vertex of the watermark and the upper edge of the output video. watermarkConfig.put("Top", 20); // The distance between the upper-left vertex of the watermark and the left edge of the output video. watermarkConfig.put("Left", 15); return watermarkConfig; }



Modify a watermark {#h2--div-id-updatewatermark-div-3}
------------------------------------------------------

You can call the UpdateWatermark operation to modify a watermark. 

For more information about the request and response parameters of this operation, see [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video watermark/UpdateWatermark.md). Sample code:

    import com.aliyuncs.vod.model.v20170321.UpdateWatermarkRequest; import com.aliyuncs.vod.model.v20170321.UpdateWatermarkResponse; /** * Modify a watermark. * Note: The file URL of an image watermark cannot be modified. If you want to modify the URL, you must create another image watermark. */ public static UpdateWatermarkResponse updateWatermark(DefaultAcsClient client) throws Exception { UpdateWatermarkRequest request = new UpdateWatermarkRequest(); request.setName("updatewatermark"); // The ID of the watermark for which you want to modify the configurations. request.setWatermarkId("421ddddd4f6e734a526fd2****"); // The configurations of the watermark. JSONObject watermarkConfig = null; // The position configurations of an image watermark. //watermarkConfig = buildImageWatermarkConfig(); // The position configurations of a text watermark. watermarkConfig = buildTextWatermarkConfig(); request.setWatermarkConfig(watermarkConfig.toJSONString()); return client.getAcsResponse(request); } /** * Call example */ public static void main(String[] args) { DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); UpdateWatermarkResponse response = new UpdateWatermarkResponse(); try { response = updateWatermark(client); // The ID of the watermark. System.out.println("WatermarkId = " + response.getWatermarkInfo().getWatermarkId()); // The position and effect configurations of the watermark. System.out.println("WatermarkConfig = " + response.getWatermarkInfo().getWatermarkConfig()); // The URL of the watermark file. If you want to modify a text watermark, leave this parameter empty. System.out.println("FileUrl = " + response.getWatermarkInfo().getFileUrl()); } catch (Exception e) { System.out.println("ErrorMessage = " + e.getLocalizedMessage()); } System.out.println("RequestId = " + response.getRequestId()); } /** * Build the parameters of an image watermark. Configure the parameters as required. * @return */ public static JSONObject buildImageWatermarkConfig() { JSONObject watermarkConfig = new JSONObject(); // The horizontal offset of the watermark on the output video. watermarkConfig.put("Dx", "10"); // The vertical offset of the watermark on the output video. watermarkConfig.put("Dy", "10"); // The width of the watermark on the output video. watermarkConfig.put("Width", "66"); // The height of the watermark on the output video. watermarkConfig.put("Height", "66"); // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner. watermarkConfig.put("ReferPos", "BottomLeft"); // The timeline of the watermark display. You can specify the start time and duration for the watermark display. JSONObject timeline = new JSONObject(); // The start time for the watermark display. timeline.put("Start", "2"); // The duration for the watermark display. timeline.put("Duration", "ToEND"); watermarkConfig.put("Timeline", timeline); return watermarkConfig; } /** * Build the parameters of a text watermark. Configure the parameters as required. * @return */ public static JSONObject buildTextWatermarkConfig() { JSONObject watermarkConfig = new JSONObject(); // The text to use as the watermark. watermarkConfig.put("Content", "testwatermark"); // The font to use for the watermark. watermarkConfig.put("FontName", "SimSun"); // The font size to use for the watermark. watermarkConfig.put("FontSize", 40); // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000. watermarkConfig.put("FontColor", "Black"); // The transparency to use for the watermark. watermarkConfig.put("FontAlpha", "0.2"); // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff. watermarkConfig.put("BorderColor", "White"); // The stroke width to use for the watermark. watermarkConfig.put("BorderWidth", 2); // The distance between the upper-left vertex of the watermark and the upper edge of the output video. watermarkConfig.put("Top", 20); // The distance between the upper-left vertex of the watermark and the left edge of the output video. watermarkConfig.put("Left", 15); return watermarkConfig; }



Delete a watermark {#h2--div-id-deletewatermark-div-4}
------------------------------------------------------

You can call the DeleteWatermark operation to delete a watermark. 

For more information about the request and response parameters of this operation, see [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video watermark/DeleteWatermark.md). Sample code:

    import com.aliyuncs.vod.model.v20170321.DeleteWatermarkRequest; import com.aliyuncs.vod.model.v20170321.DeleteWatermarkResponse; /** *Delete a watermark. */ public static DeleteWatermarkResponse deleteWatermark(DefaultAcsClient client) throws Exception { DeleteWatermarkRequest request = new DeleteWatermarkRequest(); request.setWatermarkId("53f9d796fad9d7b862b2e****"); return client.getAcsResponse(request); } /** * Call example */ public static void main(String[] args) { DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); DeleteWatermarkResponse response = new DeleteWatermarkResponse(); try { response = deleteWatermark(client); } catch (Exception e) { System.out.println("ErrorMessage = " + e.getLocalizedMessage()); } System.out.println("RequestId = " + response.getRequestId()); }



Query multiple watermarks {#h2--div-id-listwatermark-div-5}
-----------------------------------------------------------

You can call the ListWatermark operation to query multiple watermarks. 

For more information about the request and response parameters of this operation, see [ListWatermark](/intl.en-US/API Reference/Media processing/Video watermark/ListWatermark.md). Sample code:

    import com.aliyuncs.vod.model.v20170321.ListWatermarkRequest; import com.aliyuncs.vod.model.v20170321.ListWatermarkResponse; /** * Query multiple watermarks. */ public static ListWatermarkResponse listWatermark(DefaultAcsClient client) throws Exception { ListWatermarkRequest request = new ListWatermarkRequest(); return client.getAcsResponse(request); } /** * Call example */ public static void main(String[] args) { DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); ListWatermarkResponse response = new ListWatermarkResponse(); try { response = listWatermark(client); for (ListWatermarkResponse.WatermarkInfo watermarkInfo : response.getWatermarkInfos()) { // The ID of the watermark. System.out.println("WatermarkId = " + watermarkInfo.getWatermarkId()); // The position and effect configurations of the watermark. System.out.println("WatermarkConfig = " + watermarkInfo.getWatermarkConfig()); // The URL of the watermark file. If you want to query text watermarks, leave this parameter empty. System.out.println("FileUrl = " + watermarkInfo.getFileUrl()); } } catch (Exception e) { System.out.println("ErrorMessage = " + e.getLocalizedMessage()); } System.out.println("RequestId = " + response.getRequestId()); }



Query a single watermark {#h2--div-id-getwatermark-div-6}
---------------------------------------------------------

You can call the GetWatermark operation to query the details about a single watermark. 

For more information about the request and response parameters of this operation, see [GetWatermark](/intl.en-US/API Reference/Media processing/Video watermark/GetWatermark.md). Sample code:

    import com.aliyuncs.vod.model.v20170321.GetWatermarkRequest; import com.aliyuncs.vod.model.v20170321.GetWatermarkResponse; /** * Query a single watermark. */ public static GetWatermarkResponse getWatermark(DefaultAcsClient client) throws Exception { GetWatermarkRequest request = new GetWatermarkRequest(); // The ID of the watermark that you want to query. request.setWatermarkId("96d4f6e734a526fd2****"); return client.getAcsResponse(request); } /** * Call example */ public static void main(String[] args) { DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); GetWatermarkResponse response = new GetWatermarkResponse(); try { response = getWatermark(client); // The ID of the watermark. System.out.println("WatermarkId = " + response.getWatermarkInfo().getWatermarkId()); // The position and effect configurations of the watermark. System.out.println("WatermarkConfig = " + response.getWatermarkInfo().getWatermarkConfig()); // The URL of the watermark file. If you want to query a text watermark, leave this parameter empty. System.out.println("FileUrl = " + response.getWatermarkInfo().getFileUrl()); } catch (Exception e) { System.out.println("ErrorMessage = " + e.getLocalizedMessage()); } System.out.println("RequestId = " + response.getRequestId()); }



Specify a watermark as the default one {#h2--div-id-setdefaultwatermark-div-7}
------------------------------------------------------------------------------

You can call the SetDefaultWatermark operation to specify a watermark as the default one. 

For more information about the request and response parameters of this operation, see [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video watermark/SetDefaultWatermark.md). Sample code:

    import com.aliyuncs.vod.model.v20170321.SetDefaultWatermarkRequest; import com.aliyuncs.vod.model.v20170321.SetDefaultWatermarkResponse; /** * Specify a watermark as the default one. */ public static SetDefaultWatermarkResponse setDefaultWatermark(DefaultAcsClient client) throws Exception { SetDefaultWatermarkRequest request = new SetDefaultWatermarkRequest(); // The ID of the default watermark. request.setWatermarkId("82105a29c6e96d4f6****"); return client.getAcsResponse(request); } /** * Call example */ public static void main(String[] args) { DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); SetDefaultWatermarkResponse response = new SetDefaultWatermarkResponse(); try { response = setDefaultWatermark(client); } catch (Exception e) { System.out.println("ErrorMessage = " + e.getLocalizedMessage()); } System.out.println("RequestId = " + response.getRequestId()); }


