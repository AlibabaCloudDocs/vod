# Appserver趣视频接口文档

您可以阅读本文了解视频点播Appserver趣视频接口，主要包括：凭证类、User、视频类、资源、回调通知类等。

## 返回值结构说明

所有请求均返回**JSON**格式的数据，所有API只描述**data**结构的数据。

|返回参数|类型|描述|
|----|--|--|
|requestId|string|服务端生成的本次请求ID|
|code|string|服务端生成的本次请求Code|
|message|string|服务端消息多用于描述错误原因|
|data|object|服务端返回的业务结构体数据，不同业务数据结构不同|

## 凭证类接口

-   getSts：通过Token获取STS权限。

    get url：/vod/getSts

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|

    返回参数

    |名称|类型|类型|
    |--|--|--|
    |expiration|string|上传授权过期时间，视频为3000秒，过期需要刷新上传凭证|
    |accessKeyId|string|访问密钥标识|
    |accessKeySecret|string|访问密钥|
    |securityToken|string|安全令牌|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "c17f13d1-4ce8-407f-a82b-c4799f84xxx",
        "message": "",
        "code": "200",
        "data": {
            "Expiration": "2018-12-28T08:26:13Z",
            "accessKeyId": "<yourAccessKeyId>",
            "securityToken": "CAIS9QF1q6Ft5B2yfSjIr4jhLujii5gV1LfYSBfj0UxhOPZNhrbNqTz2IHxFfnloBuwfvvw+lG5U6/cYlqFtTJMAX0vAYJP1A1OgZkfzDbDasumZsJY86vT8a0vxZjf/2MjNGZKbKPrWZvaqbX3diyZ32sGUXD6+XlujQ/Lr5IBgYoZVJEDaCwBLH9BLPABvhdYHPH/KT5aXPwXtn3DbATgF2GE0yytdkf3mmpbFtkaD1wamkLFO99rLT8L6P5U2DvBWSMyo2eF6TK3F3RNL5gJCnKUM1/AVo2ef4Y3EUwEAs0vabruO6L1xKwM8fK8+Fr7+RSREIHzq0xqAAZzSIQzyi/0dmEAJpmiUciXfX6sSSCYD/3NaNxLFG+mrImN+NjnAaR38cuXV50y/4WLc18RBmW9LmQ+fXd/DroAZRWXyFgIOp3KS8rR/YyOh2ghihCoLBjhyrIgaCsRUZTu2egpBx/B/nZu4fIwp9/NoMQ4kXzIcKlNNDMwFbNRr",
            "accessKeySecret": "<yourAccessKeySecret>"
        }
    }
    ```

-   getVideoUploadAuth：传入Token，标题和视频文件名等信息获取视频上传凭证。

    get url：/vod/getVideoUploadAuth

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |title|string|是|视频标题，长度不超过128个字节，UTF8编码|
    |fileName|string|是|视频源文件名，必须带扩展名，且扩展名不区分大小写，支持的扩展名参见上传概述的限制部分|
    |fileSize|string|否|视频文件大小，单位：字节|
    |description|string|否|视频描述|
    |coverURL|string|否|自定义视频封面URL地址|
    |tags|string|否|视频标签，多个标签用英文逗号（,）分隔|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |videoId|string|视频ID|
    |uploadAddress|string|上传地址|
    |uploadAuth|string|上传凭证|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "1490ee0b-3660-4d4c-be1b-9e1d4aadxxxx",
        "message": "",
        "code": "200",
        "data": {
            "videoId": "034813ff97984171a57aefe71c84xxxx",
            "uploadAddress": "eyJFbmRwb2ludCI6Imh0dHBzOi8vb3NzLWNuLXNoYW5naGFpLmFsaXl1bmNzLmNvbSIsIkJ1Y2tldCI6Im91dGluLTEyZWJlMDFmMDI5ZDExZTliNjMzMDAxNjNlMWM4ZGJhIiwiRmlsZU5hbWUiOiJzdi8yYzc1NzhkNy0xNjdmM2I3YTg4NS8yYzc1NzhkNy0xNjdmM2I3YTg4NS5tcDQifQ==",
            "uploadAuth": "eyJTZWN1cml0eVRva2VuIjoiQ0FJUzBBUjFxNkZ0NUIyeWZTaklyNGorR3RQZ283eDBnNWFxVVZQQnZuQmpYZjFvdXZMSWhUejJJSGxQZTNGaEFPb2V2L2svbVc5VTdmb2NsclVxRXNjZUhCQ1lNSkFyc3M0SnFsUC9KcGZadjh1ODRZQURpNUNqUWJkVjJlbHNtSjI4V2Y3d2FmK0FVQlhHQ1RtZDVNTVlvOWJUY1RHbFFDWnVXLy90b0pWN2I5TVJjeENsWkQ1ZGZybC9MUmRqcjhsbzF4R3pVUEcyS1V6U24zYjNCa2hsc1JZZTcyUms4dmFIeGRhQXpSRGNnVmJtcUpjU3ZKK2pDNEM4WXM5Z0c1MTlYdHlwdm9weGJiR1Q4Q05aNXo5QTlxcDlrTTQ5L2l6YzdQNlFIMzViNFJpTkw4L1o3dFFOWHdoaWZmb2JIYTlZcmZIZ21OaGx2dkRTajQzdDF5dFZPZVpjWDBha1E1dTdrdTdaSFArb0x0OGphWXZqUDNQRTNyTHBNWUx1NFQ0OFpYVVNPRHREWWNaRFVIaHJFazRSVWpYZEk2T2Y4VXJXU1FDN1dzcjIxN290ZzdGeXlrM3M4TWFIQWtXTFg3U0IyRHdFQjRjNGFFb2tWVzRSeG5lelc2VUJhUkJwYmxkN0JxNmNWNWxPZEJSWm9LK0t6UXJKVFg5RXoycExtdUQ2ZS9MT3M3b0RWSjM3V1p0S3l1aDRZNDlkNFU4clZFalBRcWl5a1QwcEZncGZUSzFSemJQbU5MS205YmFCMjUvelcrUGREZTBkc1Znb0lGS09waUdXRzNSTE5uK3p0Sjl4YmtlRStzS1VsZmJCK1o0NFNRVjJ2SUZUVkZpSUlOd3o5QWMrdS9Mc3RCbksrNy92V0hudDVYUi91UHVncHRjZnVCbzhJNjM3MmJUSzVtQ0E1MGI5Ty9kcHhKM2xQMFIwV2dteWRuQkR4L1NmdTJrS3ZSaHBrUnZ2WWsxQXN3WElqejdoSVoxR2phRFFtaTFlZm81WG1QWEZUUW1uOGw1cEFNbXkvNjB4WHVkdmJIL3U3RVVQSytrQ0dvQUJrcGhERlVGRUtGbEtsaUlFYk9BYk0wUmRGMlNabGw2WklpY0J3VUR3cmxRbGx1MW1XajB6OEZmb0hYeG50aGJZOXV5U0ZzeWYvOEVtWlhzZVR2eXNETldjNEhUNmdnMDZFWStPN2hSOENKN1MrZWNHL0hrVUl2azB6djZrZm5jc0xzZHlwVzVtS09adGdJRDRwbU9KMFdNWHZNVkN4dXVlNUw5dDlMTmM5RTQ9IiwiQWNjZXNzS2V5SWQiOiJTVFMuTktLUWlUTmNVNFRBU3VwWnA2UXJEVTdjZyIsIkV4cGlyZVVUQ1RpbWUiOiIyMDE4LTEyLTI4VDA4OjI5OjE5WiIsIkFjY2Vzc0tleVNlY3JldCI6IkdZTlZBbXJBQnE1VVNWWW5YbWI1QmlVeEZvQ2ZVYXpTQUw0dTRaMzFDRDVSIiwiRXhwaXJhdGlvbiI6IjM2MDAiLCJSZWdpb24iOiJjbi1zaGFuZ2hhaSJ9"
        }
    }
    ```

