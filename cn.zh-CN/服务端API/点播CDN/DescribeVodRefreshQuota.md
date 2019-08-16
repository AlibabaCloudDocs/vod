# DescribeVodRefreshQuota {#doc_api_vod_DescribeVodRefreshQuota .reference}

调用DescribeVodRefreshQuota查询刷新预热URL及目录的最大限制数量和当日剩余数量。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodRefreshQuota&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodRefreshQuota|系统规定参数。取值：**DescribeVodRefreshQuota**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BlockQuota|String|500|当日存储刷新数量上限。

 |
|DirQuota|String|100|当日路径刷新数量上限。

 |
|DirRemain|String|99|当日剩余目录刷新数量。

 |
|PreloadQuota|String|500|当天预热数量上限。

 |
|PreloadRemain|String|500|当天剩余预热数量。

 |
|RequestId|String|42E0554B-80F4-4921-AED6-ACFB22CAAAD0|请求ID。

 |
|UrlQuota|String|2000|当日URL刷新数量上限。

 |
|UrlRemain|String|1996|当日剩余URL刷新数量。

 |
|blockRemain|String|500|当日剩余存储刷新数量。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodRefreshQuota
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodRefreshQuotaResponse>
    <DirQuota>100</DirQuota>
    <DirRemain>99</DirRemain>
    <RequestId>A56FC7F8-CA97-482E-9649-F77C2135BD22</RequestId>
    <UrlQuota>2000</UrlQuota>
    <UrlRemain>1996</UrlRemain>
    <PreloadQuota>500</PreloadQuota>
    <PreloadRemain>500</PreloadRemain>
</DescribeVodRefreshQuotaResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DirQuota":"100",
	"PreloadRemain":"500",
	"DirRemain":"99",
	"RequestId":"42E0554B-80F4-4921-AED6-ACFB22CAAAD0",
	"UrlQuota":"2000",
	"UrlRemain":"1996",
	"PreloadQuota":"500"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

