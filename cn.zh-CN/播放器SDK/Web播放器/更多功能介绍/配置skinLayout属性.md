配置skinLayout属性 
===================================

通过阅读本文，您可以了解skinLayout的属性、设置规则和可定义属性。

skinLayout属性 
---------------------------------

Aliplayer可以通过skinLayout属性定制以下三个组件是否显示和显示的位置。

* 播放按钮

  

* Loading动画

  

* Controlbar的UI

  




您可以通过配置播放器的CSS文件：aliplayer-min.css，修改skinLayout属性。配置方式，请参见[设置播放器皮肤](/cn.zh-CN/播放器SDK/Web播放器/更多功能介绍/如何使用皮肤.md)。

skinLayout设置规则 
-----------------------------------

* skinLayout属性未设置，则默认显示全部。

  

* skinLayout设置为空集合（\[\]）或falsh时, 则全部隐藏。

  

* 如果是直播ControlBar的children属性，则只能设置为liveDisplay、fullScreenButton和volume这3种UI组件。

  




可定义属性 
--------------------------

align属性，组件相对于父级组件的对齐方式，可选项如下所示：

* `'cc'`，相对于父组件绝对居中。

  

* `'tl'`，相对于父组件左上对齐，受同级组件的占位影响，以组件的相对位置左上角作为偏移原点，可类比于css中的`float: left`。

  

* `'tr'`，相对于父组件右上对齐，受同级组件的占位影响，以组件的相对位置右上角作为偏移原点，可类比于css中的`float: right`。

  

* `'tlabs'`，相对于父组件左上绝对对齐，不受同级组件的占位影响，以父组件左上角作为偏移原点。

  

* `'trabs'`，相对于父组件右上绝对对齐，不受同级组件的占位影响，以父组件右上角作为偏移原点。

  

* `'blabs'`，相对于父组件左下绝对对齐，不受同级组件的占位影响，以父组件左下角作为偏移原点。

  

* `'brabs'`，相对于父组件右下绝对对齐，不受同级组件的占位影响，以父组件右下角作为偏移原点。

  




x，y属性，组件相对于父级组件的位置，说明如下所示：

* x，{Number}，水平方向偏移量，偏移原点参考`align`的说明，`cc`时无效。

  

* y，{Number}，垂直方向偏移量，偏移原点参考`align`的说明，`cc`时无效。

  




点播默认配置 
---------------------------

**点播H5默认配置** 

    skinLayout:[
       {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {
          name: "H5Loading", align: "cc"
        },
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay"},
        {name:"tooltip", align:"blabs",x: 0, y: 56},
        {name: "thumbnail"},
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
            {name: "progress", align: "blabs", x: 0, y: 44},
            {name: "playButton", align: "tl", x: 15, y: 12},
            {name: "timeDisplay", align: "tl", x: 10, y: 7},
            {name: "fullScreenButton", align: "tr", x: 10, y: 12},
            {name:"subtitle", align:"tr",x:15, y:12},
            {name:"setting", align:"tr",x:15, y:12},
            {name: "volume", align: "tr", x: 5, y: 10}
          ]
        }
      ]



**点播Flash默认配置** 

    skinLayout:[
        {name:"bigPlayButton", align:"blabs", x:30, y:80},
        {
          name:"controlBar", align:"blabs", x:0, y:0,
          children: [
            {name:"progress", align:"tlabs", x: 0, y:0},
            {name:"playButton", align:"tl", x:15, y:26},
            {name:"nextButton", align:"tl", x:10, y:26},
            {name:"timeDisplay", align:"tl", x:10, y:24},
            {name:"fullScreenButton", align:"tr", x:10, y:25},
            {name:"streamButton", align:"tr", x:10, y:23},
            {name:"volume", align:"tr", x:10, y:25}
          ]
        },
        {
          name:"fullControlBar", align:"tlabs", x:0, y:0,
          children: [
            {name:"fullTitle", align:"tl", x:25, y:6},
            {name:"fullNormalScreenButton", align:"tr", x:24, y:13},
            {name:"fullTimeDisplay", align:"tr", x:10, y:12},
            {name:"fullZoom", align:"cc"}
          ]
        }
    ]



**配置效果图** ![点播默认配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5496869161/p270003.png)

直播默认配置 
---------------------------

**直播H5默认配置** 

    skinLayout: [
        {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay", align: "cc"},
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
              {name:"liveDisplay", align:"tlabs", x: 15, y:6},
              {name:"fullScreenButton", align:"tr", x:10, y: 10},
              {name:"subtitle", align:"tr",x:15, y:12},
              {name:"setting", align:"tr",x:15, y:12},
              {name:"volume", align:"tr", x:5, y:10}
            ]
        }
      ]



**直播Flash默认配置** 

    skinLayout: [
        {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay", align: "cc"},
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
              {name:"liveDisplay", align:"tlabs", x: 15, y:25},
              {name:"fullScreenButton", align:"tr",  x:10, y:25},
              {name:"volume", align:"tr",  x:10, y:25}
            ]
        }
      ]



**配置效果图** ![直播默认配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5496869161/p270004.png)
