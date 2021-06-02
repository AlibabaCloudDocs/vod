API概览 
==========================



本文为您介绍了点播服务的所有API列表。


**说明**

建议您使用[服务端SDK](/cn.zh-CN/服务端SDK/使用说明.md)来调用API。使用API时，接入地址请参见[点播中心和访问域名](/cn.zh-CN/开发指南/点播中心和访问域名.md)，使用限制，请参见使用限制。

媒体上传 
-------------------------



|                                         API                                         |                             描述                              |
|-------------------------------------------------------------------------------------|-------------------------------------------------------------|
| [CreateUploadVideo](/cn.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)           | 调用CreateUploadVideo获取视频上传地址和凭证，并创建视频信息。                     |
| [RefreshUploadVideo](/cn.zh-CN/服务端API/媒体上传/刷新视频上传凭证.md)             | 调用RefreshUploadVideo用于视频文件上传超时后重新获取视频上传凭证                   |
| [CreateUploadImage](/cn.zh-CN/服务端API/媒体上传/获取图片上传地址和凭证.md)           | 调用CreateUploadImage获取图片上传地址和凭证。                             |
| [CreateUploadAttachedMedia](/cn.zh-CN/服务端API/媒体上传/获取辅助媒资上传地址和凭证.md) | 调用CreateUploadAttachedMedia获取辅助媒资上传地址和凭证，辅助媒资包括水印、字幕文件等。    |
| [UploadMediaByURL](/cn.zh-CN/服务端API/媒体上传/URL批量拉取上传.md)              | 调用UploadMediaByURL基于源文件URL，批量拉取媒体文件进行上传。                    |
| [GetURLUploadInfos](/cn.zh-CN/服务端API/媒体上传/获取URL上传信息.md)             | 调用GetURLUploadInfos获取URL上传信息。                               |
| [DeleteMultipartUpload](/cn.zh-CN/服务端API/媒体上传/删除上传中的碎片文件.md)        | 调用DeleteMultipartUpload立即删除上传中产生的碎片文件。                      |
| [GetUploadDetails](/cn.zh-CN/服务端API/媒体上传/获取媒体上传详情.md)               | 调用GetUploadDetails通过媒资ID（支持批量）获取媒资上传详情，如上传时间、已上传比例、上传来源等信息。 |
| [RegisterMedia](/cn.zh-CN/服务端API/媒体上传/注册媒资信息.md)                    | 调用RegisterMedia进行媒资注册。                                      |



音视频播放 
--------------------------



|                                  API                                   |                     描述                     |
|------------------------------------------------------------------------|--------------------------------------------|
| [GetPlayInfo](/cn.zh-CN/服务端API/音视频播放/获取视频播放地址.md)      | 调用GetPlayInfo通过视频ID直接获取媒体文件（支持视频和音频）的播放地址。 |
| [GetVideoPlayAuth](/cn.zh-CN/服务端API/音视频播放/获取视频播放凭证.md) | 调用GetVideoPlayAuth获取视频播放时所需的播放凭证。          |



媒资管理 
-------------------------

**媒资搜索** 


|                                 API                                 |                  描述                  |
|---------------------------------------------------------------------|--------------------------------------|
| [SearchMedia](/cn.zh-CN/服务端API/媒资管理/媒资搜索/搜索媒体信息.md) | 调用SearchMedia搜索媒资信息（视频、音频、图片、辅助媒资等）。 |



**媒资分类** 


|                                   API                                   |                          描述                           |
|-------------------------------------------------------------------------|-------------------------------------------------------|
| [AddCategory](/cn.zh-CN/服务端API/媒资管理/媒资分类/创建分类.md)       | 调用AddCategory创建视频分类。最大支持三级分类，每个分类最多支持创建100个子分类。       |
| [UpdateCategory](/cn.zh-CN/服务端API/媒资管理/媒资分类/更新分类.md)    | 调用UpdateCategory修改视频分类。                               |
| [DeleteCategory](/cn.zh-CN/服务端API/媒资管理/媒资分类/删除分类.md)    | 调用DeleteCategory删除视频分类，同时会删除其下级分类（包括二级分类和三级分类），请慎重操作。 |
| [GetCategories](/cn.zh-CN/服务端API/媒资管理/媒资分类/获取分类及子分类.md) | 调用GetCategories获取指定的分类信息，及其子分类（即下一级分类）的列表。            |



**音视频管理** 


|                                     API                                     |                                    描述                                     |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| [GetVideoInfo](/cn.zh-CN/服务端API/媒资管理/音视频管理/获取视频信息.md)       | 调用GetVideoInfo通过视频ID获取视频的基本信息，包括：视频标题、描述、时长、封面URL、状态、创建时间、大小、截图、分类和标签等信息。 |
| [UpdateVideoInfo](/cn.zh-CN/服务端API/媒资管理/音视频管理/修改视频信息.md)    | 调用UpdateVideoInfo修改视频信息。                                                  |
| [UpdateVideoInfos](/cn.zh-CN/服务端API/媒资管理/音视频管理/批量修改视频信息.md) | 调用UpdateVideoInfos批量修改视频信息。                                               |
| [DeleteMezzanines](/cn.zh-CN/服务端API/媒资管理/音视频管理/批量删除源文件.md)  | 调用DeleteMezzanines批量删除源文件信息及存储。                                           |
| [DeleteStream](/cn.zh-CN/服务端API/媒资管理/音视频管理/删除媒体流.md)        | 调用DeleteStream删除媒体流(视频流，音频流)信息及存储文件，并且支持批量删除。                             |
| [DeleteVideo](/cn.zh-CN/服务端API/媒资管理/音视频管理/删除完整视频.md)        | 调用DeleteVideo删除完整视频（包括其源文件、转码后的流文件、封面截图等），支持批量删除。                         |
| [GetMezzanineInfo](/cn.zh-CN/服务端API/媒资管理/音视频管理/获取源文件信息.md)  | 调用GetMezzanineInfo获取音视频的源文件信息，包括文件地址、分辨率、码率等。                             |
| [GetVideoList](/cn.zh-CN/服务端API/媒资管理/音视频管理/获取视频信息列表.md)     | 调用GetVideoList获取视频信息列表。                                                   |
| [GetVideoInfos](/cn.zh-CN/服务端API/媒资管理/音视频管理/批量获取视频信息.md)    | 调用GetVideoInfos批量获取视频信息。                                                  |



**图片管理** 


|                                    API                                     |               描述               |
|----------------------------------------------------------------------------|--------------------------------|
| [DeleteImage](/cn.zh-CN/服务端API/媒资管理/图片管理/删除图片.md)          | 调用DeleteImage删除用户上传的图片及视频自动截图。 |
| [GetImageInfo](/cn.zh-CN/服务端API/媒资管理/图片管理/获取图片信息.md)       | 调用GetImageInfo获取图片的基本信息。       |
| [UpdateImageInfos](/cn.zh-CN/服务端API/媒资管理/图片管理/批量更新图片信息.md) | 调用UpdateImageInfos批量修改图片信息。    |
| [ListSnapshots](/cn.zh-CN/服务端API/媒资管理/图片管理/查询截图数据.md)      | 调用ListSnapshots查询指定媒体截图。       |



**辅助媒资管理** 


|                                         API                                          |                          描述                           |
|--------------------------------------------------------------------------------------|-------------------------------------------------------|
| [GetAttachedMediaInfo](/cn.zh-CN/服务端API/媒资管理/辅助媒资管理/获取辅助媒资信息.md)     | 调用GetAttachedMediaInfo批量获取辅助媒资的基本信息，包括标题、类型、标签、创建时间等。 |
| [UpdateAttachedMediaInfos](/cn.zh-CN/服务端API/媒资管理/辅助媒资管理/更新辅助媒资信息.md) | 调用UpdateAttachedMediaInfos批量修改辅助媒资信息。                 |
| [DeleteAttachedMedia](/cn.zh-CN/服务端API/媒资管理/辅助媒资管理/删除辅助媒资.md)        | 调用DeleteAttachedMedia删除辅助媒资，支持批量删除。                   |



**动图管理** 


|                                    API                                     |              描述              |
|----------------------------------------------------------------------------|------------------------------|
| [ListDynamicImage](/cn.zh-CN/服务端API/媒资管理/动图管理/查询动图列表.md)   | 调用ListDynamicImage查询视频截动图列表。 |
| [DeleteDynamicImage](/cn.zh-CN/服务端API/媒资管理/动图管理/删除动图信息.md) | 调用DeleteDynamicImage删除动图信息。  |



