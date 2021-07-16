H5自定义错误UI 
==============================

您可以通过CSS自定义皮肤和重写UI两种方式自定义H5错误UI。

默认UI 
-------------------------

Aliplayer默认的错误UI如下图所示。![ui](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2107869161/p269995.png) **错误UI开启** 

在Aliplayer2.1.0版本以后，如果用户自定义了skinLayout属性，则需要把displayError UI组件添加到skinLayout属性中，代码如下所示。更多skinLayout属性信息，请参见[skinLayout属性的配置](/intl.zh-CN/播放器SDK/Web播放器/更多功能介绍/配置skinLayout属性.md)。

    skinLayout:[
        ......
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay", align: "cc"},
        ......
      ]



自定义UI 
--------------------------

您可以通过以下两种方式自定义错误UI。

* **通过CSS自定义皮肤** 

  保留播放器原有的布局和显示，通过重写CSS自定义皮肤，从而修改背景颜色、是否显示、字体、位置等。

  相关联的CSS如下表所示。
  

  |        Class名称         |                  说明                   |
  |------------------------|---------------------------------------|
  | .prism-ErrorMessage    | 最外层容器的Class。                          |
  | .prism-error-content   | 错误消息显示区域。                             |
  | .prism-error-operation | 处理动作显示区域。                             |
  | .prism-detect-info     | 其它信息显示区域。比如uuid、requestId等，主要是用于错误诊断。 |

  




<!-- -->

* **重写UI** 

  1. 需要订阅错误事件，代码如下所示。

         player.on('error',function(e){
               //隐藏
               $('.prism-ErrorMessage').hide();
               //解析
               var errorData = e.paramData;
               console.dir(errorData);
             });

     
  
  2. 隐藏Aliplayer的错误UI。

     
  
  3. 解析paramData里面的错误。错误事件参数包含的错误字段，如下图所示。![错误字段](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2107869161/p269996.png)

     
  
  4. 赋值给UI控件。

     
  

  






