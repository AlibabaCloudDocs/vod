Media asset category 
=========================================

This topic provides examples on how to use the API operations of the media asset category module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to create, delete, and modify categories. You can also query categories and their subcategories.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Create a category {#h2--div-id-addcategory-div-2}
-------------------------------------------------

You can call the AddCategory operation to create a category.
For more information about the request and response parameters of this operation, see [AddCategory](/intl.en-US/API Reference/Media asset management/Media asset category/AddCategory.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.Sample
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    AddCategoryRequest request = new AddCategoryRequest();
                    // Specify the ID of the parent category. If this parameter is left empty, a level-1 category whose parent category ID is set to -1 is created.
                    request.ParentId = -1;
                    // Specify a name for the category.
                    request.CateName = "catename";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    AddCategoryResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    Console.WriteLine("CateId = " + response.Category.CateId);
                    Console.WriteLine("CateName = " + response.Category.CateName);
                    Console.WriteLine("ParentId = " + response.Category.ParentId);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Modify a category {#h2--div-id-updatecategory-div-3}
----------------------------------------------------

You can call the UpdateCategory operation to modify a category.
For more information about the request and response parameters of this operation, see [UpdateCategory](/intl.en-US/API Reference/Media asset management/Media asset category/UpdateCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.Sample
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    UpdateCategoryRequest request = new UpdateCategoryRequest();
                    // Specify the ID of the category.
                    request.CateId = -1;
                    // Specify a new name for the category.
                    request.CateName = "new catename";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    UpdateCategoryResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Delete a category {#h2--div-id-deletecategory-div-4}
----------------------------------------------------

You can call the DeleteCategory operation to delete a category.
For more information about the request and response parameters of this operation, see [DeleteCategory](/intl.en-US/API Reference/Media asset management/Media asset category/DeleteCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.Sample
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    DeleteCategoryRequest request = new DeleteCategoryRequest();
                    // Specify the ID of the category.
                    request.CateId = -1;
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    DeleteCategoryResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Query a category and its subcategories {#h2--div-id-getcategories-div-5}
------------------------------------------------------------------------

You can call the GetCategories operation to query a category and its subcategories.
For more information about the request and response parameters of this operation, see [GetCategories](/intl.en-US/API Reference/Media asset management/Media asset category/GetCategories.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.Sample
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetCategoriesRequest request = new GetCategoriesRequest();
                    // Specify the ID of the category. If this parameter is left empty, a parent category and its subcategories are queried. The ID of the parent category is -1.
                    request.CateId = -1;
                    request.PageNo = 1;
                    request.PageSize = 10;
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetCategoriesResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // Display category information.
                    Console.WriteLine("Category.CateId = " + response.Category1.CateId);
                    Console.WriteLine("Category.CateName = " + response.Category1.CateName);
                    Console.WriteLine("Category.ParentId = " + response.Category1.ParentId);
                    Console.WriteLine("SubTotal = " + response.SubTotal);
                    // Display subcategory information.
                    foreach (var subcategory in response.SubCategories)
                    {
                        Console.WriteLine("subcategory.CateId = " + subcategory.CateId);
                        Console.WriteLine("subcategory.CateName = " + subcategory.CateName);
                        Console.WriteLine("subcategory.ParentId = " + subcategory.ParentId);
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }


