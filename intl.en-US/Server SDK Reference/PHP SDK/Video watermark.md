Video watermark 
====================================

This topic provides examples on how to use the API operations of the video watermark module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to create, modify, delete, and query watermarks. You can also specify a watermark as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Create a watermark {#h2--div-id-addwatermark-div-2}
---------------------------------------------------

You can call the AddWatermark operation to create a watermark.

For more information about the request and response parameters of this operation, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video watermark/AddWatermark.md). Example:

    /**
     * Build the parameters of an image watermark. Configure the parameters as required.
     * @return
     */
    function buildImageWatermarkConfig() {
        $watermarkConfig = array();
        // The horizontal offset of the watermark on the output video.
        $watermarkConfig["Dx"] = "8";
        // The vertical offset of the watermark on the output video.
        $watermarkConfig["Dy"] = "8";
        // The width of the watermark on the output video.
        $watermarkConfig["Width"] = "55";
        // The height of the watermark on the output video.
        $watermarkConfig["Height"] = "55";
        // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
        $watermarkConfig["ReferPos"] = "BottomRight";
    
        // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
        $timeline = array();
        // The start time for the watermark display.
        $timeline["Start"] = "2";
        // The duration for the watermark display.
        $timeline["Duration"] = "ToEND";
        $watermarkConfig["Timeline"] = $timeline;
    
        return json_encode($watermarkConfig);
    }
    
    /**
     * Build the parameters of a text watermark. Configure the parameters as required.
     * @return
     */
    function buildTextWatermarkConfig() {
        $watermarkConfig = array();
        // The text to use as the watermark.
        $watermarkConfig["Content"] = "testwatermark";
        // The font to use for the watermark.
        $watermarkConfig["FontName"] = "SimSun";
        // The font size to use for the watermark.
        $watermarkConfig["FontSize"] = "25";
        // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
        $watermarkConfig["FontColor"] = "Black";
        // The transparency to use for the watermark.
        $watermarkConfig["FontAlpha"] = "0.2";
        // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
        $watermarkConfig["BorderColor"] = "White";
        // The stroke width to use for the watermark.
        $watermarkConfig["BorderWidth"] = "1";
        // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
        $watermarkConfig["Top"] = "20";
        // The distance between the upper-left vertex of the watermark and the left edge of the output video.
        $watermarkConfig["Left"] = "15";
    
        return json_encode($watermarkConfig);
    }
    
    /**
     * Create a watermark.
     */
    function addWatermark($client) {
        $request = new vod\AddWatermarkRequest();
        // The name of the watermark.
        $request->setName("addwatermark");
    
        // The URL of the watermark file that is stored in an OSS bucket.
        // If you want to create an image watermark, you must specify the URL of the watermark file. The OSS bucket that stores the watermark file must reside in the same region as the region where the video is stored. For example, if a video is stored in the China (Shanghai) region, it can use only a watermark file that is stored in the same region.
        $request->setFileUrl("http://192.168.0.0/16/watermark/test.png");
    
        // Watermark configurations
        // The position of the image watermark.
        $request->setWatermarkConfig(buildImageWatermarkConfig());
        // The position of the text watermark.
        //$request->setWatermarkConfig(buildTextWatermarkConfig());
    
        // The type of the watermark. Set the value to Text for text watermarks and Image for image watermarks.
        $request->setType("Image");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     * @param args
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = addWatermark($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify a watermark {#h2--div-id-updatewatermark-div-3}
------------------------------------------------------

You can call the UpdateWatermark operation to modify a watermark.
For more information about the request and response parameters of this operation, see [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video watermark/UpdateWatermark.md). Example: {#h2--div-id-updatewatermark-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Build the parameters of an image watermark. Configure the parameters as required.
     * @return
     */
    function buildImageWatermarkConfig() {
        $watermarkConfig = array();
        // The horizontal offset of the watermark on the output video.
        $watermarkConfig["Dx"] = "10";
        // The vertical offset of the watermark on the output video.
        $watermarkConfig["Dy"] = "10";
        // The width of the watermark on the output video.
        $watermarkConfig["Width"] = "66";
        // The height of the watermark on the output video.
        $watermarkConfig["Height"] = "66";
        // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
        $watermarkConfig["ReferPos"] = "BottomRight";
    
        // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
        $timeline = array();
        // The start time for the watermark display.
        $timeline["Start"] = "2";
        // The duration for the watermark display.
        $timeline["Duration"] = "ToEND";
        $watermarkConfig["Timeline"] = $timeline;
    
        return json_encode($watermarkConfig);
    }
    
    /**
     * Build the parameters of a text watermark. Configure the parameters as required.
     * @return
     */
    function buildTextWatermarkConfig() {
        $watermarkConfig = array();
        // The text to use as the watermark.
        $watermarkConfig["Content"] = "testwatermark";
        // The font to use for the watermark.
        $watermarkConfig["FontName"] = "SimSun";
        // The font size to use for the watermark.
        $watermarkConfig["FontSize"] = "40";
        // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
        $watermarkConfig["FontColor"] = "Black";
        // The transparency to use for the watermark.
        $watermarkConfig["FontAlpha"] = "0.2";
        // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
        $watermarkConfig["BorderColor"] = "White";
        // The stroke width to use for the watermark.
        $watermarkConfig["BorderWidth"] = "2";
        // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
        $watermarkConfig["Top"] = "20";
        // The distance between the upper-left vertex of the watermark and the left edge of the output video.
        $watermarkConfig["Left"] = "15";
    
        return json_encode($watermarkConfig);
    }
    
    /**
     * Call example
     * @param args
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = updateWatermark($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete a watermark {#h2--div-id-deletewatermark-div-4}
------------------------------------------------------

You can call the DeleteWatermark operation to delete a watermark.
For more information about the request and response parameters of this operation, see [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video watermark/DeleteWatermark.md). Example: {#h2--div-id-deletewatermark-div-4}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Delete a watermark.
     */
    function deleteWatermark($client) {
        $request = new vod\DeleteWatermarkRequest();
        // The ID of the watermark.
        $request->setWatermarkId("e7d983370268092176588a2c452****");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     * @param args
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = deleteWatermark($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query watermarks {#h2--div-id-listwatermark-div-5}
--------------------------------------------------

You can call the ListWatermark operation to query watermarks.
For more information about the request and response parameters of this operation, see [ListWatermark](/intl.en-US/API Reference/Media processing/Video watermark/ListWatermark.md). Example: {#h2--div-id-listwatermark-div-5}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query watermarks.
     */
    function listWatermark($client) {
        $request = new vod\ListWatermarkRequest();
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     * @param args
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = listWatermark($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query a watermark {#h2--div-id-getwatermark-div-6}
--------------------------------------------------

You can call the GetWatermark operation to query details about a watermark.
For more information about the request and response parameters of this operation, see [GetWatermark](/intl.en-US/API Reference/Media processing/Video watermark/GetWatermark.md). Example: {#h2--div-id-getwatermark-div-6}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query a watermark.
     */
    function getWatermark($client) {
        $request = new vod\GetWatermarkRequest();
        // The ID of the watermark.
        $request->setWatermarkId("bfc084674fb64486b6e5bace3052****");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     * @param args
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = getWatermark($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Specify a watermark as the default one {#h2--div-id-setdefaultwatermark-div-7}
------------------------------------------------------------------------------

You can call the SetDefaultWatermark operation to specify a watermark as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video watermark/SetDefaultWatermark.md). Example: {#h2--div-id-setdefaultwatermark-div-7}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Specify a watermark as the default one.
     */
    function setDefaultWatermark($client) {
        $request = new vod\SetDefaultWatermarkRequest();
        // The ID of the watermark.
        $request->setWatermarkId("bfc084674fb64486b6e5bace3052****");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     * @param args
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = setDefaultWatermark($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


