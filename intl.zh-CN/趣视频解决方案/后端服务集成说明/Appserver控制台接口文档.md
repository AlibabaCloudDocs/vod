# Appserver控制台接口文档

本文为您介绍趣视频控制台接口调用方法和返回值。

## 返回值结构说明

所有请求均返回此**JSON**格式的数据，所有API只描述**data**结构数据。

|返回参数|类型|描述|
|----|--|--|
|requestId|string|服务端生成的本次请求ID|
|code|string|服务端生成的本次请求Code|
|message|string|服务端消息多用于描述错误原因|
|data|object|服务端返回的业务结构体数据，不同业务数据结构不同|

## 控制台接口

-   getVideos：查询条件获取视频列表。

    get url：/console/vod/getVideos

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |pageIndex|int|否|起始页 （从1开始）|
    |pageSize|int|否|每页条数|
    |videoId|string|否|视频ID|
    |userId|string|否|用户ID|
    |title|string|否|标题|
    |startTime|string|否|开始时间|
    |endTime|string|否|结束时间|
    |userName|string|否|用户名|
    |censorStatus|string|否|审核状态|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |total|string|视频总条数|
    |videoList|List<[Video]()\>|个人中心视频信息列表|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "c3bcb60d-e85f-4e19-a50a-16bedb56165f",
      "message": "",
      "code": "200",
      "data": {
        "total": 7,
        "videoList": [
          {
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
              "userId": "2434793223202",
              "userName": "Anne",
              "avatarUrl": "https://alivc-demo-vod.aliyuncs.com/dd38cab5-2951-43a0-b9ed-ad0eebf83a70"
            },
            "transcodeStatus": "",
            "snapshotStatus": "",
            "censorStatus": "onCensor",
            "narrowTranscodeStatus": "",
            "SnapshotList": { "http://sample/covers/990f3820db2948b5b4a13d65d9a449f6-2.jpg"
                  , "http://sample/covers/sprite/990f3820db2948b5b4a13d65d9a449f6-1.jpg"
                },
            "fileUrlList": { "http://vod.aliyunsample.com/ABEBDE15CC479FD4D1329/52a53151eba5226f8e2da3b55bc57c49.mp4"
                  , "http://vod.aliyunsample.com/ABEBDE15CC479FD4D1329/52a53151eba5226f8e2da3b55bc57c49.mp4"
                }
          }
        ]
      }
    }
    ```

-   submitTranscode：发起非窄带高清转码。

    get url：/console/vod/submitTranscode

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |mediaId|String|是|视频ID|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "c3bcb60d-e85f-4e19-a50a-16bedb56165f",
      "message": "发起非窄带高清转码作业完成！",
      "code": "200",
      "data": null
    }
    ```

-   createAudit：手动人工审核。

    get url：/console/vod/createAudit

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |mediaId|String|是|视频ID|
    |status|String|是|状态，取值：    -   Blocked：屏蔽
    -   Normal：正常 |
    |reason|String|否|若审核状态为屏蔽时，需给出屏蔽的理由，最长支持128字节|
    |comment|String|否|备注|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "c312edd-1dc3-132r313rfef-qfevw42ghrnk",
      "message": "审核完成",
      "code": "200",
      "data": null
    }
    ```

-   submitTranscode：发起窄带高清转码。

    get url：/console/vod/submitTabTranscode

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |mediaId|String|是|视频ID|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "dsgb455-e85f-443f9-a50a-12323rfg34t34g",
      "message": "发起窄带高清转码作业完成！",
      "code": "200",
      "data": null
    }
    ```

-   getVideoById：根据videoId查询视频详情。

    get url：/console/vod/getVideoById

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |videoId|string|是|视频ID|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |title|string|视频标题|
    |videoId|string|视频ID|
    |description|string|视频描述|
    |duration|string|视频时长，单位：秒|
    |coverUrl|string|视频封面URL|
    |status|string|视频状态|
    |firstFrameUrl|string|首帧地址|
    |size|string|视频源文件大小，单位：字节|
    |tags|string|视频标签，多个标签使用英文逗号（,）分隔|
    |cateId|string|视频分类|
    |cateName|string|视频分类名称|
    |creationTime|string|创建时间|
    |transcodeStatus|string|转码状态|
    |snapshotStatus|string|截图状态|
    |censorStatus|string|审核状态|
    |narrowTranscodeStatus|string|窄带高清转码状态|
    |SnapshotList|list|截图列表|
    |fileUrilList|list|视频地址列表|
    |user|[User]()|用户|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "f8163b40-6192-4edc-97ec-52c6cd96e996",
      "message": "",
      "code": "200",
      "data": {
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
              "userId": "2434793223202",
              "userName": "Anne",
              "avatarUrl": "https://alivc-demo-vod.aliyuncs.com/dd38cab5-2951-43a0-b9ed-ad0eebf83a70"
            },
            "transcodeStatus": "",
            "snapshotStatus": "",
            "censorStatus": "onCensor",
            "narrowTranscodeStatus": "",
            "SnapshotList": { "http://sample/covers/990f3820db2948b5b4a13d65d9a449f6-2.jpg"
                  , "http://sample/covers/sprite/990f3820db2948b5b4a13d65d9a449f6-1.jpg"
                },
            "fileUrilList": { "http://vod.aliyunsample.com/ABEBDE15CC479FD4D1329/52a53151eba5226f8e2da3b55bc57c49.mp4"
                  , "http://vod.aliyunsample.com/ABEBDE15CC479FD4D1329/52a53151eba5226f8e2da3b55bc57c49.mp4"
                }
      }
    }
    ```

-   getRecommendVideos：查询条件获取推荐视频列表。

    get url：/console/vod/getRecommendVideos

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |pageIndex|int|否|起始页 （从1开始）|
    |pageSize|int|否|每页条数|
    |videoId|string|否|视频ID|
    |userId|string|否|用户ID|
    |title|string|否|标题|
    |startTime|string|否|开始时间|
    |endTime|string|否|结束时间|
    |userName|string|否|用户名|
    |censorStatus|string|否|审核状态|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |total|string|视频总条数|
    |videoList|List<[Video]()\>|个人中心视频信息列表|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "c3bcb60d-e85f-4e19-a50a-16bedb56165f",
      "message": "",
      "code": "200",
      "data": {
        "total": 7,
        "videoList": [
          {
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
              "userId": "2434793223202",
              "userName": "Anne",
              "avatarUrl": "https://alivc-demo-vod.aliyuncs.com/dd38cab5-2951-43a0-b9ed-ad0eebf83a70"
            },
            "transcodeStatus": "",
            "snapshotStatus": "",
            "censorStatus": "onCensor",
            "narrowTranscodeStatus": ""
          }
        ]
      }
    }
    ```

