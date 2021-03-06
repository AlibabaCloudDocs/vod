# Web播放器常见问题

Aliplayer播放器包含H5、Flash、自适应播放器，建议用户选择自适应播放器，可以根据终端类型、浏览器类型和地址协议选择最合适的播放器。视频加密播放可以使用H5播放器。

## 如何手工启用H5播放器

手工启用H5播放器有两种方式：

-   直接引用H5播放器的js文件。
-   使用自适应播放器，然后设置useH5Prism属性为true。

## 如何手工启用Flash播放器

手工启用Flash播放器有两种方式：

-   直接引用Flash播放器的js文件。
-   使用自适应播放器，然后设置useFlashPrism属性为true。

## 如何自适应播放器

根据终端类型、浏览器类型、设置的属性和地址协议选择最合适的播放器，适配的基本原则是：

-   H5优先级最高，能H5播放的绝不选择Flash，除非用户指定用Flash播放。

    useFlashPrism = true、rtmp和http-flv协议时，采用flash播放。

-   移动端采用H5播放。

    useH5Prism = true，采用H5播放。

-   PC端MP4采用H5播放。

    PC端如果浏览器或通过Aliplayer的插件支持播放m3u8，则采用H5播放，否则采用Flash播放。

-   其它都用H5播放。

## 哪些浏览器支持flash

播放应该都支持flash播放， 但是最新的一些浏览器会禁用flash，需要手工启用， 参见以下说明：

