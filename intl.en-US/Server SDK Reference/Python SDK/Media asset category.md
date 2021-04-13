Media asset category 
=========================================

This topic provides examples on how to use the API operations of the media asset category module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to create, delete, and modify categories. You can also query categories and their subcategories.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Create a category {#h2--div-id-addcategory-div-2}
-------------------------------------------------

You can call the AddCategory operation to create a category.
For more information about the request and response parameters of this operation, see [AddCategory](/intl.en-US/API Reference/Media asset management/Media asset category/AddCategory.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import AddCategoryRequest
    def add_category(clt, cateName, parentId=-1):
        request = AddCategoryRequest.AddCategoryRequest()
        request.set_CateName(cateName)
        request.set_ParentId(parentId)
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        addRes = add_category(clt, 'Category Name')
        print(json.dumps(addRes, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify a category {#h2--div-id-updatecategory-div-3}
----------------------------------------------------

You can call the UpdateCategory operation to modify a category.
For more information about the request and response parameters of this operation, see [UpdateCategory](/intl.en-US/API Reference/Media asset management/Media asset category/UpdateCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateCategoryRequest
    def update_category(clt, cateId, cateName):
        request = UpdateCategoryRequest.UpdateCategoryRequest()
        request.set_CateId(cateId)
        request.set_CateName(cateName)
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        updateRes = update_category(clt, '<cateId>', 'New Category Name')
        print(json.dumps(updateRes, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete a category {#h2--div-id-deletecategory-div-4}
----------------------------------------------------

You can call the DeleteCategory operation to delete a category.
For more information about the request and response parameters of this operation, see [DeleteCategory](/intl.en-US/API Reference/Media asset management/Media asset category/DeleteCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateCategoryRequest
    # If you delete a video category, its subcategories, including level-2 and level-3 categories, are also deleted. Perform this operation with caution.
    def delete_category(clt, cateId):
        request = DeleteCategoryRequest.DeleteCategoryRequest()
        request.set_CateId(cateId)
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        delRes = delete_category(clt, '<cateId>')
        print(json.dumps(delRes, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query a category and its subcategories {#h2--div-id-getcategories-div-5}
------------------------------------------------------------------------

You can call the GetCategories operation to query a category and its subcategories.
For more information about the request and response parameters of this operation, see [GetCategories](/intl.en-US/API Reference/Media asset management/Media asset category/GetCategories.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetCategoriesRequest
    def get_categories(clt, cateId=-1, pageNo=1, pageSize=10):
        request = GetCategoriesRequest.GetCategoriesRequest()
        request.set_CateId(cateId)
        request.set_PageNo(pageNo)
        request.set_PageSize(pageSize)
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        getRes = get_categories(clt, '<cateId>')
        print(json.dumps(getRes, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


