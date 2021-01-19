Search for media asset information 
=======================================================

You can search for and sort media asset information of videos, audio, and images in the media library. This topic describes how to search for media asset information in the console or by using API operations or SDKs. This topic also describes the limits of the two search methods and provides an example on how to search for media asset information by calling API operations.

Usage 
--------------------------

ApsaraVideo VOD provides the following two methods to search for media asset information:

* By using the ApsaraVideo VOD console

  On the **[Video and Audio](https://vod.console.aliyun.com/#/media/video/list)** page in the ApsaraVideo VOD console, you can search for media asset information by Name or ID. For more information, see [Media asset management](/intl.en-US/User Guide/Media library/Manage media assets.md).
  

* By using the APIs or SDKs

  Call the [SearchMedia](/intl.en-US/API Reference/Media management/Media Search/SearchMedia.md) operation and use the [media asset search protocol](/intl.en-US/API Reference/Appendix/Media asset search protocol.md).
  




Limits 
---------------------------

**Limits on pagination** 

To avoid performance problems caused by deep pagination, the SearchMedia operation returns only part of the data that meets the search conditions. To obtain more data or even list all data, you must use the `ScrollToken` and `SessionId` pagination identification parameters.

* Pagination parameters such as `PageNo` and `PageSize` are used to obtain some data without passing the `ScrollToken` and `SessionId` parameters. You can obtain the first **5,000** data records one time.

  

* To obtain more data or list all data, you must use the `PageNo` and `PageSize` pagination parameters and the `ScrollToken` and `SessionId` pagination identification parameters. Make sure that the number of data records on pages between the current page number and the required page number does not exceed **1,200** . When you go to the page specified by the required page number, you can obtain the next **1,200** data records. You can use your judgement to search for data until all data is obtained. You can obtain data in multiple segments based on the pagination identification parameters. However, you can obtain a maximum of **1,200** data records in each segment.

  




API examples 
---------------------------------

The following section uses video information search in the example to describe the search statement.
**Notice**

* Before you send a request, you must perform URL encoding on the request parameters.

  

* The equal signs (=), double quotation marks ("), single quotation marks ('), and parentheses used in the statement must be single-byte characters.

  





|     Category      |                                                                                                                                                                                                                                                                                                                                                                                                                                               Description                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Returned field    | By default, the SearchMedia operation returns only basic media asset information. To obtain more media asset information, you must set the `Fields` field. Obtain the `Title` and `CoverURL` parameters: Fields=Title,CoverURL  **Sample requests:**  http://vod.cn-shanghai.aliyuncs.com?Action=SearchMedia &Fields=Title,CoverURL                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Exact match       | Search for media asset information whose value of `VideoId` is `28ba2b26d540446c94cdd2c4c48090e5`: VideoId='28ba2b26d540446c94cdd2c4c48090e5'  **Sample requests:**  http://vod.cn-shanghai.aliyuncs.com?Action=SearchMedia &Match=VideoId='28ba2b26d540446c94cdd2c4c48090e5'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Fuzzy match       | Search for media asset information where `Title` contains `Music`: Title='Music'  or Title in ('Music')  **Sample requests:**  http://vod.cn-shanghai.aliyuncs.com?Action=SearchMedia &Match=Title='Music'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Multi-value query | Search for media asset information whose `Status` is `Normal` or `Checking`: Status in ('Normal','Checking')  **Sample requests:**  http://vod.cn-shanghai.aliyuncs.com?Action=SearchMedia &Match=Status in ('Normal','Checking')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Range query       | Use an open and closed interval to indicate a range. Search for media asset information whose `CreationTime` is between `2018-01-01T00:00:00Z` and `2018-02-01T00:00:00Z`: CreationTime=('2018-01-01T00:00:00Z','2018-02-01T00:00:00Z')  **Sample requests:**  http://vod.cn-shanghai.aliyuncs.com?Action=SearchMedia &Match=CreationTime=('2018-01-01T00:00:00Z','2018-02-01T00:00:00Z')  If only the left or right boundary exists, leave the other boundary empty. Search for media asset information whose `CreationTime` is later than `2018-01-01T00:00:00Z`: CreationTime=('2018-01-01T00:00:00Z',)  **Sample requests:**  http://vod.cn-shanghai.aliyuncs.com?Action=SearchMedia &Match=CreationTime=('2018-01-01T00:00:00Z',)  |
| Sort field        | Sort media asset information in reverse chronological order based on the creation time: CreationTime:Desc  **Sample requests:**  http://vod.cn-shanghai.aliyuncs.com?Action=SearchMedia &SortBy=CreationTime:Desc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |


