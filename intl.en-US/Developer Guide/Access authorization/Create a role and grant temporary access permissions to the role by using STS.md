# Create a role and grant temporary access permissions to the role by using STS

Security Token Service \(STS\) can be used to grant temporary access permissions to avoid security risks caused by leaks of RAM user passwords. This topic describes how to create a RAM user and a role and use STS to grant temporary access permissions.

Resource Access Management \(RAM\) is activated.

Permissions granted to RAM users can be used for an extended period of time, which may lead to security risks. We recommend that you generate STS temporary AccessKey pairs, customize validity periods for the AccessKey pairs, and specify complex policies to provide only minimum permissions to RAM users.

## Create a RAM user

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) with an Alibaba Cloud account.

2.  Go back to the Users page. The RAM user you created appears in the user list. When the RAM user is created, it does not have any permissions. Click **Add Permissions** in the Actions column corresponding to the RAM user.

    ![Add Permissions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0086201161/p177953.png)

3.  On the Add Permissions page, select the **AliyunSTSAssumeRoleAccess** policy from the list of policies under System Policy, and click **OK**.

    ![Select Policy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0086201161/p177961.png)


## Create a role

1.  In the left-side navigation pane of the [RAM console](https://ram.console.aliyun.com/roles), click RAM Roles. On the RAM Roles page, click **Create RAM Role**.

2.  In the Create RAM Role dialog box, select **Alibaba Cloud Account** and click **Next**.

3.  Enter a RAM role name and select **Current Alibaba Cloud Account**. Then, click **OK**.

4.  Go back to the RAM Roles page. Find the role that you created, and click **Add Permissions** in the Actions column.

5.  Select the **AliyunVODFullAccess** policy from the list of policies under System Policy, and click **OK**.

    **Note:** To control risks, we recommend that you grant permissions to RAM roles based on the principle of least privilege.

    After the permission is granted, a record is generated.


## Use STS to authorize access

You must download and install the [STS SDK](/intl.en-US/SDK Reference/STS SDK Reference/STS SDK overview.md) for the corresponding programming language or call the [AssumeRole](/intl.en-US/API Reference/API Reference (STS)/Operation interfaces/AssumeRole.md) operation. For the configurations of roles and policies, see the following example for Java.

For how to call API operations, see [What is STS?](/intl.en-US/API Reference/API Reference (STS)/What is STS?.md)

-   Sample code for Java

    After a RAM user and a RAM role are created, you can use STS to authorize access.

    The following sample code provides a simple example in Java.

    ```
    package pop;
    
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.http.MethodType;
    import com.aliyuncs.profile.DefaultProfile;
    import com.aliyuncs.profile.IClientProfile;
    import com.aliyuncs.sts.model.v20150401.AssumeRoleRequest;
    import com.aliyuncs.sts.model.v20150401.AssumeRoleResponse;
    import com.aliyuncs.vod.model.v20170321.CreateUploadVideoRequest;
    import com.aliyuncs.vod.model.v20170321.CreateUploadVideoResponse;
    
    /**
     * @author jack
     * @date 2020/5/25
     */
    public class TestStsService {
    
        public static void main(String[] args) {
            // Only RAM users can call the AssumeRole operation.
            // AccessKey pairs of Alibaba Cloud accounts cannot be used to initiate AssumeRole requests.
            // Create a RAM user in the RAM console and create an AccessKey pair for the user.
            String accessKeyId = "<access-key-id>";
            String accessKeySecret = "<access-key-secret>";
            // Request parameters for the AssumeRole operation include RoleArn, RoleSessionName, Policy, and DurationSeconds.
            // You must obtain the RoleArn value from the RAM console.
            String roleArn = "<role-arn>";
            // The RoleSessionName parameter indicates the name of the session for the temporary token. You can use this parameter to identify users in audit or identify users to whom you want to issue tokens.
            // However, you must take note of the length and naming conventions of the RoleSessionName parameter. The RoleSessionName value can contain only letters, digits, hyphens (-), and underscores (_), and cannot include spaces.
            // For more information about the naming conventions, see the format requirements in the API reference.
            String roleSessionName = "session-name";// Specify a session name.
            // Specify a policy.
            String policy = "{\n" +
                    "  \"Version\": \"1\",\n" +
                    "  \"Statement\": [\n" +
                    "    {\n" +
                    "      \"Action\": \"vod:*\",\n" +
                    "      \"Resource\": \"*\",\n" +
                    "      \"Effect\": \"Allow\"\n" +
                    "    }\n" +
                    "  ]\n" +
                    "}";
            try {
                AssumeRoleResponse response = assumeRole(accessKeyId, accessKeySecret, roleArn, roleSessionName, policy);
                System.out.println("Expiration: " + response.getCredentials().getExpiration());
                System.out.println("Access Key Id: " + response.getCredentials().getAccessKeyId());
                System.out.println("Access Key Secret: " + response.getCredentials().getAccessKeySecret());
                System.out.println("Security Token: " + response.getCredentials().getSecurityToken());
                System.out.println("RequestId: " + response.getRequestId());
    
                createUploadVideo(response.getCredentials().getAccessKeyId(), response.getCredentials().getAccessKeySecret(), response.getCredentials().getSecurityToken());
            } catch (ClientException e) {
                System.out.println("Failed to get a token.") ;
                System.out.println("Error code: " + e.getErrCode());
                System.out.println("Error message: " + e.getErrMsg());
            }
        }
    
        static AssumeRoleResponse assumeRole(String accessKeyId, String accessKeySecret, String roleArn, String roleSessionName, String policy) throws ClientException {
            try {
                // Construct a default profile. Leave the region ID unspecified.
                /*
                Note: If you set SysEndpoint to sts.aliyuncs.com, the regionId parameter is optional. Otherwise, you must set regionId to the service region in use. Example: cn-shanghai.
                For more information about the STS endpoints of regions, see [t12478.dita\#reference\_sdg\_3pv\_xdb](/intl.en-US/API Reference/API Reference (STS)/Endpoints.md).
                 */
                IClientProfile profile = DefaultProfile.getProfile("", accessKeyId, accessKeySecret);
                // Use the profile to construct a client.
                DefaultAcsClient client = new DefaultAcsClient(profile);
                // Create a AssumeRoleRequest and set the request parameters.
                final AssumeRoleRequest request = new AssumeRoleRequest();
                request.setSysEndpoint("sts.aliyuncs.com");
                request.setSysMethod(MethodType.POST);
                request.setRoleArn(roleArn);
                request.setRoleSessionName(roleSessionName);
                request.setPolicy(policy);
                // Send the request and obtain the response.
                final AssumeRoleResponse response = client.getAcsResponse(request);
                return response;
            } catch (ClientException e) {
                throw e;
            }
        }
    
        static void createUploadVideo(String accessKeyId, String accessKeySecret, String token) {
            // Specify the region of ApsaraVideo VOD. For example, if the service region is Shanghai, set regionId to cn-shanghai.
            String regionId = "cn-shanghai";
            IClientProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
            DefaultAcsClient client = new DefaultAcsClient(profile);
    
            CreateUploadVideoRequest request = new CreateUploadVideoRequest();
            request.setSecurityToken(token);
            request.setTitle("t5");
            request.setFileName("D:\\TestVideo\\t4.mp4");
            request.setFileSize(10240L);
    
            try {
                CreateUploadVideoResponse response = client.getAcsResponse(request);
                System.out.println("CreateUploadVideoRequest, " + request.getUrl());
                System.out.println("CreateUploadVideoRequest, requestId:" + response.getRequestId());
                System.out.println("UploadAddress, " + response.getUploadAddress());
                System.out.println("UploadAuth, " + response.getUploadAuth());
                System.out.println("VideoId, " + response.getVideoId());
            } catch (ClientException e) {
                System.out.println("action, error:" + e);
                e.printStackTrace();
            }
        }
    }
                    
    ```

    -   RoleArn: the ID of the role to be assumed. To obtain the RoleArn value, go to the **RAM Roles** page in the RAM console. Click the name of the RAM role and check the ARN value in the **Basic Information** section.
    -   RoleSessionName: the name of the temporary access credential. We recommend that you use different application user names to distinguish the credentials.
    -   Policy: the permission limits added when the user assumes a role.

        **Note:**

        -   The Policy parameter is passed in to limit the permissions of the temporary access credential after the role is assumed. The final permissions obtained by the temporary access credential are an intersection of the permissions of the role and the permissions specified by the Policy parameter.
        -   The Policy parameter is passed in to improve flexibility. For example, you can set this parameter to specify that only the CreateUploadVideo operation can be called.
    -   DurationSeconds: the validity period of the temporary access credential. Unit: seconds. Valid values: 900 to 3600.
    -   AccessKeyId and AccessKeySecret: the RAM user who assumes the role and its AccessKey pair.
-   [STS SDK for PHP](/intl.en-US/SDK Reference/STS SDK Reference/STS SDK for PHP.md)
-   [STS SDK for Python](/intl.en-US/SDK Reference/STS SDK Reference/STS SDK for Python.md)
-   [STS SDK for .NET](/intl.en-US/SDK Reference/STS SDK Reference/STS SDK for .NET.md)
-   [STS SDK for Node.js](/intl.en-US/SDK Reference/STS SDK Reference/STS SDK for Node.js.md)

A response is returned after the request is sent. For more information, see [Responses](/intl.en-US/API Reference/API Reference (STS)/Responses.md).

