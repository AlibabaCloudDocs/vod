# DeleteCategory {#doc_api_vod_DeleteCategory .reference}

调用DeleteCategory删除视频分类，同时会删除其下级分类（包括二级分类和三级分类），请慎重操作。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteCategory&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteCategory|系统规定参数，取值：**DeleteCategory**。

 |
|CateId|Long|是|-3300080371970025740|分类ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|dc870053-a793-492a-97fb-4b2490e92013|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://vod.cn-shanghai.aliyuncs.com/?Action=DeleteCategory
&CateId=-3300080371970025740
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteCategoryResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</DeleteCategoryResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

