视频AI 
=========================

本篇文档提供了C/C++ SDK视频AI模块相关功能的API调用示例。包含提交AI作业、查询AI作业、添加AI模板、修改AI模板、删除AI模板、查询AI模板、查询设置默认AI模板等。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/C/C++ SDK/初始化.md)。

提交AI作业 {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交AI作业功能。
接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/提交AI作业.md)。调用示例如下： {#h2--ai-div-id-submitaijob-div-2}
------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 提交作业
     */
    VodApiResponse submitAIJob(VodCredential authInfo) {
        string apiName = "SubmitAIJob";
        map<string, string> args;
        // 设置视频ID
        args["MediaId"] = "3eb19a4585bc475e995bddfd****";
        // 设置AI类型，请确保已开通该类型AI
        args["Types"] = "AIVideoCover";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



查询AI作业 {#h2--ai-div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询AI作业功能。
接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/查询AI作业.md)。调用示例如下： {#h2--ai-div-id-listaijob-div-3}
------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 查询作业
     */
    VodApiResponse listAIJob(VodCredential authInfo) {
        string apiName = "ListAIJob";
        map<string, string> args;
        // 设置作业ID
        args["JobIds"] = "979d4d7a36ae41b1a945a252****,3eb19a4585bc475e995bddea5****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



添加AI模板 {#h2--ai-div-id-addaitemplate-div-4}
-------------------------------------------

调用AddAITemplate接口，完成添加AI模板功能。
接口参数和返回字段请参见[AddAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/添加AI模板.md)。调用示例如下： {#h2--ai-div-id-addaitemplate-div-4}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 添加AI模板
     */
    VodApiResponse addAITemplate(VodCredential authInfo) {
        string apiName = "AddAITemplate";
        map<string, string> args;
        // 设置模板类型，以智能审核模板为例
        args["TemplateType"] = "AIMediaAudit";
        // 设置模板名称
        args["TemplateName"] = "我的自定义模板";
        // 设置模板详细配置
        Json::Value templateConfig;
        Json::Value auditItem;
        auditItem.append("terrorism");
        auditItem.append("porn");
        templateConfig["AuditItem"] = auditItem;
    
        Json::Value auditRange;
        auditRange.append("video");
        auditRange.append("image-cover");
        auditRange.append("text-title");
        templateConfig["AuditRange"] = auditRange;
    
        Json::Value auditContent;
        auditContent.append("screen");
        templateConfig["AuditContent"] = auditContent;
        templateConfig["AuditAutoBlock"] = "no";
        args["TemplateConfig"] = templateConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = addAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



删除AI模板 {#h2--ai-div-id-deleteaitemplate-div-5}
----------------------------------------------

调用DeleteAITemplate接口，完成删除AI模板功能。
接口参数和返回字段请参见[DeleteAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/删除AI模板.md)。调用示例如下： {#h2--ai-div-id-deleteaitemplate-div-5}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 删除AI模板
     */
    VodApiResponse deleteAITemplate(VodCredential authInfo) {
        string apiName = "DeleteAITemplate";
        map<string, string> args;
        // 设置模板ID
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d2c8****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



修改AI模板 {#h2--ai-div-id-updateaitemplate-div-6}
----------------------------------------------

调用UpdateAITemplate接口，完成修改AI模板功能。
接口参数和返回字段请参见[UpdateAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/修改AI模板.md)。调用示例如下： {#h2--ai-div-id-updateaitemplate-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 修改AI模板
     */
    VodApiResponse updateAITemplate(VodCredential authInfo) {
        string apiName = "UpdateAITemplate";
        map<string, string> args;
        // 设置模板ID
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d258****";
        // 设置模板名称
        args["TemplateName"] = "我的自定义模板";
        // 设置模板详细配置
        Json::Value templateConfig;
        Json::Value auditItem;
        auditItem.append("terrorism");
        auditItem.append("porn");
        templateConfig["AuditItem"] = auditItem;
    
        Json::Value auditRange;
        auditRange.append("video");
        auditRange.append("image-cover");
        auditRange.append("text-title");
        templateConfig["AuditRange"] = auditRange;
    
        Json::Value auditContent;
        auditContent.append("screen");
        templateConfig["AuditContent"] = auditContent;
        templateConfig["AuditAutoBlock"] = "no";
        args["TemplateConfig"] = templateConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



查询AI模板 {#h2--ai-div-id-getaitemplate-div-7}
-------------------------------------------

调用GetAITemplate接口，完成查询AI模板功能。
接口参数和返回字段请参见[GetAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板.md)。调用示例如下： {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 查询AI模板
     */
    VodApiResponse getAITemplate(VodCredential authInfo) {
        string apiName = "GetAITemplate";
        map<string, string> args;
        // 设置模板ID
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d2c832****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



查询AI模板列表 {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------

调用ListAITemplate接口，完成查询AI模板列表功能。
接口参数和返回字段请参见[ListAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板列表.md)。调用示例如下： {#h2--ai-div-id-listaitemplate-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 查询AI模板列表
     */
    VodApiResponse listAITemplate(VodCredential authInfo) {
        string apiName = "ListAITemplate";
        map<string, string> args;
        // 设置模板类型，以智能审核模板为例
        args["TemplateType"] = "AIMediaAudit";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



设置默认AI模板 {#h2--ai-div-id-setdefaultaitemplate-div-9}
----------------------------------------------------

调用SetDefaultAITemplate接口，完成设置默认AI模板功能。
接口参数和返回字段请参见[SetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/设置默认AI模板.md)。调用示例如下： {#h2--ai-div-id-setdefaultaitemplate-div-9}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 设置默认AI模板
     */
    VodApiResponse setDefaultAITemplate(VodCredential authInfo) {
        string apiName = "SetDefaultAITemplate";
        map<string, string> args;
        // 设置模板ID
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d2c8****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = setDefaultAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



查询默认AI模板 {#h2--ai-div-id-getdefaultaitemplate-div-10}
-----------------------------------------------------

调用GetDefaultAITemplate接口，完成查询默认AI模板功能。
接口参数和返回字段请参见[GetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询默认AI模板.md)。调用示例如下： {#h2--ai-div-id-getdefaultaitemplate-div-10}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    /**
     * 查询默认AI模板
     */
    VodApiResponse getDefaultAITemplate(VodCredential authInfo) {
        string apiName = "GetDefaultAITemplate";
        map<string, string> args;
        // 设置模板类型，以智能审核模板为例
        args["TemplateType"] = "AIMediaAudit";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getDefaultAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }


