Media asset category 
=========================================

This topic provides examples on how to use the API operations of the media asset category module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to create, delete, and modify categories. You can also query categories and their subcategories.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Create a category {#h2--div-id-addcategory-div-2}
-------------------------------------------------

You can call the AddCategory operation to create a category.


For more information about the request and response parameters of this operation, see [AddCategory](/intl.en-US/API Reference/Media management/Media Category/AddCategory.md). Example:

    function addCategory($client, $cateName, $parentId=-1) {
        $request = new vod\AddCategoryRequest();
        $request->setCateName($cateName); 
        $request->setParentId($parentId);
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $addRes = addCategory($client, 'Category Name');
        var_dump($addRes);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify a category {#h2--div-id-updatecategory-div-3}
----------------------------------------------------

You can call the UpdateCategory operation to modify a category.


For more information about the request and response parameters of this operation, see [UpdateCategory](/intl.en-US/API Reference/Media management/Media Category/UpdateCategory.md). Example:

    function updateCategory($client, $cateId, $cateName) {
        $request = new vod\UpdateCategoryRequest();
        $request->setCateId($cateId);
        $request->setCateName($cateName);   // The name of the category.
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $updateRes = updateCategory($client, '<Category ID>', 'New Category Name');
        var_dump($updateRes);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete a category {#h2--div-id-deletecategory-div-4}
----------------------------------------------------

You can call the DeleteCategory operation to delete a category.

For more information about the request and response parameters of this operation, see [DeleteCategory](/intl.en-US/API Reference/Media management/Media Category/DeleteCategory.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // If you delete a video category, its subcategories, including level-2 and level -3 categories, are also deleted. Perform this operation with caution.
    function deleteCategory($client, $cateId) {
        $request = new vod\DeleteCategoryRequest();
        $request->setCateId($cateId);
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $delRes = deleteCategory($client, '<Category ID>');
        var_dump($delRes);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query a category and its subcategories {#h2--div-id-getcategories-div-5}
------------------------------------------------------------------------

You can call the GetCategories operation to query a category and its subcategories.

For more information about the request and response parameters of this operation, see [GetCategories](/intl.en-US/API Reference/Media management/Media Category/GetCategories.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Query the information about the specified category and its subcategories.
    function getCategories($client, $cateId=-1, $pageNo=1, $pageSize=10) {
        $request = new vod\GetCategoriesRequest();
        $request->setCateId($cateId);   // The ID of the category. The default value -1 indicates the category ID of a root node.
        $request->setPageNo($pageNo);
        $request->setPageSize($pageSize);
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $getRes = getCategories($client, '<Category Id>');
        var_dump($getRes);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


