# 服务端SDK发布历史

## 2020-09-10 Version: 2.15.10

1.  新增：增加对北京区域的支持。上传SDK等建议修改为最新版本。
2.  新增：新增智能封面任务提交、任务查询、封面媒资信息查询接口。
3.  新增：新增动图查询接口。
4.  修改：智能审核增加MediaAuditConfiguration参数，支持ResourceType，用于支持不同类型视频的审核规格和标准

## 2020-06-22 Version: 2.15.10

1.  新增：增加对深圳区域的支持。上传SDK等建议修改为最新版本。

## 2020-06-04 Version: 2.15.9

1.  新增：DNA指纹删除SubmitMediaDNADeleteJob和查询删除任务ListMediaDNADeleteJob接口
2.  修改：查询审核结果\(GetMediaAuditResult\), 返回支持ad/logo/live结果
3.  修改：查询审核结果\(GetMediaAuditResultTimeline\), 返回支持ad/logo/live结果

## 2019-10-23 Version: 2.15.8

1.  新增：提交动图作业接口\(SubmitDynamicImageJob\)，可截取视频的某个片段为动态图片\(GIF/WebP\)。
2.  新增：提交点播工作流作业接口\(SubmitWorkflowJob\)，可对音视频发起点播工作流处理。
3.  修改：获取图片信息接口\(GetImageInfo\)，返回结构ImageInfo中新增字段AuditStatus\(图片审核状态\)。
4.  修改：获取辅助媒资信息接口\(GetAttachedMediaInfo\)，修正返回字段StorageLocation的数据类型为String。
5.  修改：提交智能审核作业接口\(SubmitAIMediaAuditJob\)，请求参数新增字段MediaType\(媒体类型\)。

## 2019-06-24 Version: 2.15.5

1.  新增：域名管理的`7个`接口，包括：
    -   添加加速域名\(AddVodDomain\)
    -   修改加速域名\(UpdateVodDomain\)
    -   删除加速域名\(DeleteVodDomain\)
    -   启用加速域名\(BatchStartVodDomain\)
    -   停用加速域名\(BatchStopVodDomain\)
    -   查询加速域名列表\(DescribeVodUserDomains\)
    -   查询域名基本信息\(DescribeVodDomainDetail\)
2.  新增：域名配置的`6`个接口，包括：
    -   批量配置域名\(BatchSetVodDomainConfigs\)
    -   查询域名配置\(DescribeVodDomainConfigs\)
    -   删除域名配置\(DeleteVodSpecificConfig\)
    -   设置域名证书\(SetVodDomainCertificate\)
    -   查询证书列表\(DescribeVodCertificateList\)
    -   查询域名证书\(escribeVodDomainCertificateInfo\)
3.  修改：模板、水印等接口支持多应用，包括添加转码模板组\(AddTranscodeTemplateGroup\)、查询转码模板组\(GetTranscodeTemplateGroup\)、查询转码模板组列表\(ListTranscodeTemplateGroup\)、添加水印\(AddWatermark\)、查询水印\(GetWatermark\)、查询水印列表\(ListWatermark\)、URL批量拉取上传\(UploadMediaByURL\)等。
4.  修改：提交媒体转码作业\(SubmitTranscodeJobs\)新增字段`UserData`，支持用户自定义的扩展字段，可用于事件通知时透传返回。

## 2019-05-16 Version: 2.15.3

1.  新增：用量查询的`4个`接口，包括：
    -   查询流量带宽用量\(DescribeVodDomainUsageData\)
    -   查询存储用量\(DescribeVodStorageData\)
    -   查询转码用量\(DescribeVodTranscodeData\)
    -   查询AI处理用量\(DescribeVodAIData\)
2.  新增：获取媒体上传详情的接口\(GetUploadDetails\)
3.  新增：查询多模态综合标签的接口\(GetAIVideoTagResult\)
4.  修改：获取辅助媒资\(GetAttachedMediaInfo\)、获取图片信息\(GetImageInfo\)接口增加返回字段`RegionId`\(存储区域\)
5.  修改：搜索媒资信息\(SearchMedia\)、获取辅助媒资\(GetAttachedMediaInfo\)、创建辅助媒资\(CreateUploadAttachedMedia\)等接口增加字段`Icon`和`OnlineStatus`，以管理短视频素材。
6.  修改：提交截图作业接口\(SubmitSnapshotJob\)新增字段`UserData`，支持用户自定义的扩展字段，可用于回调时透传返回。