-   refreshVideoUploadAuth：刷新视频凭证。

    get url：/vod/refreshVideoUploadAuth

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |videoId|string|是|视频ID|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |uploadAddress|string|上传地址|
    |uploadAuth|string|上传凭证|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "efe66931-2a98-4bd9-9c46-e3a92eeexxxx",
        "message": "",
        "code": "200",
        "data": {
            "uploadAddress": "eyJFbmRwb2ludCI6Imh0dHBzOi8vb3NzLWNuLXNoYW5naGFpLmFsaXl1bmNzLmNvbSIsIkJ1Y2tldCI6Im91dGluLTEyZWJlMDFmMDI5ZDExZTliNjMzMDAxNjNlMWM4ZGJhIiwiRmlsZU5hbWUiOiJzdi8yYzc1NzhkNy0xNjdmM2I3YTg4NS8yYzc1NzhkNy0xNjdmM2I3YTg4NS5tcDQifQ==",
            "uploadAuth": "eyJTZWN1cml0eVRva2VuIjoiQ0FJUzBBUjFxNkZ0NUIyeWZTaklyNGorR3RQZ283eDBnNWFxVVZQQnZuQmpYZjFvdXZMSWhUejJJSGxQZTNGaEFPb2V2L2svbVc5VTdmb2NsclVxRXNjZUhCQ1lNSkFyc3M0SnFsUC9KcGZadjh1ODRZQURpNUNqUWJkVjJlbHNtSjI4V2Y3d2FmK0FVQlhHQ1RtZDVNTVlvOWJUY1RHbFFDWnVXLy90b0pWN2I5TVJjeENsWkQ1ZGZybC9MUmRqcjhsbzF4R3pVUEcyS1V6U24zYjNCa2hsc1JZZTcyUms4dmFIeGRhQXpSRGNnVmJtcUpjU3ZKK2pDNEM4WXM5Z0c1MTlYdHlwdm9weGJiR1Q4Q05aNXo5QTlxcDlrTTQ5L2l6YzdQNlFIMzViNFJpTkw4L1o3dFFOWHdoaWZmb2JIYTlZcmZIZ21OaGx2dkRTajQzdDF5dFZPZVpjWDBha1E1dTdrdTdaSFArb0x0OGphWXZqUDNQRTNyTHBNWUx1NFQ0OFpYVVNPRHREWWNaRFVIaHJFazRSVWpYZEk2T2Y4VXJXU1FDN1dzcjIxN290ZzdGeXlrM3M4TWFIQWtXTFg3U0IyRHdFQjRjNGFFb2tWVzRSeG5lelc2VUJhUkJwYmxkN0JxNmNWNWxPZEJSWm9LK0t6UXJKVFg5RXoycExtdUQ2ZS9MT3M3b0RWSjM3V1p0S3l1aDRZNDlkNFU4clZFalBRcWl5a1QwcEZncGZUSzFSemJQbU5MS205YmFCMjUvelcrUGREZTBkc1Znb0lGS09waUdXRzNSTE5uK3p0Sjl4YmtlRStzS1VsZmJCK1o0NFNRVjJ2SUZUVkZpSUlOd3o5QWMrdS9Mc3RCbksrNy92V0hudDVYUi91UHVncHRjZnVCbzhJNjM3MmJUSzVtQ0E1MGI5Ty9kcHhKM2xQMFIwV2dteWRuQkR4L1NmdTJrS3ZSaHBrUnZ2WWsxQXN3WElqejdoSVoxR2phRFFtaTFlZm81WG1QWEZUUW1uOGw1cEFNbXkvNjB4WHVkdmJIL3U3RVVQSytrQ0dvQUJrcGhERlVGRUtGbEtsaUlFYk9BYk0wUmRGMlNabGw2WklpY0J3VUR3cmxRbGx1MW1XajB6OEZmb0hYeG50aGJZOXV5U0ZzeWYvOEVtWlhzZVR2eXNETldjNEhUNmdnMDZFWStPN2hSOENKN1MrZWNHL0hrVUl2azB6djZrZm5jc0xzZHlwVzVtS09adGdJRDRwbU9KMFdNWHZNVkN4dXVlNUw5dDlMTmM5RTQ9IiwiQWNjZXNzS2V5SWQiOiJTVFMuTktLUWlUTmNVNFRBU3VwWnA2UXJEVTdjZyIsIkV4cGlyZVVUQ1RpbWUiOiIyMDE4LTEyLTI4VDA4OjI5OjE5WiIsIkFjY2Vzc0tleVNlY3JldCI6IkdZTlZBbXJBQnE1VVNWWW5YbWI1QmlVeEZvQ2ZVYXpTQUw0dTRaMzFDRDVSIiwiRXhwaXJhdGlvbiI6IjM1NDEiLCJSZWdpb24iOiJjbi1zaGFuZ2hhaSJ9"
        }
    }
    ```

-   getImageUploadAuth：传入Token，图片类型等信息获取图片上传凭证。

    get url：/vod/getImageUploadAuth

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |imageType|string|是|图片类型，取值：    -   default：默认
    -   cover：封面 |
    |imageExt|string|否|图片文件扩展名，默认值：png|
    |title|string|否|图片标题|
    |tags|string|否|图片标签，多个标签用英文逗号（,）分隔|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |uploadAddress|string|上传地址|
    |uploadAuth|string|上传凭证|
    |imageURL|string|图片地址|
    |imageId|string|图片ID|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "c9fc9bf0-b172-441c-9624-2b700204xxxx",
        "message": "",
        "code": "200",
        "data": {
            "uploadAddress": "eyJFbmRwb2ludCI6Imh0dHBzOi8vb3NzLWNuLXNoYW5naGFpLmFsaXl1bmNzLmNvbSIsIkJ1Y2tldCI6Im91dGluLTEyZWJlMDFmMDI5ZDExZTliNjMzMDAxNjNlMWM4ZGJhIiwiRmlsZU5hbWUiOiJpbWFnZS9jb3Zlci84RUI3MDMxODhGOUQ0OTIwQjZFM0ExREREQjc5N0I1MC02LTIuanBnIn0=",
            "uploadAuth": "eyJTZWN1cml0eVRva2VuIjoiQ0FJUzB3UjFxNkZ0NUIyeWZTaklyNG4rUHNEdHF1a1pnSWl2TUczcHNWSUVQOHRJM29uamhUejJJSGxQZTNGaEFPb2V2L2svbVc5VTdmb2NsclVxRXNjZUhCQ1lNSkFyc3M0SnFsUC9KcGZadjh1ODRZQURpNUNqUVljejU5WnNtSjI4V2Y3d2FmK0FVQkxHQ1RtZDVNQVlvOWJUY1RHbFFDWnVXLy90b0pWN2I5TVJjeENsWkQ1ZGZybC9MUmRqcjhsbzF4R3pVUEcyS1V6U24zYjNCa2hsc1JZZTcyUms4dmFIeGRhQXpSRGNnVmJtcUpjU3ZKK2pDNEM4WXM5Z0c1MTlYdHlwdm9weGJiR1Q4Q05aNXo5QTlxcDlrTTQ5L2l6YzdQNlFIMzViNFJpTkw4L1o3dFFOWHdoaWZmb2JIYTlZcmZIZ21OaGx2dkRTajQzdDF5dFZPZVpjWDBha1E1dTdrdTdaSFArb0x0OGphWXZqUDNQRTNyTHBNWUx1NFQ0OFpYVVNPRHREWWNaRFVIaHJFazRSVWpYZEk2T2Y4VXJXU1FDN1dzcjIxN290ZzdGeXlrM3M4TWFIQWtXTFg3U0IyRHdFQjRjNGFFb2tWVzRSeG5lelc2VUJhUkJwYmxkN0JxNmNWNWxPZEJSWm9LK0t6UXJKVFg5RXoycExtdUQ2ZS9MT3M3b0RWSjM3V1p0S3l1aDRZNDlkNFU4clZFalBRcWl5a1Qwa0ZncGZUSzFSemJQbU5MS205YmFCMjUvelcrUGREZTBkc1Znb0pWS0RwaUdXRzNSTE5uK3p0Sjl4YmtlRStzS1VsZmJCK1o0NFNRVjJ2SUZUVkZpSUlOd3o5QWMrdS9Mc3RCbksrNy92V0hudC8yOHg5ZFNmdmFzM3NCVTBMNmI4M3JYTjVHV0c1Q0xPT3BOVXdwbUhCRGRkSmoyc1lHRjh6ZnlvZ1hZS21nc01pV25jT1d4RXNnL09qVGZwSnBWS2o2eldtUzhmWHZsSjVjM2NTaWE5K0Z0bkJlbUE2cTB3UmZoWWUrUkRRbWtjWTdMYU1CV01Hb0FCRDlpdzM2ZENFcmJMUFRUb3JaYi9lL0NYQW12YjdVWHFySTZWNHFNWmJLYk1WMzU1ZWR4Ni9WM21kd0p0VHdOMHF5NXFNTFFvSXdZem56bmZkaFZ4U0ZObVA2aFVlU204Q1ZkSUJMUVFwaWZxR2hyVDJRTEtadVVxTHplRDBqU01FUllnclNZRGo3cVRJUUM1aVZ5T2l3K0dORGxscmlUREwvV1BXQkVMSVFBPSIsIkFjY2Vzc0tleUlkIjoiU1RTLk5KS3V6WUc2ODdKRDJLWFVSUTNEZDFMSGciLCJFeHBpcmVVVENUaW1lIjoiMjAxOC0xMi0yOFQwODo0OTozNFoiLCJBY2Nlc3NLZXlTZWNyZXQiOiJIMWlkWUFucXFQaDNIQWs1dFpDaUJjRzJpQTdRSm1pM01pM25OQjc4Z3ZkVCIsIkV4cGlyYXRpb24iOiIzNTY2IiwiUmVnaW9uIjoiY24tc2hhbmdoYWkifQ==",
            "imageId": "76ac9d24882544e7a2b94758d34bceac",
            "imageURL": "https://outin-12ebe01f029d11e9b63300163e1c8dba.oss-cn-shanghai.aliyuncs.com/image/cover/8EB703188F9D4920B6E3A1DDDB797B50-6-2.jpg?Expires=1545987008&OSSAccessKeyId=XXXXXXX&Signature=cb6kwDuABBH%2FUDk7qviXy0MC2mE%3D"
        }
    }
    ```


