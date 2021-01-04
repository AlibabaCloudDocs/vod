Media asset category 
=========================================

This topic provides examples on how to use the API operations of the media asset category module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to create, delete, and modify categories. You can also query categories and their subcategories.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Create a category {#h2--div-id-addcategory-div-2}
-------------------------------------------------

You can call the AddCategory operation to create a category.
For more information about the request and response parameters of this operation, see [AddCategory](/intl.en-US/API Reference/Media management/Media Category/AddCategory.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("AddCategory", {
        ParentId: -1,         // The ID of the parent category. If this parameter is left empty, a level-1 category whose parent category ID is set to -1 is created.
        CateName: 'Category name'    // The name of the category.
    }, {}).then(function (response) {
        if (response.Category){
            // The information about the created category.
            console.log('ParentId = ' + response.Category.ParentId);
            console.log('CateId = ' + response.Category.CateId);
            console.log('CateName = ' + response.Category.CateName);
            console.log('Level = ' + response.Category.Level);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify a category {#h2--div-id-updatecategory-div-3}
----------------------------------------------------

You can call the UpdateCategory operation to modify a category.
For more information about the request and response parameters of this operation, see [UpdateCategory](/intl.en-US/API Reference/Media management/Media Category/UpdateCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("UpdateCategory", {
        CateId: -1,    // The ID of the category.
        CateName: 'Category name 2'   // The name of the category.
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete a category {#h2--div-id-deletecategory-div-4}
----------------------------------------------------

You can call the DeleteCategory operation to delete a category.
For more information about the request and response parameters of this operation, see [DeleteCategory](/intl.en-US/API Reference/Media management/Media Category/DeleteCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DeleteCategory", {
        CateId: -1    // The ID of the category.
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query a category and its subcategories {#h2--div-id-getcategories-div-5}
------------------------------------------------------------------------

You can call the GetCategories operation to query a category and its subcategories.
For more information about the request and response parameters of this operation, see [GetCategories](/intl.en-US/API Reference/Media management/Media Category/GetCategories.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetCategories", {
        CateId: -1,
        PageNo: 1,
        PageSize: 10
    }, {}).then(function (response) {
        // The information about the category.
        if (response.Category){
            console.log('ParentId = ' + response.Category.ParentId);
            console.log('CateId = ' + response.Category.CateId);
            console.log('CateName = ' + response.Category.CateName);
            console.log('Level = ' + response.Category.Level);
            console.log('SubTotal = ' + response.SubTotal);
        }
        if (response.SubCategories && response.SubCategories.Category && response.SubCategories.Category.length > 0){
            for (var i=0; i<response.SubCategories.Category.length; i++){
                var subCategory = response.SubCategories.Category[i];
                console.log('SubCategories.ParentId = ' + subCategory.ParentId);
                console.log('SubCategories.CateId = ' + subCategory.CateId);
                console.log('SubCategories.CateName = ' + subCategory.CateName);
                console.log('SubCategories.Level = ' + subCategory.Level);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


