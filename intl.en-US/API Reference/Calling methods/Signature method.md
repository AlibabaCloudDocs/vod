# Signature method

This topic describes the signature method of HTTP or HTTPS requests that are sent by using the ApsaraVideo VOD API and provides the sample code.

## Overview

You must sign all HTTP or HTTPS requests to ensure security. Alibaba Cloud uses the request signature to verify the identity of the API caller. ApsaraVideo VOD implements symmetric encryption with an AccessKey pair to verify the identity of the request sender. You can obtain the AccessKey ID and AccessKey secret on the AccessKey Management page in the Alibaba Cloud Management Console.

-   The AccessKey ID is used to verify the identity of the user.
-   The AccessKey secret is used to encrypt and verify the signature string on the server. You must keep your AccessKey secret strictly confidential.

**Note:** Alibaba Cloud provides SDKs for multiple programming languages, including third-party SDKs. This simplifies signature signing. For more information, download [SDKs](https://develop.aliyun.com/tools/sdk?spm=a2c4g.11186623.2.32.4a2b6322i39q7C#/java).

## Generate a signature string

1.  Create and encode a canonicalized query string.

    1.  Create a canonicalized query string.

        Create a canonicalized query string by arranging the request parameters in alphabetical order. The request parameters include all [common request parameters](/intl.en-US/API Reference/Calling methods/Common parameters.md) and operation-specific parameters except the `Signature` parameter.

    2.  Encode the canonicalized query string.

        Encode the names and values of request parameters in UTF-8 based on [RFC 3986](https://tools.ietf.org/html/rfc3986?spm=a2c4g.11186623.2.34.28e26322iVuuhj). The following encoding rules are used:

        -   Uppercase letters, lowercase letters, digits, and some special characters such as hyphens `(-)`, underscores `(_)`, periods `(.)`, and tildes `(~)` do not need to be encoded.
        -   Other characters must be percent encoded in the `%XY` format. `XY` represents the ASCII code of the characters in hexadecimal notation. For example, double quotation marks \(`"`\) are encoded as `%22`.
        -   Extended UTF-8 characters are encoded in the `%XY%ZA…` format.
        -   Spaces must be encoded as `%20`. Do not encode spaces as plus signs \(`+`\).

            **Note:** The preceding encoding method is similar to but slightly different from the application/x-www-form-urlencoded MIME-type encoding algorithm. If you use java.net.URLEncoder in the Java standard library, use percentEncode to encode request parameters and their values. In the encoded query string, replace the plus sign \(`+`\) with `%20`, the asterisk \(`*`\) with `%2A`, and `%7E` with a tilde \(`~`\). This way, you can obtain an encoded string that matches the preceding encoding rules.

    3.  Separate the encoded parameter names from their encoded values with equal signs \(`=`\).

    4.  Connect the encoded request parameters with ampersands \(`&`\).

        **Note:** These parameters must be arranged in the same order as that in **Step a**.

2.  Generate the signature string.

    1.  Create a string-to-sign from the encoded canonicalized query string.

        You can also use percentEncode to encode the canonicalized query string that is created in the preceding step. Comply with the following rules to create a string-to-sign:

        ```
        StringToSign=
        HTTPMethod + "&" + //HTTPMethod: the HTTP method that is used to make the request, such as GET.
        percentEncode("/") + "&" + //percentEncode("/"): Encode the forward slashes (/) in UTF-8 as %2F.
        percentEncode(CanonicalizedQueryString) //Encode the canonicalized query string created in Step 1.
        ```

    2.  Calculate the HMAC value of the string-to-sign by using the AccessKey secret as the key.

        Calculate the hash-based message authentication code \(HMAC\) value of the string-to-sign based on [RFC 2104](https://www.ietf.org/rfc/rfc2104.txt?spm=a2c4g.11186623.2.35.65e06322uljeMu&file=rfc2104.txt).

        **Note:** Use the SHA1 algorithm to calculate the HMAC value of the string-to-sign. The AccessKey secret appended by an ampersand \(&\) \(ASCII code 38\) is used as the key for HMAC calculation.

    3.  Encode the HMAC value.

        Encode the HMAC value in [Base64](https://wenku.baidu.com/view/1b9ea72bed630b1c59eeb579.html?spm=a2c4g.11186623.2.36.65e06322evXY3s) to obtain the signature string.

    4.  Add the signature string.

        Add the signature string to the request as the `Signature` parameter. The result is the signed API request.

        **Note:** Before the signature string is added to the request as the Signature parameter, the string must be URL-encoded based on [RFC 3986](https://tools.ietf.org/html/rfc3986?spm=a2c4g.11186623.2.34.28e26322iVuuhj).


## Sample requests

1.  The GetVideoPlayAuth operation is used as an example. Assume that the `AccessKey ID` is `testAccessKeyId` and the `AccessKey secret` is `testAccessKeySecret`. The following example shows the request URL to be signed:

    ```
    http://vod.cn-shanghai.aliyuncs.com/?TimeStamp=2017-10-10T12:02:54Z&Format=JSON&AccessKeyId=testAccessKeyId&Action=GetVideoPlayAuth&SignatureMethod=HMAC-SHA1&SignatureNonce=8f8a035d-6496-4268-afd4-67c22837e38d&Version=2017-03-21&SignatureVersion=1.0&VideoId=5aed81b74ba84920be578cdfe004af4b
                
    ```

2.  The following string is the string-to-sign:

    ```
    GET&%2F&AccessKeyId%3DtestAccessKeyId%26Action%3DGetVideoPlayAuth%26Format%3DJSON%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D8f8a035d-6496-4268-afd4-67c22837e38d%26SignatureVersion%3D1.0%26Timestamp%3D2017-10-10T12%253A02%253A54Z%26Version%3D2017-03-21%26VideoId%3D5aed81b74ba84920be578cdfe004af4b
    
    ```

3.  The `AccessKey secret` is `testAccessKeySecret`. Therefore, the key used for the HMAC calculation is `testAccessKeySecret&`. The following string is the calculated signature string:

    ```
     Ibgh7y8Vp47LBuAsf5Xhi1SvDss%3D
                
    ```

4.  Add the signature string as the `Signature` parameter to the request URL. The following URL is the signed request URL:

    ```
    http://vod.cn-shanghai.aliyuncs.com?AccessKeyId=testAccessKeyId&Action=GetVideoPlayAuth&Format=JSON&SignatureMethod=HMAC-SHA1&SignatureNonce=8f8a035d-6496-4268-afd4-67c22837e38d&SignatureVersion=1.0&Timestamp=2017-10-10T12%3A02%3A54Z&Version=2017-03-21&VideoId=5aed81b74ba84920be578cdfe004af4b&Signature=Ibgh7y8Vp47LBuAsf5Xhi1SvDss%3D
    ```


## Sample code in Java

You must obtain a signature string, a timestamp, and a random number by writing code for each API request. The following code provides an example on how to obtain the values. For more information about how to set the remaining common request parameters, see the Common parameters topic.

**Note:** The following sample code can be used without a third-party library or package.

1.  Generate a signature string for the Signature parameter.

    1.  Create and encode a canonicalized query string.

        Create a canonicalized query string by arranging the request parameters in alphabetical order of the parameter names and perform URL encoding on the canonicalized query string. The following code provides an example:

        ```
        /* Perform URL encoding on all parameter names and values. */
        public static List<String> getAllParams(Map<String, String> publicParams, Map<String, String> privateParams) {
            List<String> encodeParams = new ArrayList<String>();
            if (publicParams ! = null) {
                for (String key : publicParams.keySet()) {
                    String value = publicParams.get(key);
                    // Perform URL encoding on the parameter name and value.
                    String encodeKey = percentEncode(key);
                    String encodeVal = percentEncode(value);
                    encodeParams.add(encodeKey + "=" + encodeVal);
                }
            }
            if (privateParams ! = null) {
                for (String key : privateParams.keySet()) {
                    String value = privateParams.get(key);
                    // Perform URL encoding on the parameter name and value.
                    String encodeKey = percentEncode(key);
                    String encodeVal = percentEncode(value);
                    encodeParams.add(encodeKey + "=" + encodeVal);
                }
            }
            return encodeParams;
        }
        /* Obtain the canonicalized query string. */
        public static String getCQS(List<String> allParams) {
            ParamsComparator paramsComparator = new ParamsComparator();
            Collections.sort(allParams, paramsComparator);
            String cqString = "";
            for (int i = 0; i < allParams.size(); i++) {
                cqString += allParams.get(i);
                if (i ! = allParams.size() - 1) {
                    cqString += "&";
                }
            }
            return cqString;
        }
        /* Use a parameter string comparator to arrange parameters in alphabetical order. */
        public static class ParamsComparator implements Comparator<String> {
            @Override
            public int compare(String lhs, String rhs) {
                return lhs.compareTo(rhs);
            }
        }
                    
        ```

    2.  The following code provides an example on how to construct a string-to-sign:

        ```
        /* Construct a string-to-sign. */
        String StringToSign = httpMethod + "&" + percentEncode("/") + "&" + percentEncode(CanonicalizedQueryString);
        /* Replace special characters with escape characters. */
        public static String percentEncode(String value) {
          try {
            String urlEncodeOrignStr = URLEncoder.encode(value, "UTF-8");
            String plusReplaced = urlEncodeOrignStr.replace("+", "%20");
            String starReplaced = plusReplaced.replace("*", "%2A");
            String waveReplaced = starReplaced.replace("%7E", "~");
            return waveReplaced;
          } catch (UnsupportedEncodingException e) {
            e.printStackTrace();
          }
          return value;
        }
                    
        ```

    3.  The following code provides an example on how to calculate the HMAC value of the string-to-sign:

        ```
        public static byte[] hmacSHA1Signature(String accessKeySecret, String stringToSign) {
            try {
                String key = accessKeySecret + "&";
                try {
                      SecretKeySpec signKey = new SecretKeySpec(key.getBytes(), "HmacSHA1");
                      Mac mac = Mac.getInstance("HmacSHA1");
                      mac.init(signKey);
                      return mac.doFinal(stringToSign.getBytes());
                } catch (Exception e) {
                      throw new SignatureException("Failed to generate HMAC : " + e.getMessage());
                }
            } catch (SignatureException e) {
                e.printStackTrace();
            }
            return null;
        }
                    
        ```

    4.  Encode the HMAC value to generate the signature string.

        The encoded value is the signature string. The following code provides an example on how to encode the HMAC value calculated in 1.3 into a string based on the Base64 encoding rules:

        ```
        public static String newStringByBase64(byte[] bytes)
                 throws UnsupportedEncodingException {
            if (bytes == null || bytes.length == 0) {
                return null;
            }
            return new String(new BASE64Encoder().encode(bytes));
        }
                    
        ```

2.  Generate a timestamp.

    Generate a UTC timestamp, such as 2017-10-10T12:02:54Z, for the TimeStamp parameter.

    ```
    /* Generate a UTC timestamp that represents the current UTC time. */
    public static String generateTimestamp() {
        Date date = new Date(System.currentTimeMillis());
        SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss'Z'");
        df.setTimeZone(new SimpleTimeZone(0, "GMT"));
        return df.format(date);
    }
                
    ```

3.  The following code provides an example on how to generate a random number for the SignatureNonce parameter:

    ```
    public static String generateRandom() {
        String signatureNonce = UUID.randomUUID().toString();
        return signatureNonce;
    }         
    ```


## References

You can use the server API SDKs so that you do not need to calculate a signature. The following SDKs in different languages are provided:

-   [JAVA SDK](/intl.en-US/Server SDK Reference/SDK for Java/Installation.md)
-   [Python SDK](/intl.en-US/Server SDK Reference/Python SDK/Installation.md)
-   [.NET SDK](/intl.en-US/Server SDK Reference/.NET SDK/Installation.md)
-   [Node.js](/intl.en-US/Server SDK Reference/Node.js SDK/Installation.md)
-   [Go SDK](/intl.en-US/Server SDK Reference/Go SDK/Installation.md)
-   [C/C++ SDK](/intl.en-US/Server SDK Reference/C/C++ SDK/Installation.md)

**Note:** The server API SDKs encapsulate the operations of the [ApsaraVideo VOD API](/intl.en-US/API Reference/List of operations by function.md) and provide sample code for you to call the operations.

## Other signature examples

If you need to calculate a signature, view the sample code of calculating a signature with Alibaba Cloud SDKs by clicking the following links:

-   [aliyun-openapi-php-sdk](https://github.com/aliyun/aliyun-openapi-php-sdk/blob/master/aliyun-php-sdk-core/RpcAcsRequest.php)
-   [aliyun-openapi-python-sdk](https://github.com/aliyun/aliyun-openapi-python-sdk/blob/master/aliyun-python-sdk-core/aliyunsdkcore/auth/composer/rpc_signature_composer.py)
-   [aliyun-openapi-net-sdk](https://github.com/aliyun/aliyun-openapi-net-sdk/blob/master/aliyun-net-sdk-core/Auth/RpcSignatureComposer.cs)
-   [alibaba-cloud-sdk-go](https://github.com/aliyun/alibaba-cloud-sdk-go/blob/master/sdk/auth/rpc_signature_composer.go)
-   [openapi-core-nodejs-sdk](https://github.com/aliyun/openapi-core-nodejs-sdk/blob/master/lib/rpc.js)
-   [aliyun-openapi-cpp-sdk](https://github.com/aliyun/aliyun-openapi-cpp-sdk/blob/master/core/src/RpcServiceClient.cc)

