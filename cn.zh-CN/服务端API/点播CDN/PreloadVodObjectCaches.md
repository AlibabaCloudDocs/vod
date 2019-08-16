# PreloadVodObjectCaches {#doc_api_vod_PreloadVodObjectCaches .reference}

调用PreloadVodObjectCaches将源站的内容主动预热到L2 Cache节点上，首次访问可直接命中缓存，缓解源站压力。支持post请求，参数用form表单。

**说明：** 

-   同一账号每天最多可提交预热URL请求共500条，目前不支持目录级别的预热。
-   刷新预热类接口包含**RefreshVodObjectCaches**刷新接口和**PreloadVodObjectCaches**预热接口。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=PreloadVodObjectCaches&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PreloadVodObjectCaches|系统规定参数。取值：**PreloadVodObjectCaches**。

 |
|ObjectPath|String|是|vod.test.com/test.txt|输入示例：a.com/image/1.png，多个URL间用换行符（\\n或\\r\\n）分隔。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PreloadTaskId|String|95248880|预热返回的任务ID，多个任务ID用半角逗号分隔。

 |
|RequestId|String|E5BD4B50-7A02-493A-AE0B-97B9024B4135|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=PreloadVodObjectCaches
&ObjectPath=a.com/image/1.png
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<PreloadVodObjectCachesResponse>
    <PreloadTaskId>95250421</PreloadTaskId>
    <RequestId>5FF9B16E-FBAC-48E5-9052-65B5F0184DB3</RequestId>
</PreloadVodObjectCachesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E5BD4B50-7A02-493A-AE0B-97B9024B4135",
	"PreloadTaskId":"95248880"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

