# 获取视频DNA结果

调用GetMediaDNAResult获取视频DNA结果。视频DNA作业完成后，可通过此接口实时查询DNA结果。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetMediaDNAResult&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMediaDNAResult|系统规定参数，取值：**GetMediaDNAResult**。 |
|MediaId|String|是|88c6ca184c0e\*\*\*\*\*a5b665e2a126797|视频ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DNAResult|Struct| |DNA结果。 |
|VideoDNA|Array of VideoDNA| |视频DNA识别结果。 |
|Detail|Array of Detail| |相似视频详情，包括视频的位置、时长等。 |
|Duplication|Struct| |库中视频的开始时间和时长。 |
|Duration|String|12.0|视频的时长。 |
|Start|String|2.0|视频的开始时间。 |
|Input|Struct| |输入视频的开始时间和时长。 |
|Duration|String|12.0|视频的时长。 |
|Start|String|2.0|视频的开始时间。 |
|PrimaryKey|String|6ad8987da46f4b\*\*\*\*\*490ce2873745|相似视频ID。 |
|Similarity|String|0.98|视频相似度。 |
|RequestId|String|63FC4896-E956-4B\*\*\*\*\*7D-134FF1BC597A|请求ID。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetMediaDNAResult
&MediaId=88c6ca184c0e*****a5b665e2a126797
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetMediaDNAResultResponse>
	  <RequestId>63FC4896-E956-4B*****7D-134FF1BC597A</RequestId>
	  <DNAResult>
		    <VideoDNA>
			      <Similarity>0.98</Similarity>
			      <PrimaryKey>6ad8987da46f4b*****490ce2873745</PrimaryKey>
			      <Detail>
				        <Input>
					          <Start>2.0</Start>
					          <Duration>12.0</Duration>
				        </Input>
				        <Duplication>
					          <Start>2.0</Start>
					          <Duration>12.1</Duration>
				        </Duplication>
			      </Detail>
		    </VideoDNA>
	  </DNAResult>
</GetMediaDNAResultResponse>
```

`JSON` 格式

```
{
    "RequestId":"63FC4896-E956-4B*****7D-134FF1BC597A",
    "DNAResult":{
        "VideoDNA":[
            {
                "Similarity":"0.98",
                "PrimaryKey":"6ad8987da46f4b*****490ce2873745",
                "Detail":[
                    {
                        "Input":{
                            "Start":"2.0",
                            "Duration":"12.0"
                        },
                        "Duplication":{
                            "Start":"2.0",
                            "Duration":"12.1"
                        }
                    }
                ]
            }
        ]
    }
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## SDK示例

建议使用 [服务端SDK](~~101789~~) 来调用API，此API各语言调用的示例代码，请参考如下：

-   [Java](https://help.aliyun.com/document_detail/100691.html?spm=a2c4g.11186623.2.19.34f0c60cIiQ7eA#GetMediaDNAResult)
-   [Python](https://help.aliyun.com/document_detail/101182.html?spm=a2c4g.11186623.2.20.34f0c60cIiQ7eA#GetMediaDNAResult)
-   [PHP](https://help.aliyun.com/document_detail/101167.html?spm=a2c4g.11186623.2.21.34f0c60cIiQ7eA#GetMediaDNAResult)
-   [.NET](https://help.aliyun.com/document_detail/100845.html?spm=a2c4g.11186623.2.22.34f0c60cIiQ7eA#GetMediaDNAResult)
-   [Node.js](https://help.aliyun.com/document_detail/101565.html?spm=a2c4g.11186623.2.23.34f0c60cIiQ7eA#GetMediaDNAResult)
-   [Go](https://help.aliyun.com/document_detail/101576.html?spm=a2c4g.11186623.2.24.34f0c60cIiQ7eA#GetMediaDNAResult)
-   [C/C++](https://help.aliyun.com/document_detail/102989.html?spm=a2c4g.11186623.2.25.34f0c60cIiQ7eA#GetMediaDNAResult)