## 凭证类（无Token）

-   getSts：获取STS权限。

    get url：/demo/getSts

    返回参数

    |名称|类型|类型|
    |--|--|--|
    |expiration|string|上传授权过期时间，视频为3000秒，过期需要刷新上传凭证|
    |accessKeyId|string|访问密钥标志|
    |accessKeySecret|string|访问密钥|
    |securityToken|string|安全令牌|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "c17f13d1-4ce8-407f-a82b-c4799f84xxxx",
        "message": "",
        "code": "200",
        "data": {
            "Expiration": "2018-12-28T08:26:13Z",
            "accessKeyId": "<yourAccessKeyId>",
            "securityToken": "CAIS9QF1q6Ft5B2yfSjIr4jhLujii5gV1LfYSBfj0UxhOPZNhrbNqTz2IHxFfnloBuwfvvw+lG5U6/cYlqFtTJMAX0vAYJP1A1OgZkfzDbDasumZsJY86vT8a0vxZjf/2MjNGZKbKPrWZvaqbX3diyZ32sGUXD6+XlujQ/Lr5IBgYoZVJEDaCwBLH9BLPABvhdYHPH/KT5aXPwXtn3DbATgF2GE0yytdkf3mmpbFtkaD1wamkLFO99rLT8L6P5U2DvBWSMyo2eF6TK3F3RNL5gJCnKUM1/AVo2ef4Y3EUwEAs0vabruO6L1xKwM8fK8+Fr7+RSREIHzq0xqAAZzSIQzyi/0dmEAJpmiUciXfX6sSSCYD/3NaNxLFG+mrImN+NjnAaR38cuXV50y/4WLc18RBmW9LmQ+fXd/DroAZRWXyFgIOp3KS8rR/YyOh2ghihCoLBjhyrIgaCsRUZTu2egpBx/B/nZu4fIwp9/NoMQ4kXzIcKlNNDMwFbNRr",
            "accessKeySecret": "<yourAccessKeySecret>"
        }
    }
    ```

-   getVideoUploadAuth：传入标题和视频文件名等信息获取视频上传凭证。

    get url：/demo/getVideoUploadAuth

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |title|string|是|视频标题，长度不超过128个字节，UTF8编码|
    |fileName|string|是|视频源文件名，必须带扩展名，且扩展名不区分大小写，支持的扩展名参见上传概述的限制部分|
    |fileSize|string|否|视频文件大小，单位：字节|
    |description|string|否|视频描述|
    |coverURL|string|否|自定义视频封面URL地址|
    |tags|string|否|视频标签，多个标签用英文逗号（,）分隔|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |videoId|string|视频ID|
    |uploadAddress|string|上传地址|
    |uploadAuth|string|上传凭证|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "1490ee0b-3660-4d4c-be1b-9e1d4aadxxxx",
        "message": "",
        "code": "200",
        "data": {
            "videoId": "034813ff97984171a57aefe71c84xxxx",
            "uploadAddress": "eyJFbmRwb2ludCI6Imh0dHBzOi8vb3NzLWNuLXNoYW5naGFpLmFsaXl1bmNzLmNvbSIsIkJ1Y2tldCI6Im91dGluLTEyZWJlMDFmMDI5ZDExZTliNjMzMDAxNjNlMWM4ZGJhIiwiRmlsZU5hbWUiOiJzdi8yYzc1NzhkNy0xNjdmM2I3YTg4NS8yYzc1NzhkNy0xNjdmM2I3YTg4NS5tcDQifQ==",
            "uploadAuth": "eyJTZWN1cml0eVRva2VuIjoiQ0FJUzBBUjFxNkZ0NUIyeWZTaklyNGorR3RQZ283eDBnNWFxVVZQQnZuQmpYZjFvdXZMSWhUejJJSGxQZTNGaEFPb2V2L2svbVc5VTdmb2NsclVxRXNjZUhCQ1lNSkFyc3M0SnFsUC9KcGZadjh1ODRZQURpNUNqUWJkVjJlbHNtSjI4V2Y3d2FmK0FVQlhHQ1RtZDVNTVlvOWJUY1RHbFFDWnVXLy90b0pWN2I5TVJjeENsWkQ1ZGZybC9MUmRqcjhsbzF4R3pVUEcyS1V6U24zYjNCa2hsc1JZZTcyUms4dmFIeGRhQXpSRGNnVmJtcUpjU3ZKK2pDNEM4WXM5Z0c1MTlYdHlwdm9weGJiR1Q4Q05aNXo5QTlxcDlrTTQ5L2l6YzdQNlFIMzViNFJpTkw4L1o3dFFOWHdoaWZmb2JIYTlZcmZIZ21OaGx2dkRTajQzdDF5dFZPZVpjWDBha1E1dTdrdTdaSFArb0x0OGphWXZqUDNQRTNyTHBNWUx1NFQ0OFpYVVNPRHREWWNaRFVIaHJFazRSVWpYZEk2T2Y4VXJXU1FDN1dzcjIxN290ZzdGeXlrM3M4TWFIQWtXTFg3U0IyRHdFQjRjNGFFb2tWVzRSeG5lelc2VUJhUkJwYmxkN0JxNmNWNWxPZEJSWm9LK0t6UXJKVFg5RXoycExtdUQ2ZS9MT3M3b0RWSjM3V1p0S3l1aDRZNDlkNFU4clZFalBRcWl5a1QwcEZncGZUSzFSemJQbU5MS205YmFCMjUvelcrUGREZTBkc1Znb0lGS09waUdXRzNSTE5uK3p0Sjl4YmtlRStzS1VsZmJCK1o0NFNRVjJ2SUZUVkZpSUlOd3o5QWMrdS9Mc3RCbksrNy92V0hudDVYUi91UHVncHRjZnVCbzhJNjM3MmJUSzVtQ0E1MGI5Ty9kcHhKM2xQMFIwV2dteWRuQkR4L1NmdTJrS3ZSaHBrUnZ2WWsxQXN3WElqejdoSVoxR2phRFFtaTFlZm81WG1QWEZUUW1uOGw1cEFNbXkvNjB4WHVkdmJIL3U3RVVQSytrQ0dvQUJrcGhERlVGRUtGbEtsaUlFYk9BYk0wUmRGMlNabGw2WklpY0J3VUR3cmxRbGx1MW1XajB6OEZmb0hYeG50aGJZOXV5U0ZzeWYvOEVtWlhzZVR2eXNETldjNEhUNmdnMDZFWStPN2hSOENKN1MrZWNHL0hrVUl2azB6djZrZm5jc0xzZHlwVzVtS09adGdJRDRwbU9KMFdNWHZNVkN4dXVlNUw5dDlMTmM5RTQ9IiwiQWNjZXNzS2V5SWQiOiJTVFMuTktLUWlUTmNVNFRBU3VwWnA2UXJEVTdjZyIsIkV4cGlyZVVUQ1RpbWUiOiIyMDE4LTEyLTI4VDA4OjI5OjE5WiIsIkFjY2Vzc0tleVNlY3JldCI6IkdZTlZBbXJBQnE1VVNWWW5YbWI1QmlVeEZvQ2ZVYXpTQUw0dTRaMzFDRDVSIiwiRXhwaXJhdGlvbiI6IjM2MDAiLCJSZWdpb24iOiJjbi1zaGFuZ2hhaSJ9"
        }
    }
    ```

