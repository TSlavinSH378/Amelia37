This demonstration creates a timeline graph of data stored in a Script task and sent as a JSON string for display by Amelia.
![](attachments/11939967/11939968.png)
Figure. doTimelineGraph BPN
# Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doTimelineGraph. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create Suggested Responses

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say this is a large timeline graph in chat | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | creates large timeline | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | send the integration message jsonString | Sends the variable jsonString to Amelia's interface for display of interactive calendar |
| 4 | say that was a timeline graph |  |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
# A Script to Create a Timeline Graph
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
def largeTimeline =
'''
{
    "action": "addChatMessage",
    "payload": {
        "componentType": "MessageIntegration",
        "subComponentType": "TimeSelector",
        "subComponentProps": {
            "selected": "1M",
            "dates": [
              "1D",
              "1W",
              "1M",
              "6M",
              "1Y",
              "ALL"
            ],
            "dateStrings": {
              "1D": "PAST DAY",
              "1W": "PAST WEEK",
              "1M": "PAST MO",
              "6M": "PAST 6MOS",
              "1Y": "PAST YR",
              "ALL": "ALL"
            },
            "subComponents": [
              {
                "size": "large",
                "graphType": "timeline",
                "dates": {
                  "1D": {
                    "primary": "+$300.00",
                    "secondary": "8%"
                  },
                  "1W": {
                    "primary": "+$1000.00",
                    "secondary": "25%"
                  },
                  "1M": {
                    "primary": "+$4,000.00",
                    "secondary": "100%"
                  },
                  "6M": {
                    "primary": "+$24,000.00",
                    "secondary": "400%"
                  },
                  "1Y": {
                    "primary": "+$100,000.00",
                    "secondary": "1000%"
                  },
                  "ALL": {
                    "primary": "-$100,000,000.00",
                    "secondary": "10000%"
                  }
                },
                "1D": {
                    "sections": [
                      {
                        "dataPoints": [
                          {
                            "x": 1,
                            "y": 3,
                            "date": "Sept 11, 2017"
                          },
                          {
                            "x": 2,
                            "y": 9,
                            "date": "Sept 13, 2017"
                          }
                        ],
                        "lineColor": "blue",
                        "primaryValue": "$19,020.22",
                        "title": "Account Balance"
                      }
                    ]
                },
                "1W": {
                  "sections": [
                      {
                        "dataPoints": [
                          {
                            "x": 5,
                            "y": 12,
                            "date": "Sept 11, 2017"
                          },
                          {
                            "x": 6,
                            "y": 3,
                            "date": "Sept 13, 2017"
                          }
                        ],
                        "lineColor": "blue",
                        "primaryValue": "$9,000.00",
                        "title": "Account Balance"
                      }
                    ]
                },
                "1M": {
                  "sections": [
                  {
                    "dataPoints": [
                      {
                        "x": 3,
                        "y": 15,
                        "date": "Sept 11, 2017"
                      },
                      {
                        "x": 4,
                        "y": 11,
                        "date": "Sept 12, 2017"
                      },
                      {
                        "x": 5,
                        "y": 12,
                        "date": "Sept 13, 2017"
                      },
                      {
                        "x": 6,
                        "y": 3,
                        "date": "Sept 14, 2017"
                      }
                    ],
                    "lineColor": "blue",
                    "primaryValue": "$35,720.30",
                    "title": "Account Balance"
                  }
                ]
                },
                "6M": {
                   "sections": [
                  {
                    "dataPoints": [
                      {
                        "x": 1,
                        "y": 10,
                        "date": "Sept 11, 2017"
                      },
                      {
                        "x": 2,
                        "y": 5,
                        "date": "Sept 12, 2017"
                      },
                      {
                        "x": 3,
                        "y": 15,
                        "date": "Sept 13, 2017"
                      },
                      {
                        "x": 4,
                        "y": 11,
                        "date": "Sept 14, 2017"
                      },
                      {
                        "x": 5,
                        "y": 12,
                        "date": "Sept 15, 2017"
                      },
                      {
                        "x": 6,
                        "y": 3,
                        "date": "Sept 16, 2017"
                      }
                    ],
                    "lineColor": "blue",
                    "primaryValue": "$19,020.22",
                    "title": "Account Balance"
                  }
                ]
                },
                "1Y": {
                  "sections": [
                      {
                        "dataPoints": [
                          {
                            "x": 1,
                            "y": 10,
                            "date": "Sept 11, 2017"
                          },
                          {
                            "x": 2,
                            "y": 5,
                            "date": "Sept 12, 2017"
                          },
                          {
                            "x": 3,
                            "y": 15,
                            "date": "Sept 13, 2017"
                          },
                          {
                            "x": 4,
                            "y": 11,
                            "date": "Sept 14, 2017"
                          },
                          {
                            "x": 5,
                            "y": 12,
                            "date": "Sept 15, 2017"
                          },
                          {
                            "x": 6,
                            "y": 3,
                            "date": "Sept 16, 2017"
                          },
                          {
                            "x": 7,
                            "y": 5,
                            "date": "Sept 17, 2017"
                          },
                          {
                            "x": 8,
                            "y": 6,
                            "date": "Sept 18, 2017"
                          },
                          {
                            "x": 9,
                            "y": 11,
                            "date": "Sept 19, 2017"
                          },
                          {
                            "x": 10,
                            "y": 1,
                            "date": "Sept 20, 2017"
                          },
                          {
                            "x": 11,
                            "y": 3,
                            "date": "Sept 21, 2017"
                          },
                          {
                            "x": 12,
                            "y": 5,
                            "date": "Sept 22, 2017"
                          },
                          {
                            "x": 13,
                            "y": 8,
                            "date": "Sept 23, 2017"
                          },
                          {
                            "x": 14,
                            "y": 12,
                            "date": "Sept 24, 2017"
                          },
                          {
                            "x": 15,
                            "y": 15,
                            "date": "Sept 25, 2017"
                          }
                        ],
                        "lineColor": "blue",
                        "primaryValue": "$19,020.22",
                        "title": "Account Balance"
                      }
                  ]
                },
                "ALL": {
                  "sections": [
                      {
                        "dataPoints": [
                          {
                            "x": 1,
                            "y": 10,
                            "date": "Sept 11, 2017"
                          },
                          {
                            "x": 2,
                            "y": 5,
                            "date": "Sept 12, 2017"
                          },
                          {
                            "x": 3,
                            "y": 15,
                            "date": "Sept 13, 2017"
                          },
                          {
                            "x": 4,
                            "y": 11,
                            "date": "Sept 14, 2017"
                          },
                          {
                            "x": 5,
                            "y": 12,
                            "date": "Sept 15, 2017"
                          },
                          {
                            "x": 6,
                            "y": 3,
                            "date": "Sept 16, 2017"
                          },
                          {
                            "x": 7,
                            "y": 5,
                            "date": "Sept 17, 2017"
                          },
                          {
                            "x": 8,
                            "y": 6,
                            "date": "Sept 18, 2017"
                          },
                          {
                            "x": 9,
                            "y": 11,
                            "date": "Sept 19, 2017"
                          },
                          {
                            "x": 10,
                            "y": 1,
                            "date": "Sept 20, 2017"
                          },
                          {
                            "x": 11,
                            "y": 3,
                            "date": "Sept 21, 2017"
                          },
                          {
                            "x": 12,
                            "y": 5,
                            "date": "Sept 22, 2017"
                          },
                          {
                            "x": 13,
                            "y": 8,
                            "date": "Sept 23, 2017"
                          },
                          {
                            "x": 14,
                            "y": 12,
                            "date": "Sept 24, 2017"
                          },
                          {
                            "x": 15,
                            "y": 8,
                            "date": "Sept 25, 2017"
                          },
                          {
                            "x": 16,
                            "y": 12,
                            "date": "Sept 26, 2017"
                          },
                          {
                            "x": 17,
                            "y": 9,
                            "date": "Sept 27, 2017"
                          },
                          {
                            "x": 18,
                            "y": 5,
                            "date": "Sept 28, 2017"
                          },
                          {
                            "x": 19,
                            "y": 12,
                            "date": "Oct 03, 2017"
                          },
                          {
                            "x": 19,
                            "y": 14,
                            "date": "Oct 04, 2017"
                          },
                          {
                            "x": 20,
                            "y": 18,
                            "date": "Oct 05, 2017"
                          },
                          {
                            "x": 21,
                            "y": 21,
                            "date": "Oct 08, 2017"
                          }
                        ],
                        "lineColor": "blue",
                        "primaryValue": "$19,020.22",
                        "title": "Account Balance"
                      }
                  ]
                }
              }
            ]
        }
    }
}
'''
execution.setVariable("jsonString", largeTimeline)
```
# Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doTimelineGraph workflow by typing this command in the chat interface:
    ``` groovy
    run the workflow doTimelineGraph
    ```
3.  Amelia displays a timeline graph above the input area.  
    ![](attachments/11939967/11939969.png)  
    Figure. Output of doTimelineGraph BPN  
4.  Amelia displays the the last Say task in the BPN.
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-8-23_13-8-59.png](attachments/11939967/11939968.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-8-23_13-7-11.png](attachments/11939967/11939969.png) (image/png)  
