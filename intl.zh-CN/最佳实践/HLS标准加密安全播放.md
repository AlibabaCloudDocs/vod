# HLS标准加密安全播放

通过阅读本文，您可以了解HLS标准加密安全播放的原理、实现流程以及示例代码。

## 简介

为了加强标准加密视频在解密播放时解密密钥的安全性，业务方需要同时提供令牌服务和解密服务，其中令牌服务生成鉴权令牌，解密服务用于验证令牌和获取解密密钥。

**说明：**

-   令牌是被CDN改写到解密接口上，所以在使用标准加密前必须先开启CDN域名的令牌改写功能。
-   非CDN播放地址，不支持处理令牌参数。

## 基本原理

标准加密视频的解密播放时，令牌生成以及令牌校验需要业务方封装服务，其他逻辑过程都封装在阿里云播放器中，基本原理如下：

**说明：** 如是非阿里云播放器，需要业务方自行封装解密播放处理过程。

![基本原理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6640194061/p180180.png)

## 准备条件

标准加密视频在进行解密播放时，需要业务方提供令牌服务和解密服务，其中解密服务是用于获取视频的解密密钥，而令牌服务是用于生成鉴权令牌。

**令牌服务**

生成令牌时，可以通过业务方用户ID、视频播放终端\(Web、iOS、Android\)、视频ID等信息按照一定方式生成令牌。

**说明：**

