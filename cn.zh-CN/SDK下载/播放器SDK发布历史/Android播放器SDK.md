# Android播放器SDK

本文为您介绍了阿里云Android播放器在不同更新时间对应的更新功能。

## 2020-11-17

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2020-11-17|V5.2.2|-   解决播放一个时长为0的点播HLS崩溃问题。
-   解决播放60FPS的视频，视频延迟问题。
-   解决stop接口慢的问题。
-   解决artc播放时设置的max\_buffer\_duration过小导致播放不起来的问题。
-   解决倍速播放stop后再播放，视频丢帧问题。
-   解决有elst box的MP4文件播放快进问题。
-   解决列表播放断网后导致视频播放失败问题。
-   解决超低帧率视频播放，音频卡顿问题。
-   优化音量设置逻辑。
-   添加HEVC硬解码黑名单。

|[Android播放器SDK 5.2.2](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.2.2/ApsaraVideo_videoPlay_v5.2.2_Android_20201116.zip)|

## 2020-09-30

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2020-09-30|V5.2.1|-   完善HLS格式的兼容性，支持FMP4分片，支持aac es流ID3解析，支持多分片字幕。
-   demuxer支持插件自定义消息传递通道。
-   分离artc包，降低artc和播放器SDK的版本耦合。
-   支持WideVine DRM。
-   修复某些手机后台播放音频卡顿问题。
-   支持HEVC硬解码器黑名单设置。
-   支持content:// 协议。
-   支持扩展外部播放器。

|[Android播放器SDK 5.2.1](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.2.1/ApsaraVideo_videoPlay_v5.2.1_Android_20200930.zip)|

## 2020-09-22

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2020-09-22|V5.1.6|-   优化进度显示逻辑。
-   优化外挂字幕显示。
-   修复rtmp长时间播放出现音视频不同步问题。
-   优化使用vid列表播放的起播速度。
-   修复播放器stop后视频旋转角度未清除问题。
-   优化软解码的稳定性。
-   修复采样率大于48k的视频播放快进问题。
-   修复某些设备视频硬解后台播放解码器无法工作的问题。

|[Android播放器SDK 5.1.6](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.1.6/ApsaraVideo_videoPlay_v5.1.6_Android_20200922.zip)|

## 2020-07-22

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2020-07-22|V5.1.5|播放器SDK 支持RTS低延迟直播拉流。RTS支持aac、opus、H.264编码，支持平滑追帧等特性。|[Android播放器SDK 5.1.5](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.1.5/ApsaraVideo_videoPlay_v5.1.5_Android_20200722.zip)|

## 2020-07-07

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2020-07-07|V5.1.4|-   支持STS加密直播的播放。
-   增加设置IPV4/V6解析。
-   增加播放器轻量预缓存功能。
-   增加视频背景色设置。
-   降低HLS直播延迟，支持设置起播分片。
-   播放器兼容性优化。
-   播放器内核开源CicadaPlayer。

|[Android播放器SDK 5.1.4](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/5.1.4/ApsaraVideo_videoPlay_v5.1.4_Android_20200707.zip)|

## 2020-03-16

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2020-03-16|V4.7.4|-   增加获取FPS的接口，增加视频渲染回调接口。
-   提升SDK的稳定性。

|[Android播放器SDK 4.7.4](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/4.7.4/ApsaraVideo_videoPlay_v4.7.4_Android_20200316.zip)|

## 2019-12-11

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-12-11|V4.7.3|-   支持设置多码率流的启播码率。
-   优化音视频同步逻辑。
-   提升SDK的稳定性。

|[Android播放器SDK 4.7.3](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/4.7.3/ApsaraVideo_videoPlay_v4.7.3_Android_20191211.zip)|

## 2019-11-1

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-11-1|V4.7.2|-   增加了点播切换清晰度时的精准Seek。
-   支持直播追帧。
-   提升了SDK稳定性。

|[Android播放器SDK 4.7.2](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/4.7.2/ApsaraVideo_videoPlay_v4.7.2_Android_20191030.zip)|

## 2019-09-18

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-09-18|V4.7.1|-   支持获取H.264的SEI信息。
-   支持FLV直播追赶。

|[Android播放器SDK 4.7.1](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/4.7.1/ApsaraVideo_videoPlay_v4.7.1_Android_20190918.zip)|

