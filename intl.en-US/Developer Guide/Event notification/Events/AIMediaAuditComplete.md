# AIMediaAuditComplete

This topic describes the AIMediaAuditComplete event as well as its notification content and sample callbacks.

## Event type

AIMediaAuditComplete

## Event description

The AIMediaAuditComplete event is generated after automated review is complete.

**Note:** ApsaraVideo VOD stores snapshots cited in an automated review result for free for up to **two weeks**. After that, the snapshots are automatically deleted.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **AIMediaAuditComplete**.|
|JobId|String|Yes|The ID of the automated review job. The value is the same as the JobId value returned by the SubmitAIMediaAuditJob operation.|
|MediaId|String|Yes|The ID of the video.|
|Status|String|Yes|Indicates whether the automated review job is complete. Valid values:-   **success**: The automated review job is complete.
-   **fail**: The automated review job failed to be complete. |
|Code|String|No|The error code. This parameter is available when an error occurs in the automated review job.|
|Message|String|No|The error message. This parameter is available when an error occurs in the automated review job.|
|Data|String|Yes|The automated review result. The value is a JSON string. For more information, see the "AIMediaAuditResult" section in [AI processing parameters](/intl.en-US/API Reference/Appendix/Video AI parameters.md).|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{
    "EventTime": "2017-03-20T07:49:17Z",
    "EventType": "AIMediaAuditComplete",
    "JobId": "43q91jdh7df****",
    "MediaId": "SHEN38505NDF9****",
    "Status": "success",
    "Code": "0",
    "Message": "OK",
    "Data": {
            "AbnormalModules":"video",
            "Label":"porn",
            "Suggestion":"review",
            "VideoResult":{
                "Suggestion":"review",
                "TerrorismResult":{
                    "TopList":[
                        {
                            "Score":"100.0000000000",
                            "Label":"normal",
                            "Timestamp":"3005",
                            "Url":"http://temp-tes*****et.oss-cn-shanghai.aliyuncs.com/aivideocensor/****.jpg"
                        },
                        {
                            "Score":"100.0000000000",
                            "Label":"normal",
                            "Timestamp":"15005",
                            "Url":"http://temp-tes*****et.oss-cn-shanghai.aliyuncs.com/aivideocensor/****.jpg"
                        }
                    ],
                    "Suggestion":"pass",
                    "MaxScore":"100.0000000000",
                    "AverageScore":"100.0000000000",
                    "Label":"normal",
                    "CounterList":[
                        {
                            "Label":"terrorism",
                            "Count":0
                        },
                        {
                            "Label":"outfit",
                            "Count":0
                        },
                        {
                            "Label":"logo",
                            "Count":0
                        },
                        {
                            "Label":"weapon",
                            "Count":0
                        },
                        {
                            "Label":"politics",
                            "Count":0
                        },
                        {
                            "Label":"others",
                            "Count":0
                        },
                        {
                            "Label":"normal",
                            "Count":16
                        }
                    ]
                },
                "Label":"porn",
                "PornResult":{
                    "TopList":[
                        {
                            "Score":"92.4800000000",
                            "Label":"sexy",
                            "Timestamp":"1005",
                            "Url":"http://temp-tes*****et.oss-cn-shanghai.aliyuncs.com/aivideocensor/****.jpg"
                        },
                        {
                            "Score":"91.8200000000",
                            "Label":"sexy",
                            "Timestamp":"9005",
                            "Url":"http://temp-tes*****et.oss-cn-shanghai.aliyuncs.com/aivideocensor/****.jpg"
                        }
                    ],
                    "Suggestion":"review",
                    "MaxScore":"92.4800000000",
                    "AverageScore":"81.7066666667",
                    "Label":"sexy",
                    "CounterList":[
                        {
                            "Label":"porn",
                            "Count":0
                        },
                        {
                            "Label":"sexy",
                            "Count":6
                        },
                        {
                            "Label":"normal",
                            "Count":10
                        }
                    ]
                }
            },
            "ImageResult":[
                {
                    "Suggestion":"pass",
                    "Type":"cover",
                    "Label":"normal",
                    "Url":"http://www.test.com/43q91jdh7df****.jpg",
                    "Result":[
                        {
                            "Suggestion":"pass",
                            "Score":"65.25",
                            "Label":"normal",
                            "Scene":"porn"
                        },
                        {
                            "Suggestion":"pass",
                            "Score":"100.0",
                            "Label":"normal",
                            "Scene":"terrorism"
                        }
                    ]
                }
            ],
            "TextResult":[
                {
                    "Suggestion":"pass",
                    "Type":"title",
                    "Score":"99.91",
                    "Content":"1111",
                    "Label":"normal",
                    "Scene":"antispam"
                }
            ]
        }
}
```

