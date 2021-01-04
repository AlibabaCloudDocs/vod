Media asset category 
=========================================

This topic provides examples on how to use the API operations of the media asset category module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to create, delete, and modify categories. You can also query categories and their subcategories.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Create a category {#h2--div-id-addcategory-div-2}
-------------------------------------------------

You can call the AddCategory operation to create a category.

For more information about the request and response parameters of this operation, see [AddCategory](/intl.en-US/API Reference/Media management/Media Category/AddCategory.md). Example:

    import com.aliyuncs.vod.model.v20170321.AddCategoryRequest;
    import com.aliyuncs.vod.model.v20170321.AddCategoryResponse;
    
    /* Create a category. */
    public static AddCategoryResponse addCategory(DefaultAcsClient client) throws Exception {
        AddCategoryRequest request = new AddCategoryRequest();
        // The ID of the parent category. If this parameter is left empty, a level-1 category whose parent category ID is set to -1 is created.
        request.setParentId(-1L);
        // The name of the category.
        request.setCateName("CateName");
        return client.getAcsResponse(request);
    }
    
    /* Call example */
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        AddCategoryResponse response = new AddCategoryResponse();
        try {
            response = addCategory(client);
            // The information about the created category.
            System.out.print("ParentId = " + response.getCategory().getParentId() + "\n");
            System.out.print("CateId = " + response.getCategory().getCateId() + "\n");
            System.out.print("CateName = " + response.getCategory().getCateName() + "\n");
            System.out.print("Level = " + response.getCategory().getLevel() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Modify a category {#h2--div-id-updatecategory-div-3}
----------------------------------------------------

You can call the UpdateCategory operation to modify a category.

For more information about the request and response parameters of this operation, see [UpdateCategory](/intl.en-US/API Reference/Media management/Media Category/UpdateCategory.md). Example:

    import com.aliyuncs.vod.model.v20170321.UpdateCategoryRequest;
    import com.aliyuncs.vod.model.v20170321.UpdateCategoryResponse;
    
    /* Modify a category. * /
    public static UpdateCategoryResponse updateCategory(DefaultAcsClient client) throws Exception {
        UpdateCategoryRequest request = new UpdateCategoryRequest();
        // The ID of the category.
        request.setCateId(-1L);
        // The name of the category.
        request.setCateName("CateName");
        return client.getAcsResponse(request);
    }
    
    /* Call example */
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        UpdateCategoryResponse response = new UpdateCategoryResponse();
        try {
            response = updateCategory(client);
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Delete a category {#h2--div-id-deletecategory-div-4}
----------------------------------------------------

You can call the DeleteCategory operation to delete a category.

For more information about the request and response parameters of this operation, see [DeleteCategory](/intl.en-US/API Reference/Media management/Media Category/DeleteCategory.md). Example:

    import com.aliyuncs.vod.model.v20170321.DeleteCategoryRequest;
    import com.aliyuncs.vod.model.v20170321.DeleteCategoryResponse;
    
    /* Delete a category. */
    public static DeleteCategoryResponse deleteCategory(DefaultAcsClient client) throws Exception {
        DeleteCategoryRequest request = new DeleteCategoryRequest();
        // The ID of the category that you want to delete.
        request.setCateId(-1L);
        return client.getAcsResponse(request);
    }
    
    /* Call example */
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your  AccessKeySecret>");
        DeleteCategoryResponse response = new DeleteCategoryResponse();
        try {
            response = deleteCategory(client);
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Query a category and its subcategories {#h2--div-id-getcategories-div-5}
------------------------------------------------------------------------

You can call the GetCategories operation to query a category and its subcategories.

For more information about the request and response parameters of this operation, see [GetCategories](/intl.en-US/API Reference/Media management/Media Category/GetCategories.md). Example:

    import com.aliyuncs.vod.model.v20170321.GetCategoriesRequest;
    import com.aliyuncs.vod.model.v20170321.GetCategoriesResponse;
    
    /* Call example */
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your  AccessKeySecret>");
        GetCategoriesResponse response = new GetCategoriesResponse();
        try {
            // The ID of the category.
            Long cateId = -1L;
            // The number of the page to return.
            Long pageNo = 1L;
            // The number of entries to return on each page.
            Long pageSize = 10L;
            response = getCategories(client, cateId, pageNo, pageSize);
            // The information about the specified category.
            System.out.print("ParentId = " + response.getCategory1().getParentId() + "\n");
            System.out.print("CateId = " + response.getCategory1().getCateId() + "\n");
            System.out.print("CateName = " + response.getCategory1().getCateName() + "\n");
            System.out.print("Level = " + response.getCategory1().getLevel() + "\n");
            System.out.print("SubTotal = " + response.getSubTotal()+ "\n");
            // The subcategories for the specified category.
            for (GetCategoriesResponse.Category category : response.getSubCategories()) {
                System.out.print("SubCategories.ParentId = " + category.getParentId() + "\n");
                System.out.print("SubCategories.CateId = " + category.getCateId() + "\n");
                System.out.print("SubCategories.CateName = " + category.getCateName() + "\n");
                System.out.print("SubCategories.Level = " + category.getLevel() + "\n");
            }
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }
    
    /* Query a category and its subcategories. */
    public static GetCategoriesResponse getCategories(DefaultAcsClient client, Long cateId, Long pageNo, Long pageSize) throws Exception {
        GetCategoriesRequest request = new GetCategoriesRequest();
        request.setCateId(cateId);
        request.setPageNo(pageNo);
        request.setPageSize(pageSize);
        return client.getAcsResponse(request);
    }


