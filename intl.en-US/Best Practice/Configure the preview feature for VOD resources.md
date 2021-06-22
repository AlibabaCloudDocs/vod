# Configure the preview feature for VOD resources

ApsaraVideo VOD provides a complete preview solution. You can specify whether to allow users to preview a specified duration of a video or view the complete video. ApsaraVideo VOD provides streaming URLs that contain the specified preview duration to limit video playback.

## Prerequisites

The preview solution adopts the following basic principle: The Content Delivery Network \(CDN\) URL that is used to play a specific video contains the specified preview duration for the video. When a request to play the video is received, Alibaba Cloud CDN authenticates the request. If the request passes the authentication, Alibaba Cloud CDN returns the specified content for preview. Otherwise, Alibaba Cloud CDN rejects the request and returns status code 403.

-   A domain name for CDN is configured in the ApsaraVideo VOD console. The preview feature is implemented on top of Alibaba Cloud CDN.
-   The authentication type A for URL signing is enabled. To prevent the preview duration from being tampered with, the preview duration is included in the calculation result of the auth\_key field.
-   The object chunking and video seeking features are enabled for the domain name. For more information, see [Configure object chunking](/intl.en-US/User Guide/Domain management/Video-related settings/Configure object chunking.md) and [Video seeking](/intl.en-US/User Guide/Domain management/Video-related settings/Video seeking.md).

## Procedure

![Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8843815161/p185004.png)

1.  Set the preview feature.

    1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).
    2.  In the left-side navigation pane, find **Configuration Management**.
    3.  Choose **CDN Configuration** \> **Domain Names**. The Domain Names page appears.
    4.  Find the domain name that you want to configure and click **Configure**.
    5.  Click **Resource Access Control**.
    6.  Click the **URL Authentication** tab. On the URL Authentication tab, click **Modify**.
    7.  In the URL Authentication dialog box, turn on **URL Authentication** and **Support Previewing**, set the parameters as required, and then click **OK**.
    For more information, see [Configure URL signing](/intl.en-US/User Guide/Domain management/Access control/Configure URL signing.md).

    **Note:** If the preview feature is disabled for the domain name, do not include the preview duration in your request for video playback. Otherwise, a streaming URL that you cannot access is returned.

2.  Send a preview request.

    Send a request to ApsaraVideo VOD for video playback. In the request, set the preview duration. For more information, see the "[Methods for obtaining preview URLs](#section_986_kf2_9ry)" section of this topic.

3.  Obtain the preview URL.
4.  Use the preview URL to access Alibaba Cloud CDN. Then, Alibaba Cloud CDN returns the specified content for preview.

## Methods for obtaining preview URLs

**Use the ApsaraVideo VOD API**

**Note:**

-   To use the preview feature, make sure that a domain name for CDN is configured.
-   If the preview feature is disabled for the domain name, do not include the preview duration in your request for video playback. Otherwise, a streaming URL that you cannot access is returned.
-   ApsaraVideo VOD supports the preview of MP4 and M3U8 files.
-   The preview duration is determined based on keyframes. Therefore, we recommend that you do not apply the preview feature to short videos. For long videos, we recommend that you set the preview duration to at least 30 seconds. The default keyframe interval of transcoded files is 10 seconds. You can modify the keyframe interval in transcoding templates.
-   The preview granularity of M3U8 files is the duration of each TS segment. If the specified preview duration is not an integral multiple of the TS segment duration, the preview duration is extended. For example, if the TS segment duration is 10 seconds and the preview duration is 15 seconds, Alibaba Cloud CDN returns the specified content of 20 seconds for preview.

You can set the preview duration in the `PreviewTime` parameter of [PlayConfig](/intl.en-US/API Reference/Appendix/Request parameters.md) when you call the [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) operation. The following code provides an example:

```
package com.ali.vod.test;

import com.alibaba.fastjson.JSONObject;
import com.aliyun.oss.ClientException;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.vod.model.v20170321.GetPlayInfoRequest;
import com.aliyuncs.vod.model.v20170321.GetPlayInfoResponse;

/**
 * @author wb-zzb
 * @date 2020/6/3
 */
public class VodPreviewTest {
    public static void main(String[] args) {
        // Select a region of ApsaraVideo VOD. For more information, see [VOD centers and access domains](https://help.aliyun.com/document_detail/98194.html?spm=a2c4g.11186623.6.612.51c6534bqLs9Wd).
        String regionId = "cn-shanghai";
        String accessKeyId = "<your accessKeyId>";
        String accessKeySecret = "<your accessKeySecret>";
        String videoId = "595d020bad3*****f37433451720";
        DefaultAcsClient client = InitVodClient(regionId, accessKeyId, accessKeySecret);
        GetPlayInfoResponse response = null;
        try {
            response = getPlayInfo(client, videoId);
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println("response = " + JSONObject.toJSONString(response));

    }

    /**
     * Initialize the client.
     *
     * @param regionId
     * @param accessKeyId
     * @param accessKeySecret
     * @return
     * @throws ClientException
     */
    public static DefaultAcsClient InitVodClient(String regionId, String accessKeyId, String accessKeySecret) throws ClientException {
        DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
        DefaultAcsClient client = new DefaultAcsClient(profile);
        return client;
    }

    /**
     * Obtain the streaming URL.
     *
     * @param client
     * @param videoId
     * @return
     * @throws Exception
     */
    public static GetPlayInfoResponse getPlayInfo(DefaultAcsClient client, String videoId) throws Exception {
        GetPlayInfoRequest request = new GetPlayInfoRequest();
        request.setVideoId(videoId);
        // Set the expiration time, in seconds. Default value: 3600.
        request.setAuthTimeout(3600L);
        request.setFormats("mp4");
        JSONObject playConfig = new JSONObject();
        // Set the preview duration, in seconds. Minimum value: 1.
        playConfig.put("PreviewTime", "30");
        request.setPlayConfig(playConfig.toJSONString());
        return client.getAcsResponse(request);
    }
}
                
```

## Calculate the preview duration

Run code to generate the auth\_key field. To calculate the preview duration, perform the following steps:

1.  Add the `previewTime` parameter to calculate the preview duration when you calculate the MD5 hash value for URL signing. To calculate the MD5 hash value, use the `MD5(uri-timestamp-rand-uid-auth_key-preview_time)` method. For more information, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).

    **Note:** To allow users to view the complete video, do not set the previewTime parameter or include the previewTime parameter in the calculation of the auth\_key field.

2.  Append `&end=` + `previewTime` to the calculation result of the auth\_key field at the end.``

The following code provides an example:

```
    private String generateRand() {
        return UUID.randomUUID().toString().replaceAll("-", "");
    }

    public String genAuthKey(String object, String privateKey, Long expireTime, Long previewTime) {
        String rand = "0";
        String uid = "0";
        if (StringUtils.isBlank(privateKey)) {
            return "";
        }
        rand = generateRand();
        long timestamp = System.currentTimeMillis() / 1000 + (expireTime == null ? 0 : expireTime);
        String authStr = timestamp + "-" + rand + "-" + uid;
        String md5Str = object + "-" + authStr + "-" + privateKey;
        if(previewTime!=0)
            md5Str = md5Str + "-" + previewTime;
        String auth_key = authStr + "-" + MD5Util.md5( md5Str);
        return auth_key;
    }

    public void previewTest() throws Exception {
        try {
            String key = "your cdn auth key";
            String fileUrl = "http://test.yourdomain.com/test/bee21427ca3346848835c1bd786054c5-19bd8528c1d51576cd726cf86471ca0****.mp4";
            URL url = new URL(fileUrl);
            String file = url.getFile();
            Long previewtime = 120L;
            Long expireTime = 1800L;
            String auth_key =genAuthKey(file, key, expireTime, previewtime);
            fileUrl = fileUrl + "?auth_key=" + auth_key;
            if(previewtime != 0)
                fileUrl = fileUrl + "&end=" + previewtime;
            System.out.println(fileUrl);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
            
```