-   refreshVideoUploadAuth：刷新视频凭证。

    get url：/demo/refreshVideoUploadAuth

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |videoId|string|是|视频ID|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |uploadAddress|string|上传地址|
    |uploadAuth|string|上传凭证|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "efe66931-2a98-4bd9-9c46-e3a92eeexxxx",
        "message": "",
        "code": "200",
        "data": {
            "uploadAddress": "eyJFbmRwb2ludCI6Imh0dHBzOi8vb3NzLWNuLXNoYW5naGFpLmFsaXl1bmNzLmNvbSIsIkJ1Y2tldCI6Im91dGluLTEyZWJlMDFmMDI5ZDExZTliNjMzMDAxNjNlMWM4ZGJhIiwiRmlsZU5hbWUiOiJzdi8yYzc1NzhkNy0xNjdmM2I3YTg4NS8yYzc1NzhkNy0xNjdmM2I3YTg4NS5tcDQifQ==",
            "uploadAuth": "eyJTZWN1cml0eVRva2VuIjoiQ0FJUzBBUjFxNkZ0NUIyeWZTaklyNGorR3RQZ283eDBnNWFxVVZQQnZuQmpYZjFvdXZMSWhUejJJSGxQZTNGaEFPb2V2L2svbVc5VTdmb2NsclVxRXNjZUhCQ1lNSkFyc3M0SnFsUC9KcGZadjh1ODRZQURpNUNqUWJkVjJlbHNtSjI4V2Y3d2FmK0FVQlhHQ1RtZDVNTVlvOWJUY1RHbFFDWnVXLy90b0pWN2I5TVJjeENsWkQ1ZGZybC9MUmRqcjhsbzF4R3pVUEcyS1V6U24zYjNCa2hsc1JZZTcyUms4dmFIeGRhQXpSRGNnVmJtcUpjU3ZKK2pDNEM4WXM5Z0c1MTlYdHlwdm9weGJiR1Q4Q05aNXo5QTlxcDlrTTQ5L2l6YzdQNlFIMzViNFJpTkw4L1o3dFFOWHdoaWZmb2JIYTlZcmZIZ21OaGx2dkRTajQzdDF5dFZPZVpjWDBha1E1dTdrdTdaSFArb0x0OGphWXZqUDNQRTNyTHBNWUx1NFQ0OFpYVVNPRHREWWNaRFVIaHJFazRSVWpYZEk2T2Y4VXJXU1FDN1dzcjIxN290ZzdGeXlrM3M4TWFIQWtXTFg3U0IyRHdFQjRjNGFFb2tWVzRSeG5lelc2VUJhUkJwYmxkN0JxNmNWNWxPZEJSWm9LK0t6UXJKVFg5RXoycExtdUQ2ZS9MT3M3b0RWSjM3V1p0S3l1aDRZNDlkNFU4clZFalBRcWl5a1QwcEZncGZUSzFSemJQbU5MS205YmFCMjUvelcrUGREZTBkc1Znb0lGS09waUdXRzNSTE5uK3p0Sjl4YmtlRStzS1VsZmJCK1o0NFNRVjJ2SUZUVkZpSUlOd3o5QWMrdS9Mc3RCbksrNy92V0hudDVYUi91UHVncHRjZnVCbzhJNjM3MmJUSzVtQ0E1MGI5Ty9kcHhKM2xQMFIwV2dteWRuQkR4L1NmdTJrS3ZSaHBrUnZ2WWsxQXN3WElqejdoSVoxR2phRFFtaTFlZm81WG1QWEZUUW1uOGw1cEFNbXkvNjB4WHVkdmJIL3U3RVVQSytrQ0dvQUJrcGhERlVGRUtGbEtsaUlFYk9BYk0wUmRGMlNabGw2WklpY0J3VUR3cmxRbGx1MW1XajB6OEZmb0hYeG50aGJZOXV5U0ZzeWYvOEVtWlhzZVR2eXNETldjNEhUNmdnMDZFWStPN2hSOENKN1MrZWNHL0hrVUl2azB6djZrZm5jc0xzZHlwVzVtS09adGdJRDRwbU9KMFdNWHZNVkN4dXVlNUw5dDlMTmM5RTQ9IiwiQWNjZXNzS2V5SWQiOiJTVFMuTktLUWlUTmNVNFRBU3VwWnA2UXJEVTdjZyIsIkV4cGlyZVVUQ1RpbWUiOiIyMDE4LTEyLTI4VDA4OjI5OjE5WiIsIkFjY2Vzc0tleVNlY3JldCI6IkdZTlZBbXJBQnE1VVNWWW5YbWI1QmlVeEZvQ2ZVYXpTQUw0dTRaMzFDRDVSIiwiRXhwaXJhdGlvbiI6IjM1NDEiLCJSZWdpb24iOiJjbi1zaGFuZ2hhaSJ9"
        }
    }
    ```

-   getVideoPlayAuth：获取视频播放凭证。

    get url：/demo/getVideoPlayAuth

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |videoId|string|是|视频ID|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |coverURL|string|封面地址|
    |duration|string|视频大小|
    |videoId|string|视频ID|
    |playAuth|string|播放凭证|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "b766e688-1fee-4635-9ed8-e86529d8xxxx",
        "message": "",
        "code": "200",
        "data": {
            "coverURL": "https://alivc-demo-vod.aliyuncs.com/5ef00e3c0ef24547a6dcff851be0b6ab/snapshots/a02dfc16dfab48a6ae27529edc906cd7-00002.jpg",
            "duration": "10.4167",
            "videoId": "5ef00e3c0ef24547a6dcff851be0xxxx",
            "playAuth": "eyJTZWN1cml0eVRva2VuIjoiQ0FJUzN3SjFxNkZ0NUIyeWZTaklyNG41SDhueGhvd1MrN2UvTkczNm9EZzJTczF1bUpidWxqejJJSGxQZTNGaEFPb2V2L2svbVc5VTdmb2Nsck1xRXNjZUhCQ1lNSkFyc3M0SnFsUC9KcExGc3QySjZyOEpqc1ZHeEpkTDVsdXBzdlhKYXNEVkVma3VFNVhFTWlJNS8wMGU2TC8rY2lyWVhEN0JHSmFWaUpsaFE4MEtWdzJqRjFSdkQ4dFhJUTBRazYxOUszemRaOW1nTGlidWkzdnhDa1J2MkhCaWptOHR4cW1qL015UTV4MzFpMXYweStCM3dZSHRPY3FjYThCOU1ZMVdUc3Uxdm9oemFyR1Q2Q3BaK2psTStxQVU2cWxZNG1YcnM5cUhFa0ZOd0JpWFNaMjJsT2RpTndoa2ZLTTNOcmRacGZ6bjc1MUN0L2ZVaXA3OHhtUW1YNGdYY1Z5R0d0RHhrWk9aUXJ6emJZNWhLK2lnQVJtWGpJRFRiS3VTbWhnL2ZIY1dPRGxOZjljY01YSnFBWFF1TUdxRGNmRC9xUW1RT2xiK0cvWGFqUHBxajRBSjVsSHA3TWVNR1YrRGVMeVF5aDBFSWFVN2EwNDRxTDZvYnQ4WG1zUWFnQUVyWk03Z3BsL2hta01MM0d1WW5pK1RValZDdlF0bTdiOGpRZEJUN3pmZGxIV0RJa282REZ6T3VWckFLMDRSWjgxTkJEOG1wbWp6a0Q4RXozWVVQcWJkVmNOZGJzWVBKS1kyTnMyNDZRc2Q3U01STi9uR3h2NDJMU2xnejJyVytEa3E5UWYrYnJ5RklNUFNIWWNkY3o2QlZVN3diVWRuOHRXWmd5dUs1UlFtNGc9PSIsIkF1dGhJbmZvIjoie1wiQ2FsbGVyXCI6XCJQZG93YUpCVnMzSm9ySXBRMmNqS1JTNFo3cGRyZHFHeXBTUWVFMXZ6V05vPVxcclxcblwiLFwiRXhwaXJlVGltZVwiOlwiMjAxOS0wMS0xNlQwODo0NTo1M1pcIixcIk1lZGlhSWRcIjpcIjVlZjAwZTNjMGVmMjQ1NDdhNmRjZmY4NTFiZTBiNmFiXCIsXCJQbGF5RG9tYWluXCI6XCJhbGl2Yy1kZW1vLXZvZC5hbGl5dW5jcy5jb21cIixcIlNpZ25hdHVyZVwiOlwiNTZvRVJoRHBKbXZXQ0xaSUlvb1A3MFozQXFNPVwifSIsIlZpZGVvTWV0YSI6eyJTdGF0dXMiOiJOb3JtYWwiLCJWaWRlb0lkIjoiNWVmMDBlM2MwZWYyNDU0N2E2ZGNmZjg1MWJlMGI2YWIiLCJUaXRsZSI6IuWknOaZrzIiLCJDb3ZlclVSTCI6Imh0dHBzOi8vYWxpdmMtZGVtby12b2QuYWxpeXVuY3MuY29tLzVlZjAwZTNjMGVmMjQ1NDdhNmRjZmY4NTFiZTBiNmFiL3NuYXBzaG90cy9hMDJkZmMxNmRmYWI0OGE2YWUyNzUyOWVkYzkwNmNkNy0wMDAwMi5qcGciLCJEdXJhdGlvbiI6MTAuNDE2N30sIkFjY2Vzc0tleUlkIjoiU1RTLk5KTFRzRWtTM0x1VDZLS0Q4Y0ZCQndTRXQiLCJQbGF5RG9tYWluIjoiYWxpdmMtZGVtby12b2QuYWxpeXVuY3MuY29tIiwiQWNjZXNzS2V5U2VjcmV0IjoiOXcyNVlDeXVyblpxM2YyN3ZBQTNxZVJhYWZVSzhvVTFuUXN2aGJ3UUhVR0giLCJSZWdpb24iOiJjbi1zaGFuZ2hhaSIsIkN1c3RvbWVySWQiOjExMDMxNDQ1MzM0MjYzODZ9"
        }
    }
    ```