## 2019-04-11 Version: 2.15.2

1.  新增：多应用管理和授权的`9个`接口，包括：
    -   创建应用\(CreateAppInfo\)
    -   查询应用信息\(GetAppInfos\)
    -   获取应用信息列表\(ListAppInfo\)
    -   更新应用信息\(UpdateAppInfo\)
    -   删除应用\(DeleteAppInfo\)
    -   为身份实体附加应用授权\(AttachAppPolicyToIdentity\)
    -   为身份实体撤销应用授权\(DetachAppPolicyFromIdentity\)
    -   查询身份实体被授予的应用权限列表\(ListAppPoliciesForIdentity\)
    -   迁移资源到新应用\(MoveAppResource\)
2.  新增：事件通知\(消息回调\)配置的`3个`接口，包括：
    -   设置事件通知配置\(SetMessageCallback\)
    -   查询事件通知配置\(GetMessageCallback\)
    -   删除事件通知配置\(DeleteMessageCallback\)
3.  新增：辅助媒资相关的`3个`接口，包括：
    -   获取辅助媒资信息\(GetAttachedMedia\)
    -   更新辅助媒资信息\(UpdateAttachedMediaInfos\)
    -   删除辅助媒资\(DeleteAttachedMedia\)
4.  新增：删除上传中产生的碎片文件的接口\(DeleteMultipartUpload\)
5.  修改：媒体上传、媒资管理的相关接口支持多应用，上传、搜索和列表接口新增`AppId`参数，如CreateUploadVideo、SearchMedia等；DeleteVideo接口增加`NonExistVideoIds`和`ForbiddenVideoIds`字段，UpdateVideoInfos接口增加`ForbiddenVideoIds`字段。
6.  修改：云剪辑支持多区域、多素材类型，GetEditingProject接口增加返回字段`StorageLocation`和`RegionId`；SearchEditingProject接口增加返回字段`StorageLocation`、`RegionId`和`Duration`；GetEditingProjectMaterials接口增加请求参数`MaterialType`。
7.  修改：转码支持自定义文件路径等，GetTranscodeTemplateGroup接口增加返回字段`TranscodeFileRegular`、`Clip`和`Rotate`。
8.  修改：搜索媒资接口SearchMedia支持辅助媒资，新增返回字段`AttachedMedia`。
9.  修改：获取分类列表接口GetCategories增加返回字段`SubTotal`\(子分类个数\)。
10. 修改：媒资管理支持自定义媒资字段，GetVideoInfo和GetVideoInfos接口，新增请求参数`AddtionType`，可指定获取自定义媒资信息，对应返回字段`CustomMediaInfo`。

## 2019-02-28 Version: 2.15.1

1.  新增：查询视频转码信息的`3个`接口，包括：
    -   查询视频转码摘要\(GetTranscodeSummary\)
    -   查询转码任务列表\(ListTranscodeTask\)
    -   查询转码任务详情\(GetTranscodeTask\)
2.  修改：删除转码模板组接口\(DeleteTranscodeTemplateGroup\)，增加请求参数`TranscodeTemplateIds`\(可删除模板组下的转码模板\)、`ForceDelGroup`\(可强制删除整个模板组\)，返回字段增加`NonExistTranscodeTemplateIds`。
3.  修改：获取源文件信息接口\(GetMezzanineInfo\)，返回字段`VideoStream`增加子项`Rotate`\(视频旋转标记\)。
4.  修改：获取图片信息接口\(GetImageInfo\)，增加返回字段`Status`\(图片状态\)。
5.  修改：修改视频信息接口\(UpdateVideoInfo\)增加请求参数`CustomMediaInfo`, 获取视频信息接口\(GetVideoInfo\)、搜索媒资信息接口\(SearchMedia\)增加返回字段`CustomMediaInfo`，表示用户自定义媒资信息。同时，SearchMedia还增加了媒体审核相关字段。
6.  删除：废弃旧的删除转码模板接口\(DeleteTranscodeTemplates\)，功能被DeleteTranscodeTemplateGroup替代。

## 2019-01-30 Version: 2.15.0

本次更新主要是清理了部分不再使用或仅控制台使用的接口，以免对您造成不必要的干扰，详情如下： 1. 新增：查询URL上传任务的接口GetURLUploadInfos

1.  删除：部分不再使用的接口
    -   点播CDN相关的旧版即将下线的接口，如DescribeDomainBpsData等，替换为[新版CDN接口](/cn.zh-CN/服务端API/API概览.mdsection_kcd_ury_w4b)
    -   旧版点播AI相关接口，如SubmitAIASRJob等，替换为[新版AI接口](/cn.zh-CN/服务端API/API概览.md)
    -   旧版播放器曾使用过但现已不再支持的GetVideoPlayInfo接口
2.  删除：部分仅控制台使用的接口，避免误用，如OpenVodService等

**说明：** 所有点播支持的接口请参考[API概览](/cn.zh-CN/服务端API/API概览.md)

## 2019-01-15 Version: 2.12.0

1.  新增：转码模板相关的`7个`接口，包括：
    -   添加转码模板组\(AddTranscodeTemplateGroup\)
    -   修改转码模板组\(UpdateTranscodeTemplateGroup\)
    -   删除转码模板组\(DeleteTranscodeTemplateGroup\)
    -   查询转码模板组\(GetTranscodeTemplateGroup\)
    -   获取转码模板组列表\(ListTranscodeTemplateGroup\)
    -   设置默认转码模板组\(SetDefaultTranscodeTemplateGroup\)
    -   删除模板组的转码模板\(DeleteTranscodeTemplates\)
2.  新增：AI模板相关的`7个`接口，包括：
    -   添加AI模板\(AddAITemplate\)
    -   修改AI模板\(UpdateAITemplate\)
    -   删除AI模板\(DeleteAITemplate\)
    -   查询AI模板\(GetAITemplate\)
    -   获取AI模板列表\(ListAITemplate\)
    -   设置默认的AI模板\(SetDefaultAITemplate\)
    -   获取默认的AI模板\(GetDefaultAITemplate\)
3.  新增：智能审核相关的`5个`接口，包括

    -   提交智能审核作业\(SubmitAIMediaAuditJob\)
    -   查询智能审核作业\(GetAIMediaAuditJob\)
    -   获取智能审核结果摘要\(GetMediaAuditResult\)
    -   获取智能审核结果详情\(GetMediaAuditResultDetail\)
    -   获取智能审核结果时间线\(GetMediaAuditResultTimeline\)
    **说明：** 原有的智能审核接口SubmitAIJob、ListAIJob、GetAuditResult、GetAuditResultDetail后续不再迭代，请使用最新的接口。

4.  新增：点播CDN相关的`7个`接口，包括

    -   查询加速域名的流量数据\(DescribeVodDomainTrafficData\)
    -   查询加速域名的网络带宽\(DescribeVodDomainBpsData\)
    -   预热缓存\(PreloadVodObjectCaches\)，可将源站媒体文件主动预热到CDN Cache节点上
    -   刷新缓存\(RefreshVodObjectCaches\)，可批量刷新CDN Cache节点上的内容
    -   查询刷新和预热状态\(DescribeVodRefreshTasks\)
    -   查询刷新预热次数限制和余量\(DescribeVodRefreshQuota\)
    -   下载域名日志\(DescribeVodDomainLog\)，可获取指定域名的CDN原始访问日志下载地址。
    **说明：** 原有的CDN相关接口后续不再迭代，请使用最新的接口，新、旧版本接口差异请参考[点播CDN新版API更新说明](/cn.zh-CN/服务端API/点播CDN/旧版API(即将下线)/新版API更新说明.md)。

5.  修改：提交媒体转码作业接口\(SubmitTranscodeJobs\)支持参数`Priority`，可设置提交作业的优先级
6.  修改：上传相关的接口支持`UserData`参数，可设置消息回调地址和自定义扩展字段等，包括：URL批量拉取上传\(UploadMediaByURL\)、获取图片上传地址和凭证\(CreateUploadImage\)、获取辅助媒资上传地址和凭证\(CreateUploadAttachedMedia\)

## 2018-12-16 Version: 2.11.9

1.  新增：添加媒体序列AddMediaSequences接口，该接口可用于在剪辑合成场景下，添加带入出点\(开始和结束时间\)的音视频素材列表，素材可以是离线的音视频文件，也可以是实时的直播流。

## 2018-11-30 Version: 2.11.8

1.  新增：截图模板相关的`5个`接口，包括
    -   添加截图模板\(AddVodTemplate\)
    -   修改截图模板\(UpdateVodTemplate\)
    -   删除截图模板\(DeleteVodTemplate\)
    -   查询单个截图模板\(GetVodTemplate\)
2.  新增：获取辅助媒资上传地址和凭证的接口CreateUploadAttachedMedia，辅助媒资包括水印、字幕文件等。

## 2018-11-21 Version: 2.11.7

1.  新增：视频水印相关的`6个`接口，包括
    -   添加水印\(AddWatermark\)
    -   修改水印\(UpdateWatermark\)
    -   删除水印\(DeleteWatermark\)
    -   查询单个水印\(GetWatermark\)
    -   查询水印列表\(ListWatermarks\)
    -   设置默认水印\(SetDefaultWatermark\)
2.  新增：注册媒资信息接口RegisterMedia，支持对已存在于OSS的音视频媒体文件注册媒资，但前提是该OSS bucket已线下接入点播。
3.  修改：提交媒体转码作业接口\(SubmitTranscodeJobs\)支持参数`OverrideParams`，可在提交转码时替换设置的模板参数，如替换图片、文字水印。

## 2018-10-11 Version: 2.11.6

1.  新增：媒资管理相关的`2个`接口，包括
    -   批量删除源文件\(DeleteMezzanines\)，支持批量删除上传的音视频源文件。
    -   批量更新图片信息\(UpdateImageInfos\)，可批量更新图片的标题、简介、标签、分类等信息。
2.  修改：获取视频播放凭证接口\(GetVideoPlayAuth\)支持参数`PlayConfig`，可自定义播放设置，如指定CDN加速域名进行播放。

## 2018-08-17 Version: 2.11.5

1.  新增：删除图片接口\(DeleteImage\)，可批量删除上传的图片文件、视频封面截图等。
2.  修改：获取源文件信息\(GetMezzanineInfo\)，支持参数`AdditionType`和`OutputType`。AdditionType可指定返回的附加信息，OutputType可指定地址类型，如OSS源站存储地址或CDN加速地址。
3.  修改：获取视频播放地址接口\(GetPlayInfo\)增加返回字段`CreationTime`和`ModificationTime`，分别表示音视频创建和最近更新的UTC时间。

## 2018-08-04 Version: 2.11.4

1.  新增：媒体审核相关的`2个`接口，包括
    -   设置审核安全IP\(SetAuditSecurityIp\)，当视频状态为审核中或屏蔽状态时，只有来自审核安全IP的请求才能播放。
    -   获取审核安全IP列表\(ListAuditSecurityIp\)
2.  新增：URL批量拉取上传接口\(UploadMediaByURL\)，可批量拉取指定的URL的媒体文件上传到点播。
3.  修改：获取视频信息接口\(GetVideoInfo\)、批量获取视频信息接口\(GetVideoInfos\)，新增返回字段`StorageLocation`和`TemplateGroupId`，分别表示视频的存储地址、上传时指定的转码模板组ID。
4.  获取视频播放地址接口\(GetPlayInfo\)，新增返回字段`OutputType`和`Status`，分别表示播放地址的类型\(存储地址或加速地址\)、视频状态。

## 2018-07-10 Version: 2.11.3

1.  新增：媒体审核相关的`2个`接口，包括
    -   人工审核接口\(CreateAudit\)，可人工审核\(屏蔽或通过\)音视频。
    -   获取人工审核历史\(GetAuditHistory\)，可查下审核的历史记录。
2.  新增：媒资管理相关的`4个`接口，包括
    -   批量获取视频信息\(GetVideoInfos\)
    -   批量修改视频信息\(UpdateVideoInfos\)
    -   搜索媒资信息\(SearchMedia\)，支持对视频、音频、图片等媒资信息进行搜索、过滤、排序等。
    -   查询截图数据\(ListSnapshots\)
3.  修改：获取源文件信息接口\(GetMezzanineInfo\)，新增返回字段`VideoStreamList`\(视频流信息\)和`AudioStreamList`\(音频流信息\)。

## 2018-07-03 Version: 2.11.2

1.  修改：视频剪辑合成接口\(ProduceEditingProjectVideo\)支持参数`UserData`，可自定义消息回调地址等设置。

## 2018-06-22 Version: 2.11.1

1.  修改：获取视频播放地址接口\(GetPlayInfo\)支持参数`ResultType`，可指定返回数据类型，如返回所有转码输出的流；同时返回字段增加`WatermarkId`，表示使用的视频水印ID，可用来区分转码输出的流是否带有水印。

## 2018-05-10 Version: 2.11.0

1.  新增：提交导播台视频预处理接口\(SubmitPreprocessJobs\)，支持对用于导播台的音视频进行预处理。
2.  修改：获取源文件信息接口\(GetMezzanineInfo\)、获取视频信息接口\(GetVideoInfo\)、获取视频播放地址接口\(GetPlayInfo\)，增加返回字段`PreprocessStatus`\(导播台预处理状态\)。
3.  修改：获取直转点视频列表接口\(ListLiveRecordVideo\)，新增返回字段`CreationTime`\(视频创建的UTC时间\)和`StorageLocation`\(存储地址\)。
4.  修改：、获取视频信息接口\(GetVideoInfo\)支持参数`OutputType`，可指定返回播放地址的类型\(存储地址或加速地址\)。

## 2018-04-01 Version: 2.10.0

1.  新增：数据统计相关的`4个`接口，包括：
    -   播放数据总量统计\(DescribePlayUserTotal\)，可获取指定时间范围内的每日播放数总量统计。
    -   播放数据均量统计\(DescribePlayUserAvg\)，可获取指定时间范围内的每日播放数据均量统计。
    -   TOP视频播放数据统计\(DescribePlayTopVideos\)，可获取每日TOP视频的播放数据统计（包括VV、UV和播放总时长）。
    -   单视频播放数据统计\(DescribePlayVideoStatis\)，可获取指定视频在指定时间范围内的每日播放统计数据。
2.  新增：点播CDN相关的`4个`接口，包括：
    -   预热缓存\(PushObjectCache\)，将源站媒体文件主动预热到CDN Cache节点上，首次访问可直接命中缓存，缓解源站压力。
    -   刷新缓存\(RefreshObjectCaches\)，可批量刷新CDN Cache节点上的内容。
    -   查询刷新和预热状态\(DescribeRefreshTasks\)
    -   查询刷新预热次数限制和余量\(DescribeRefreshQuota\)
3.  新增：媒体处理相关的`2个`接口，包括：
    -   提交媒体转码作业\(SubmitTranscodeJobs\)，可对音视频主动发起转码、重转码。
    -   提交媒体截图作业\(SubmitSnapshotJob\)，支持对视频发起普通截图、雪碧图截图。
4.  修改：视频剪辑合成接口\(ProduceEditingProjectVideo\)，支持`2个`新增参数：
    -   MediaMetadata，设置合成视频的元数据，如标题、简介、标签、分类等。
    -   ProduceConfig，合成时的配置，如TemplateGroupId，视频合成完后，以合成文件为源文件，启动转码时所使用的转码模板组ID。

## 2017-12-21 Version: 2.9.0

1.  新增：获取直转点视频列表接口\(ListLiveRecordVideo\)，可获取直播录制到点播的视频列表。

## 2017-12-07 Version: 2.8.0

1.  新增：查询AI作业接口\(ListAIJob\)，可批量查询视频AI作业信息。

## 2017-11-29 Version: 2.7.0

1.  获取视频播放地址接口GetPlayInfo, 增加按清晰度筛选媒体流地址。
2.  刷新视频上传凭证接口RefreshUploadVideo, 返回数据增加UploadAddress。
3.  获取视频上传凭证和地址接口CreateUploadVideo, 增加模板组ID\(TemplateGroupId\)参数, 支持用户自定义模板组功能。
4.  获取视频信息接口GetVideoInfo, 增加指定返回数据类型\(ResultTypes\)参数, 返回AI处理结果。
5.  新增视频分类相关接口, 包括提交视频分类作业SubmitAIASRJob和查询视频分类作业ListAIASRJob。
6.  新增提交AI作业的通用接口SubmitAIJob, 增加5项新的AI能力\(视频标注,视频文本识别,名人识别,政治人物识别敏感人物识别\), 并支持针对单个资源一次提交多个AI Feature。
7.  获取图片上传地址和凭证接口CreateUploadImage, 输入参数增加Title\(标题\), Tags\(标签\),OriginalFileName\(图片原始文件名\)字段, 输出参数增加ImageId\(图片Id\)字段。
8.  新增获取图片信息接口GetImageInfo。

