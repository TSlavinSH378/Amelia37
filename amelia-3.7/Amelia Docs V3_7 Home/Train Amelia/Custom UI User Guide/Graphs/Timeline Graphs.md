# Chat Log
Single series and multiple series timeline graphs can display in the chat log conversation area, as part of the conversation.
## Large Single Series Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large single series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396831/23396988.png)
Figure. Simple BPN to Display a Single Series Timeline Graph in the Chat Log
Running the simple BPN with the code below will display a timeline graph in the chat notes area, on the right side of the screen.
![](attachments/23396831/23396986.png)
Figure. Output of a Simple BPN to Display a Single Series Timeline Graph in the Chat Log
A BPN Script task will display a pre-populated timeline graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large Single Series Timeline Graph Code** Expand source
``` groovy
def jsonString = '''
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
                            "keyColor": "#ffb317",
                            "bannerValue": "$19,020.22",
                            "primary": "+$300.00",
                            "secondary": "8%",
                            "timePeriod": "PAST DAY",
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
                            "keyColor": "#ffb317",
                            "bannerValue": "$9,000.00",
                            "primary": "+$1000.00",
                            "secondary": "25%",
                            "timePeriod": "PAST WEEK",
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
                        "keyColor": "#ffb317",
                        "bannerValue": "$35,720.30",
                        "primary": "+$4,000.00",
                        "secondary": "100%",
                        "timePeriod": "PAST MO",
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
                        "keyColor": "#ffb317",
                        "bannerValue": "$19,020.22",
                        "primary": "+$24,000.00",
                        "secondary": "400%",
                        "timePeriod": "PAST 6MO",
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
                        "keyColor": "#ffb317",
                        "bannerValue": "$19,020.22",
                        "primary": "+$100,000.00",
                        "secondary": "1000%",
                        "timePeriod": "PAST YR",
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
                            "keyColor": "#ffb317",
                            "bannerValue": "$19,020.22",
                            "primary": "-$100,000,000.00",
                            "secondary": "10000%",
                            "timePeriod": "ALL",
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
messageService.sendIntegrationMessage(jsonString)
```
## Large Multiple Series Timeline Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large multiple series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396831/23396991.png)
Figure. Simple BPN to Display a Large Multiple Series Timeline Graph in the Chat Log
Running the simple BPN with the code below will display a timeline graph in the chat log.
![](attachments/23396831/23396990.png)
Figure. Output of a Simple BPN to Display a Multiple Series Timeline Graph in the Chat Log
A BPN Script task will display a pre-populated timeline graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large Multiple Series Timeline Graph Code** Expand source
``` groovy
def jsonString = '''
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
                          },
                          {
                            "x": 7,
                            "y": 4,
                            "date": "Sept 26, 2017"
                          }
                        ],
                        "keyColor": "#79c7e3",
                        "bannerValue": "$29,020.22",
                        "title": "Account Balance"
                      },
                      {
                        "dataPoints": [
                        {
                          "x": 1,
                          "y": 10,
                          "date": "Sept 11, 2017"
                        },
                        {
                          "x": 2,
                          "y": 2,
                          "date": "Sept 12, 2017"
                        },
                        {
                          "x": 7,
                          "y": 8,
                          "date": "Sept 24, 2017"
                        }
                      ],
                        "keyColor": "#1a3177",
                        "bannerValue": "$15,222.00",
                        "title": "Income"
                      },
                      {
                        "dataPoints": [
                            {
                              "x": 1,
                              "y": 4,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 2,
                              "y": 6,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 5,
                              "y": 8,
                              "date": "Sept 25, 2017"
                            }
                          ],
                        "keyColor": "#12939a",
                        "bannerValue": "$8,672.24",
                        "title": "Expenses"
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
                        "keyColor": "#79c7e3",
                        "bannerValue": "$19,020.22",
                        "title": "Account Balance"
                      },
                      {
                        "dataPoints": [
                            {
                              "x": 5,
                              "y": 2,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 6,
                              "y": 4,
                              "date": "Sept 12, 2017"
                            }
                          ],
                        "keyColor": "#1a3177",
                        "bannerValue": "$5,222.00",
                        "title": "Income"
                      },
                      {
                        "dataPoints": [
                            {
                              "x": 5,
                              "y": 10,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 6,
                              "y": 9,
                              "date": "Sept 12, 2017"
                            }
                          ],
                        "keyColor": "#12939a",
                        "bannerValue": "$1,672.24",
                        "title": "Expenses"
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
                        "keyColor": "#79c7e3",
                        "bannerValue": "$29,020.22",
                        "title": "Account Balance"
                      },
                      {
                        "dataPoints": [
                            {
                              "x": 3,
                              "y": 1,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 4,
                              "y": 3,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 5,
                              "y": 7,
                              "date": "Sept 13, 2017"
                            },
                            {
                              "x": 6,
                              "y": 9,
                              "date": "Sept 41, 2017"
                            }
                          ],
                        "keyColor": "#1a3177",
                        "bannerValue": "$8,222.00",
                        "title": "Income"
                      },
                      {
                        "dataPoints": [
                            {
                              "x": 3,
                              "y": 1,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 4,
                              "y": 10,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 5,
                              "y": 3,
                              "date": "Sept 13 2017"
                            },
                            {
                              "x": 6,
                              "y": 9,
                              "date": "Sept 14, 2017"
                            }
                          ],
                        "keyColor": "#12939a",
                        "bannerValue": "$7,672.24",
                        "title": "Expenses"
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
                        "keyColor": "#79c7e3",
                        "bannerValue": "$9,820.22",
                        "title": "Account Balance"
                      },
                      {
                        "dataPoints": [
                        {
                          "x": 1,
                          "y": 1,
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
                          "y": 12,
                          "date": "Sept 14, 2017"
                        },
                        {
                          "x": 5,
                          "y": 14,
                          "date": "Sept 15, 2017"
                        },
                        {
                          "x": 6,
                          "y": 3,
                          "date": "Sept 16, 2017"
                        }
                      ],
                        "keyColor": "#1a3177",
                        "bannerValue": "$13,222.00",
                        "title": "Income"
                      },
                      {
                        "dataPoints": [
                        {
                          "x": 1,
                          "y": 9,
                          "date": "Sept 11, 2017"
                        },
                        {
                          "x": 2,
                          "y": 11,
                          "date": "Sept 12, 2017"
                        },
                        {
                          "x": 3,
                          "y": 12,
                          "date": "Sept 13, 2017"
                        },
                        {
                          "x": 4,
                          "y": 3,
                          "date": "Sept 14, 2017"
                        },
                        {
                          "x": 5,
                          "y": 5,
                          "date": "Sept 15, 2017"
                        },
                        {
                          "x": 6,
                          "y": 3,
                          "date": "Sept 16, 2017"
                        }
                      ],
                        "keyColor": "#12939a",
                        "bannerValue": "$3,672.24",
                        "title": "Expenses"
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
                        "keyColor": "#79c7e3",
                        "bannerValue": "$8,888.22",
                        "title": "Account Balance"
                      },
                      {
                        "dataPoints": [
                        {
                          "x": 1,
                          "y": 3,
                          "date": "Sept 11, 2017"
                        },
                        {
                          "x": 2,
                          "y": 5,
                          "date": "Sept 12, 2017"
                        },
                        {
                          "x": 3,
                          "y": 17,
                          "date": "Sept 13, 2017"
                        },
                        {
                          "x": 4,
                          "y": 13,
                          "date": "Sept 14, 2017"
                        },
                        {
                          "x": 5,
                          "y": 9,
                          "date": "Sept 15, 2017"
                        },
                        {
                          "x": 6,
                          "y": 3,
                          "date": "Sept 16, 2017"
                        },
                        {
                          "x": 7,
                          "y": 6,
                          "date": "Sept 17, 2017"
                        },
                        {
                          "x": 8,
                          "y": 9,
                          "date": "Sept 18, 2017"
                        },
                        {
                          "x": 9,
                          "y": 10,
                          "date": "Sept 19, 2017"
                        },
                        {
                          "x": 10,
                          "y": 12,
                          "date": "Sept 20, 2017"
                        },
                        {
                          "x": 11,
                          "y": 13,
                          "date": "Sept 21, 2017"
                        },
                        {
                          "x": 12,
                          "y": 15,
                          "date": "Sept 22, 2017"
                        },
                        {
                          "x": 13,
                          "y": 9,
                          "date": "Sept 23, 2017"
                        },
                        {
                          "x": 14,
                          "y": 2,
                          "date": "Sept 24, 2017"
                        },
                        {
                          "x": 15,
                          "y": 5,
                          "date": "Sept 25, 2017"
                        }
                      ],
                        "keyColor": "#1a3177",
                        "bannerValue": "$5,555.00",
                        "title": "Income"
                      },
                      {
                        "dataPoints": [
                        {
                          "x": 1,
                          "y": 10,
                          "date": "Sept 11, 2017"
                        },
                        {
                          "x": 2,
                          "y": 11,
                          "date": "Sept 12, 2017"
                        },
                        {
                          "x": 3,
                          "y": 12,
                          "date": "Sept 13, 2017"
                        },
                        {
                          "x": 4,
                          "y": 13,
                          "date": "Sept 14, 2017"
                        },
                        {
                          "x": 5,
                          "y": 15,
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
                          "y": 2,
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
                          "y": 4,
                          "date": "Sept 23, 2017"
                        },
                        {
                          "x": 14,
                          "y": 10,
                          "date": "Sept 24, 2017"
                        },
                        {
                          "x": 15,
                          "y": 11,
                          "date": "Sept 25, 2017"
                        }
                      ],
                        "keyColor": "#12939a",
                        "bannerValue": "$1,111.24",
                        "title": "Expenses"
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
                        "keyColor": "#79c7e3",
                        "bannerValue": "$9,999.22",
                        "title": "Account Balance"
                      },
                      {
                        "dataPoints": [
                            {
                              "x": 1,
                              "y": 3,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 2,
                              "y": 5,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 3,
                              "y": 9,
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
                              "y": 18,
                              "date": "Sept 16, 2017"
                            },
                            {
                              "x": 7,
                              "y": 15,
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
                              "y": 5,
                              "date": "Sept 20, 2017"
                            },
                            {
                              "x": 11,
                              "y": 9,
                              "date": "Sept 21, 2017"
                            },
                            {
                              "x": 12,
                              "y": 11,
                              "date": "Sept 22, 2017"
                            },
                            {
                              "x": 13,
                              "y": 14,
                              "date": "Sept 23, 2017"
                            },
                            {
                              "x": 14,
                              "y": 7,
                              "date": "Sept 24, 2017"
                            },
                            {
                              "x": 15,
                              "y": 8,
                              "date": "Sept 25, 2017"
                            },
                            {
                              "x": 16,
                              "y": 2,
                              "date": "Sept 26, 2017"
                            },
                            {
                              "x": 17,
                              "y": 3,
                              "date": "Sept 27, 2017"
                            },
                            {
                              "x": 18,
                              "y": 5,
                              "date": "Oct 11, 2017"
                            },
                            {
                              "x": 19,
                              "y": 3,
                              "date": "Oct 12, 2017"
                            },
                            {
                              "x": 19,
                              "y": 5,
                              "date": "Oct 13, 2017"
                            },
                            {
                              "x": 20,
                              "y": 9,
                              "date": "Oct 14, 2017"
                            },
                            {
                              "x": 21,
                              "y": 21,
                              "date": "Oct 15, 2017"
                            }
                          ],
                        "keyColor": "#1a3177",
                        "bannerValue": "$2,222.00",
                        "title": "Income"
                      },
                      {
                        "dataPoints": [
                            {
                              "x": 1,
                              "y": 11,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 2,
                              "y": 7,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 3,
                              "y": 9,
                              "date": "Sept 13, 2017"
                            },
                            {
                              "x": 4,
                              "y": 11,
                              "date": "Sept 14, 2017"
                            },
                            {
                              "x": 5,
                              "y": 15,
                              "date": "Sept 15, 2017"
                            },
                            {
                              "x": 6,
                              "y": 18,
                              "date": "Sept 16, 2017"
                            },
                            {
                              "x": 7,
                              "y": 3,
                              "date": "Sept 17, 2017"
                            },
                            {
                              "x": 8,
                              "y": 5,
                              "date": "Sept 18, 2017"
                            },
                            {
                              "x": 9,
                              "y": 1,
                              "date": "Sept 19, 2017"
                            },
                            {
                              "x": 10,
                              "y": 7,
                              "date": "Sept 20, 2017"
                            },
                            {
                              "x": 11,
                              "y": 8,
                              "date": "Sept 21, 2017"
                            },
                            {
                              "x": 12,
                              "y": 2,
                              "date": "Sept 22, 2017"
                            },
                            {
                              "x": 13,
                              "y": 1,
                              "date": "Sept 23, 2017"
                            },
                            {
                              "x": 14,
                              "y": 11,
                              "date": "Sept 24, 2017"
                            },
                            {
                              "x": 15,
                              "y": 15,
                              "date": "Sept 25, 2017"
                            },
                            {
                              "x": 16,
                              "y": 16,
                              "date": "Sept 26, 2017"
                            },
                            {
                              "x": 17,
                              "y": 8,
                              "date": "Sept 27, 2017"
                            },
                            {
                              "x": 18,
                              "y": 9,
                              "date": "Oct 12, 2017"
                            },
                            {
                              "x": 19,
                              "y": 10,
                              "date": "Oct 13, 2017"
                            },
                            {
                              "x": 19,
                              "y": 12,
                              "date": "Oct 14, 2017"
                            },
                            {
                              "x": 20,
                              "y": 18,
                              "date": "Oct 15, 2017"
                            },
                            {
                              "x": 21,
                              "y": 15,
                              "date": "Oct 16, 2017"
                            }
                          ],
                        "keyColor": "#12939a",
                        "bannerValue": "$9,672.24",
                        "title": "Expenses"
                      }
                   ]
                }
              }
            ]
        }
    }
}
'''
messageService.sendIntegrationMessage(jsonString)
```
# Chat Notes
Large and small timeline graphs, with single and multiple series, can display in a chat note on the right side of the screen.
## Large Timeline Single Series Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large single series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396831/23396992.png)
Figure. Simple BPN to Display a Large Single Series Timeline Graph in a Chat Note
Running the simple BPN with the code below will display a large single series timeline graph in the chat notes area, on the right side of the screen.
![](attachments/23396831/23396985.png)
Figure. Output of a Simple BPN to Display a Large Single Series Timeline Graph in the Chat Log
A BPN Script task will display a pre-populated timeline graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large Single Series Graph Code for Chat Note** Expand source
``` groovy
def largeTimelineMetric = '''
    {
      "subcomponent": "Markup",
      "markupType": "TimeSelector",
      "label": "Large Timeline with Time Selector",
      "markupProps": {
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
          "graphType": "timeline",
          "size": "large",
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
                "keyColor": "blue",
                "bannerValue": "$19,020.22",
                "primary": "+$300.00",
                "secondary": "8%",
                "timePeriod": "PAST DAY",
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
                "keyColor": "blue",
                "bannerValue": "$9,000.00",
                            "primary": "+$1000.00",
                            "secondary": "25%",
                            "timePeriod": "PAST WEEK",
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
                "keyColor": "blue",
                "bannerValue": "$35,720.30",
                        "primary": "+$4,000.00",
                        "secondary": "100%",
                        "timePeriod": "PAST MO",
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
                "keyColor": "blue",
                "bannerValue": "$19,020.22",
                        "primary": "+$24,000.00",
                        "secondary": "400%",
                        "timePeriod": "PAST 6MO",
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
                "keyColor": "blue",
                "bannerValue": "$19,020.22",
                        "primary": "+$100,000.00",
                        "secondary": "1000%",
                        "timePeriod": "PAST YR",
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
                "keyColor": "blue",
                "bannerValue": "$19,020.22",
                            "primary": "-$100,000,000.00",
                            "secondary": "10000%",
                            "timePeriod": "ALL",
                            "title": "Account Balance"
              }
            ]
          }
        }
      ]
      }
    }
    '''
def jsonString = '''
    {
        "action":"addChatNotesIntegration",
        "componentType": "ChatNote",
        "header": "Updated Header",
        "payload": [{
          "component": "ChatNote",
          "title": "Chat Note B",
          "actionProcess": {
            "actionName": "edit-chat-note-B",
            "actionArguments":{
                "section": "image",
                "testVar": "some variable"},
            "actionMessage": "Edit the section"},
          "subcomponents": [''' + largeTimelineMetric + ''']
      }]}
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Large Timeline Graph with Multiple Series
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large multiple series graph in a chat note. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396831/23396999.png)
Figure. Simple BPN to Display a Large Multiple Series Timeline Graph in a Chat Note
Running the simple BPN with the code below will display a timeline graph in a chat note.
![](attachments/23396831/23396998.png)
Figure. Output of a Simple BPN to Display a Multiple Series Timeline Graph in a Chat Note
A BPN Script task will display a pre-populated timeline graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large Multiple Series Timeline Graph Code for Chat Note** Expand source
``` groovy
def largeTimelineLargeMetric = '''
    {
      "subcomponent": "Markup",
      "markupType": "TimeSelector",
      "label": "Large Timeline with time Selector and multiple sections",
      "markupProps": {
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
                              },
                              {
                                "x": 7,
                                "y": 4,
                                "date": "Sept 26, 2017"
                              }
                            ],
                            "keyColor": "#79c7e3",
                            "bannerValue": "$29,020.22",
                            "title": "Account Balance"
                          },
                          {
                            "dataPoints": [
                            {
                              "x": 1,
                              "y": 10,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 2,
                              "y": 2,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 7,
                              "y": 8,
                              "date": "Sept 24, 2017"
                            }
                          ],
                            "keyColor": "#1a3177",
                            "bannerValue": "$15,222.00",
                            "title": "Income"
                          },
                          {
                            "dataPoints": [
                                {
                                  "x": 1,
                                  "y": 4,
                                  "date": "Sept 11, 2017"
                                },
                                {
                                  "x": 2,
                                  "y": 6,
                                  "date": "Sept 12, 2017"
                                },
                                {
                                  "x": 5,
                                  "y": 8,
                                  "date": "Sept 25, 2017"
                                }
                              ],
                            "keyColor": "#12939a",
                            "bannerValue": "$8,672.24",
                            "title": "Expenses"
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
                            "keyColor": "#79c7e3",
                            "bannerValue": "$19,020.22",
                            "title": "Account Balance"
                          },
                          {
                            "dataPoints": [
                                {
                                  "x": 5,
                                  "y": 2,
                                  "date": "Sept 11, 2017"
                                },
                                {
                                  "x": 6,
                                  "y": 4,
                                  "date": "Sept 12, 2017"
                                }
                              ],
                            "keyColor": "#1a3177",
                            "bannerValue": "$5,222.00",
                            "title": "Income"
                          },
                          {
                            "dataPoints": [
                                {
                                  "x": 5,
                                  "y": 10,
                                  "date": "Sept 11, 2017"
                                },
                                {
                                  "x": 6,
                                  "y": 9,
                                  "date": "Sept 12, 2017"
                                }
                              ],
                            "keyColor": "#12939a",
                            "bannerValue": "$1,672.24",
                            "title": "Expenses"
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
                            "keyColor": "#79c7e3",
                            "bannerValue": "$29,020.22",
                            "title": "Account Balance"
                          },
                          {
                            "dataPoints": [
                                {
                                  "x": 3,
                                  "y": 1,
                                  "date": "Sept 11, 2017"
                                },
                                {
                                  "x": 4,
                                  "y": 3,
                                  "date": "Sept 12, 2017"
                                },
                                {
                                  "x": 5,
                                  "y": 7,
                                  "date": "Sept 13, 2017"
                                },
                                {
                                  "x": 6,
                                  "y": 9,
                                  "date": "Sept 41, 2017"
                                }
                              ],
                            "keyColor": "#1a3177",
                            "bannerValue": "$8,222.00",
                            "title": "Income"
                          },
                          {
                            "dataPoints": [
                                {
                                  "x": 3,
                                  "y": 1,
                                  "date": "Sept 11, 2017"
                                },
                                {
                                  "x": 4,
                                  "y": 10,
                                  "date": "Sept 12, 2017"
                                },
                                {
                                  "x": 5,
                                  "y": 3,
                                  "date": "Sept 13 2017"
                                },
                                {
                                  "x": 6,
                                  "y": 9,
                                  "date": "Sept 14, 2017"
                                }
                              ],
                            "keyColor": "#12939a",
                            "bannerValue": "$7,672.24",
                            "title": "Expenses"
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
                            "keyColor": "#79c7e3",
                            "bannerValue": "$9,820.22",
                            "title": "Account Balance"
                          },
                          {
                            "dataPoints": [
                            {
                              "x": 1,
                              "y": 1,
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
                              "y": 12,
                              "date": "Sept 14, 2017"
                            },
                            {
                              "x": 5,
                              "y": 14,
                              "date": "Sept 15, 2017"
                            },
                            {
                              "x": 6,
                              "y": 3,
                              "date": "Sept 16, 2017"
                            }
                          ],
                            "keyColor": "#1a3177",
                            "bannerValue": "$13,222.00",
                            "title": "Income"
                          },
                          {
                            "dataPoints": [
                            {
                              "x": 1,
                              "y": 9,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 2,
                              "y": 11,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 3,
                              "y": 12,
                              "date": "Sept 13, 2017"
                            },
                            {
                              "x": 4,
                              "y": 3,
                              "date": "Sept 14, 2017"
                            },
                            {
                              "x": 5,
                              "y": 5,
                              "date": "Sept 15, 2017"
                            },
                            {
                              "x": 6,
                              "y": 3,
                              "date": "Sept 16, 2017"
                            }
                          ],
                            "keyColor": "#12939a",
                            "bannerValue": "$3,672.24",
                            "title": "Expenses"
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
                            "keyColor": "#79c7e3",
                            "bannerValue": "$8,888.22",
                            "title": "Account Balance"
                          },
                          {
                            "dataPoints": [
                            {
                              "x": 1,
                              "y": 3,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 2,
                              "y": 5,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 3,
                              "y": 17,
                              "date": "Sept 13, 2017"
                            },
                            {
                              "x": 4,
                              "y": 13,
                              "date": "Sept 14, 2017"
                            },
                            {
                              "x": 5,
                              "y": 9,
                              "date": "Sept 15, 2017"
                            },
                            {
                              "x": 6,
                              "y": 3,
                              "date": "Sept 16, 2017"
                            },
                            {
                              "x": 7,
                              "y": 6,
                              "date": "Sept 17, 2017"
                            },
                            {
                              "x": 8,
                              "y": 9,
                              "date": "Sept 18, 2017"
                            },
                            {
                              "x": 9,
                              "y": 10,
                              "date": "Sept 19, 2017"
                            },
                            {
                              "x": 10,
                              "y": 12,
                              "date": "Sept 20, 2017"
                            },
                            {
                              "x": 11,
                              "y": 13,
                              "date": "Sept 21, 2017"
                            },
                            {
                              "x": 12,
                              "y": 15,
                              "date": "Sept 22, 2017"
                            },
                            {
                              "x": 13,
                              "y": 9,
                              "date": "Sept 23, 2017"
                            },
                            {
                              "x": 14,
                              "y": 2,
                              "date": "Sept 24, 2017"
                            },
                            {
                              "x": 15,
                              "y": 5,
                              "date": "Sept 25, 2017"
                            }
                          ],
                            "keyColor": "#1a3177",
                            "bannerValue": "$5,555.00",
                            "title": "Income"
                          },
                          {
                            "dataPoints": [
                            {
                              "x": 1,
                              "y": 10,
                              "date": "Sept 11, 2017"
                            },
                            {
                              "x": 2,
                              "y": 11,
                              "date": "Sept 12, 2017"
                            },
                            {
                              "x": 3,
                              "y": 12,
                              "date": "Sept 13, 2017"
                            },
                            {
                              "x": 4,
                              "y": 13,
                              "date": "Sept 14, 2017"
                            },
                            {
                              "x": 5,
                              "y": 15,
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
                              "y": 2,
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
                              "y": 4,
                              "date": "Sept 23, 2017"
                            },
                            {
                              "x": 14,
                              "y": 10,
                              "date": "Sept 24, 2017"
                            },
                            {
                              "x": 15,
                              "y": 11,
                              "date": "Sept 25, 2017"
                            }
                          ],
                            "keyColor": "#12939a",
                            "bannerValue": "$1,111.24",
                            "title": "Expenses"
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
                            "keyColor": "#79c7e3",
                            "bannerValue": "$9,999.22",
                            "title": "Account Balance"
                          },
                          {
                            "dataPoints": [
                                {
                                  "x": 1,
                                  "y": 3,
                                  "date": "Sept 11, 2017"
                                },
                                {
                                  "x": 2,
                                  "y": 5,
                                  "date": "Sept 12, 2017"
                                },
                                {
                                  "x": 3,
                                  "y": 9,
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
                                  "y": 18,
                                  "date": "Sept 16, 2017"
                                },
                                {
                                  "x": 7,
                                  "y": 15,
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
                                  "y": 5,
                                  "date": "Sept 20, 2017"
                                },
                                {
                                  "x": 11,
                                  "y": 9,
                                  "date": "Sept 21, 2017"
                                },
                                {
                                  "x": 12,
                                  "y": 11,
                                  "date": "Sept 22, 2017"
                                },
                                {
                                  "x": 13,
                                  "y": 14,
                                  "date": "Sept 23, 2017"
                                },
                                {
                                  "x": 14,
                                  "y": 7,
                                  "date": "Sept 24, 2017"
                                },
                                {
                                  "x": 15,
                                  "y": 8,
                                  "date": "Sept 25, 2017"
                                },
                                {
                                  "x": 16,
                                  "y": 2,
                                  "date": "Sept 26, 2017"
                                },
                                {
                                  "x": 17,
                                  "y": 3,
                                  "date": "Sept 27, 2017"
                                },
                                {
                                  "x": 18,
                                  "y": 5,
                                  "date": "Oct 11, 2017"
                                },
                                {
                                  "x": 19,
                                  "y": 3,
                                  "date": "Oct 12, 2017"
                                },
                                {
                                  "x": 19,
                                  "y": 5,
                                  "date": "Oct 13, 2017"
                                },
                                {
                                  "x": 20,
                                  "y": 9,
                                  "date": "Oct 14, 2017"
                                },
                                {
                                  "x": 21,
                                  "y": 21,
                                  "date": "Oct 15, 2017"
                                }
                              ],
                            "keyColor": "#1a3177",
                            "bannerValue": "$2,222.00",
                            "title": "Income"
                          },
                          {
                            "dataPoints": [
                                {
                                  "x": 1,
                                  "y": 11,
                                  "date": "Sept 11, 2017"
                                },
                                {
                                  "x": 2,
                                  "y": 7,
                                  "date": "Sept 12, 2017"
                                },
                                {
                                  "x": 3,
                                  "y": 9,
                                  "date": "Sept 13, 2017"
                                },
                                {
                                  "x": 4,
                                  "y": 11,
                                  "date": "Sept 14, 2017"
                                },
                                {
                                  "x": 5,
                                  "y": 15,
                                  "date": "Sept 15, 2017"
                                },
                                {
                                  "x": 6,
                                  "y": 18,
                                  "date": "Sept 16, 2017"
                                },
                                {
                                  "x": 7,
                                  "y": 3,
                                  "date": "Sept 17, 2017"
                                },
                                {
                                  "x": 8,
                                  "y": 5,
                                  "date": "Sept 18, 2017"
                                },
                                {
                                  "x": 9,
                                  "y": 1,
                                  "date": "Sept 19, 2017"
                                },
                                {
                                  "x": 10,
                                  "y": 7,
                                  "date": "Sept 20, 2017"
                                },
                                {
                                  "x": 11,
                                  "y": 8,
                                  "date": "Sept 21, 2017"
                                },
                                {
                                  "x": 12,
                                  "y": 2,
                                  "date": "Sept 22, 2017"
                                },
                                {
                                  "x": 13,
                                  "y": 1,
                                  "date": "Sept 23, 2017"
                                },
                                {
                                  "x": 14,
                                  "y": 11,
                                  "date": "Sept 24, 2017"
                                },
                                {
                                  "x": 15,
                                  "y": 15,
                                  "date": "Sept 25, 2017"
                                },
                                {
                                  "x": 16,
                                  "y": 16,
                                  "date": "Sept 26, 2017"
                                },
                                {
                                  "x": 17,
                                  "y": 8,
                                  "date": "Sept 27, 2017"
                                },
                                {
                                  "x": 18,
                                  "y": 9,
                                  "date": "Oct 12, 2017"
                                },
                                {
                                  "x": 19,
                                  "y": 10,
                                  "date": "Oct 13, 2017"
                                },
                                {
                                  "x": 19,
                                  "y": 12,
                                  "date": "Oct 14, 2017"
                                },
                                {
                                  "x": 20,
                                  "y": 18,
                                  "date": "Oct 15, 2017"
                                },
                                {
                                  "x": 21,
                                  "y": 15,
                                  "date": "Oct 16, 2017"
                                }
                              ],
                            "keyColor": "#12939a",
                            "bannerValue": "$9,672.24",
                            "title": "Expenses"
                          }
                       ]
                    }
                  }
                ]
      }
    }
    '''
def jsonString = '''
    {
        "action":"addChatNotesIntegration",
        "componentType": "ChatNote",
        "header": "Updated Header",
        "payload": [{
          "component": "ChatNote",
          "title": "Chat Note B",
          "actionProcess": {
            "actionName": "edit-chat-note-B",
            "actionArguments":{
                "section": "image",
                "testVar": "some variable"},
            "actionMessage": "Edit the section"},
          "subcomponents": [''' + largeTimelineLargeMetric + ''']
    }]}
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Small Timeline Graph with Time Selector
> [!warning]  
>
> Small timeline and pie graphs in the chat notes area must appear in pairs. For example, while one small pie chart cannot display in the chat notes area, a small pie chart and a small timeline can display.
>
> When a single small pie chart is sent to the custom user interface, the error message, "Looks like you are missing a component in your graph group. It should be exactly two of them, not less or more," appears in the chat note.

For details to create a small timeline in a chat note, please use the [Small Pie Graph in Chat Notes](Pie-Graphs_23396833.html#PieGraphs-SmallPieTimeline) instructions.
