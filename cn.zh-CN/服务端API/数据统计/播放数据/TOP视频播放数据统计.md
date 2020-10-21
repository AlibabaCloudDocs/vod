# TOP视频播放数据统计

获取每日TOP视频的播放数据统计（包括VV、UV和播放总时长）。

**说明：**

-   最多可查询该日 Top1000 的视频播放统计数据，Top视频列表默认基于VV数排序。
-   仅支持使用了阿里云点播播放器SDK的播放数据统计。
-   以北京时间（UTC+8）为基准，每天上午9点生成前一天的播放数据统计。
-   支持查询 2018-01-01 起的数据，数据查询的起止时间跨度最大为90天。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribePlayTopVideos&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribePlayTopVideos|操作接口名，系统规定参数。取值：DescribePlayTopVideos |
|BizDate|String|是|2016-06-29T13:00:00Z|日期，UTC格式。 |
|PageNo|Long|否|1|分页的页码，默认值：**1**。 |
|PageSize|Long|否|100|每页大小。

 -   默认值为**100**。
-   最大值为**1000**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageSize|Long|100|每页大小。 |
|PageNo|Long|1|分页的页码。 |
|TotalNum|Long|2|TOP视频播放统计数据的总条数。 |
|TopPlayVideos|Array of TopPlayVideoStatis| |用户每天播放top统计数据。 |
|TopPlayVideoStatis| | | |
|VideoId|String|2a8d4cb9ecbb487681473a15\*\*\*\*8fda|视频ID。 |
|PlayDuration|String|4640369|播放时长，单位：毫秒。 |
|Title|String|4路（2路加密）：流畅-HLS-加密+标清-MP4+高清-H|视频名称。 |
|VV|String|107|播放次数。 |
|UV|String|1|播放用户数。 |
|RequestId|String|4B0BCF9F-2FD5-4817-\*\*\*\*-7BEBBE3AF90B"|请求ID。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribePlayTopVideos
&BizDate=2016-06-29T13:00:00Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribePlayTopVideosResponse>
      <TopPlayVideos>
            <TopPlayVideoStatis>
                  <VideoId>2a8d4cb9ecbb487681473**53aba8fda</VideoId>
                  <VV>107</VV>
                  <Title>4路（2路加密）：流畅-HLS-加密+标清-MP4+高清-H</Title>
                  <UV>1</UV>
                  <PlayDuration>4640369</PlayDuration>
            </TopPlayVideoStatis>
            <TopPlayVideoStatis>
                  <VideoId>cca9dbd11b7045808cc9b**c56f5bad2</VideoId>
                  <VV>33</VV>
                  <Title>2路（全加密）：标清-HLS-加密+超清-HLS-加密</Title>
                  <UV>1</UV>
                  <PlayDuration>4689369</PlayDuration>
            </TopPlayVideoStatis>
      </TopPlayVideos>
      <PageSize>1000</PageSize>
      <PageNo>1</PageNo>
      <Total>150</Total>
      <RequestId>4B0BCF9F-2FD5-4817-****-7BEBBE3AF90B</RequestId>
</DescribePlayTopVideosResponse>
```

`JSON` 格式

```
{
    "TopPlayVideos": {
        "TopPlayVideoStatis": [
            {
                "VideoId": "2a8d4cb9ecbb487681473**53aba8fda", 
                "VV": "107", 
                "Title": "4路（2路加密）：流畅-HLS-加密+标清-MP4+高清-H", 
                "UV": "1",
                "PlayDuration":"4640369"
            }, 
            {
                "VideoId": "cca9dbd11b7045808cc9b**c56f5bad2", 
                "VV": "33", 
                "Title": "2路（全加密）：标清-HLS-加密+超清-HLS-加密", 
                "UV": "1",
                "PlayDuration":"4689369"
            }
           
        ]
    }, 
    "PageSize": "1000",
    "PageNo":  "1",
    "Total": "150",
    "RequestId": "4B0BCF9F-2FD5-4817-****-7BEBBE3AF90B"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## 接口错误码

下表列举了本接口特有的错误码。

|错误代码

|错误信息

|HTTP 状态码

|说明 |
|------|------|----------|----|
|InternalError

|The request processing has failed due to some unknown error.

|500

|后台发生未知错误。 |
|InvalidBizDate.Malformed

|Specified BizDate is malformed.

|400

|BizDate格式错误，应为UTC格式，例如：2018-06-29T13:00:00Z。 |
|InvalidBizDate.BeyondCurrent

|EndTime beyond current time.

|400

|BizDate不能超过当前时间。 |

