Media category 
===================================

This topic provides examples on how to use the API operations of the media category module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to create, delete, and modify categories. You can also query categories and the subcategories.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Create a category {#h2--div-id-addcategory-div-2}
-------------------------------------------------

You can call the AddCategory operation to create a category.

For more information about the request and response parameters of this operation, see [AddCategory](/intl.en-US/API Reference/Media asset management/Media asset category/AddCategory.md). Example:

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /* Create a category. */
    VodApiResponse addCategory(VodCredential authInfo) {
        string apiName = "AddCategory";
        map<string, string> args;
        // The ID of the category. If this parameter is left empty, a level-1 subcategory is created, with the ID of the root category set to -1.
        args["ParentId"] = "-1";
        // The name of the category. The name can contain a maximum of 64 bytes and must be encoded in UTF-8.
        args["CateName"] = "CateName";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = addCategory(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify a category {#h2--div-id-updatecategory-div-3}
----------------------------------------------------

You can call the UpdateCategory operation to modify a category.

For more information about the request and response parameters of this operation, see [UpdateCategory](/intl.en-US/API Reference/Media asset management/Media asset category/UpdateCategory.md). Example:

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /* Modify a category. */
    VodApiResponse updateCategory(VodCredential authInfo) {
        string apiName = "UpdateCategory";
        map<string, string> args;
        args["CateId"] = "<CateId>";
        // The name of the category. The name can contain a maximum of 64 bytes and must be encoded in UTF-8.
        args["CateName"] = "CateName";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateCategory(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete a category {#h2--div-id-deletecategory-div-4}
----------------------------------------------------

You can call the DeleteCategory operation to delete a category.

For more information about the request and response parameters of this operation, see [DeleteCategory](/intl.en-US/API Reference/Media asset management/Media asset category/DeleteCategory.md). Example:

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /* Delete a category. */
    VodApiResponse deleteCategory(VodCredential authInfo) {
        string apiName = "DeleteCategory";
        map<string, string> args;
        args["CateId"] = "<CateId>";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteCategory(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query a category and the subcategories {#h2--div-id-getcategories-div-5}
------------------------------------------------------------------------

You can call the GetCategories operation to query a category and the subcategories.

For more information about the request and response parameters of this operation, see [GetCategories](/intl.en-US/API Reference/Media asset management/Media asset category/GetCategories.md). Example:

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /* Query a category and the subcategories. */
    VodApiResponse getCategories(VodCredential authInfo) {
        string apiName = "GetCategories";
        map<string, string> args;
        args["CateId"] = "<CateId>";
        args["PageNo"] = "1";
        args["PageSize"] = "10";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getCategories(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }


