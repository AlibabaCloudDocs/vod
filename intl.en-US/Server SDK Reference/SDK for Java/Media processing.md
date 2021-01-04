# Media processing

This topic provides examples on how to use the API operations of the media processing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to submit transcoding and snapshot jobs, query snapshot data, and preprocess videos in the production studio.

## Initialize a client

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

## Submit a transcoding job

You can call the SubmitTranscodeJobs operation to submit a transcoding job.

For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). Example:

```
import com.aliyuncs.vod.model.v20170321.SubmitTranscodeJobsRequest;
import com.aliyuncs.vod.model.v20170321.SubmitTranscodeJobsResponse;

/**
 * Submit a transcoding job.
 */
public static SubmitTranscodeJobsResponse submitTranscodeJobs(DefaultAcsClient client) throws Exception {
    SubmitTranscodeJobsRequest request = new SubmitTranscodeJobsRequest();
    // The ID of the video that you want to transcode.
    request.setVideoId("34a6ca54f5c140eece85a289****");
    // The ID of the transcoding template.
    request.setTemplateGroupId("e8aa925a9798c630d30cd****");
    // Build the parameters that are required to replace a watermark. You must create these parameters only when you want to replace a watermark.
    JSONObject overrideParams = buildOverrideParams();
    // The overriding parameters. You can change the values of some watermark-related parameters. You must specify these parameters only when you want to replace a watermark.
    request.setOverrideParams(overrideParams.toJSONString());
    // Build the configuration parameters that are required for standard encryption. You must create these parameters only for standard encryption.
    JSONObject encryptConfig = buildEncryptConfig(client);
    // The configurations for HLS standard encryption. You must specify these parameters only for standard encryption.
    request.setEncryptConfig(encryptConfig.toJSONString());
    return client.getAcsResponse(request);
}


/**
 * Call example
 */
public static void main(String[] args) throws ClientException {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    SubmitTranscodeJobsResponse response = new SubmitTranscodeJobsResponse();
    try {
        response = submitTranscodeJobs(client);
        // The task ID.
        System.out.println("JobId = " + response.getTranscodeJobs().get(0).getJobId());
    } catch (Exception e) {
        System.out.println("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.println("RequestId = " + response.getRequestId());
}

/**
 * Build the configurations of HTTP Live Streaming (HLS) encryption.
 * @return
 * @throws ClientException
 */
public static JSONObject buildEncryptConfig(DefaultAcsClient client) throws ClientException {
    // The service key that is provided by ApsaraVideo VOD. To view the service key, you must select the region where the key resides and find the key whose description is vod in the KMS console.
    String serviceKey = "<Your Service Key>";
    // Create a data key for encryption. The response contains the plaintext and ciphertext of the data key.
    // Transfer only the ciphertext of the data key for standard video encryption.
    // Note: We recommend that you separately initialize the KMS client to ensure that you can call KMS operations in the correct region. For more information, see the "Initialization" topic to specify the correct region.
    GenerateDataKeyResponse response = generateDataKey(client, serviceKey);
    JSONObject encryptConfig = new JSONObject();
    // The URI of the operation that is used to decrypt the data key. To obtain the URI, concatenate the URL of the decryption service and the ciphertext of the data key. The ciphertext to decrypt varies among videos.
    // You can customize the name of the Ciphertext parameter. The name in this example is only for reference.
    encryptConfig.put("DecryptKeyUri", "http://decrypt.demo.com/decrypt?" +
            "Ciphertext=" + response.getCiphertextBlob());
    // The type of the key service. Set the value to KMS.
    encryptConfig.put("KeyServiceType", "KMS");
    // The ciphertext of the data key.
    encryptConfig.put("CipherText", response.getCiphertextBlob());
    return encryptConfig;
}

/**
 * 1. Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark.
 * 2. Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
 * 3. You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
 * Note: The watermark file and the video must be stored on the same origin server.
 * @return
 */
public static JSONObject buildOverrideParams() {
    JSONObject overrideParams = new JSONObject();
    JSONArray watermarks = new JSONArray();
    // Override the file URL of the image watermark.
    JSONObject watermark1 = new JSONObject();
    // The ID of the watermark whose image you want to override. The ID must be associated with the transcoding template.
    watermark1.put("WatermarkId", "2ea587477c5a1bc8b57****");
    // The file URL of the new image that is stored in an OSS bucket. The new image and the video must be stored on the same origin server.
    watermark1.put("FileUrl", "https:192.168.0.0/16);

    // Override the content of the text watermark.
    JSONObject watermark2 = new JSONObject();
    // The ID of the watermark whose content you want to override. The ID must be associated with the transcoding template.
    watermark2.put("WatermarkId", "d297ba31ac5242d207****");
    // The new content of the watermark.
    watermark2.put("Content", "User ID:6****");
    watermarks.add(watermark2);
    overrideParams.put("Watermarks", watermarks);
    return overrideParams;
}

/**
 * Create a data key for encryption. The response contains the plaintext and ciphertext of the data key. You need only to transfer the ciphertext to ApsaraVideo VOD.
 * Note: You must set the value of the KeySpec parameter to AES_128. The NumberOfBytes parameter is not supported.
 * @ param client The client for KMS SDKs.
 * @ param serviceKey // The service key that is provided by ApsaraVideo VOD to generate data keys. The description of this service key is vod in the Key Management Service (KMS) console.
 * @return
 * @throws ClientException
 */
public static GenerateDataKeyResponse generateDataKey(DefaultAcsClient client, String serviceKey) throws ClientException {
    GenerateDataKeyRequest request = new GenerateDataKeyRequest();
    request.setKeyId(serviceKey);
    request.setKeySpec("AES_128");
    return client.getAcsResponse(request);
}
```