媒体处理 
-------------------------

**发起处理** 


|                                       API                                       |                         描述                         |
|---------------------------------------------------------------------------------|----------------------------------------------------|
| [SubmitTranscodeJobs](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体转码作业.md)   | 调用SubmitTranscodeJobs提交媒体转码作业，开始异步转码处理。            |
| [SubmitSnapshotJob](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体截图作业.md)     | 调用SubmitSnapshotJob提交视频截图作业，开始异步截图处理。支持普通截图和雪碧图截图。 |
| [SubmitDynamicImageJob](/cn.zh-CN/服务端API/媒体处理/发起处理/提交媒体动图作业.md) | 调用SubmitDynamicImageJob提交媒体动图作业，开始异步处理。            |
| [SubmitPreprocessJobs](/cn.zh-CN/服务端API/媒体处理/发起处理/导播台视频预处理.md)  | 调用SubmitPreprocessJobs提交导播台视频预处理。                  |
| [SubmitWorkflowJob](/cn.zh-CN/服务端API/媒体处理/发起处理/提交点播工作流作业.md)    | 调用SubmitWorkflowJob，可对音视频发起点播工作流处理。                |



**转码模板** 


|                                            API                                             |                                   描述                                   |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| [AddTranscodeTemplateGroup](/cn.zh-CN/服务端API/媒体处理/转码模板/创建转码模板组.md)         | 调用AddTranscodeTemplateGroup添加转码配置信息，可创建新的转码模板组，或者向指定模板组中添加新的转码模板。      |
| [UpdateTranscodeTemplateGroup](/cn.zh-CN/服务端API/媒体处理/转码模板/修改转码配置.md)       | 调用UpdateTranscodeTemplateGroup修改转码配置信息，可修改转码模板组下指定的转码模板配置。             |
| [DeleteTranscodeTemplateGroup](/cn.zh-CN/服务端API/媒体处理/转码模板/删除转码配置.md)       | 调用DeleteTranscodeTemplateGroup删除转码配置信息，可删除转码模板组下的部分转码模板，也可强制删除整个转码模板组。 |
| [ListTranscodeTemplateGroup](/cn.zh-CN/服务端API/媒体处理/转码模板/查询转码配置列表.md)       | 调用ListTranscodeTemplateGroup查询转码模板配置列表。                                |
| [SetDefaultTranscodeTemplateGroup](/cn.zh-CN/服务端API/媒体处理/转码模板/设置默认转码配置.md) | 调用SetDefaultTranscodeTemplateGroup设置默认转码模板配置。                          |
| [GetTranscodeTemplateGroup](/cn.zh-CN/服务端API/媒体处理/转码模板/查询转码配置详情.md)        | 调用GetTranscodeTemplateGroup根据转码模板组ID查询转码配置的详细信息。                       |



**视频水印** 


|                                     API                                     |              描述              |
|-----------------------------------------------------------------------------|------------------------------|
| [AddWatermark](/cn.zh-CN/服务端API/媒体处理/视频水印/添加水印.md)          | 调用AddWatermark添加水印数据。        |
| [UpdateWatermark](/cn.zh-CN/服务端API/媒体处理/视频水印/修改水印.md)       | 调用UpdateWatermark更新水印数据。     |
| [DeleteWatermark](/cn.zh-CN/服务端API/媒体处理/视频水印/删除水印.md)       | 调用DeleteWatermark删除水印。       |
| [ListWatermark](/cn.zh-CN/服务端API/媒体处理/视频水印/查询水印列表.md)       | 调用ListWatermark查询用户水印数据列表。   |
| [GetWatermark](/cn.zh-CN/服务端API/媒体处理/视频水印/查询单个水印.md)        | 调用GetWatermark查询单个水印数据。      |
| [SetDefaultWatermark](/cn.zh-CN/服务端API/媒体处理/视频水印/设置默认水印.md) | 调用SetDefaultWatermark设置默认水印。 |



**截图模板** 


|                                    API                                    |             描述             |
|---------------------------------------------------------------------------|----------------------------|
| [AddVodTemplate](/cn.zh-CN/服务端API/媒体处理/截图模板/添加截图模板.md)    | 调用AddVodTemplate添加截图模板。    |
| [UpdateVodTemplate](/cn.zh-CN/服务端API/媒体处理/截图模板/修改截图模板.md) | 调用UpdateVodTemplate修改截图模板。 |
| [DeleteVodTemplate](/cn.zh-CN/服务端API/媒体处理/截图模板/删除截图模板.md) | 调用DeleteVodTemplate删除截图模板。 |
| [ListVodTemplate](/cn.zh-CN/服务端API/媒体处理/截图模板/查询截图模板列表.md) | 调用ListVodTemplate查询截图模板列表。 |
| [GetVodTemplate](/cn.zh-CN/服务端API/媒体处理/截图模板/查询单个截图模板.md)  | 调用GetVodTemplate查询单个截图模板。  |



**转码任务** 


|                                      API                                      |                                         描述                                          |
|-------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| [GetTranscodeSummary](/cn.zh-CN/服务端API/媒体处理/转码任务/查询视频转码摘要.md) | 调用GetTranscodeSummary根据视频ID查询视频转码摘要，包括视频转码状态、转码进展等汇总信息。由于可能存在多次转码，故该接口只返回最近一次的转码摘要。 |
| [ListTranscodeTask](/cn.zh-CN/服务端API/媒体处理/转码任务/查询转码任务列表.md)   | 调用ListTranscodeTask根据视频ID查询视频历史转码任务信息，该接口不返回具体的作业信息。                                |
| [GetTranscodeTask](/cn.zh-CN/服务端API/媒体处理/转码任务/查询转码任务详情.md)    | 调用GetTranscodeTask根据转码任务ID查询转码作业详细信息。                                               |



视频剪辑（云剪辑） 
------------------------------

**剪辑合成** 


|                                       API                                        |                     描述                     |
|----------------------------------------------------------------------------------|--------------------------------------------|
| [ProduceEditingProjectVideo](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/视频合成.md) | 调用ProduceEditingProjectVideo将一个或多个视频合成为成品。 |



**剪辑工程管理** 


|                                              API                                              |                      描述                      |
|-----------------------------------------------------------------------------------------------|----------------------------------------------|
| [AddEditingProject](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/云剪辑工程管理/创建云剪辑工程.md)            | 调用AddEditingProject创建云剪辑工程（视频编辑任务）。          |
| [UpdateEditingProject](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/云剪辑工程管理/修改云剪辑工程.md)         | 调用UpdateEditingProject修改云剪辑工程（视频编辑任务）。       |
| [DeleteEditingProject](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/云剪辑工程管理/删除云剪辑工程.md)         | 调用DeleteEditingProject删除云剪辑工程，支持批量删除。        |
| [GetEditingProject](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/云剪辑工程管理/获取单个云剪辑工程.md)          | 调用GetEditingProject获取云剪辑工程（视频编辑任务）的详细信息。     |
| [SearchEditingProject](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/云剪辑工程管理/搜索云剪辑工程.md)         | 调用SearchEditingProject搜索云剪辑工程（视频编辑列表）。       |
| [SetEditingProjectMaterials](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/云剪辑工程管理/设置云剪辑工程素材.md) | 调用SetEditingProjectMaterials设置云剪辑工程的待剪辑素材。   |
| [GetEditingProjectMaterials](/cn.zh-CN/服务端API/视频剪辑(云剪辑)/云剪辑工程管理/获取云剪辑工程素材.md) | 调用GetEditingProjectMaterials获取云剪辑工程的待剪辑素材列表。 |



媒体审核 
-------------------------

**审核设置** 


|                                       API                                       |                描述                |
|---------------------------------------------------------------------------------|----------------------------------|
| [SetAuditSecurityIp](/cn.zh-CN/服务端API/媒体审核/审核设置/设置审核安全IP.md)    | 调用SetAuditSecurityIp设置审核安全IP。    |
| [ListAuditSecurityIp](/cn.zh-CN/服务端API/媒体审核/审核设置/获取审核安全IP列表.md) | 调用ListAuditSecurityIp获取审核安全IP列表。 |



**人工审核** 