-   标准播放器在播放视频时只会请求一次解密密钥，所以令牌最好只能使用一次且具备过期时间等特性。
-   令牌生成校验，请参见[令牌示例代码](#section_1ho_4ps_3rr)。

**解密服务**

解密服务主要对调用方进行鉴权和返回解密密钥。

-   根据传递的令牌参数，判断令牌的有效性，如：是否是令牌服务生成、令牌是否过期、是否已经被使用过等。
-   如果令牌校验通过，则根据密文密钥获取到明文密钥并将明文密钥通过base64decode后返回。

**说明：**

-   此处鉴权主要是指校验令牌的有效性，且令牌只能通过MtsHlsUriToken参数传递到解密服务。
-   解密服务，请参见[解密服务示例代码](#section_dln_tgj_h8x)。

## 实现过程

标准加密视频在解密播放时会经历以下几个处理阶段：

**说明：**

-   此处主要解析阿里云播放器在标准加密视频解密播放的处理逻辑。
-   非阿里云播放器需要自行封装请求播放服务过程，获取到加密视频地址后直接给播放器进行解密播放即可，详细请参见[获取视频播放地址](/intl.zh-CN/服务端API/音视频播放/获取视频播放地址.md)。

1.  业务方需要先调用令牌服务颁发令牌Token。
2.  令牌服务根据传递的信息生成令牌Token。
3.  令牌服务将生成的令牌Token返回给调用方。

    **说明：** 以上步骤不属于阿里云播器处理过程，需要业务方单独调用令牌服务生成令牌Token并传递给播放器，而使用的是非阿里云播放器，那么业务方可选择将该步集成到播放器播放处理逻辑中。

4.  调用方通过播放器提供的PlayConfig参数，将令牌Token设置到MtsHlsUriToken上。
5.  播放器获取设置的MtsHlsUriToken参数、播放的视频ID等信息，从播放服务获取播放地址。

    **说明：**

    播放服务接收到请求，将MtsHlsUriToken参数拼接在标准加密视频地址上并返回给播放器。

    例如：`http://demo.com/ddf56e501d07402796c468bbea08ec8c/9e712e72879b93f8933d5f9eca4bacaa-fd-encrypt-stream.m3u8?MtsHlsUriToken=NWItZGU5ZWEwODRlMzky`。

6.  播放器获取到标准加密M3U8地址并请求M3U8。
7.  CDN改写M3U8内容，将MtsHlsUriToken改写到解密接口上。例如：

    ![SDN改写](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7640194061/p180181.png)

8.  播放器解析M3U8内容并获取到解密接口并请求获取解密密钥。例如：

    `http://demo.com/ddf56e501d07402796c468bbea08ec8c/9e712e72879b93f8933d5f9eca4bacaa-fd-encrypt-stream.m3u8?MtsHlsUriToken=NWItZGU5ZWEwODRlMzky`。

9.  解密服务接收到请求，调用令牌接口校验令牌Token的有效性。
10. 令牌Token校验通过，则将明文密钥通过base64的code解码后返回给播放器。
11. 播放器在获取到解密密钥后，将对标准加密视频进行解密播放。

    **说明：** 通用播放器在播放视频时，只会在解密播放前调用一次解密接口获取密钥，后续解密播放过程不会再次请求解密接口。


## 令牌示例代码

本示例代码主要是对令牌生成和令牌校验相关实现的模板代码，不作为实际部署代码。

**说明：**

-   以下代码仅仅提供令牌Token生成和校验逻辑的一个范例模板，不作为实际部署代码用。
-   该示例代码的令牌生成采用简单的AES加密生成，业务方也可自行实现其他生成方式。
-   关于生成的令牌Token的存储、获取由业务方自行实现。

```
public class PlayToken {
    //非AES生成方式，无需以下参数
    private static String ENCRYPT_KEY = "";
    private static String INIT_VECTOR = "";
    /**
     * 根据传递的参数生成令牌
     * 说明：
     *  1、参数可以是业务方的用户ID、播放终端类型等信息
     *  2、调用令牌接口时生成令牌Token
     * @param args
     * @return
     */
    public String generateToken(String... args) throws Exception {
        if (null == args || args.length <= 0) {
            return null;
        }
        String base = StringUtils.join(Arrays.asList(args), "_");
        //设置30S后，该token过期，过期时间可以自行调整
        long expire = System.currentTimeMillis() + 30000L;
        base += "_" + expire;
        //生成token
        String token = encrypt(base, ENCRYPT_KEY);
        //保存token，用于解密时校验token的有效性，例如：过期时间、token的使用次数
        saveToken(token);
        return token;
    }
    /**
     * 验证token的有效性
     * 说明：
     *  1、解密接口在返回播放密钥前，需要先校验Token的合法性和有效性
     *  2、强烈建议同时校验Token的过期时间以及Token的有效使用次数
     * @param token
     * @return
     * @throws Exception
     */
    public boolean validateToken(String token) throws Exception {
        if (null == token || "".equals(token)) {
            return false;
        }
        String base = decrypt(token, ENCRYPT_KEY);
        //先校验token的有效时间
        Long expireTime = Long.valueOf(base.substring(base.lastIndexOf("_") + 1));
        if (System.currentTimeMillis() > expireTime) {
            return false;
        }
        //从DB获取token信息，判断token的有效性，业务方可自行实现
        TokenInfo dbToken = getToken(token);
        //判断是否已经使用过该token
        if (dbToken == null || dbToken.useCount > 0) {
            return false;
        }
        //获取到业务属性信息，用于校验
        String businessInfo = base.substring(0, base.lastIndexOf("_"));
        String[] items = businessInfo.split("_");
        //校验业务信息的合法性，业务方实现
        return validateInfo(items);
    }
    /**
     * 保存Token到DB
     * 业务方自行实现
     *
     * @param token
     */
    public void saveToken(String token) {
        //TODO 存储Token
    }
    /**
     * 查询Token
     * 业务方自行实现
     *
     * @param token
     */
    public TokenInfo getToken(String token) {
        //TODO 从DB 获取Token信息，用于校验有效性和合法性
        return null;
    }
    /**
     * 校验业务信息的有效性，业务方可自行实现
     *
     * @param infos
     * @return
     */
    public boolean validateInfo(String... infos) {
        //TODO 校验信息的有效性，例如UID是否有效等
        return true;
    }
    /**
     * AES加密生成Token
     *
     * @param key
     * @param value
     * @return
     * @throws Exception
     */
    public String encrypt(String key, String value) throws Exception {
        IvParameterSpec e = new IvParameterSpec(INIT_VECTOR.getBytes("UTF-8"));
        SecretKeySpec skeySpec = new SecretKeySpec(key.getBytes("UTF-8"), "AES");
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5PADDING");
        cipher.init(Cipher.ENCRYPT_MODE, skeySpec, e);
        byte[] encrypted = cipher.doFinal(value.getBytes());
        return Base64.encodeBase64String(encrypted);
    }
    /**
     * AES解密token
     *
     * @param key
     * @param encrypted
     * @return
     * @throws Exception
     */
    public String decrypt(String key, String encrypted) throws Exception {
        IvParameterSpec e = new IvParameterSpec(INIT_VECTOR.getBytes("UTF-8"));
        SecretKeySpec skeySpec = new SecretKeySpec(key.getBytes("UTF-8"), "AES");
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5PADDING");
        cipher.init(Cipher.DECRYPT_MODE, skeySpec, e);
        byte[] original = cipher.doFinal(Base64.decodeBase64(encrypted));
        return new String(original);
    }
    /**
     * Token信息，业务方可提供更多信息，这里仅仅给出示例
     */
    class Token {
        //Token的有效使用次数，分布式环境需要注意同步修改问题
        int useCount;
        //token内容
        String token;
    }}
```

## 解密服务示例代码

**说明：** 以下代码可直接运行启动，但仅仅作为测试使用，不可作为线上正式部署。

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.http.ProtocolType;
import com.aliyuncs.kms.model.v20160120.DecryptRequest;
import com.aliyuncs.kms.model.v20160120.DecryptResponse;
import com.aliyuncs.profile.DefaultProfile;
import com.sun.net.httpserver.Headers;
import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;
import com.sun.net.httpserver.spi.HttpServerProvider;
import org.apache.commons.codec.binary.Base64;
import java.io.IOException;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.InetSocketAddress;
import java.net.URI;import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class HlsDecryptServer {
    private static DefaultAcsClient client;
    static {
        //KMS的区域，必须与视频对应区域
        String region = "<视频对应区域>";
        //访问KMS的授权AK信息
        String accessKeyId = "<Your AccessKeyId>";
        String accessKeySecret = "<Your AccessKeySecrect>";
        client = new DefaultAcsClient(DefaultProfile.getProfile(region, accessKeyId, accessKeySecret));
    }
    /**
     * 说明：
     * 1、接收解密请求，获取密文密钥和令牌Token
     * 2、调用KMS decrypt接口获取明文密钥
     * 3、将明文密钥base64decode返回
     */
    public class HlsDecryptHandler implements HttpHandler {
        /**
         * 处理解密请求
         * @param httpExchange
         * @throws IOException
         */
        public void handle(HttpExchange httpExchange) throws IOException {
            String requestMethod = httpExchange.getRequestMethod();
            if ("GET".equalsIgnoreCase(requestMethod)) {
                //校验token的有效性
                String token = getMtsHlsUriToken(httpExchange);
                boolean validRe = validateToken(token);
                if (!validRe) {
                    return;
                }
                //从URL中取得密文密钥
                String ciphertext = getCiphertext(httpExchange);
                if (null == ciphertext)
                    return;
                //从KMS中解密出来，并Base64 decode
                byte[] key = decrypt(ciphertext);
                //设置header
                setHeader(httpExchange, key);
                //返回base64decode之后的密钥
                OutputStream responseBody = httpExchange.getResponseBody();
                responseBody.write(key);
                responseBody.close();
            }
        }
        private void setHeader(HttpExchange httpExchange, byte[] key) throws IOException {
            Headers responseHeaders = httpExchange.getResponseHeaders();
            responseHeaders.set("Access-Control-Allow-Origin", "*");
            httpExchange.sendResponseHeaders(HttpURLConnection.HTTP_OK, key.length);
        }
        /** 
        * 调用KMS decrypt接口解密，并将明文base64decode
         * @param ciphertext
         * @return
         */ 
       private byte[] decrypt(String ciphertext) {
            DecryptRequest request = new DecryptRequest();
            request.setCiphertextBlob(ciphertext);
            request.setProtocol(ProtocolType.HTTPS);
            try {
                DecryptResponse response = client.getAcsResponse(request);
                String plaintext = response.getPlaintext();
                //注意：需要base64 decode
                return Base64.decodeBase64(plaintext);
            } catch (ClientException e) {
                e.printStackTrace();
                return null;
            }
        }
        /**
         * 校验令牌有效性
         * @param token
         * @return
         */
        private boolean validateToken(String token) {
            if (null == token || "".equals(token)) {
                return false;
            }
            //TODO 业务方实现令牌有效性校验
            return true;
        }
        /**
         * 从URL中获取密文密钥参数
         * @param httpExchange
         * @return
         */
        private String getCiphertext(HttpExchange httpExchange) {
            URI uri = httpExchange.getRequestURI();
            String queryString = uri.getQuery();
            String pattern = "Ciphertext=(\\w*)";
            Pattern r = Pattern.compile(pattern);
            Matcher m = r.matcher(queryString);
            if (m.find())
                return m.group(1);
            else {
                System.out.println("Not Found Ciphertext Param");
                return null;
            }
        }
        /**
         * 获取Token参数
         *
         * @param httpExchange
         * @return
         */
        private String getMtsHlsUriToken(HttpExchange httpExchange) {
            URI uri = httpExchange.getRequestURI();
            String queryString = uri.getQuery();
            String pattern = "MtsHlsUriToken=(\\w*)";
            Pattern r = Pattern.compile(pattern);
            Matcher m = r.matcher(queryString);
            if (m.find())
                return m.group(1);
            else {
                System.out.println("Not Found MtsHlsUriToken Param");
                return null;
            }
        }
    }
    /**
     * 服务启动
     *
     * @throws IOException
     */
    private void serviceBootStrap() throws IOException {
        HttpServerProvider provider = HttpServerProvider.provider();
        //监听端口9999,能同时接受30个请求
        HttpServer httpserver = provider.createHttpServer(new InetSocketAddress(9999), 30);
        httpserver.createContext("/", new HlsDecryptHandler());
        httpserver.start();
        System.out.println("hls decrypt server started");
    }
    public static void main(String[] args) throws IOException {
        HlsDecryptServer server = new HlsDecryptServer();
        server.serviceBootStrap();
    }}
```