-   getImageUploadAuth： 传入图片类型等信息获取图片上传凭证。

    get url：/demo/getImageUploadAuth

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |imageType|string|是|图片类型，取值：    -   default：默认
    -   cover：封面 |
    |imageExt|string|否|图片文件扩展名，默认值：png|
    |title|string|否|图片标题|
    |tags|string|否|图片标签，多个标签用英文逗号（,）分隔|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |uploadAddress|string|上传地址|
    |uploadAuth|string|上传凭证|
    |imageURL|string|图片地址|
    |imageId|string|图片ID|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "c9fc9bf0-b172-441c-9624-2b700204xxxx",
        "message": "",
        "code": "200",
        "data": {
            "uploadAddress": "eyJFbmRwb2ludCI6Imh0dHBzOi8vb3NzLWNuLXNoYW5naGFpLmFsaXl1bmNzLmNvbSIsIkJ1Y2tldCI6Im91dGluLTEyZWJlMDFmMDI5ZDExZTliNjMzMDAxNjNlMWM4ZGJhIiwiRmlsZU5hbWUiOiJpbWFnZS9jb3Zlci84RUI3MDMxODhGOUQ0OTIwQjZFM0ExREREQjc5N0I1MC02LTIuanBnIn0=",
            "uploadAuth": "eyJTZWN1cml0eVRva2VuIjoiQ0FJUzB3UjFxNkZ0NUIyeWZTaklyNG4rUHNEdHF1a1pnSWl2TUczcHNWSUVQOHRJM29uamhUejJJSGxQZTNGaEFPb2V2L2svbVc5VTdmb2NsclVxRXNjZUhCQ1lNSkFyc3M0SnFsUC9KcGZadjh1ODRZQURpNUNqUVljejU5WnNtSjI4V2Y3d2FmK0FVQkxHQ1RtZDVNQVlvOWJUY1RHbFFDWnVXLy90b0pWN2I5TVJjeENsWkQ1ZGZybC9MUmRqcjhsbzF4R3pVUEcyS1V6U24zYjNCa2hsc1JZZTcyUms4dmFIeGRhQXpSRGNnVmJtcUpjU3ZKK2pDNEM4WXM5Z0c1MTlYdHlwdm9weGJiR1Q4Q05aNXo5QTlxcDlrTTQ5L2l6YzdQNlFIMzViNFJpTkw4L1o3dFFOWHdoaWZmb2JIYTlZcmZIZ21OaGx2dkRTajQzdDF5dFZPZVpjWDBha1E1dTdrdTdaSFArb0x0OGphWXZqUDNQRTNyTHBNWUx1NFQ0OFpYVVNPRHREWWNaRFVIaHJFazRSVWpYZEk2T2Y4VXJXU1FDN1dzcjIxN290ZzdGeXlrM3M4TWFIQWtXTFg3U0IyRHdFQjRjNGFFb2tWVzRSeG5lelc2VUJhUkJwYmxkN0JxNmNWNWxPZEJSWm9LK0t6UXJKVFg5RXoycExtdUQ2ZS9MT3M3b0RWSjM3V1p0S3l1aDRZNDlkNFU4clZFalBRcWl5a1Qwa0ZncGZUSzFSemJQbU5MS205YmFCMjUvelcrUGREZTBkc1Znb0pWS0RwaUdXRzNSTE5uK3p0Sjl4YmtlRStzS1VsZmJCK1o0NFNRVjJ2SUZUVkZpSUlOd3o5QWMrdS9Mc3RCbksrNy92V0hudC8yOHg5ZFNmdmFzM3NCVTBMNmI4M3JYTjVHV0c1Q0xPT3BOVXdwbUhCRGRkSmoyc1lHRjh6ZnlvZ1hZS21nc01pV25jT1d4RXNnL09qVGZwSnBWS2o2eldtUzhmWHZsSjVjM2NTaWE5K0Z0bkJlbUE2cTB3UmZoWWUrUkRRbWtjWTdMYU1CV01Hb0FCRDlpdzM2ZENFcmJMUFRUb3JaYi9lL0NYQW12YjdVWHFySTZWNHFNWmJLYk1WMzU1ZWR4Ni9WM21kd0p0VHdOMHF5NXFNTFFvSXdZem56bmZkaFZ4U0ZObVA2aFVlU204Q1ZkSUJMUVFwaWZxR2hyVDJRTEtadVVxTHplRDBqU01FUllnclNZRGo3cVRJUUM1aVZ5T2l3K0dORGxscmlUREwvV1BXQkVMSVFBPSIsIkFjY2Vzc0tleUlkIjoiU1RTLk5KS3V6WUc2ODdKRDJLWFVSUTNEZDFMSGciLCJFeHBpcmVVVENUaW1lIjoiMjAxOC0xMi0yOFQwODo0OTozNFoiLCJBY2Nlc3NLZXlTZWNyZXQiOiJIMWlkWUFucXFQaDNIQWs1dFpDaUJjRzJpQTdRSm1pM01pM25OQjc4Z3ZkVCIsIkV4cGlyYXRpb24iOiIzNTY2IiwiUmVnaW9uIjoiY24tc2hhbmdoYWkifQ==",
            "imageId": "76ac9d24882544e7a2b94758d34bxxxx",
            "imageURL": "https://outin-12ebe01f029d11e9b63300163e1c8dba.oss-cn-shanghai.aliyuncs.com/image/cover/8EB703188F9D4920B6E3A1DDDB797B50-6-2.jpg?Expires=1545987008&OSSAccessKeyId=XXXXXXXX&Signature=cb6kwDuABBH%2FUDk7qviXy0MC2mE%3D"
        }
    }
    ```


## User接口

-   login：用户登录。

    get url：/user/login

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |username|string|是|用户名|
    |password|string|是|密码|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |token|string|用户系统的Token|

    返回示例

    ```
    {
        "result": "true",
        "code": "200",
        "requestId": "ad5ce518-aafd-47ef-bd42-36a809a1xxxx",
        "message": null,
        "data": {}
    }
    }
    ```

-   register：用户注册。

    get url：/user/register

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |username|string|是|用户名|
    |password|string|是|密码|

    返回示例

    ```
    {
        "result": "true",
        "code": "200",
        "requestId": "ad5ce518-aafd-47ef-bd42-36a809a1xxxx",
        "message": null,
        "data": {}
    }
    }
    ```

-   updateUser：修改用户名。

    post url：/user/updateUser

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |userId|string|是|用户ID|
    |nickname|string|是|用户昵称|

    返回示例

    ```
    {
        "result": "true",
        "code": "200",
        "requestId": "ad5ce518-aafd-47ef-bd42-36a809a1xxxx",
        "message": null,
        "data": {}
    }
    }
    ```

-   randomUser：生成随机用户，包括：用户ID、Token、用户昵称、用户头像、推流地址、FLV播放地址和HLS播放地址。

    get url：/user/randomUser

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |userId|string|用户ID|
    |token|string|用户系统的Token|
    |nickName|string|用户昵称|
    |avatar|string|用户头像|
    |gmtCreate|string|创建时间|
    |gmtModified|string|修改时间|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "d5b1f423-0186-41d0-bf20-98606472xxxx",
        "message": null,
        "data": {
            "id": "37",
            "userId": "243124930xxxx",
            "token": "234fwef23-fsdf4f7-ahjktghsrt65ujs87rukmslsgbfxlry91",
            "nickName": "8313e974-f6a8-4527-af6e-8b4c3a4f1xxxx",
            "gmtCreate": "2018-11-16 15:40:18",
            "gmtModified": ""
        }
    }
    ```