|                                    API                                    |                  描述                  |
|---------------------------------------------------------------------------|--------------------------------------|
| [CreateAudit](/cn.zh-CN/服务端API/媒体审核/人工审核/人工审核.md)         | 调用CreateAudit进行人工审核，可用于审核视频、音频等媒体信息。 |
| [GetAuditHistory](/cn.zh-CN/服务端API/媒体审核/人工审核/获取人工审核历史.md) | 调用GetAuditHistory获取人工审核的历史记录。        |



**智能审核** 


|                                             API                                              |                                描述                                |
|----------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [SubmitAIMediaAuditJob](/cn.zh-CN/服务端API/媒体审核/智能审核/提交智能审核作业.md)              | 调用SubmitAIMediaAuditJob提交智能审核作业。作业在提交成功后会异步执行，不保证接口返回时作业已处理完成。   |
| [SubmitAIImageAuditJob](/cn.zh-CN/服务端API/媒体审核/智能审核/提交图片智能审核作业.md)            | 调用SubmitAIImageAuditJob提交图片智能审核任务，作业在提交成功后会异步执行，不保证接口返回时作业已处理完成。 |
| [GetAIMediaAuditJob](/cn.zh-CN/服务端API/媒体审核/智能审核/查询智能审核作业.md)                 | 调用GetAIMediaAuditJob查询智能审核作业。在提交AI作业后，会进行异步处理，通过此接口可以实时查询作业信息。   |
| [GetMediaAuditResult](/cn.zh-CN/服务端API/媒体审核/智能审核/获取智能审核结果摘要.md)              | 调用GetMediaAuditResult获取智能审核结果摘要信息。                               |
| [GetMediaAuditResultDetail](/cn.zh-CN/服务端API/媒体审核/智能审核/获取智能审核结果详情.md)        | 调用GetMediaAuditResultDetail获取智能审核结果详情。通过此接口可实时查询审核结果详情。          |
| [GetMediaAuditResultTimeline](/cn.zh-CN/服务端API/媒体审核/智能审核/获取智能审核结果时间线.md)     | 调用GetMediaAuditResultTimeline获取到所有违规内容截图的时间线。                    |
| [GetMediaAuditAudioResultDetail](/cn.zh-CN/服务端API/媒体审核/智能审核/获取智能音频审核结果详情.md) | 调用GetMediaAuditAudioResultDetail获取音频审核详情。                        |



视频AI 
-------------------------

**基础接口** 


|                              API                               |                         描述                          |
|----------------------------------------------------------------|-----------------------------------------------------|
| [SubmitAIJob](/cn.zh-CN/服务端API/视频AI/提交AI作业.md) | 调用SubmitAIJob提交AI作业。作业在提交成功后会异步执行，不保证接口返回时作业已处理完成。  |
| [ListAIJob](/cn.zh-CN/服务端API/视频AI/查询AI作业.md)   | 调用ListAIJob查询AI作业。在提交AI作业后，会进行异步处理，通过此接口可以实时查询作业信息。 |



**AI模板** 


|                                      API                                       |               描述                |
|--------------------------------------------------------------------------------|---------------------------------|
| [AddAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/添加AI模板.md)          | 调用AddAITemplate添加AI模板。          |
| [DeleteAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/删除AI模板.md)       | 调用DeleteAITemplate删除AI模板。       |
| [UpdateAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/修改AI模板.md)       | 调用UpdateAITemplate修改AI模板。       |
| [GetAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板.md)          | 调用GetAITemplate查询AI模板。          |
| [ListAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板列表.md)       | 调用ListAITemplate查询AI模板列表。       |
| [SetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/设置默认AI模板.md) | 调用SetDefaultAITemplate设置默认AI模板。 |
| [GetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询默认AI模板.md) | 调用GetDefaultAITemplate查询默认AI模板。 |



**视频DNA** 


|                                      API                                      |                            描述                            |
|-------------------------------------------------------------------------------|----------------------------------------------------------|
| [GetMediaDNAResult](/cn.zh-CN/服务端API/视频AI/视频DNA/获取视频DNA结果.md) | 调用GetMediaDNAResult获取视频DNA结果。视频DNA作业完成后，可通过此接口实时查询DNA结果。 |



**智能标签** 


|                                     API                                     |               描述               |
|-----------------------------------------------------------------------------|--------------------------------|
| [GetMediaDNAResult](/cn.zh-CN/服务端API/视频AI/智能标签/获取智能标签结果.md) | 调用GetAIVideoTagResult获取智能标签结果。 |



