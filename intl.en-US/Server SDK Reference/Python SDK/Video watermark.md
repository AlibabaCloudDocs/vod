Video watermark 
====================================

This topic provides examples on how to use the API operations of the video watermark module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to create, modify, delete, and query watermarks. You can also specify a watermark as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Create a watermark {#h2--div-id-addwatermark-div-2}
---------------------------------------------------

You can call the AddWatermark operation to create a watermark.
For more information about the request and response parameters of this operation, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video watermark/AddWatermark.md). Example:
**Note**
* For more information about how to obtain the upload URL and credential, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).


* For more information about how to upload a watermark file to an Object Storage Service (OSS), see [OSS Upload](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).


 {#h2--div-id-addwatermark-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import AddWatermarkRequest
    def add_watermark(clt):
        request = AddWatermarkRequest.AddWatermarkRequest()
    
        request.set_Name('watermark-sample')
        # If you want to create an image watermark, you must specify the URL of the watermark file. The OSS bucket that stores the watermark file must reside in the same region as the region where the video is stored. For example, if a video is stored in the China (Shanghai) region, it can use only a watermark file that is stored in the same region.
        request.set_FileUrl('http://sample.oss-cn-shanghai.aliyuncs.com/watermark/test.png')
    
        # Example on how to configure a text watermark:
        request.set_Type('Text')
        # Specify the content, font, font size, color, transparency, and other configurations of the text watermark.
        watermarkConfig = {'Content': 'watermark Text', 'FontName': 'SimSun', 'FontSize': 25, 'FontColor': 'Black',
                           'FontAlpha': 0.2, 'BorderColor': 'White', 'BorderWidth': 1, 'Top': 20, 'Left': 15}
        request.set_WatermarkConfig(json.dumps(watermarkConfig))
    
        """
        # Example on how to configure an image watermark:
        request.set_Type('Image')
        # The start time and duration for the watermark display.
        timeline = {'Start': 2, 'Duration': 'ToEND'}
        # The position configurations of a text watermark.
        watermarkConfig = {'Dx': 8, 'Dy': 8, 'Width': 55, 'Height': 55, 'ReferPos': 'BottomRight', 'Timeline': timeline}
        request.set_WatermarkConfig(json.dumps(watermarkConfig))
        """
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        watermark = add_watermark(clt)
        print(json.dumps(watermark, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify a watermark {#h2--div-id-updatewatermark-div-3}
------------------------------------------------------

You can call the UpdateWatermark operation to modify a watermark.
For more information about the request and response parameters of this operation, see [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video watermark/UpdateWatermark.md). Example:
**Notice**
You cannot modify the URL of an image watermark file by calling this operation. If you want to modify the URL, create another watermark. {#h2--div-id-updatewatermark-div-3}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateWatermarkRequest
    def update_watermark(clt):
        request = UpdateWatermarkRequest.UpdateWatermarkRequest()
        request.set_WatermarkId('<watermarkId>')
        request.set_Name('new-watermark-name')
    
        # Example on how to modify a text watermark:
        # The watermark configurations, including the text, font, font size, font color, and transparency to use for the watermark.
        watermarkConfig = {'Content': 'watermark Text', 'FontName': 'SimSun', 'FontSize': 25, 'FontColor': 'Black',
                           'FontAlpha': 0.2, 'BorderColor': 'White', 'BorderWidth': 1, 'Top': 20, 'Left': 15}
        request.set_WatermarkConfig(json.dumps(watermarkConfig))
    
        """
        # Example on how to configure an image watermark:
        # The start time and duration for the watermark display.
        timeline = {'Start': 2, 'Duration': 'ToEND'}
        # The position configurations of an image watermark.
        watermarkConfig = {'Dx': 8, 'Dy': 8, 'Width': 55, 'Height': 55, 'ReferPos': 'BottomRight', 'Timeline': timeline}
        request.set_WatermarkConfig(json.dumps(watermarkConfig))
        """
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        watermark = update_watermark(clt)
        print(json.dumps(watermark, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete a watermark {#h2--div-id-deletewatermark-div-4}
------------------------------------------------------

You can call the DeleteWatermark operation to delete a watermark.
For more information about the request and response parameters of this operation, see [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video watermark/DeleteWatermark.md). Example: {#h2--div-id-deletewatermark-div-4}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteWatermarkRequest
    def delete_watermark(clt):
        request = DeleteWatermarkRequest.DeleteWatermarkRequest()
        request.set_WatermarkId('<watermarkId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = delete_watermark(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query watermarks {#h2--div-id-listwatermark-div-5}
--------------------------------------------------

You can call the ListWatermark operation to query watermarks.
For more information about the request and response parameters of this operation, see [ListWatermark](/intl.en-US/API Reference/Media processing/Video watermark/ListWatermark.md). Example: {#h2--div-id-listwatermark-div-5}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import ListWatermarkRequest
    def list_watermark(clt):
        request = ListWatermarkRequest.ListWatermarkRequest()
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        watermarks = list_watermark(clt)
        print(watermarks['WatermarkInfos'])
        print(json.dumps(watermarks, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query a watermark {#h2--div-id-getwatermark-div-6}
--------------------------------------------------

You can call the GetWatermark operation to query a watermark.
For more information about the request and response parameters of this operation, see [GetWatermark](/intl.en-US/API Reference/Media processing/Video watermark/GetWatermark.md). Example: {#h2--div-id-getwatermark-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetWatermarkRequest
    def get_watermark(clt):
        request = GetWatermarkRequest.GetWatermarkRequest()
        request.set_WatermarkId('<watermarkId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        watermark = get_watermark(clt)
        print(watermark['WatermarkInfo'])
        print(json.dumps(watermark, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Specify a watermark as the default one {#h2--div-id-setdefaultwatermark-div-7}
------------------------------------------------------------------------------

You can call the SetDefaultWatermark operation to specify a watermark as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video watermark/SetDefaultWatermark.md). Example: {#h2--div-id-setdefaultwatermark-div-7}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import SetDefaultWatermarkRequest
    def set_default_watermark(clt):
        request = SetDefaultWatermarkRequest.SetDefaultWatermarkRequest()
        request.set_WatermarkId('<watermarkId>')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = set_default_watermark(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


