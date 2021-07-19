# 基于RAM Policy实现自定义授权

自定义授权可以满足用户个性化的授权策略需求，RAM控制台提供了可视化配置和脚本配置两种配置方式。本文为您介绍授权的基本概念、使用场景、基本步骤和授权的语法、示例。

## 使用场景

由于系统策略的授权粒度比较粗，很多时候并不能满足您的细粒度权限控制的需求，此时可以使用此时可以基于RAM Policy实现自定义授权。

## 授权操作

您可以在RAM控制台的[新建自定义权限策略](https://ram.console.aliyun.com/policies/new?spm=a2c4g.11186623.2.18.37cd51f3RgSMm5)页面，新建自定义权限策略。具体操作，请参见[创建自定义策略](/intl.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)。

## 可视化配置

选择**可视化配置**，单击**添加授权语句**，即可通过可视化的方式配置权利效力、产品/服务、操作名称、资源和限制条件。

![可视化配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4653816061/p184476.png)

## 授权语法

在开始设置前，需要先了解权限策略的基本元素和语法结构，更多信息，请参见[权限策略基本元素](/intl.zh-CN/权限策略管理/权限策略语言/权限策略基本元素.md)和[权限策略语法和结构](/intl.zh-CN/权限策略管理/权限策略语言/权限策略语法和结构.md)。

以点播系统策略`AliyunVODPlayAuth`为例：

```
{
    "Version": "1",
    "Statement": [
        {
            "Action": [
                "vod:GetPlayInfo",
                "vod:GetVideoPlayAuth",
                "vod:GetVideoPlayInfo",
                "vod:GetVideoInfo"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ]
}
```

参数解释如下：

-   **Version**

    Version定义了Policy的版本，本文档中 Version 可以固定设置为1。

-   **Statement**

    通过Statement描述授权语义，其中可以根据业务场景包含多条语义，每条包含对Action、Effect、Resource 和 Condition的描述。每次请求，系统会逐条依次匹配检查，所有匹配成功的Statement会根据Effect的设置不同分为通过（Allow）、禁止（Deny），其中禁止（Deny）的优先。如果匹配成功的都为通过，该条请求即鉴权通过。如果匹配成功有一条禁止，或者没有任何条目匹配成功，该条请求被禁止访问。

-   **Action**

    点播支持的Action操作与API一一对应，格式为`vod:API名称`，如上面示例的播放操作：`vod:GetPlayInfo`，注意多个使用英文逗号分隔。通过指定授权的Action列表，就能组合出想要的权限分组。

    所有可用操作，请参见[API概览](/intl.zh-CN/服务端API/API概览.md)。

-   **Resource**

    Resource指代的是VOD上面的某个具体的资源或者某些资源（支持通配符\*），Resource的规则是`acs:vod:{region}:*`。Resource也是一个列表，可以有多个Resource。其中的region字段暂不支持，请设置为`*`。由于点播现在没有进一步区分资源，故一般建议授权点播时Resource填`*`。

-   **Condition**

    Condition代表Policy授权的一些条件，对访问来源等进行限制，为可选项。

    支持的条件如下：

    |Condition|功能|合法取值|
    |---------|--|----|
    |acs:SourceIp|指定 IP 地址或网段|普通的IP，支持通配符\*|
    |acs:SecureTransport|是否是 HTTPS 协议|**true**或者**false**|
    |acs:MFAPresent|用户登录时是否使用了多因素认证|**true**或者**false**|
    |acs:CurrentTime|指定合法的访问时间（云端接收到请求的时间）|ISO8601格式，例如：**2012-11-11T23:59:59Z**|


下文示例表示只允许IP来源为`42.160.1.0`的请求者访问播放接口：

```
{
    "Version": "1",
    "Statement": [
        {
            "Action": [
                "vod:GetPlayInfo",
                "vod:GetVideoPlayAuth",
                "vod:GetVideoPlayInfo",
                "vod:GetVideoInfo"
            ],
            "Resource": "*",
            "Effect": "Allow",
            "Condition":
             {
                "IpAddress":
                 {
                    "acs:SourceIp": "42.160.1.0"
                  }
              }
        }
    ]
}
```

## 授权示例

根据[API概览](/intl.zh-CN/服务端API/API概览.md)，可以得到所有对应的Action，进而分组控制权限，以下以授予媒体审核、云剪辑权限为例。

-   **授予使用媒体审核的权限**

    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Action": [
                    "vod:SetAuditSecurityIp",
                    "vod:ListAuditSecurityIp",
                    "vod:CreateAudit",
                    "vod:GetAuditHistory",
                    "vod:SubmitAIMediaAuditJob",
                    "vod:GetAIMediaAuditJob",
                    "vod:GetMediaAuditResult",
                    "vod:GetMediaAuditResultDetail",
                    "vod:GetMediaAuditResultTimeline"
                ],
                "Resource": "*",
                "Effect": "Allow"
            }
        ]
    }
    ```

-   **授予使用云剪辑的权限**

    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Action": [
                    "vod:ProduceEditingProjectVideo",
                    "vod:AddEditingProject",
                    "vod:UpdateEditingProject",
                    "vod:DeleteEditingProject",
                    "vod:GetEditingProject",
                    "vod:SearchEditingProject",
                    "vod:SetEditingProjectMaterials",
                    "vod:GetEditingProjectMaterials"
                ],
                "Resource": "*",
                "Effect": "Allow"
            }
        ]
    }
    ```


**说明：** 以上示例中，该API分组下如果增加了新的接口，则需要相应更新`Action`部分的列表。