## 视频类接口

-   videoPublish：视频发布（向后台插入上传的视频，届时个人中心能够查看发布的视频）。

    post url：/vod/videoPublish

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |title|string|否|视频标题|
    |videoId|string|否|视频ID|
    |description|string|否|视频描述|
    |duration|float|否|视频时长，单位：秒|
    |coverUrl|string|否|视频封面URL|
    |size|int|否|视频源文件大小，单位：字节|
    |tags|string|否|视频标签，多个标签用英文逗号（,）分隔|
    |cateId|int|否|视频分类|
    |cateName|string|否|视频分类名称|

    返回示例

    ```
    {
        "result": "true",
        "code": "200",
        "requestId": "ad5ce518-aafd-47ef-bd42-36a809a1xxxx",
        "message": null,
        "data": {}
    }
    }
    ```

-   getRecommendVideoList：获取推荐视频。

    get url：/vod/getRecommendVideoList

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |pageIndex|int|是|起始页|
    |pageSize|int|是|每页条数|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |total|string|视频总条数|
    |videoList|List<[Video](/cn.zh-CN/趣视频解决方案/后端服务集成说明/数据类型.md)\>|视频信息列表|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "27596e99-0083-4701-80b5-90969f55xxxx",
        "message": "",
        "code": "200",
        "data": {
            "total": 59,
            "videoList": [{
                "id": "110",
                "videoId": "a34f34e0fc744d00a5269e8a7c6a60c7",
                "title": "热气球",
                "description": "热气球",
                "duration": 7,
                "coverUrl": "https://alivc-demo-vod.aliyuncs.com/a34f34e0fc744d00a5269e8a7c6a60c7/snapshots/0c3a4b0e8f37494f83202d6e6bb83ecc-00001.jpg",
                "creationTime": "",
                "status": "1",
                "firstFrameUrl": "https://alivc-demo-vod.aliyuncs.com/a34f34e0fc744d00a5269e8a7c6a60c7/snapshots/0c3a4b0e8f37494f83202d6e6bb83ecc-00001.jpg",
                "size": 389938,
                "cateId": 1,
                "cateName": "推荐列表",
                "tags": "热气球",
                "shareUrl": "",
                "user": {
                    "userId": "2435470766044",
                    "userName": "",
                    "avatarUrl": ""
                },
                "transcodeStatus": "",
                "snapshotStatus": "",
                "censorStatus": "",
                "narrowTranscodeStatus": "",
                "fileUrl": "https://alivc-demo-vod.aliyuncs.com/a34f34e0fc744d00a5269e8a7c6a60c7/02528a756dd04693dc3c44d68b1bcf28-fd.mp4"
            },
            {
                "id": "109",
                "videoId": "febc0388fab9491d8199bdad1958b756",
                "title": "沙滩椅",
                "description": "沙滩椅",
                "duration": 16,
                "coverUrl": "https://alivc-demo-vod.aliyuncs.com/febc0388fab9491d8199bdad1958b756/snapshots/6b6ad9bfc80d4bc49f96e6111cbffd02-00002.jpg",
                "creationTime": "",
                "status": "1",
                "firstFrameUrl": "https://alivc-demo-vod.aliyuncs.com/febc0388fab9491d8199bdad1958b756/snapshots/6b6ad9bfc80d4bc49f96e6111cbffd02-00002.jpg",
                "size": 2763135,
                "cateId": 1,
                "cateName": "推荐列表",
                "tags": "沙滩椅",
                "shareUrl": "",
                "user": {
                    "userId": "243547076xxxx",
                    "userName": "",
                    "avatarUrl": ""
                },
                "transcodeStatus": "",
                "snapshotStatus": "",
                "censorStatus": "",
                "narrowTranscodeStatus": "",
                "fileUrl": "https://alivc-demo-vod.aliyuncs.com/a34f34e0fc744d00a5269e8a7c6a60c7/02528a756dd04693dc3c44d68b1bcf28-fd.mp4"
            }]
        }
    }
    ```

-   getPersonalVideoList：获取个人中心视频。

    get url：/vod/getPersonalVideoList

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |pageIndex|int|是|起始页（从1开始）|
    |pageSize|int|是|每页条数|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |total|string|视频总条数|
    |videoList|List<[Video](/cn.zh-CN/趣视频解决方案/后端服务集成说明/数据类型.md)\>|个人中心视频信息列表|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "c3bcb60d-e85f-4e19-a50a-16bedb56xxxx",
        "message": "",
        "code": "200",
        "data": {
            "total": 7,
            "videoList": [{
                "id": "25",
                "videoId": "23rfewc23",
                "title": "test video",
                "description": "test33",
                "duration": 12,
                "coverUrl": "https://alivc-demo-vod.aliyuncs.com/image9sfsa0-dfcoverurl.png",
                "creationTime": "2019-01-09 22:11:29.0",
                "status": "",
                "firstFrameUrl": "",
                "size": 56,
                "cateId": 12,
                "cateName": "12",
                "tags": "测试",
                "shareUrl": "",
                "user": {
                    "userId": "243479322xxxx",
                    "userName": "xx",
                    "avatarUrl": "https://alivc-demo-vod.aliyuncs.com/dd38cab5-2951-43a0-b9ed-ad0eebf83a70"
                },
                "transcodeStatus": "",
                "snapshotStatus": "",
                "censorStatus": "onCensor",
                "narrowTranscodeStatus": ""
            }]
        }
    }
    ```

-   deleteVideoById：删除视频。

    post url：/vod/deleteVideoById

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |token|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |videoId|string|是|视频ID|
    |userId|string|是|用户ID|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "f8163b40-6192-4edc-97ec-52c6cd96xxxx",
        "message": "删除完成",
        "code": "200",
        "data": null
    }
    ```


## 通知回调类接口

智能审核完成回调，视频转码完成回调，截图完成回调

通过提交智能审核作业，视频转码作业，截图作业后，在控制台配置回调设置，并在服务端用回调方法接收控制台传递过来的请求头的参数，回调内容公共参数及对应事件类型如下。

|名称|类型|描述|
|--|--|--|
|EventTime|string|事件产生时间，为UTC时间：yyyy-MM-ddTHH:mm:ssZ|
|EventType|string|事件类型|
|VideoId|string|视频ID|
|Status|string|处理状态，取值：-   success：成功
-   fail：失败 |

**EventType**

|事件类型|EventType|
|----|---------|
|StreamTranscodeComplete|视频单个清晰度转码完成|
|SnapshotComplete|视频截图完成|
|AIVideoCensorComplete|智能审核完成|

当一个事件完成，会携带数据请求回调，数据类型服务端接收到请求，更新数据库。

## 音乐类接口

-   getRecommendMusic：获取热门音乐。

    get url：/music/getRecommendMusic

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |pageNo|string|是|起始页，取值范围：1~50|
    |pageSize|string|是|每页条数，取值范围：1~50|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |total|string|视频总条数|
    |musicList|List<MusicInfo\>|歌曲信息列表|

    MusicInfo

    |名称|类型|描述|
    |--|--|--|
    |musicId|string|歌曲ID（唯一标识）|
    |title|string|歌曲显示名称|
    |artistName|string|艺术家名称|
    |duration|string|时长|
    |source|string|来源（暂时从太合音乐（TaiHe）获取资源）|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "56a393dc-b1f9-4641-b998-6a7ff40dxxxx",
        "message": "",
        "code": "200",
        "data": {
            "musicList": [{
                "musicId": "T10033153675",
                "title": "超感应",
                "artistName": "N.O.D",
                "duration": "219",
                "source": "TaiHe"
            },
            {
                "musicId": "T10033153447",
                "title": "Candybae",
                "artistName": "N.O.D",
                "duration": "200",
                "source": "TaiHe"
            },
            {
                "musicId": "T10033153645",
                "title": "Ring Ring Ring",
                "artistName": "N.O.D",
                "duration": "208",
                "source": "TaiHe"
            }],
            "total": "40"
        }
    }
    ```

-   getPlayPath：根据音乐ID查询播放地址。

    get url：/music/getPlayPath

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |musicId|string|是|音乐ID|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |playPath|string|播放路径|
    |expireTime|string|有效期|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "56a393dc-b1f9-4641-b998-6a7ff40dxxxx",
        "message": "",
        "code": "200",
        "data": {
            "playPath": "https://audio01.dmhmusic.com/117_15_T10033153675_64_4_1_0_sdk-ts/0105/M00/B2/F4/ChR45VnaKfaAK01QABrJJdrL4Yk.64.aac?xcode=af09abf9f9e26b644165614d13a46776755f023",
            "expireTime": "1551772473"
        }
    }
    ```


## 资源类接口

-   getPasterInfo：获取动图类别信息。

    get url：/resource/getPasterInfo

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |id|int|动图类别ID|
    |icon|string|图标|
    |description|string|描述|
    |level|int|等级|
    |name|string|名称|
    |preview|string|预览|
    |sort|int|排列序号|
    |type|int|类型|
    |createTime|string|创建时间|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "cc52d16b-3c1d-4694-abf1-c0633ddaxxxx",
        "message": "",
        "code": "200",
        "data": [{
            "id": 84,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/85157CBE88A14CBC95C5216F3D0579D1-6-2.png",
            "description": "情人节动图",
            "name": "最美情人节",
            "level": 1,
            "preview": "http://30.40.34.91:8080/?id=84",
            "sort": 46,
            "type": 1,
            "createTime": "2019-03-19 14:32:38.0"
        },
        {
            "id": 108,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/44F675192F144BDA9B2A324F7664911E-6-2.png",
            "description": "新年素材",
            "name": "2017春节快乐2",
            "level": 1,
            "preview": "http://30.40.34.91:8080/?id=108",
            "sort": 45,
            "type": 1,
            "createTime": "2019-03-19 14:32:18.0"
        }]
    }
    ```

-   getPasterList：根据动图类别ID查找动图包信息。

    get url：/resource/getPasterList

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |pasterId|string|是|动图类别ID|
    |type|string|是|动图类型，取值：    -   1：前置动图
    -   2：后置动图 |

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |id|string|动图类别ID|
    |fontId|int|字体ID|
    |icon|string|图标|
    |name|string|名称|
    |url|string|下载路径|
    |preview|string|预览图|
    |sort|int|排列序号|
    |type|int|类型|
    |createTime|string|创建时间|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "395f0d19-7f3d-4df3-ac56-e7715e4fxxxx",
        "message": "",
        "code": "200",
        "data": [{
            "id": 1083,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/145F371646EB4CA595A7BD6C43F0EA9E-6-2.jpg",
            "url": "http://alivc-demo-vod.aliyuncs.com/video/material/9862890CE93C4248B8B1F6F2C96E4289-7-4.mat",
            "preview": "http://alivc-demo-vod.aliyuncs.com/image/default/12044FD09B6C432B874A925952F526F2-6-2.gif",
            "name": "bianpao",
            "sort": 0,
            "type": 0,
            "fontId": 0,
            "createTime": "2019-03-19 14:32:18.0"
        },
        {
            "id": 1092,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/F78BDD275CE84186A67730BC93BF23ED-6-2.jpg",
            "url": "http://alivc-demo-vod.aliyuncs.com/video/material/ABE3DAE450C3482896BA5AEAE8C82283-7-4.mat",
            "preview": "http://alivc-demo-vod.aliyuncs.com/image/default/4154C9D2FE3A4B4191A58357F1C403C6-6-2.gif",
            "name": "zhaofudamo",
            "sort": 0,
            "type": 0,
            "fontId": 0,
            "createTime": "2019-03-19 14:32:19.0"
        }]
    }
    ```

-   getFrontPasterList：查询前置动图包。

    get url：/resource/getFrontPasterList

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |id|int|动图类别ID|
    |fontId|string|字体ID|
    |icon|string|图标|
    |name|string|名称|
    |url|string|下载路径|
    |preview|string|预览|
    |sort|string|排列序号|
    |type|string|类型|
    |createTime|string|创建时间|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "0423771c-ad6b-4557-9ef1-ce71fcb0xxxx",
        "message": "",
        "code": "200",
        "data": [{
            "id": 5871,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/EFA0567FF6CE4E6D866A25D909DE05C3-6-2.jpg",
            "mediaId": 0,
            "url": "http://alivc-demo-vod.aliyuncs.com/video/material/BD74BC09CB3341169F319727340B78CF-7-4.mat",
            "preview": "http://alivc-demo-vod.aliyuncs.com/image/default/2A768BDC4D024366BCCBFF950C2B3051-6-2.gif",
            "name": "bixin",
            "duration": 0,
            "desc": "",
            "sort": 0,
            "aspect": 0,
            "type": 0,
            "fontId": 0,
            "createTime": "2019-03-19 14:32:45.0"
        },
        {
            "id": 5872,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/497006AE17DB46FA9DAFE6B5405D9576-6-2.jpg",
            "mediaId": 0,
            "url": "http://alivc-demo-vod.aliyuncs.com/video/material/7E3079293ACE44A48271E1D6CB07D217-7-4.mat",
            "preview": "http://alivc-demo-vod.aliyuncs.com/image/default/E6567EDDD03540C7931980928CA12E05-6-2.gif",
            "name": "gaobai",
            "duration": 0,
            "desc": "",
            "sort": 0,
            "aspect": 0,
            "type": 0,
            "fontId": 0,
            "createTime": "2019-03-19 14:32:46.0"
        },
        {
            "id": 5873,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/CB1BB92B7BCB44E28AA50F26C96D0109-6-2.jpg",
            "mediaId": 0,
            "url": "http://alivc-demo-vod.aliyuncs.com/video/material/A5EBA7E610D84265B53539964EFD89C4-7-4.mat",
            "preview": "http://alivc-demo-vod.aliyuncs.com/image/default/E1BF246F042A4A30A0E7F41673316BD7-6-2.gif",
            "name": "liwune",
            "duration": 0,
            "desc": "",
            "sort": 0,
            "aspect": 0,
            "type": 0,
            "fontId": 0,
            "createTime": "2019-03-19 14:32:48.0"
        }]
    }
    ```

