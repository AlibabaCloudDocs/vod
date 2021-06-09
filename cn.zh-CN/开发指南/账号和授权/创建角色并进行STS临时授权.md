# 创建角色并进行STS临时授权

使用STS临时授权可以有效避免RAM用户密码泄露导致的安全风险，本文为您如何创建RAM用户，创建角色，并进行STS临时授权。

如果您之前没有使用过阿里云控制台，需要先开通服务。

RAM用户的权限是可长期使用的，易导致安全风险。建议您生成STS临时AK，自定义过期时间，并且指定复杂的策略来对不同的RAM用户进行限制，仅提供最小的权限。

## 创建RAM用户

1.  使用阿里云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  单击左侧导航栏**用户**，进入用户管理页面，单击页面中的**创建用户**。

    ![用户管理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3355793061/p177869.png)

3.  勾选**编程访问**，单击**确定**。

    此时创建了一个拥有和主账号一样完全访问VOD权限的RAM用户。

    ![创建用户](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0112204061/p177870.png)

    单击**确定**后会弹出手机验证窗口，完成验证码验证后，自动生成该RAM用户的AccessKey。

    ![生成AK](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1112204061/p177876.png)

4.  单击用户信息右侧的**复制**，保存用户登录名称、登录密码、AK对等用户信息。

    **说明：** 请保存用户信息并妥善保管，用于后续的访问。

5.  返回用户管理界面，这里显示账号已创建。创建完成之后，该RAM用户还是没有任何权限，单击右边的**添加权限** 。

    ![添加权限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3020404061/p177953.png)

6.  在添加权限页面，选择**AliyunSTSAssumeRoleAccess**策略，单击**确定**。

    ![选择策略](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3020404061/p177961.png)


## 创建角色

1.  打开[RAM控制台](https://ram.console.aliyun.com/roles)，进入RAM角色管理页面，单击**创建RAM角色**。

    ![创建RAM角色](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4020404061/p177972.png)

2.  在创建RAM角色页面，选择**阿里云账号**，单击**下一步**。

    ![创建RAM角色-1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4020404061/p177974.png)

3.  输入角色名称，选择**当前云账号**，单击**完成**。

    ![创建RAM角色-2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4020404061/p177977.png)

    创建完成后，进入如下页面：

    ![创建完成](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4020404061/p178014.png)

4.  返回RAM角色管理页面，找到刚创建的角色，单击角色信息右侧的**添加权限**。

    ![添加权限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4020404061/p178018.png)

5.  给角色添加**AliyunVODFullAccess**系统授权，并单击**确定**。

    ![授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4020404061/p178021.png)

    **说明：** 为控制风险，建议采用最小权限。

    完成授权后，会生成一条授权成功的记录。

    ![授权成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4020404061/p178022.png)


## STS授权访问

请下载和安装对应语言版本的[STS SDK](/cn.zh-CN/SDK参考/SDK参考（STS）/STS SDK概览.md)或直接调用[AssumeRole](/cn.zh-CN/API参考/API 参考（STS）/操作接口/AssumeRole.md)接口。 角色和策略等的配置请参见下文示例（以Java为例）。

调用方法，请参见[什么是STS](/cn.zh-CN/API参考/API 参考（STS）/什么是STS.md)。

-   Java代码示例

    完成创建RAM用户和角色后，一切准备就绪，可以正式使用STS来授权访问了。

    这里使用一个简单的STS的Java示例。

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
            // 只有RAM用户（子账号）才能调用 AssumeRole 接口
            // 阿里云主账号的AccessKeys不能用于发起AssumeRole请求
            // 请首先在RAM控制台创建一个RAM用户，并为这个用户创建AccessKeys
            String accessKeyId = "<access-key-id>";
            String accessKeySecret = "<access-key-secret>";
            // AssumeRole API 请求参数: RoleArn, RoleSessionName, Policy, and DurationSeconds
            // RoleArn 需要在 RAM 控制台上获取
            String roleArn = "<role-arn>";
            // RoleSessionName 是临时Token的会话名称，自己指定用于标识你的用户，主要用于审计，或者用于区分Token颁发给谁
            // 但是注意RoleSessionName的长度和规则，不要有空格，只能有'-' '_' 字母和数字等字符
            // 具体规则请参考API文档中的格式要求
            String roleSessionName = "session-name";// 自定义即可
            // 定制你的policy
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
                System.out.println("Failed to get a token.");
                System.out.println("Error code: " + e.getErrCode());
                System.out.println("Error message: " + e.getErrMsg());
            }
        }
    
        static AssumeRoleResponse assumeRole(String accessKeyId, String accessKeySecret, String roleArn, String roleSessionName, String policy) throws ClientException {
            try {
                //构造default profile（参数留空，无需添加Region ID）
                /*
                说明：当设置SysEndpoint为sts.aliyuncs.com时，regionId可填可不填；反之，regionId必填，根据使用的服务区域填写，例如：cn-shanghai
                详情参考STS各地域的Endpoint，请参见[t12478.dita\#reference\_sdg\_3pv\_xdb](/cn.zh-CN/API参考/API 参考（STS）/接入地址.md)。
                 */
                IClientProfile profile = DefaultProfile.getProfile("", accessKeyId, accessKeySecret);
                //用profile构造client
                DefaultAcsClient client = new DefaultAcsClient(profile);
                // 创建一个 AssumeRoleRequest 并设置请求参数
                final AssumeRoleRequest request = new AssumeRoleRequest();
                request.setSysEndpoint("sts.aliyuncs.com");
                request.setSysMethod(MethodType.POST);
                request.setRoleArn(roleArn);
                request.setRoleSessionName(roleSessionName);
                request.setPolicy(policy);
                // 发起请求，并得到response
                final AssumeRoleResponse response = client.getAcsResponse(request);
                return response;
            } catch (ClientException e) {
                throw e;
            }
        }
    
        static void createUploadVideo(String accessKeyId, String accessKeySecret, String token) {
            // 点播服务所在的Region，接入服务中心为上海，则填cn-shanghai
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

    -   RoleArn：需要扮演的角色ID，角色的ID可以在**角色管理**\>**基本信息**中找到。
    -   RoleSessionName：一个用来标示临时凭证的名称，一般来说建议使用不同的应用程序用户来区分。
    -   Policy：在扮演角色的时候额外加上的一个权限限制。

        **说明：**

        -   这里需要解释一下Policy，这里传入的Policy是用来限制扮演角色之后的临时凭证的权限。最后临时凭证获得的权限是角色的权限和这里传入的Policy的交集。
        -   在扮演角色的时候传入Policy的原因是为了灵活性，比如只能现在使用CreateUploadVideo接口。
    -   DurationSeconds：临时凭证的有效期，单位是s，最小为900，最大为3600。
    -   id和secret：需要扮演角色的RAM用户，及其AccessKey。
-   [PHP示例](/cn.zh-CN/SDK参考/SDK参考（STS）/PHP示例.md)
-   [Python示例](/cn.zh-CN/SDK参考/SDK参考（STS）/Python示例.md)
-   [.NET示例](/cn.zh-CN/SDK参考/SDK参考（STS）/.NET示例.md)
-   [Node.js示例](/cn.zh-CN/SDK参考/SDK参考（STS）/Node.js示例.md)

请求发出后，会返回结果，更多信息，请参见[返回结果](/cn.zh-CN/API参考/API 参考（STS）/返回结果.md)。