**智能封面** 


|                                     API                                      |                 描述                 |
|------------------------------------------------------------------------------|------------------------------------|
| [SubmitAIImageJob](/cn.zh-CN/服务端API/视频AI/智能封面/提交AI图片任务.md)   | 调用SubmitAIImageJob提交AI图片处理任务。      |
| [GetAIImageJobs](/cn.zh-CN/服务端API/视频AI/智能封面/查询AI图片任务列表.md)   | 调用GetAIImageJobs查询AI图片任务列表。        |
| [ListAIImageInfo](/cn.zh-CN/服务端API/视频AI/智能封面/查询智能封面信息.md)    | 调用ListAIImageInfo查询指定视频下的AI图片结果信息。 |
| [DeleteAIImageInfos](/cn.zh-CN/服务端API/视频AI/智能封面/删除AI图片信息.md) | 调用DeleteAIImageInfos删除AI图片信息。      |



直播转点播 
--------------------------



|                                    API                                     |                描述                 |
|----------------------------------------------------------------------------|-----------------------------------|
| [ListLiveRecordVideo](/cn.zh-CN/服务端API/直播转点播/获取直转点视频列表.md) | 调用ListLiveRecordVideo获取直播转点播视频列表。 |



点播CDN 
--------------------------

**数据监控** 


|                                            API                                             |                           描述                           |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------|
| [DescribeVodDomainTrafficData](/cn.zh-CN/服务端API/点播CDN/数据监控/查询加速域名的流量数据.md) | 调用DescribeVodDomainTrafficData获取加速域名的网络流量监控数据，单位：byte。 |
| [DescribeVodDomainBpsData](/cn.zh-CN/服务端API/点播CDN/数据监控/查询加速域名的网络带宽.md)     | 调用DescribeVodDomainBpsData获取加速域名的网络带宽监控数据。             |



**域名管理** 


|                                        API                                         |                              描述                               |
|------------------------------------------------------------------------------------|---------------------------------------------------------------|
| [AddVodDomain](/cn.zh-CN/服务端API/点播CDN/域名管理/添加加速域名.md)              | 调用AddVodDomain添加点播加速域名。每次只能提交一个加速域名，一个用户最多添加20个域名。            |
| [UpdateVodDomain](/cn.zh-CN/服务端API/点播CDN/域名管理/修改加速域名.md)           | 调用UpdateVodDomain修改加速域名。                                      |
| [DeleteVodDomain](/cn.zh-CN/服务端API/点播CDN/域名管理/删除加速域名.md)           | 调用DeleteVodDomain删除已添加的点播加速域名。                                |
| [BatchStartVodDomain](/cn.zh-CN/服务端API/点播CDN/域名管理/启用加速域名.md)       | 调用BatchStartVodDomain启用状态为"停用"的点播加速域名，将DomainStatus变更为online。 |
| [BatchStopVodDomain](/cn.zh-CN/服务端API/点播CDN/域名管理/停用加速域名.md)        | 调用BatchStopVodDomain批量停用点播加速域名，将DomainStatus变更为Offline。       |
| [DescribeVodUserDomains](/cn.zh-CN/服务端API/点播CDN/域名管理/查询加速域名列表.md)  | 调用DescribeVodUserDomains查询用户名下所有的点播加速域名列表。                    |
| [DescribeVodDomainDetail](/cn.zh-CN/服务端API/点播CDN/域名管理/查询域名基本信息.md) | 调用DescribeVodDomainDetail获取指定点播域名配置的基本信息。                     |



**域名验证** 


|                                         API                                         |                 描述                  |
|-------------------------------------------------------------------------------------|-------------------------------------|
| [VerifyVodDomainOwner](/cn.zh-CN/服务端API/点播CDN/域名验证/域名归属校验.md)       | 调用VerifyVodDomainOwner校验域名归属。       |
| [DescribeVodVerifyContent](/cn.zh-CN/服务端API/点播CDN/域名验证/获取归属校验内容.md) | 调用DescribeVodVerifyContent获取归属校验内容。 |





**域名配置** 


