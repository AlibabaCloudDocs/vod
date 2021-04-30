Error codes 
================================

This topic describes the common error codes. You can determine the error cause based on the description of error codes. 

Common errors 
----------------------------------



|        Error code         |                                     Error message                                     | HTTP status code |                                                                                                                                              Description                                                                                                                                              |
|---------------------------|---------------------------------------------------------------------------------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MissingParameter          | The input parameter \\ that is mandatory for processing this request is not supplied. | 400              | The error message returned because a required parameter is not set.                                                                                                                                                                                                                                   |
| InvalidParameter          | The specified parameter \\ is not valid.                                              | 400              | The error message returned because the specified parameter is invalid.                                                                                                                                                                                                                                |
| OperationDenied           | Your account does not open VOD service yet.                                           | 403              | The error message returned because ApsaraVideo VOD is not activated for your account.                                                                                                                                                                                                                 |
| OperationDenied.Suspended | Your VOD service is suspended.                                                        | 403              | The error message returned because your Alibaba Cloud account has overdue payments. Add funds to your account.                                                                                                                                                                                        |
| Forbidden                 | User not authorized to operate on the specified resource.                             | 403              | The error message returned because you are not authorized to perform the operation.In most cases, this error occurs because your account is not granted the relevant permissions. For more information, see [Overview](/intl.en-US/Developer Guide/Access authorization/Overview.md). |
| InternalError             | The request processing has failed due to some unknown error.                          | 500              | The error message returned because an unknown error occurred in the background. Try again later or contact customer service representatives.                                                                                                                                                          |
| ServiceUnAvailable        | The request has failed due to a temporary failure of the server.                      | 503              | The error message returned because the service is unavailable.                                                                                                                                                                                                                                        |


