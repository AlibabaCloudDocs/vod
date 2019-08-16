# GetEditingProject {#doc_api_vod_GetEditingProject .reference}

调用GetEditingProject获取云剪辑工程（视频编辑任务）的详细信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetEditingProject&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetEditingProject|系统规定参数。取值：**GetEditingProject**。

 |
|ProjectId|String|是|fb2101bf24bf41c78b2754cb318787dc|云剪辑工程ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Project| | |云剪辑工程。

 |
|CoverURL|String|" "|云剪辑工程封面URL。

 |
|CreationTime|String|2017-10-23 13:33:40|云剪辑工程创建时间。UTC时间，格式为：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|Description|String|testdescription|云剪辑工程描述。

 |
|ModifiedTime|String|2017-10-23 14:27:26|云剪辑工程最新修改时间。UTC时间，格式为：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|ProjectId|String|25cfc178d2de418baace77aebed6afcd|云剪辑工程ID。

 |
|RegionId|String|cn-shanghai|地域。

 |
|Status|String|Normal|云剪辑工程状态。

 |
|StorageLocation|String|location\_s|存储区域。

 |
|Timeline|String|\{\\"TimelineIn\\":0,\\"TimelineOut\\":9.42\}|云剪辑工程时间线。

 |
|Title|String|视频\_1508736815000|云剪辑工程标题。

 |
|RequestId|String|63E8B7C7-4812-46F4-A8AD-0FA56029AC86|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetEditingProject
&ProjectId=fb2101bf24bf41c78b2754cb318787dc
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetEditingProjectResponse>
  <RequestId>63E8B7C7-4812-46F4-A8AD-0FA56029AC86</RequestId>
	  <Project>
		    <ProjectId>25cfc178d2de418baace77aebed6afcd</ProjectId>
		    <Status>Normal</Status>
		    <Duration>22.66</Duration>
		    <Title>视频_1508736815000</Title>
		    <CreateTime>2017-10-23 13:33:40</CreateTime>
		    <ModifyTime>2017-10-23 14:27:26</ModifyTime>
		    <Timeline>{"Id":"New_Timeline","Name":"","Status":0,"CreationTime":"2017-10-23T13:33:35Z","ModifiedTime":null,"Duration":22.66,"Size":0,"CurrentRuler":10,"CurrentPosition":16.92,"VideoTracks":[{"Count":3,"Duration":22.66,"VideoTrackClips":[{"Id":"VCLIP_89425482","VideoId":"07c2b35dd2f342da98b8c3e45e456a41","Title":"487_副本 6","Index":0,"CutFlag":true,"TextFlag":true,"DeWatermarkFlag":false,"Duration":9.42,"VirginDuration":9.42,"Width":640,"Height":360,"URL":"http://vod.testtestapsaravideo.cn/07c2b35dd2f342da98b8c3e45e456a41/c228bc42b97047299108fcf9796c9223-699a80a29a15c59c9d0868389f86cc3f.mp4","CoverURL":"","SpriteURLs":"http://vod.testtestapsaravideo.cn/material_big_snapshot/07c2b35dd2f342da98b8c3e45e456a4100001.jpg?auth_key=","In":5.74,"Out":15.16,"TimelineIn":0,"TimelineOut":9.42,"Effects":[{"Type":"Text","Name":"横幅文字","Font":"SimSun","FontFace":{"Bold":false,"Italic":false,"Underline":false},"FontColor":"#ffffff","FontSize":20,"FontColorOpacity":1,"Content":"test","X":"0.3000","Y":"0.7000","Bold":"false","Italic":"false","Underline":"false","Height":23.599999999999998,"Width":41,"FEHeight":281.25,"FEWidth":500,"In":5.74,"Out":15.16,"TimelineIn":0,"TimelineOut":9.42}]},{"Id":"VCLIP_77584432","VideoId":"0f325c15738d4bfa85456f2a7e91b2ff","Title":"487_副本 6","Index":1,"CutFlag":true,"TextFlag":false,"DeWatermarkFlag":true,"Duration":7.5,"VirginDuration":15.16,"Width":640,"Height":360,"URL":"http://vod.testtestapsaravideo.cn/0f325c15738d4bfa85456f2a7e91b2ff/ba9dd0e93a4c4ec288abea8f11d7ec94-699a80a29a15c59c9d0868389f86cc3f.mp4","CoverURL;":"","SpriteURLs":"http://vod.testtestapsaravideo.cn/material_big_snapshot/0f325c15738d4bfa85456f2a7e91b2ff00001.jpg?auth_key=","In":0,"Out":7.5,"TimelineIn":9.42,"TimelineOut":16.92,"Effects":[{"Type":"DeWatermark","Name":"水印/遮标","SubType":"Delogo_Blur","X":"0.7660","Y":"0.0333","Width":100,"Height":50,"FEHeight":281.25,"FEWidth":500,"In":0,"Out":7.5,"TimelineIn":9.42,"TimelineOut":16.92}]},{"Id":"07c2b35dd2f342da98b8c3e45e456a41_1","Title":"487_副本 6","VideoId":"07c2b35dd2f342da98b8c3e45e456a41","Index":2,"CutFlag":true,"TextFlag":true,"DeWatermarkFlag":true,"Duration":5.74,"VirginDuration":15.16,"URL":"http://vod.testtestapsaravideo.cn/07c2b35dd2f342da98b8c3e45e456a41/c228bc42b97047299108fcf9796c9223-699a80a29a15c59c9d0868389f86cc3f.mp4","CoverURL":"","SpriteURLs":"http://vod.testtestapsaravideo.cn/material_big_snapshot/07c2b35dd2f342da98b8c3e45e456a4100001.jpg?auth_key=","Width":640,"Height":360,"In":0,"Out":5.74,"TimelineIn":16.92,"TimelineOut":22.66,"Effects":[{"Type":"Text","Name":"横幅文字","Font":"SimSun","FontFace":{"Bold":false,"Italic":false,"Underline":false},"FontColor":"#ffffff","FontSize":20,"FontColorOpacity":1,"Content":"logo","X":"0.3000","Y":"0.7000","Bold":"false","Italic":"false","Underline":"false","Height":23.599999999999998,"Width":41,"FEHeight":281.25,"FEWidth":500,"In":0,"Out":5.74,"TimelineIn":16.92,"TimelineOut":22.66},{"Type":"DeWatermark","Name":"水印/遮标","SubType":"Delogo_Blur","X":"0.0300","Y":"0.0547","Width":100,"Height":50,"FEHeight":281.25,"FEWidth":500,"In":0,"Out":5.74,"TimelineIn":16.92,"TimelineOut":22.66}]}]}],"AudioTracks":[{"Count":0,"Duration":0,"AudioTrackClips":[]}]}</Timeline>
	  </Project>
</GetEditingProjectResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"63E8B7C7-4812-46F4-A8AD-0FA56029AC86",
	"Project":{
		"Status":"Normal",
		"CreateTime":"2017-10-23 13:33:40",
		"Duration":22.66,
		"ModifyTime":"2017-10-23 14:27:26",
		"Timeline":"{\"Id\":\"New_Timeline\",\"Name\":\"\",\"Status\":0,\"CreationTime\":\"2017-10-23T13:33:35Z\",\"ModifiedTime\":null,\"Duration\":22.66,\"Size\":0,\"CurrentRuler\":10,\"CurrentPosition\":16.92,\"VideoTracks\":[{\"Count\":3,\"Duration\":22.66,\"VideoTrackClips\":[{\"Id\":\"VCLIP_89425482\",\"VideoId\":\"07c2b35dd2f342da98b8c3e45e456a41\",\"Title\":\"487_副本 6\",\"Index\":0,\"CutFlag\":true,\"TextFlag\":true,\"DeWatermarkFlag\":false,\"Duration\":9.42,\"VirginDuration\":9.42,\"Width\":640,\"Height\":360,\"URL\":\"http://vod.testtestapsaravideo.cn/07c2b35dd2f342da98b8c3e45e456a41/c228bc42b97047299108fcf9796c9223-699a80a29a15c59c9d0868389f86cc3f.mp4\",\"CoverURL\":\"\",\"SpriteURLs\":\"http://vod.testtestapsaravideo.cn/material_big_snapshot/07c2b35dd2f342da98b8c3e45e456a4100001.jpg?auth_key=\",\"In\":5.74,\"Out\":15.16,\"TimelineIn\":0,\"TimelineOut\":9.42,\"Effects\":[{\"Type\":\"Text\",\"Name\":\"横幅文字\",\"Font\":\"SimSun\",\"FontFace\":{\"Bold\":false,\"Italic\":false,\"Underline\":false},\"FontColor\":\"#ffffff\",\"FontSize\":20,\"FontColorOpacity\":1,\"Content\":\"test\",\"X\":\"0.3000\",\"Y\":\"0.7000\",\"Bold\":\"false\",\"Italic\":\"false\",\"Underline\":\"false\",\"Height\":23.599999999999998,\"Width\":41,\"FEHeight\":281.25,\"FEWidth\":500,\"In\":5.74,\"Out\":15.16,\"TimelineIn\":0,\"TimelineOut\":9.42}]},{\"Id\":\"VCLIP_77584432\",\"VideoId\":\"0f325c15738d4bfa85456f2a7e91b2ff\",\"Title\":\"487_副本 6\",\"Index\":1,\"CutFlag\":true,\"TextFlag\":false,\"DeWatermarkFlag\":true,\"Duration\":7.5,\"VirginDuration\":15.16,\"Width\":640,\"Height\":360,\"URL\":\"http://vod.testtestapsaravideo.cn/0f325c15738d4bfa85456f2a7e91b2ff/ba9dd0e93a4c4ec288abea8f11d7ec94-699a80a29a15c59c9d0868389f86cc3f.mp4\",\"CoverURL;\":\"\",\"SpriteURLs\":\"http://vod.testtestapsaravideo.cn/material_big_snapshot/0f325c15738d4bfa85456f2a7e91b2ff00001.jpg?auth_key=\",\"In\":0,\"Out\":7.5,\"TimelineIn\":9.42,\"TimelineOut\":16.92,\"Effects\":[{\"Type\":\"DeWatermark\",\"Name\":\"水印/遮标\",\"SubType\":\"Delogo_Blur\",\"X\":\"0.7660\",\"Y\":\"0.0333\",\"Width\":100,\"Height\":50,\"FEHeight\":281.25,\"FEWidth\":500,\"In\":0,\"Out\":7.5,\"TimelineIn\":9.42,\"TimelineOut\":16.92}]},{\"Id\":\"07c2b35dd2f342da98b8c3e45e456a41_1\",\"Title\":\"487_副本 6\",\"VideoId\":\"07c2b35dd2f342da98b8c3e45e456a41\",\"Index\":2,\"CutFlag\":true,\"TextFlag\":true,\"DeWatermarkFlag\":true,\"Duration\":5.74,\"VirginDuration\":15.16,\"URL\":\"http://vod.testtestapsaravideo.cn/07c2b35dd2f342da98b8c3e45e456a41/c228bc42b97047299108fcf9796c9223-699a80a29a15c59c9d0868389f86cc3f.mp4\",\"CoverURL\":\"\",\"SpriteURLs\":\"http://vod.testtestapsaravideo.cn/material_big_snapshot/07c2b35dd2f342da98b8c3e45e456a4100001.jpg?auth_key=\",\"Width\":640,\"Height\":360,\"In\":0,\"Out\":5.74,\"TimelineIn\":16.92,\"TimelineOut\":22.66,\"Effects\":[{\"Type\":\"Text\",\"Name\":\"横幅文字\",\"Font\":\"SimSun\",\"FontFace\":{\"Bold\":false,\"Italic\":false,\"Underline\":false},\"FontColor\":\"#ffffff\",\"FontSize\":20,\"FontColorOpacity\":1,\"Content\":\"logo\",\"X\":\"0.3000\",\"Y\":\"0.7000\",\"Bold\":\"false\",\"Italic\":\"false\",\"Underline\":\"false\",\"Height\":23.599999999999998,\"Width\":41,\"FEHeight\":281.25,\"FEWidth\":500,\"In\":0,\"Out\":5.74,\"TimelineIn\":16.92,\"TimelineOut\":22.66},{\"Type\":\"DeWatermark\",\"Name\":\"水印/遮标\",\"SubType\":\"Delogo_Blur\",\"X\":\"0.0300\",\"Y\":\"0.0547\",\"Width\":100,\"Height\":50,\"FEHeight\":281.25,\"FEWidth\":500,\"In\":0,\"Out\":5.74,\"TimelineIn\":16.92,\"TimelineOut\":22.66}]}]}],\"AudioTracks\":[{\"Count\":0,\"Duration\":0,\"AudioTrackClips\":[]}]}",
		"ProjectId":"25cfc178d2de418baace77aebed6afcd",
		"Title":"视频_1508736815000"
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

