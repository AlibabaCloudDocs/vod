Responses 
==============================

This topic describes the responses of the ApsaraVideo VOD API.

Response description 
-----------------------------------------

Responses are returned in the JSON or XML format. The default response format is XML. To change the format, you can set the `Format` parameter in requests.

The sample responses provided in the API reference are formatted with line feeds and indentations for better readability. However, the actual responses are not formatted with line feeds or indentations.

Sample success responses 
---------------------------------------------

* XML format

      <? xml version="1.0" encoding="UTF-8" ? >
      <!--Result root node-->
      <Operation name+Response>
          <!--Return request tag-->
          <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
          <!--Return result data-->
      </Operation name+Response>
                                      

  

* JSON format

      {
          "RequestId": "4C467B38-3910-447D-87BC-AC049166F216", /* Return result data */
      }
                                      

  




Sample error responses 
-------------------------------------------

If an error occurs when you call an operation, an error response that consists of the error code, error message, and request ID is returned. The HTTP status code is 4xx or 5xx. You can troubleshoot an error based on the error code returned. For more information, see [Error codes](/intl.en-US/API Reference/Error codes.md). If the error persists, you can submit a [ticket](https://selfservice.console.aliyun.com/ticket/category/vod/today) and provide the host ID and request ID to get technical support from Alibaba Cloud.

* XML format

      <? xml version="1.0" encoding="UTF-8"? > 
      <Error>
                      <RequestId>8906582E-6722-409A-A6C4-0E7863B733A5</RequestId> 
                      <HostId>vod.cn-shanghai.aliyuncs.com</HostId> 
                      <Code>UnsupportedOperation</Code>
                      <Message>The specified action is not supported. </Message>
              </Error>
                                              

  

* JSON format

              {
                      "RequestId": "8906582E-6722-409A-A6C4-0E7863B733A5", 
                      "HostId": "vod.cn-shanghai.aliyuncs.com",
                      "Code": "UnsupportedOperation",
                      "Message": "The specified action is not supported."
              }
                                              

  



