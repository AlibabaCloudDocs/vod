# Use custom policies

You can use custom policies to meet a variety of requirements for access control. The RAM console allows you to configure custom policies in visualized or script mode. This topic describes the basic terms, scenarios, procedure, syntax, and examples of custom policies.

## Scenario

System policies are coarse-grained. You can use custom policies to implement fine-grained access control.

## Procedure

You can create a custom policy on the [Create Custom Policy](https://ram.console.aliyun.com/policies/new?spm=a2c4g.11186623.2.18.37cd51f3RgSMm5) page in the RAM console. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

## Visualization mode

Select **Visualized** and click **Add Statement**. You can specify the permission effect, product/service, actions, resources, and conditions in a visualized manner.

![Visualization mode](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6998039061/p184476.png)

## Syntax

Before you configure a RAM policy, you must understand the basic elements and syntax of RAM policies. For more information, see [Policy elements](/intl.en-US/Policy Management/Policy language/Policy elements.md) and [Policy structure and syntax](/intl.en-US/Policy Management/Policy language/Policy structure and syntax.md).

The following example shows the `AliyunVODPlayAuth` policy.

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

Parameters:

-   **Version**

    Version defines the version of the policy. In this example, Version is set to 1.

-   **Statement**

    One policy can contain multiple statements. Each statement contains the following elements: Action, Effect, Resource, and Condition. The system checks the statements of each request. Matched statements can have Effect configurations of Allow and Deny. Matched statements where Effect is set to Deny take precedence. If all matched statements have Effect configurations of Allow, this request passes the authentication. If one matched statement has the Effect configuration of Deny or no other entries match the policy, this request is denied.

-   **Action**

    Actions in ApsaraVideo VOD correspond to API operations. The Action value is in the `vod:API operation` format. For example, `vod:GetPlayInfo` in this example indicates a playback operation. Multiple Action values are separated with commas \(,\). You can specify multiple Action values to obtain a permission group.

    For all available operations, see [List of operations by function](/intl.en-US/API Reference/API overview.md).

-   **Resource**

    Resource specifies one or more VOD resources that authorized users can access. Asterisks \(\*\) can be used as wildcards. Resource values are in the `acs:vod:{region}:*` format. You can specify multiple resources in the Resource value. The region field is unavailable. Set it to an asterisk \(`*`\). ApsaraVideo VOD does not divide permissions for resources. We recommend that you set Resource to an asterisk \(`*`\).

-   **Condition**

    Optional. Condition specifies access control conditions of the policy.

    The following table describes the supported conditions.

    |Condition|Feature|Valid value|
    |---------|-------|-----------|
    |acs:SourceIp|Specifies an IP address or a CIDR block|IP addresses. Asterisks \(\*\) can be used.|
    |acs:SecureTransport|Specifies whether HTTPS is used for access.|**true** or **false**|
    |acs:MFAPresent|Specifies whether multi-factor authentication \(MFA\) is used during user logon.|**true** or **false**|
    |acs:CurrentTime|Specifies the valid time when the request is received.|Values in the ISO 8601 standard. Example: **2012-11-11T23:59:59Z**.|


The following example shows a policy to allow requesters only from IP address 42.160.1.0 to call the specified playback actions:

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

## Examples

ApsaraVideo VOD provides corresponding API operations for each action. For more information, see [List of operations by function](/intl.en-US/API Reference/API overview.md). The following examples show policies for media review and online editing.

-   **Policy for media review**

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

-   **Policy for online editing**

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


**Note:** If new API operations are available, the `Action` values must be updated.

