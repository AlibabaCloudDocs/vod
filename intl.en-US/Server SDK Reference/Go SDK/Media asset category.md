Media asset category 
=========================================

This topic provides examples on how to use the API operations of the media asset category module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to create, delete, and modify categories. You can also query categories and their subcategories.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Create a category {#h2--div-id-addcategory-div-2}
-------------------------------------------------

You can call the AddCategory operation to create a category.
For more information about the request and response parameters of this operation, see [AddCategory](/intl.en-US/API Reference/Media asset management/Media asset category/AddCategory.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyAddCategory(client *vod.Client) (response *vod.AddCategoryResponse, err error) {
        request := vod.CreateAddCategoryRequest()
        request.CateName = "sample category name"
        request.ParentId = "-1"
        request.AcceptFormat = "JSON"
    
        return client.AddCategory(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyAddCategory(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.Category.CateId)
    }



Modify a category {#h2--div-id-updatecategory-div-3}
----------------------------------------------------

You can call the UpdateCategory operation to modify a category.
For more information about the request and response parameters of this operation, see [UpdateCategory](/intl.en-US/API Reference/Media asset management/Media asset category/UpdateCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyUpdateCategory(client *vod.Client) (response *vod.UpdateCategoryResponse, err error) {
        request := vod.CreateUpdateCategoryRequest()
        request.CateId = "<CateId>"
        request.CateName = "sample category name"
        request.AcceptFormat = "JSON"
    
        return client.UpdateCategory(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateCategory(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
    }



Delete a category {#h2--div-id-deletecategory-div-4}
----------------------------------------------------

You can call the DeleteCategory operation to delete a category.
For more information about the request and response parameters of this operation, see [DeleteCategory](/intl.en-US/API Reference/Media asset management/Media asset category/DeleteCategory.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteCategory(client *vod.Client) (response *vod.DeleteCategoryResponse, err error) {
        request := vod.CreateDeleteCategoryRequest()
        request.CateId = "<CateId>"
        request.AcceptFormat = "JSON"
    
        return client.DeleteCategory(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteCategory(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
    }



Query a category and its subcategories {#h2--div-id-getcategories-div-5}
------------------------------------------------------------------------

You can call the GetCategories operation to query a category and its subcategories.
For more information about the request and response parameters of this operation, see [GetCategories](/intl.en-US/API Reference/Media asset management/Media asset category/GetCategories.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetCategories(client *vod.Client) (response *vod.GetCategoriesResponse, err error) {
        request := vod.CreateGetCategoriesRequest()
        request.CateId = "<CateId>"
        request.PageNo = "1"
        request.PageSize = "20"
        request.AcceptFormat = "JSON"
    
        return client.GetCategories(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetCategories(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
    }