## 2017-11-03 Version: 2.6.0

1.  获取视频播放地址接口GetPlayInfo，增加二次鉴权参数，返回结构体PlayInfo中增加JobId。
2.  获取视频播放凭证接口GetVideoPlayAuth，增加二次鉴权参数，支持用户自定义AuthInfo过期时间。
3.  新增删除流信息接口DeleteStream，根据JobId删除某一路媒体流文件及信息。
4.  新增提交截图作业接口SubmitSnapshotJob。
5.  新增云剪辑工程及视频合成相关接口，创建云剪辑工程AddEditingProject、修改云剪辑工程UpdateEditingProject、合成成品视频ProduceEditingProjectVideo、设置云剪辑工程素材 SetEditingProjectMaterials、获取云剪辑工程素材GetEditingProjectMaterials、获取单个云剪辑工程GetEditingProject、搜索云剪辑工程SearchEditingProject、删除云剪辑工程DeleteEditingProject。
6.  新增点播cdn资源监控及日志下载相关接口，日志信息－下载域名日志DescribeCdnDomainLogs、资源监控－查询网络带宽DescribeDomainBpsData、资源监控－查询流量数据DescribeDomainFlowData。
7.  新增视频暴恐涉政鉴别\(AI\)相关接口，提交视频暴恐涉政鉴别作业SubmitAIVideoTerrorismRecogJob、查询视频暴恐涉政鉴别作业ListAIVideoTerrorismRecogJob。
8.  新增视频内容审核\(AI\)相关接口，提交视频内容审核作业SubmitAIVideoCensorJob、查询视频内容审核作业ListAIVideoCensorJob。

## 2017-10-15 Version: 2.5.0

1.  新增语音识别文本相关接口，包括提交语音识别作业SubmitAIASRJob、查询语音识别作业ListAIASRJob
2.  新增视频摘要相关接口，包括提交视频摘要作业SubmitAIVideoSummaryJob、查询视频摘要作业ListAIVideoSummaryJob
3.  视频AI智能首图和视频鉴黄相关接口SubmitAIVideoCoverJob、ListAIVideoCoverJob、SubmitAIVideoPornRecogJob、ListAIVideoPornRecogJob, 返回结构体Job中，将Id字段重命名为JobId。
4.  获取视频播放地址接口GetPlayInfo，返回结构体PlayInfo中, 增加流类型StreamType, 如果输出为视频流, 取值: video, 输出为音频流, 取值: audio。

## 2017-09-20 Version: 2.4.0

1.  增加了获取源文件地址接口GetMezzanineInfo接口。
2.  提交视频智能首图服务SubmitAIVideoCoverJob：请求参数增加MediaId字段，废弃Input字段（之前尚无使用），将原Input字段放在AIVideoCoverConfig之下 ；返回值中的Job参数增加MediaId字段。
3.  查询视频智能首图服务ListAIVideoCoverJob：返回参数的层级调整：AIVideoCoverJobList作为数组返回，返回值中的Job参数增加MediaId字段。
4.  提交视频鉴黄服务SubmitAIVideoPornRecogJob：接口的请求参数，VideoId字段改名为MediaId；返回值中的Job参数增加MediaId字段。
5.  查询视频鉴黄服务ListAIVideoPornRecogJob：返回值中的Job参数增加MediaId字段。

## 2017-09-01 Version: 2.3.1

1.  增加了提交视频智能首图作业SubmitAIVideoCoverJob接口。
2.  增加了获取视频智能首图作业ListAIVideoCoverJob接口。
3.  提交视频智能鉴黄作业SubmitAIVideoPornRecogJob接口。
4.  获取视频智能鉴黄作业ListAIVideoPornRecogJob接口。
5.  获取视频上传地址和凭证CreateUploadVideo接口增加TranscodeMode和UserData参数。