-   [IE使用说明](https://answers.microsoft.com/zh-hans/ie/forum/ie11-iewindows8_1/windows-81ie/99696880-fbd9-4ac4-b43c-45fbb06f84e5)
-   [Firefox使用说明](https://support.mozilla.org/zh-CN/kb/Flash%E6%8F%92%E4%BB%B6#w_uiiunigoce-flash)
-   [Chrome使用说明](https://helpx.adobe.com/cn/flash-player/kb/enabling-flash-player-chrome.html)

## flash播放器对mp4/flv无法拖拽

mp4与flv拖拽需要CDN添加支持，是通过播放器发送带时间的请求到CDN，CDN返回该时间段的视频数据。如果要实现拖拽，需要以下两个条件：

-   文件索引信息需要在视频的头部，mp4包含视频时间戳等索引信息，以及flv的meta信息要在视频最前面，播放器解析到视频索引信息后，才可以依据拖拽的位置通过索引信息拿到指定位置的数据点，去向CDN发送请求。
-   CDN支持带时间/byte range的请求，需要在CDN控制台开启，如果在控制台开启，请参见[配置拖拽播放](/cn.zh-CN/域名管理/视频相关/配置拖拽播放.md)。

## 解决Andorid微信上自动弹出全屏播放

Android手机在微信和QQ浏览器里自动全屏播放，这是腾讯浏览器的内置行为，不能修改，原因是由于腾讯浏览器挟持了video标签，由腾讯内置的播放器播放视频，但可以启用同层播放功能，可以解决视频覆盖Dom元素的问题[如何启用H5的同层播放](/cn.zh-CN/常见问题/如何启用H5的同层播放.md)。

## 在微信里如何自动播放

```
<script src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>
<script>
function autoPlay() {            
wx.config({
                // 配置信息, 即使不正确也能使用 wx.ready
                debug: false,
                appId: '',
                timestamp: 1,
                nonceStr: '',
                signature: '',
                jsApiList: []
            });
            wx.ready(function() {
                var video=$(player.el()).find('video')[0];
                video.play();
            });
    };
    // 解决ios不自动播放的问题
    autoPlay();
</script>
```

## 播放器如何初始播放位置

H5播放器：

```
var seeked = false;
player.on('canplaythrough',function  (e) {  
if(!seeked)
  {
    seeked = true;
    player.seek(100);
  }
});
```

Flash 播放器：

```
var seeked = false;
player.on('loadedmetadata',function  (e) {
  if(!seeked)
  {
    seeked = true;
    player.seek(20);
  }
});
```

## 如何禁用进度条

自定义skinLayout属性， 去掉整个controlBar或者controlBar下面的子项， 比如progress：

```
skinLayout: [                   
    {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
    {
      name: "H5Loading", align: "cc"
    },
    {
      name: "controlBar", align: "blabs", x: 0, y: 0,
      children: [
        //{name: "progress", align: "tlabs", x: 0, y: 0},
        {name: "playButton", align: "tl", x: 15, y: 26},
        {name: "timeDisplay", align: "tl", x: 10, y: 24},
        {name: "fullScreenButton", align: "tr", x: 20, y: 25},
        {name: "volume", align: "tr", x: 20, y: 25},
      ]
    }
  ]
```

## 如何切换vid和playauth

H5播放器，直接调用replayByVidAndPlayauth方法：

```
 player.replayByVidAndPlayauth(newVid, newPlayAuth)
```

Flash播放器需要销毁，根据新的vid和playauth重新创建一个：

```
//销毁
     flashPlayer.dispose();
     $('#flashPlayer').empty();
     //重新创建
     flashPlayer = new Aliplayer({
            id: 'flashPlayer',
            autoplay: true,
            playsinline:true,
            vid: newVid,
            playauth: newPlayAuth,
            useFlashPrism:true
        });
```

## 如何定时获取播放时间

通过定时器每秒调用播放器的getCurrentTime方法获取播放时间，在暂停、出错和结束播放时清除定时器。

```
 var timer = null;
function getTime(){
    var currentTime = player.getCurrentTime();
   //to do
   timer = setTimeout(getTime,1000);
}
//清除定时器
function clear(){
   if(timer)
   {
      clearTimeout(timer);
      timer = null;
   }
}
player.on('ended',function  (e) {
  clear();
 });
player.on('pause',function  (e) {
  clear();
 });
player.on('error',function  (e) {
  clear();
 });
```

## 如何调整H5播放器的播放按钮的大小和位置

重写CSS，比如减小一倍：

```
 .prism-player .prism-big-play-btn {
    width: 45px;
    height: 45px;
    background-size: 128px 256px;
}
```

位置可以通过设置skinLayout里bigPlayButton的x、y属性：

```
skinLayout: [
    {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
    {
      name: "H5Loading", align: "cc"
    },
    {
      name: "controlBar", align: "blabs", x: 0, y: 0,
      children: [
        {name: "progress", align: "tlabs", x: 0, y: 0},
        {name: "playButton", align: "tl", x: 15, y: 26},
        {name: "timeDisplay", align: "tl", x: 10, y: 24},
        {name: "fullScreenButton", align: "tr", x: 20, y: 25},
        {name: "volume", align: "tr", x: 20, y: 25},
      ]
    }
  ]
```

## 手机端播放视频不希望弹出全屏，要小窗播放问题

手机端不希望全屏播放，iOS可以设置属性playsinline为true。

Android手机在微信和QQ浏览器里自动全屏播放，这是腾讯浏览器的内置行为，不能修改，原因是由于腾讯浏览器挟持了video标签，由腾讯内置的播放器播放视频，但可以启用同层播放功能，可以解决视频覆盖Dom元素的问题[如何启用H5的同层播放](/cn.zh-CN/常见问题/如何启用H5的同层播放.md)。

## 启用IE浏览器以最高级别的可用模式显示内容

小于IE10的浏览器需要启用最高级别的可用模式显示内容模式：

```
<meta http-equiv="x-ua-compatible" content="IE=edge" >
```

## Flash播放器播放m3u8提示跨域错误

播放器跨域访问时需要添加策略文件，即在视频播放链接所在域名的根目录下，添加crossdomain.xml文件，其中添加播放器所在域名的权限。

例如：`http://test1.com/app/test.m3u8`需要添加到`http://test1.com/crossdomain.xml`。

```
<?xml version="1.0" encoding="UTF-8"?>
<cross-domain-policy>
    <allow-access-from domain="*"/>
    <allow-http-request-headers-from domain="*" headers="*" secure="false"/>
</cross-domain-policy>
```

## Flash播放器封面图片无法显示

-   确认cover字段输入URL是否有效。
-   确认cover输入的URL所在域名是否存在有效的crossdomain.xml文件。

