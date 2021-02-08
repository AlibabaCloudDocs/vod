# GetCategories

Queries the information about the specified category and its subcategories.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetCategories&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetCategories|The operation that you want to perform. Set the value to **GetCategories**. |
|CateId|Long|No|49339|The ID of the category. Default value: **-1**, which indicates the parent category ID of a level 1 category. |
|PageNo|Long|No|1|The number of the page where the subcategories to be returned are listed. Default value: **1**. |
|PageSize|Long|No|10|The number of entries to return on each page of the subcategory list. Default value: **10**. Maximum value: **100**. |
|SortBy|String|No|CreationTime:Desc|The method for sorting the results. Valid values:

 -   **CreationTime:Desc** \(default\): The results are sorted in reverse chronological order based on the creation time.
-   **CreationTime:Asc**: The results are sorted in chronological order based on the creation time. |
|Type|String|No|default|The type of the category. Valid values:

 -   **default** \(default\): default category
-   **material**: material category |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|SubTotal|Long|3795|The total number of subcategories. |
|Category|Struct| |The information about the specified category. |
|CateId|Long|100|The ID of the video category. |
|CateName|String|Movie|The name of the category.

 -   The value can be up to 64 bytes in length.
-   The string must be encoded in the UTF-8 format. |
|Level|Long|0|The level of the category. A value of **0** indicates a level 1 category. |
|ParentId|Long|-1|The ID of the parent category. The parent category ID of a level 1 category is **-1**. |
|Type|String|default|The type of the category. Valid values:

 -   **default** \(default\): default category
-   **material**: material category |
|SubCategories|Array of Category| |The list of subcategories. |
|Category| | | |
|CateId|Long|100|The ID of the video category. |
|CateName|String|Movie|The name of the category.

 -   The value can be up to 64 bytes in length.
-   The string must be encoded in the UTF-8 format. |
|Level|Long|0|The level of the category. A value of **0** indicates a level 1 category. |
|ParentId|Long|-1|The ID of the parent category. The parent category ID of a level 1 category is **-1**. |
|SubTotal|Long|1|The total number of subcategories. |
|Type|String|default|The type of the category. Valid values:

 -   **default** \(default\): default category
-   **material**: material category |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetCategories
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetCategoriesResponse>
      <Category>
            <ParentId>-1</ParentId>
            <Type>default</Type>
            <Level>0</Level>
            <CateName>Movie</CateName>
            <CateId>100</CateId>
      </Category>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <SubTotal>1</SubTotal>
      <SubCategories>
            <Category>
                  <ParentId>-1</ParentId>
                  <Type>default</Type>
                  <Level>0</Level>
                  <CateName>Movie</CateName>
                  <CateId>100</CateId>
                  <SubTotal>1</SubTotal>
            </Category>
      </SubCategories>
</GetCategoriesResponse>
```

`JSON` format

```
{
    "Category": {
        "ParentId": "-1",
        "Type": "default",
        "Level": "0",
        "CateName": "Movie",
        "CateId": "100"
    },
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "SubTotal": "1",
    "SubCategories": {
        "Category": [{
            "ParentId": "-1",
            "Type": "default",
            "Level": "0",
            "CateName": "Movie",
            "CateId": "100",
            "SubTotal": "1"
        }]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## Common errors

The following table describes the common errors that this operation can return.

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|InvalidCateId.NotFound

|The CateId not exist.

|404

|The error message returned because the specified category ID does not exist. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

