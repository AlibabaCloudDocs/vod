视频DNA 
==========================

本篇文档提供了C/C++ SDK视频DNA模块相关功能的API调用示例。包含提交视频DNA作业、查询视频DNA作业、获取视频DNA结果。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/C/C++ SDK/初始化.md)。

提交视频DNA作业 {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------

调用SubmitAIJob接口，完成提交视频DNA作业功能。

接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/提交AI作业.md)。调用示例如下：

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
        args["MediaId"] = "3eb19a4585bc475e995bdd78fd****";
        // 设置AI类型，类型为AIMediaDNA
        args["Types"] = "AIMediaDNA";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



查询视频DNA作业 {#h2--dna-div-id-listaijob-div-3}
-------------------------------------------

调用ListAIJob接口，完成查询视频DNA作业功能。

接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/查询AI作业.md)。调用示例如下：

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
        args["JobIds"] = "979d4d7a36ae41b1a945a288****,3eb19a4585bc475e995bddea65****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



获取视频DNA结果 {#h2--dna-div-id-getmediadnaresult-div-4}
---------------------------------------------------

调用GetMediaDNAResult接口，完成获取视频DNA结果功能。

接口参数和返回字段请参见[GetMediaDNAResult](/cn.zh-CN/服务端API/视频AI/视频DNA/获取视频DNA结果.md)。调用示例如下：

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 查询结果
     */
    VodApiResponse getMediaDNAResult(VodCredential authInfo) {
        string apiName = "GetMediaDNAResult";
        map<string, string> args;
        // 设置视频ID
        args["MediaId"] = "3eb19a4585bc475e995bdd78****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // 请求示例
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getMediaDNAResult(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }


