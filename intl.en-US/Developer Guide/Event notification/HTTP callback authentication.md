# HTTP callback authentication

ApsaraVideo VOD allows you to add a specific signature header to each HTTP \(HTTPS\) callback request. In this way, the server that receives callback messages can authenticate the signature to prevent illegal or invalid requests. This topic describes the parameters, rules, and precautions of HTTP callback authentication.

## Authentication parameters

The following table lists the authentication parameters that can be added to HTTP callback request headers.

|Parameter|Description|
|---------|-----------|
|X-VOD-TIMESTAMP|The UNIX timestamp when the callback request is sent. The value is a 10-digit positive integer that represents the number of seconds that have elapsed since 00:00:00 Thursday, 1 January 1970.|
|X-VOD-SIGNATURE|The signature string, which is an MD5 value of 32 characters. For more information, see the following section.|

## Signature algorithm

The value of the X-VOD-SIGNATURE parameter is calculated based on the parameters listed in the following table.

|Parameter|Example|Description|
|---------|-------|-----------|
|Callback URL|https://www.example.com/your/callback|The callback URL that you configured.|
|X-VOD-TIMESTAMP|1519375990|The UNIX timestamp when the callback request is sent. The value is a 10-digit positive integer that represents the number of seconds that have elapsed since 00:00:00 Thursday, 1 January 1970.|
|PrivateKey|test123|The signature key that you specified.|

Concatenate the preceding three parameters by separating them with vertical bars \(\|\), and then calculate the MD5 value of the concatenated string. The MD5 value is used as the value of the X-VOD-SIGNATURE parameter.

```
MD5Content = Callback URL|X-VOD-TIMESTAMP|PrivateKey
X-VOD-SIGNATURE = md5sum(MD5Content)
```

Example:

```
X-VOD-SIGNATURE = md5sum(https://www.example.com/your/callback|1519375990|test123) = c72b60894140fa98920f1279219b****
```

## Authentication rules

-   The callback message receiving server concatenates the callback URL, X-VOD-TIMESTAMP, and PrivateKey into a string and calculates the MD5 value of the string. Then, the callback message receiving server compares the MD5 value with the obtained X-VOD-SIGNATURE value. If the two values are different, the callback message receiving server determines the request as invalid.
-   The callback message receiving server obtains the current time and calculates the difference between the current time and the time specified by the X-VOD-TIMESTAMP parameter in the callback request. If the time difference exceeds the value set by the server \(for example, 5 minutes\), the callback message receiving server determines the request as invalid.

    **Note:** The calculated time difference may be inaccurate due to incorrect time settings. Therefore, the time difference verification is optional. You can decide whether to enable it on the callback message receiving server.


## PrivateKey switching

If you change the PrivateKey value, the callback message receiving server must support authentication based on both the old and new keys to ensure the callback service is not affected. In this case, the callback message receiving server can implement authentication based on the old and new keys.

We recommend that you perform the following operations to switch the keys.

1.  Define a new value for the PrivateKey parameter.
2.  Upgrade the callback message receiving server so that it supports both the old and new keys.
3.  Update the PrivateKey to the new value in the ApsaraVideo VOD console.
4.  After a period of time, remove the support for the old key from the callback message receiving server.
5.  The PrivateKey value is changed.

## Other precautions

-   Callback authentication is optional. We recommend that you enable callback authentication. When the PrivateKey parameter is set, callback requests carry all authentication-related content for the callback message receiving server to perform authentication. You can determine whether to enable authentication on the server.
-   If you do not set the PrivateKey parameter, you can still use the callback service normally.