|                                            API                                            |                        描述                        |
|-------------------------------------------------------------------------------------------|--------------------------------------------------|
| [BatchSetVodDomainConfigs](/cn.zh-CN/服务端API/点播CDN/域名配置/批量配置域名.md)         | 调用BatchSetVodDomainConfigs批量配置加速域名。              |
| [DescribeVodDomainConfigs](/cn.zh-CN/服务端API/点播CDN/域名配置/查询域名配置.md)         | 调用DescribeVodDomainConfigs查询域名配置，一次可查询多个功能配置。    |
| [DeleteVodSpecificConfig](/cn.zh-CN/服务端API/点播CDN/域名配置/删除域名配置.md)          | 调用DeleteVodSpecificConfig删除点播加速域名的配置。            |
| [SetVodDomainCertificate](/cn.zh-CN/服务端API/点播CDN/域名配置/设置域名证书启用及修改信息.md)   | 调用SetVodDomainCertificate设置某域名下证书功能是否启用及修改证书信息。  |
| [DescribeVodCertificateList](/cn.zh-CN/服务端API/点播CDN/域名配置/查询证书列表.md)       | 调用DescribeVodCertificateList获取证书列表信息。            |
| [DescribeVodDomainCertificateInfo](/cn.zh-CN/服务端API/点播CDN/域名配置/查询域名证书.md) | 调用DescribeVodDomainCertificateInfo获取指定加速域名的证书信息。 |



**刷新预热** 


|                                           API                                           |                                          描述                                           |
|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| [PreloadVodObjectCaches](/cn.zh-CN/服务端API/点播CDN/刷新预热/预热缓存.md)           | 调用PreloadVodObjectCaches将源站的内容主动预热到L2 Cache节点上，首次访问可直接命中缓存，缓解源站压力。支持post请求，参数用form表单。 |
| [RefreshVodObjectCaches](/cn.zh-CN/服务端API/点播CDN/刷新预热/刷新缓存.md)           | 调用RefreshVodObjectCaches刷新节点上的文件内容。指定URL内容刷新至Cache节点，支持URL批量刷新。支持post请求，参数用form表单。    |
| [DescribeVodRefreshTasks](/cn.zh-CN/服务端API/点播CDN/刷新预热/查询刷新和预热状态.md)     | 调用DescribeVodRefreshTasks查询刷新和预热状态是否生效。                                               |
| [DescribeVodRefreshQuota](/cn.zh-CN/服务端API/点播CDN/刷新预热/查询刷新预热次数限制和余量.md) | 调用DescribeVodRefreshQuota查询刷新预热URL及目录的最大限制数量和当日剩余数量。                                  |



**日志管理** 


|                                      API                                      |                     描述                      |
|-------------------------------------------------------------------------------|---------------------------------------------|
| [DescribeVodDomainLog](/cn.zh-CN/服务端API/点播CDN/日志管理/查询域名日志.md) | 调用DescribeVodDomainLog获取指定域名的CDN原始访问日志下载地址。 |



数据统计 
-------------------------

**用量数据** 


|                                         API                                          |                        描述                         |
|--------------------------------------------------------------------------------------|---------------------------------------------------|
| [DescribeVodDomainUsageData](/cn.zh-CN/服务端API/数据统计/用量数据/查询流量带宽用量.md) | 调用DescribeVodDomainUsageData查询加速流量或带宽用量数据。        |
| [DescribeVodStorageData](/cn.zh-CN/服务端API/数据统计/用量数据/查询存储用量.md)       | 调用DescribeVodStorageData查询媒资管理（存储空间、存储流出流量）的用量数据。 |
| [DescribeVodTranscodeData](/cn.zh-CN/服务端API/数据统计/用量数据/查询转码用量数据.md)   | 调用DescribeVodTranscodeData查询转码用量数据。               |
| [DescribeVodAIData](/cn.zh-CN/服务端API/数据统计/用量数据/查询AI处理用量数据.md)        | 调用DescribeVodAIData查询AI处理（智能审核、视频DNA等）的用量数据。      |



**播放数据** 


