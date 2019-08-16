# RefreshVodObjectCaches {#doc_api_vod_RefreshVodObjectCaches .reference}

调用RefreshVodObjectCaches刷新节点上的文件内容。指定URL内容刷新至Cache节点，支持URL批量刷新。支持post请求，参数用form表单。

**说明：** 限制：

-   同一账号每天最多可提交刷新URL请求共2000条，刷新目录共100个。
-   刷新预热类接口包含**RefreshVodObjectCaches**刷新接口和**PreloadVodObjectCaches**预热接口。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=RefreshVodObjectCaches&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RefreshVodObjectCaches|系统规定参数。取值：**RefreshVodObjectCaches**。

 |
|ObjectPath|String|是|abc.com/image/1.png|输入示例：abc.com/image/1.png，多个URL用换行符（\\n或\\r\\n）分隔。

 |
|ObjectType|String|否|File|刷新的类型。取值范围：

 -   File（默认值）
-   Directory

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RefreshTaskId|String|704222904|刷新返回的任务ID，多个任务ID用半角逗号分隔。

 |
|RequestId|String|D61E4801-EAFF-4A63-AAE1-FBF6CE1CFD1C|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=RefreshVodObjectCaches
&ObjectPath=abc.com/image/1.png
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RefreshVodObjectCachesResponse>
    <RefreshTaskId>704225667</RefreshTaskId>
    <RequestId>AB14769A-A5F2-4CCD-B85B-3368DFF63C0A</RequestId>
</RefreshVodObjectCachesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RefreshTaskId":"704222904",
	"RequestId":"D61E4801-EAFF-4A63-AAE1-FBF6CE1CFD1C"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