## Submit a snapshot job

You can call the SubmitSnapshotJob operation to submit a snapshot job.

For more information about the request and response parameters of this operation, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitSnapshotJob.md). Example:

**Note:** For more information about how to create a snapshot template, see [Create a snapshot template](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md).

```
import com.aliyuncs.vod.model.v20170321.SubmitSnapshotJobRequest;
import com.aliyuncs.vod.model.v20170321.SubmitSnapshotJobResponse;

/**
 * Submit a snapshot job.
 */
public static SubmitSnapshotJobResponse submitSnapshotJob(DefaultAcsClient client) throws Exception {
    SubmitSnapshotJobRequest request = new SubmitSnapshotJobRequest();
    // The ID of the video for which you want to create snapshots. We recommend that you use the ID of the snapshot template.
    request.setVideoId("4d237a8270084849bf4207876181****");
    // The ID of the snapshot template.
    request.setSnapshotTemplateId("5d745e6b8baadf589e0702426cfc6****");

    // If you specify the SnapshotTemplateId parameter, the following parameters are ignored:
    request.setCount(50L);
    request.setSpecifiedOffsetTime(0L);
    request.setInterval(1L);
    request.setWidth("200");
    request.setHeight("200");
    JSONObject spriteSnapshotConfig = buildSnapshotTemplateConfig();
    request.setSpriteSnapshotConfig(spriteSnapshotConfig.toJSONString());
    return client.getAcsResponse(request);
}

/**
 * Build the configurations of the image sprite snapshot.
 * @return
 */
public static JSONObject buildSnapshotTemplateConfig() {
    JSONObject spriteSnapshotConfig = new JSONObject();
    spriteSnapshotConfig.put("CellWidth", "120");
    spriteSnapshotConfig.put("CellHeight", "68");
    spriteSnapshotConfig.put("Columns", "3");
    spriteSnapshotConfig.put("Lines", "10");
    spriteSnapshotConfig.put("Padding", "20");
    spriteSnapshotConfig.put("Margin", "50");
    // Whether to retain the source image after an image sprite is generated.
    spriteSnapshotConfig.put("KeepCellPic", "keep");
    spriteSnapshotConfig.put("Color", "tomato");
    return spriteSnapshotConfig;
}

/**
 * Call example
 */
public static void main(String[] args) throws ClientException {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    SubmitSnapshotJobResponse response = new SubmitSnapshotJobResponse();
    try {
        response = submitSnapshotJob(client);
        // The task ID.
        System.out.println("JobId = " + response.getSnapshotJob().getJobId());
    } catch (Exception e) {
        System.out.println("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.println("RequestId = " + response.getRequestId());
}
```

## Query snapshot data

You can call the ListSnapshots operation to query snapshot data.

For more information about the request and response parameters of this operation, see [ListSnapshots](/intl.en-US/API Reference/Media management/Image Management/ListSnapshots.md). Example:

```
import com.aliyuncs.vod.model.v20170321.ListSnapshotsRequest;
import com.aliyuncs.vod.model.v20170321.ListSnapshotsResponse;


/**
 * Query snapshot data.
 */
public static ListSnapshotsResponse listSnapshots(DefaultAcsClient client) throws Exception {
    ListSnapshotsRequest request = new ListSnapshotsRequest();
    // The video ID.
    request.setVideoId("c86c0ceba9796535****");
    // The snapshot type.
    request.setSnapshotType("CoverSnapshot");
    request.setPageNo("1");
    request.setPageSize("20");
    return client.getAcsResponse(request);
}


/**
 * Call example
 */
public static void main(String[] args) throws ClientException {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    ListSnapshotsResponse response = new ListSnapshotsResponse();
    try {
        response = listSnapshots(client);
        // The snapshot URL.
        System.out.println("Url = " + response.getMediaSnapshot().getSnapshots().get(0).getUrl());
    } catch (Exception e) {
        System.out.println("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.println("RequestId = " + response.getRequestId());
}
```

## Preprocess videos in the production studio

You can call the SubmitPreprocessJobs operation to preprocess videos in the production studio.

For more information about the request and response parameters of this operation, see [SubmitPreprocessJobs](). Example:

```
import com.aliyuncs.vod.model.v20170321.SubmitPreprocessJobsRequest;
import com.aliyuncs.vod.model.v20170321.SubmitPreprocessJobsResponse;

/**
 * Preprocess videos in the production studio.
 */
public static SubmitPreprocessJobsResponse submitPreprocessJobs(DefaultAcsClient client) throws Exception {
    SubmitPreprocessJobsRequest request = new SubmitPreprocessJobsRequest();
    // The video ID.
    request.setVideoId("c86c0ceb8db54ae09796535****");
    request.setPreprocessType("PreprocessType");
    return client.getAcsResponse(request);
}


/**
 * Call example
 */
public static void main(String[] args) throws ClientException {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    SubmitPreprocessJobsResponse response = new SubmitPreprocessJobsResponse();
    try {
        response = submitPreprocessJobs(client);
        // The task ID.
        System.out.println("JobId = " + response.getPreprocessJobs().get(0).getJobId());
    } catch (Exception e) {
        System.out.println("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.println("RequestId = " + response.getRequestId());
}
```