-   getTextPaster：字幕类别信息。

    get rul：/resource/getTextPaster

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |id|int|动图类别ID|
    |icon|string|图标|
    |description|string|描述|
    |name|string|名称|
    |preview|string|预览|
    |sort|int|排列序号|
    |type|int|类型|
    |createTime|string|创建时间|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "23b4de5e-0b89-40f0-b78c-d4122537xxxx",
        "message": "",
        "code": "200",
        "data": [{
            "id": 189,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/BB11DAF8ED0842408A4A04F09893D454-6-2.png",
            "description": "气泡框",
            "name": "气泡框",
            "preview": "http://30.40.34.91:8080/?type=text&id=189",
            "sort": 3,
            "type": 2,
            "createTime": "2019-03-19 14:21:58.0"
        },
        {
            "id": 196,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/7858EDE1DCD8457E976BCAB42FB9845D-6-2.png",
            "description": "简洁气泡框",
            "name": "简单气泡",
            "preview": "http://30.40.34.91:8080/?type=text&id=196",
            "sort": 2,
            "type": 2,
            "createTime": "2019-03-19 14:21:42.0"
        }]
    }
    ```

-   getTextPasterList：根据字幕类别ID查找字幕包信息。

    get url：/resource/getTextPasterList

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |textPasterId|String|是|字幕类别ID|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |id|int|字幕包ID|
    |fontId|int|字体ID|
    |icon|string|图标|
    |name|string|名称|
    |url|string|下载路径|
    |preview|string|预览|
    |sort|int|排列序号|
    |type|int|类型|
    |createTime|string|创建时间|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "49ec9fc0-d2e2-4702-afe3-a1fadda7xxxx",
        "message": "",
        "code": "200",
        "data": [{
            "id": 963,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/4326259B143E4D5EB979CFE2D021608D-6-2.jpg",
            "mediaId": 1849,
            "url": "http://alivc-demo-vod.aliyuncs.com/video/material/599ED868D7DC405BB3EE093FFCFEF576-7-4.mat",
            "preview": "http://alivc-demo-vod.aliyuncs.com/image/default/B43F76D23D58401C9ABD90AD3C623BAC-6-2.gif",
            "name": "beiers",
            "duration": 0,
            "desc": "",
            "sort": 0,
            "type": 0,
            "fontId": 52,
            "createTime": "2019-03-19 14:21:42.0"
        },
        {
            "id": 964,
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/1148257C961547848690C275B860B340-6-2.jpg",
            "mediaId": 1862,
            "url": "http://alivc-demo-vod.aliyuncs.com/video/material/15CD1557EAAC49B1BA2FD3C30236A657-7-4.mat",
            "preview": "http://alivc-demo-vod.aliyuncs.com/image/default/79DB242DD30446AC91DC74EAC3384271-6-2.gif",
            "name": "yajing",
            "duration": 0,
            "desc": "",
            "sort": 0,
            "type": 0,
            "fontId": 89,
            "createTime": "2019-03-19 14:21:43.0"
        }]
    }
    ```

-   getMv：查找MV信息。

    get url：/resource/getMv

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |id|int|MV ID|
    |icon|string|图标|
    |duration|string|时长|
    |name|string|名称|
    |previewPic|string|播放预览图|
    |previewMp4|string|播放链接|
    |sort|int|排列序号|
    |createTime|string|创建时间|
    |aspectList|List<Aspect\>|MV列表|

    Aspect

    |名称|类型|描述|
    |--|--|--|
    |aspect|string|MV宽高比例    -   1:1
    -   4:3
    -   16:9 |
    |download|string|下载地址|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "3dae0e53-39ff-4376-bc8d-e94c3380xxxx",
        "message": "",
        "code": "200",
        "data": [{
            "id": 104,
            "previewPic": "http://alivc-demo-vod.aliyuncs.com/image/default/FB35E16CC72C4B85AF6C776EB8034947-6-2.png",
            "previewMp4": "http://alivc-demo-vod.aliyuncs.com/video/material/EC8C09EB055248B1A1DD8803D08D4D16-7-4.mp4",
            "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/DFB64DE1892B4DEAA34F01D594D5AE81-6-2.png",
            "duration": 15,
            "name": "relax",
            "sort": 8,
            "createTime": "2019-03-19 14:21:21.0",
            "aspectList": [{
                "aspect": 1,
                "download": "http://alivc-demo-vod.aliyuncs.com/video/material/14FF3D3297CF442A9A3E160C5F191752-7-4.mat"
            },
            {
                "aspect": 2,
                "download": "http://alivc-demo-vod.aliyuncs.com/video/material/53CC516C4B3A49CABD0B13A093CABCCE-7-4.mat"
            },
            {
                "aspect": 3,
                "download": "http://alivc-demo-vod.aliyuncs.com/video/material/CB7444406A0B4249A80897EFF6E40B8B-7-4.mat"
            }]
        }]
    }
    ```


## 字体接口

getFont：根据字体ID获取字体信息。

get url：/resource/getFont

参数

|名称|类型|是否必填|描述|
|--|--|----|--|
|fontId|string|否|字体ID（不传则查出全部）|

返回参数

|名称|类型|描述|
|--|--|--|
|id|int|字体ID|
|banner|string|标语|
|name|string|名称|
|url|string|下载路径|
|icon|string|图标|
|sort|int|排列序号|

返回示例

```
{
    "result": "true",
    "requestId": "b9c72eb4-9d42-4fda-934c-23c60493xxxx",
    "message": "",
    "code": "200",
    "data": {
        "id": 52,
        "name": "趣.憧憬",
        "banner": "http://alivc-demo-vod.aliyuncs.com/image/default/BD4E71CE644043019E89A5737A79AC51-6-2.jpg",
        "icon": "http://alivc-demo-vod.aliyuncs.com/image/default/C1F83D29D3B64C3C87CF7E3BDEF3B08F-6-2.jpg",
        "url": "http://alivc-demo-vod.aliyuncs.com/video/material/B12F02D94A184481A9DE629ECFCD8C0D-7-4.mat",
        "sort": 1
    }
}
```