-   recommendVideo：推荐视频到推荐列表中。

    post url：/console/vod/recommendVideo

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |title|string|否|视频标题|
    |videoId|string|否|视频ID|
    |userId|string|否|用户ID|
    |description|string|否|视频描述|
    |duration|String|否|视频时长，单位：秒|
    |coverUrl|string|否|视频封面URL|
    |size|String|否|视频源文件大小，单位：字节|
    |tags|string|否|视频标签，多个标签使用英文逗号（,）分隔|
    |cateId|String|否|视频分类|
    |cateName|string|否|视频分类名称|
    |firstFrameUrl|string|否|首帧图|
    |transcodeStatus|String|否|转码状态（非窄带高清）|
    |snapshotStatus|string|否|截图状态|
    |censorStatus|String|否|审核状态|
    |isNarrow|String|否|是否窄带高清|
    |isCache|String|否|是否预热|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "f8163b40-6192-4edc-97ec-52c6cd96e996",
      "message": "插入推荐视频成功！",
      "code": "200",
      "data":null
    }
    ```

-   pushObjectCache：预热缓存。

    post url：/console/vod/pushObjectCache

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |objectPath|string|否|对象地址，输入示例：a.com/image/1.png，多个URL间用换行符（\\n或\\r\\n）分隔 。|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "f8163b40-6192-4edc-97ec-52c6cd96e996",
      "message": "预热完成",
      "code": "200",
      "data":null
    }
    ```

-   getRecommendVideoById：根据videoId查询推荐视频详情。

    get url：/console/vod/getRecommendVideoById

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |videoId|string|是|视频ID|

    返回参数

    |名称|类型|描述|
    |--|--|--|
    |title|string|视频标题|
    |videoId|string|视频ID|
    |description|string|视频描述|
    |duration|string|视频时长，单位：秒|
    |coverUrl|string|视频封面URL|
    |status|string|视频状态|
    |firstFrameUrl|string|首帧地址|
    |size|string|视频源文件大小，单位：字节|
    |tags|string|视频标签，多个标签使用英文逗号（,）分隔|
    |cateId|string|视频分类|
    |cateName|string|视频分类名称|
    |creationTime|string|创建时间|
    |transcodeStatus|string|转码状态|
    |snapshotStatus|string|截图状态|
    |censorStatus|string|审核状态|
    |narrowTranscodeStatus|string|窄带高清转码状态|
    |SnapshotList|list|截图列表|
    |fileUrilList|list|视频地址列表|
    |user|[User]()|用户|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "f8163b40-6192-4edc-97ec-52c6cd96e996",
      "message": "根据videoId获取视频详情完成！",
      "code": "200",
      "data": {
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
              "userId": "2434793223202",
              "userName": "Anne",
              "avatarUrl": "https://alivc-demo-vod.aliyuncs.com/dd38cab5-2951-43a0-b9ed-ad0eebf83a70"
            },
            "transcodeStatus": "success",
            "snapshotStatus": "success",
            "censorStatus": "onCensor",
            "narrowTranscodeStatus": "onCensor"
      }
    }
    ```

-   deleteVideoById：删除视频。

    post url：/console/vod/deleteVideoById

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |videoId|string|是|视频ID|
    |userId|string|是|用户ID|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "f9a8sdf09iaf3-2f23r23-0965iyhk4",
      "message": 删除完成！,
      "code": "200",
      "data":null
    }
    ```

-   deleteRecommendById：取消推荐。

    post url：/console/vod/deleteRecommendById

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |consoletoken|string|是|趣视频客户系统的Token验证，用户可以替换为自己的系统验证方式|
    |videoId|string|是|视频ID|

    返回示例

    ```
    {
      "result": "true",
      "requestId": "f8163b40-6192-4edc-97ec-52c6cd96e996",
      "message": "取消推荐完成",
      "code": "200",
      "data":null
    }
    ```

-   login：控制台登录。

    post url：/console/user/login

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |userName|string|是|用户名|
    |password|string|是|密码|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "c30f63ed-3f66-45e9-9df0-a15e7d3a7e6a",
        "message": "登录成功！",
        "code": "200",
        "data": {
            "consoleToken": "12351232334123456781548765480698"
        }
    }
    ```

-   signOut：控制台退出登录。

    post url：/console/user/signOut

    参数

    |名称|类型|是否必填|描述|
    |--|--|----|--|
    |userName|string|是|用户名|
    |password|string|是|密码|

    返回示例

    ```
    {
        "result": "true",
        "requestId": "d4b6405b-86fb-45e7-826c-68b69926147b",
        "message": "退出完成！",
        "code": "200",
        "data": null
    }
    ```