|                                        API                                         |                           描述                            |
|------------------------------------------------------------------------------------|---------------------------------------------------------|
| [DescribePlayTopVideos](/cn.zh-CN/服务端API/数据统计/播放数据/TOP视频播放数据统计.md) | 调用DescribePlayTopVideos获取每日TOP视频的播放数据统计（包括VV、UV和播放总时长）。 |
| [DescribePlayUserAvg](/cn.zh-CN/服务端API/数据统计/播放数据/播放数据均量统计.md)      | 调用DescribePlayUserAvg获取指定时间范围内的每日播放数据均量统计。              |
| [DescribePlayUserTotal](/cn.zh-CN/服务端API/数据统计/播放数据/播放数据总量统计.md)    | 调用DescribePlayUserTotal获取指定时间范围内的每日播放数据总量统计。            |
| [DescribePlayVideoStatis](/cn.zh-CN/服务端API/数据统计/播放数据/单视频播放数据统计.md) | 调用DescribePlayVideoStatis获取指定视频在指定时间范围内的每日播放统计数据。       |



多应用体系 
--------------------------

**应用管理** 


|                                  API                                   |                描述                 |
|------------------------------------------------------------------------|-----------------------------------|
| [CreateAppInfo](/cn.zh-CN/服务端API/多应用体系/应用管理/创建应用.md)   | 调用CreateAppInfo创建新的应用。            |
| [GetAppInfos](/cn.zh-CN/服务端API/多应用体系/应用管理/查询应用信息.md)   | 调用GetAppInfos通过应用ID查询应用信息，支持批量查询。 |
| [ListAppInfo](/cn.zh-CN/服务端API/多应用体系/应用管理/获取应用信息列表.md) | 调用ListAppInfo根据查询条件获取有权限的应用信息列表。  |
| [UpdateAppInfo](/cn.zh-CN/服务端API/多应用体系/应用管理/更新应用信息.md) | 调用UpdateAppInfo更新应用信息。            |
| [DeleteAppInfo](/cn.zh-CN/服务端API/多应用体系/应用管理/删除应用.md)   | 调用DeleteAppInfo删除应用信息。            |



**授权管理** 


|                                              API                                              |                               描述                               |
|-----------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| [AttachAppPolicyToIdentity](/cn.zh-CN/服务端API/多应用体系/授权管理/为身份实体附加应用授权.md)       | 调用AttachAppPolicyToIdentity为指定身份（RAM用户或角色）附加点播应用的访问权限。         |
| [ListAppPoliciesForIdentity](/cn.zh-CN/服务端API/多应用体系/授权管理/查询身份实体被授予的应用权限列表.md) | 调用ListAppPoliciesForIdentity列出指定账号身份（RAM子账号或RAM角色）被授予的应用权限的列表。 |
| [DetachAppPolicyFromIdentity](/cn.zh-CN/服务端API/多应用体系/授权管理/为身份实体撤销应用授权.md)     | 调用DetachAppPolicyFromIdentity为指定账号身份（RAM子账号或RAM角色）撤销指定的应用授权。   |



**资源迁移** 


|                                    API                                     |                   描述                   |
|----------------------------------------------------------------------------|----------------------------------------|
| [MoveAppResource](/cn.zh-CN/服务端API/多应用体系/资源迁移/迁移资源到新应用.md) | 调用MoveAppResource将媒资等资源从一个应用迁移到另外一个应用。 |



全局配置 
-------------------------

**事件通知** 


|                                       API                                       |                      描述                       |
|---------------------------------------------------------------------------------|-----------------------------------------------|
| [SetMessageCallback](/cn.zh-CN/服务端API/全局配置/事件通知/设置事件通知配置.md)    | 调用SetMessageCallback设置事件通知的回调方式、回调地址、事件类型。    |
| [GetMessageCallback](/cn.zh-CN/服务端API/全局配置/事件通知/查询事件通知配置.md)    | 调用GetMessageCallback查询事件通知的回调方式、回调地址、事件类型。    |
| [DeleteMessageCallback](/cn.zh-CN/服务端API/全局配置/事件通知/删除事件通知配置.md) | 调用DeleteMessageCallback删除事件通知的回调方式、回调地址、事件类型。 |



**存储管理** 


|                                      API                                      |                         描述                         |
|-------------------------------------------------------------------------------|----------------------------------------------------|
| [SetCrossdomainContent](/cn.zh-CN/服务端API/全局配置/存储管理/更新跨域文件.md) | 调用SetCrossdomainContent更新点播跨域文件crossdomain.xml的内容。 |