## 2019-08-19

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-08-19|V4.7.0|-   支持Webvtt缩略图功能。
-   支持精准Seek功能。
-   支持设置请求视频的加密类型。
-   包含[超低延时直播](https://promotion.aliyun.com/ntms/lowlatencylive.html)

|[Android播放器SDK 4.7.0](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/playVideo/4.7.0/ApsaraVideo_videoPlay_v4.7.0_Android_20190809.zip)|

## 2019-08-02

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-08-02|V4.5.0|-   全新播放器接口AliPlayer，提升易用性。
-   支持H.265软硬解码、支持直播H.265播放。
-   Android支持H.264硬解码。
-   支持试看功能。
-   支持短视频列表播放的AliListPlayer。
-   支持HLS MasterPlaylist播放。
-   支持多音轨、多字幕、多码率以及缩略图。
-   支持多码率无缝切换和自适应切换。
-   边播边缓存支持MP4 URL缓存，支持获取缓存文件名。
-   全新离线下载接口，优化下载体验。

|[Android播放器SDK 4.5.0](https://vod-download.cn-shanghai.aliyuncs.com/sdk/player/4.5.0/ApsaraVideo_videoPlay_v4.5.0_Android_20190708.zip)|

## 2019-06-28

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-06-28|V3.4.11|解决与短视频SDK集成冲突问题。|[Android播放器SDK 3.4.11](https://vod-download.cn-shanghai.aliyuncs.com/sdk/player/3.4.11/ApsaraVideo_videoPlay_v3.4.11_Android_20190627.zip)|

## 2019-06-12

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-06-12|V3.4.10|-   点播播放增加region参数支持国际化。
-   支持点播音频播放和下载。
-   修复相关崩溃问题。

|[Android播放器SDK 3.4.10](https://vod-download.cn-shanghai.aliyuncs.com/sdk/player/3.4.10/ApsaraVideo_videoPlay_v3.4.10_Android_20190612.zip)|

## 2019-01-04

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2019-01-04|V3.4.9|-   优化循环播放。
-   修复重播黑边。
-   修复短视频场景下快速滑动视频列表崩溃问题。

|[Android播放器SDK 3.4.9](https://vod-download.cn-shanghai.aliyuncs.com/sdk/player/3.4.9/ApsaraVideo_videoPlay_v3.4.9_Android_20190104.zip)|

## 2018-08-25

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-08-25|V3.4.7|-   修复暂停后Seek，画面不能立即更新。
-   修复断网后Seek，不报错的问题。
-   修复删除后不能重新下载的问题。

|[Android播放器SDK 3.4.7](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1535337264624/ApsaraVideo_Player_v3.4.7_Android_20170825.zip)|

## 2018-06-21

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-06-21|V3.4.6|-   新增HLS标准加密下载。
-   新增获取视频角度接口。
-   新增traceID埋点接口。

|[Android播放器SDK 3.4.6](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1529551730657/AliyunPlayerSDK_android_3.4.6_20180621.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1529551671229/AliyunPlayerDemo_android_3.4.6_20180621.zip) |

## 2018-05-27

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-05-27|V3.4.5|-   修复Seek到结尾报4003错误。
-   修复不能Seek到开头的问题。
-   修复播放过程中断网，Seek到缓存区外报错。
-   UI播放器开源。

|[Android播放器SDK 3.4.5](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1527413416523/AliyunPlayerSDK_android_3.4.5_20180527.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1527411981774/AliyunPlayerDemo_android_3.4.5_20180527.zip) |

## 2018-04-25

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-04-25|V3.4.3|修复带封面图MP3无法播放问题。|[Android播放器SDK 3.4.3](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1524628346935/AliyunPlayerSDK_android_3.4.3_20180425.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1524628267192/AliyunPlayerDemo_android_3.4.3_20180425.zip) |

## 2018-04-18

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-04-18|V3.4.2|-   新增防盗链referer设置。
-   优化数据日志。

|[Android播放器SDK 3.4.2](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1524067479096/AliyunPlayerSDK_android_3.4.2_20180418.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1524067388086/AliyunPlayerDemo_android_3.4.2_20180418.zip) |

## 2018-02-26

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-02-26|V3.4.0|-   新增直播时移功能。
-   新增MPS安全下载。
-   新增连续播放示例Demo。

|[Android播放器SDK 3.4.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1518347514464/AliyunPlayerSDK_android_3.4.0_20180211.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1518347540660/AliyunPlayerDemo_android_3.4.0_20180211.zip) |

## 2018-02-06

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-02-06|V3.3.4|-   修复因时区引起的STS过期问题。
-   修复缓存保存视频旋转meta信息的丢失问题。
-   内部接口使用https请求。
-   优化STS过期和播放状态错误提示。
-   新增支持变分辨率视频播放。

|[Android播放器SDK 3.3.4](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1517928354668/AliyunPlayerSDK_android_3.3.4_20180206.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1517928217548/AliyunPlayerDemo_android_3.3.4_20180206.zip) |

## 2018-01-24

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2018-01-24|V3.3.3|新增直播答题播放功能。|[Android播放器SDK 3.3.3](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516788577963/AliyunPlayerSDK_android_3.3.3_20180124.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1516788601327/AliyunPlayerDemo_android_3.3.3_20180124.zip) |

## 2017-12-13

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2017-12-13|V3.3.0|-   新增开始循环播放回调接口。
-   新增视频渲染旋转角度接口。
-   新增视频画面镜像接口。
-   使用URL播放的视频也可以使用边播边缓存功能。

|[Android播放器SDK 3.3.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1513163986499/AliyunPlayerSDK_android_3.3.0_20171213.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1513163907575/AliyunPlayerDemo_android_3.3.0_20171213.zip) |

## 2017-11-23

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2017-11-23|V3.2.2|-   修复推流SDK退后台播放无声音问题。
-   修复未使用Stop，销毁播放器时崩溃。

|[Android播放器SDK 3.2.2](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1511447292886/AliyunPlayerSDK_android_3.2.2_20171123.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1511447341703/AliyunPlayerDemo_android_3.2.0220171123.zip) |

## 2017-11-15

|日期|版本|修改内容|历史版本|
|--|--|----|----|
|2017-11-15|V3.2.0|-   增加循环播放功能。
-   增加截图功能。
-   Cache内Seek。
-   Demo优化，合并基础播放器和高级播放器。

|[Android播放器SDK 3.2.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1510825566716/AliyunPlayerSDK_android_3.2.0_20171115.zip)

[示例代码](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/51992/cn_zh/1510825653399/AliyunPlayerDemo_android_3.2.0_20171115.zip) |

