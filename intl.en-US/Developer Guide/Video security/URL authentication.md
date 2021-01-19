# URL authentication

The URL authentication feature protects the content uploaded to ApsaraVideo VOD against illegal download and hotlinking. This feature can be configured in the ApsaraVideo VOD console. This topic describes the principle of and the method to implement URL authentication.

## Background information

To prevent hotlink issues, you can configure a Referer blacklist or whitelist to protect the security of origin resources. However, the Referer content can be forged. Therefore, URL authentication is a more effective method.

## Principles

URL authentication works with both origin servers and CDN nodes to protect origin servers from hotlink issues.

1.  The CDN node provide encrypted URLs for users. The encrypted URLs contain permission information to be verified.
2.  Users send signed URLs to CDN nodes.
3.  The CDN node verifies the permission information in the signed URL to determine the legality of the request. The CDN node responds to legal requests and rejects illegal requests. This protects the resources of CDN client sites.

## Configuration

You can configure URL authentication on the [Domain Names](https://vod.console.aliyun.com/#/domain/list) page in the console. For more information, see [URL signing](/intl.en-US/User Guide/Domain management/Access control/URL authentication.md).

-   After URL authentication is enabled, ApsaraVideo Player SDK and the API or SDK that is used to obtain playback URLs automatically generate playback URLs that have a validity period. To generate a dynamic signed URL, use the following authentication method:

    **Note:** After URL authentication is enabled, the URLs of video, audio, thumbnail, and snapshot files are signed.

-   The primary and secondary keys are equally effective. The secondary key is used to ensure a smooth switchover. If the primary key is changed, all the generated playback URLs that have the original primary key immediately become invalid. When you switch the primary key to the secondary key, the generated playback URLs that use the original primary key remain valid for a period of time. This ensures a smooth switchover. The secondary key is still available.
-   After you specify the Default Validity Period parameter for the required domain name, all URLs that use the domain name have the specified validity period. You can also customize the validity period for a single URL.

    **Note:** If the Default Validity Period parameter is specified, CDN appends the default validity period to the timestamp parameter value to determine the expiration time of a URL.


## Authentication methods

-   Signed URL structure

    A signed URL consists of a file URL and an access token \(auth\_key\). Example:

    ```
    http://DomainName/Filename?auth_key=timestamp-rand-uid-md5hash
    ```

    The value of the md5hash parameter in the access token is calculated by the MD5 algorithm based on the authentication key and expiration time. The access token has a specific validity period. The following table describes the timestamp, rand, uid, and md5hash parameters.

-   The following table describes the fields in a signed URL.

    |Field|Description|
    |-----|-----------|
    |timestamp|The URL expiration time. The value is a UNIX timestamp. The timestamp follows the UNIX time format. It is the number of seconds that have elapsed since 00:00:00 Thursday, 1 January 1970. CDN adds the value of the `Default Validity Period` parameter to the timestamp parameter value to determine the expiration time of a URL.When the time that is determined by the added values of the `Default Validity Period` parameter and the timestamp parameter elapses, a signed URL expires. In this case, CDN returns HTTP status code 403.

For example, if the timestamp parameter is set to 1597474800 \(15:00:00 August 15, 2020\) and the `Default Validity Period` parameter is set to 30 minutes, the actual expiration time is 15:30:00 August 15, 2020. |
    |rand|The random number. Typically, the value is set to 0. To generate a different URL each time, you can use the UUID as the random number.|
    |uid|The additional parameter. Typically, the value is set to 0.|
    |md5hash|The string that is calculated by using the MD5 algorithm. The string is 32 characters in length, and can contain digits and lowercase letters.    -   URI: the relative path of the requested file. The path excludes parameters. Example: /Filename.
    -   PrivateKey: the authentication key that is configured in the ApsaraVideo VOD console. The primary key or secondary key can be used.
    -   md5sum: the function that is used to calculate the MD5 hash. Use the MD5 hash calculation function that is provided by your development language.
Example:

    ```
sstring = "URI-timestamp-rand-uid-PrivateKey" 
md5hash = md5sum(sstring)
    ``` |

-   Examples

    Assumption:

    1.  The URL of the requested file. Example:

        ```
        http://192.168.0.0/16/video/standard/1K.html
        ```

    2.  Set the authentication key to aliyuncdnexp1234, which is the primary key or secondary key that is configured in the ApsaraVideo VOD console.
    3.  Set the expiration time of the signed URL to 00:00:00 October 10, 2015.
    4.  Both the rand and uid fields are set to 0.
    Result:

    1.  The calculated UNIX timestamp of the signed URL that has the specified expiration time is 1444435200.
    2.  The string that is used to calculate the md5hash value. Example:

        ```
        /video/standard/1K.html-1444435200-0-0-aliyuncdnexp1234"
        ```

    3.  Calculate the `md5hash` value. Example:

        ```
        md5hash = md5sum("/video/standard/1K.html-1444435200-0-0-aliyuncdnexp1234") = 80cd3862d699b7118eed99103f2a3a4f
        ```

    4.  The URL of the request. Example:

        ```
        http://cdn.example.com/video/standard/1K.html?auth_key=1444435200-0-0-80cd3862d699b7118eed99103f2a3a4f
        ```

        **Note:** In the preceding URL, the auth\_key parameter indicates the access token that is contained in the signed URL.


