{% version "3.x" %}
Pie graphs can be displayed in Amelia's conversation in the custom user interface. Data is sent with an integration message from a BPN Script task to the interface.
# Chat Log
Pie graphs can display in the chat log area, as part of the conversation.
## Large Pie Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large pie graph in the chat log. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
Figure. Simple BPN to Display a Large Pie Graph in the Chat Log
Running the simple BPN with the code below will display large pie graph in the chat log.
Figure. Output of a Simple BPN to Display a Large Pie Graph in the Chat Log
A BPN Script task will display a pre-populated large graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](https://docs.ipsoft.com/display/AmeliaDocsV37/Graphs#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large Pie Graph Code in Chat Log** Expand source
``` groovy
def jsonString = '''
    {
      "action": "addChatMessage",
      "payload": {
        "componentType": "MessageIntegration",
        "subComponentType": "TimeSelector",
        "subComponentProps": {
          "hasPieChart": "true",
          "selected": "MAY",
          "dates": [
            "JAN",
            "FEB",
            "MAR",
            "APR",
            "MAY",
            "JUN"
          ],
          "dateStrings": {},
          "subComponents": [
            { 
                "graphType": "metrics",
                "metricComponents": [
                {
                    "graphType": "metric",
                    "title": "Entertainment",
                    "keyColor": "#3C32BC",
                    "dates": {
                        "JAN": {
                            "primary": "$100",
                            "secondary": "1%"
                        },
                        "FEB": {
                            "primary": "$500",
                            "secondary": "5%"
                        },
                        "MAR": {
                            "primary": "$1700",
                            "secondary": "17%"
                        },
                        "APR": {
                            "primary": "$100",
                            "secondary": "1%"
                        },
                        "MAY": {
                            "primary": "$1400",
                            "secondary": "14%"
                        },
                        "JUN": {
                            "primary": "$300",
                            "secondary": "3%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Groceries",
                    "keyColor": "#FCB027",
                    "dates": {
                        "JAN": {
                            "primary": "$1000",
                            "secondary": "10%"
                        },
                        "FEB": {
                            "primary": "$800",
                            "secondary": "8%"
                        },
                        "MAR": {
                            "primary": "$2300",
                            "secondary": "23%"
                        },
                        "APR": {
                            "primary": "$300",
                            "secondary": "3%"
                        },
                        "MAY": {
                            "primary": "$400",
                            "secondary": "44%"
                        },
                        "JUN": {
                            "primary": "$500",
                            "secondary": "5%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Mortgage",
                    "keyColor": "#5A65FB",
                    "dates": {
                        "JAN": {
                            "primary": "$2000",
                            "secondary": "20%"
                        },
                        "FEB": {
                            "primary": "$1500",
                            "secondary": "15%"
                        },
                        "MAR": {
                            "primary": "$2500",
                            "secondary": "25%"
                        },
                        "APR": {
                            "primary": "$400",
                            "secondary": "4%"
                        },
                        "MAY": {
                            "primary": "$1600",
                            "secondary": "16%"
                        },
                        "JUN": {
                            "primary": "$900",
                            "secondary": "9%"
                        }
                    }
                }]},
            {
              "title": "Spending",
              "dates": {},
              "JAN": {
                "dataPoints": [
                  {
                    "value": 1,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "1%"
                  },
                  {
                    "value": 10,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "10%"
                  },
                  {
                    "value": 20,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "20%"
                  }
                ],
                "primaryValue": "$33,444",
                "title": "Mortgage"
              },
              "FEB": {
                "dataPoints": [
                  {
                    "value": 5,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "5%"
                  },
                  {
                    "value": 8,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "8%"
                  },
                  {
                    "value": 15,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "15%"
                  }
                ],
                "primaryValue": "$33,444",
                "fullCircleValue": "100",
                "title": "Mortgage"
              },
              "MAR": {
                "dataPoints": [
                  {
                    "value": 17,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "17%"
                  },
                  {
                    "value": 23,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "23%"
                  },
                  {
                    "value": 25,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "25%"
                  }
                ],
                "fullCircleValue": "65",
                "primaryValue": "$33,444",
                "title": "Mortgage"
              },
              "APR": {
                "dataPoints": [
                  {
                    "value": 1,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "1%"
                  },
                  {
                    "value": 3,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "3%"
                  },
                  {
                    "value": 4,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "4%"
                  }
                ],
                "fullCircleValue": "10",
                "primaryValue": "$33,444",
                "title": "Mortgage"
              },
              "MAY": {
                "dataPoints": [
                  {
                    "value": 14,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "14%"
                  },
                  {
                    "value": 4,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "4%"
                  },
                  {
                    "value": 16,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "16%"
                  }
                ],
                "primaryValue": "$33,444",
                "fullCircleValue": "50",
                "title": "Mortgage"
              },
              "JUN": {
                "dataPoints": [
                  {
                    "value": 3,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "3%"
                  },
                  {
                    "value": 5,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "5%"
                  },
                  {
                    "value": 9,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "9%"
                  }
                ],
                "fullCircleValue": "20",
                "primaryValue": "$33,444",
                "title": "Mortgage"
              },
              "graphType": "pie",
              "size": "large"
            }
          ]
        }
      }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Small Pie Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a small pie graph in the chat log. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396833/23396972.png)
Figure. Simple BPN to Display a Small Pie Graph in the Chat Log
Running the simple BPN with the code below will display small pie graph in the chat log.
![](attachments/23396833/23396971.png)
Figure. Output of a Simple BPN to Display a Small Pie Graph in the Chat Log
A BPN Script task will display a pre-populated small graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](https://docs.ipsoft.com/display/AmeliaDocsV37/Graphs#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Small Pie Graph Code in Chat Log** Expand source
``` groovy
def jsonString = '''
    {
      "action": "addChatMessage",
      "payload": {
        "componentType": "MessageIntegration",
        "subComponentType": "TimeSelector",
        "subComponentProps": {
          "hasPieChart": "true",
          "selected": "MAY",
          "dates": [
            "APR",
            "MAY",
            "JUN"
          ],
          "dateStrings": {},
          "subComponents": [
            { 
                "graphType": "metrics",
                "metricComponents": [
                {
                    "graphType": "metric",
                    "title": "Entertainment",
                    "keyColor": "#3C32BC",
                    "dates": {
                        "APR": {
                            "primary": "$100",
                            "secondary": "1%"
                        },
                        "MAY": {
                            "primary": "$1400",
                            "secondary": "14%"
                        },
                        "JUN": {
                            "primary": "$300",
                            "secondary": "3%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Groceries",
                    "keyColor": "#FCB027",
                    "dates": {
                        "APR": {
                            "primary": "$300",
                            "secondary": "3%"
                        },
                        "MAY": {
                            "primary": "$400",
                            "secondary": "44%"
                        },
                        "JUN": {
                            "primary": "$500",
                            "secondary": "5%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Mortgage",
                    "keyColor": "#5A65FB",
                    "dates": {
                        "APR": {
                            "primary": "$400",
                            "secondary": "4%"
                        },
                        "MAY": {
                            "primary": "$1600",
                            "secondary": "16%"
                        },
                        "JUN": {
                            "primary": "$900",
                            "secondary": "9%"
                        }
                    }
                }]},
            {
              "title": "Spending",
              "dates": {},
                        "APR": {
                "dataPoints": [
                  {
                    "value": 1,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "1%"
                  },
                  {
                    "value": 3,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "3%"
                  },
                  {
                    "value": 4,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "4%"
                  }
                ],
                "fullCircleValue": "10",
                "primaryValue": "$33,444",
                "title": "Mortgage"
              },
              "MAY": {
                "dataPoints": [
                  {
                    "value": 14,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "14%"
                  },
                  {
                    "value": 4,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "4%"
                  },
                  {
                    "value": 16,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "16%"
                  }
                ],
                "primaryValue": "$33,444",
                "fullCircleValue": "50",
                "title": "Mortgage"
              },
              "JUN": {
                "dataPoints": [
                  {
                    "value": 3,
                    "color": "#3C32BC",
                    "label": "ENTERTAINMENT",
                    "subLabel": "3%"
                  },
                  {
                    "value": 5,
                    "color": "#FCB027",
                    "label": "GROCERIES",
                    "subLabel": "5%"
                  },
                  {
                    "value": 9,
                    "color": "#5A65FB",
                    "label": "MORTGAGE",
                    "subLabel": "9%"
                  }
                ],
                "fullCircleValue": "20",
                "primaryValue": "$33,444",
                "title": "Mortgage"
              },
              "graphType": "pie",
              "size": "small"
            }
          ]
        }
      }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
# Chat Notes
Pie graphs can display in a chat note on the right side of the screen.
## Large Pie Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large pie graph in the chat note area. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396833/23396951.png)
Figure. Simple BPN to Display a Large Pie Graph in a Chat Note
Running the simple BPN with the code below will display large pie graph in the chat notes area, on the right side of the screen.
![](attachments/23396833/23396952.png)
Figure. Output of a Simple BPN to Display a Large and Small Pie Graphs in a Chat Note
A BPN Script task will display a pre-populated large pie graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](https://docs.ipsoft.com/display/AmeliaDocsV37/Graphs#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large and Small Pie Graph Code in Chat Note** Expand source
``` groovy
def jsonString = '''
{
  "action": "addChatMessage",
  "payload": {
    "componentType": "MessageIntegration",
    "subComponentType": "TimeSelector",
    "subComponentProps": {
      "hasPieChart": "true",
      "selected": "MAY",
      "dates": [
        "JAN",
        "FEB",
        "MAR",
        "APR",
        "MAY",
        "JUN"
      ],
      "dateStrings": {},
      "subComponents": [
        {
            "graphType": "metrics",
            "metricComponents": [
            {
                "graphType": "metric",
                "title": "Entertainment",
                "keyColor": "#3C32BC",
                "dates": {
                    "JAN": {
                        "primary": "$100",
                        "secondary": "1%"
                    },
                    "FEB": {
                        "primary": "$500",
                        "secondary": "5%"
                    },
                    "MAR": {
                        "primary": "$1700",
                        "secondary": "17%"
                    },
                    "APR": {
                        "primary": "$100",
                        "secondary": "1%"
                    },
                    "MAY": {
                        "primary": "$1400",
                        "secondary": "14%"
                    },
                    "JUN": {
                        "primary": "$300",
                        "secondary": "3%"
                    }
                }
            },
            {
                "graphType": "metric",
                "title": "Groceries",
                "keyColor": "#FCB027",
                "dates": {
                    "JAN": {
                        "primary": "$1000",
                        "secondary": "10%"
                    },
                    "FEB": {
                        "primary": "$800",
                        "secondary": "8%"
                    },
                    "MAR": {
                        "primary": "$2300",
                        "secondary": "23%"
                    },
                    "APR": {
                        "primary": "$300",
                        "secondary": "3%"
                    },
                    "MAY": {
                        "primary": "$400",
                        "secondary": "44%"
                    },
                    "JUN": {
                        "primary": "$500",
                        "secondary": "5%"
                    }
                }
            },
            {
                "graphType": "metric",
                "title": "Mortgage",
                "keyColor": "#5A65FB",
                "dates": {
                    "JAN": {
                        "primary": "$2000",
                        "secondary": "20%"
                    },
                    "FEB": {
                        "primary": "$1500",
                        "secondary": "15%"
                    },
                    "MAR": {
                        "primary": "$2500",
                        "secondary": "25%"
                    },
                    "APR": {
                        "primary": "$400",
                        "secondary": "4%"
                    },
                    "MAY": {
                        "primary": "$1600",
                        "secondary": "16%"
                    },
                    "JUN": {
                        "primary": "$900",
                        "secondary": "9%"
                    }
                }
            }]},
        {
          "title": "Spending",
          "dates": {},
          "JAN": {
            "dataPoints": [
              {
                "value": 1,
                "color": "#3C32BC",
                "label": "ENTERTAINMENT",
                "subLabel": "1%"
              },
              {
                "value": 10,
                "color": "#FCB027",
                "label": "GROCERIES",
                "subLabel": "10%"
              },
              {
                "value": 20,
                "color": "#5A65FB",
                "label": "MORTGAGE",
                "subLabel": "20%"
              }
            ],
            "primaryValue": "$33,444",
            "title": "Mortgage"
          },
          "FEB": {
            "dataPoints": [
              {
                "value": 5,
                "color": "#3C32BC",
                "label": "ENTERTAINMENT",
                "subLabel": "5%"
              },
              {
                "value": 8,
                "color": "#FCB027",
                "label": "GROCERIES",
                "subLabel": "8%"
              },
              {
                "value": 15,
                "color": "#5A65FB",
                "label": "MORTGAGE",
                "subLabel": "15%"
              }
            ],
            "primaryValue": "$33,444",
            "fullCircleValue": "100",
            "title": "Mortgage"
          },
          "MAR": {
            "dataPoints": [
              {
                "value": 17,
                "color": "#3C32BC",
                "label": "ENTERTAINMENT",
                "subLabel": "17%"
              },
              {
                "value": 23,
                "color": "#FCB027",
                "label": "GROCERIES",
                "subLabel": "23%"
              },
              {
                "value": 25,
                "color": "#5A65FB",
                "label": "MORTGAGE",
                "subLabel": "25%"
              }
            ],
            "fullCircleValue": "65",
            "primaryValue": "$33,444",
            "title": "Mortgage"
          },
          "APR": {
            "dataPoints": [
              {
                "value": 1,
                "color": "#3C32BC",
                "label": "ENTERTAINMENT",
                "subLabel": "1%"
              },
              {
                "value": 3,
                "color": "#FCB027",
                "label": "GROCERIES",
                "subLabel": "3%"
              },
              {
                "value": 4,
                "color": "#5A65FB",
                "label": "MORTGAGE",
                "subLabel": "4%"
              }
            ],
            "fullCircleValue": "10",
            "primaryValue": "$33,444",
            "title": "Mortgage"
          },
          "MAY": {
            "dataPoints": [
              {
                "value": 14,
                "color": "#3C32BC",
                "label": "ENTERTAINMENT",
                "subLabel": "14%"
              },
              {
                "value": 4,
                "color": "#FCB027",
                "label": "GROCERIES",
                "subLabel": "4%"
              },
              {
                "value": 16,
                "color": "#5A65FB",
                "label": "MORTGAGE",
                "subLabel": "16%"
              }
            ],
            "primaryValue": "$33,444",
            "fullCircleValue": "50",
            "title": "Mortgage"
          },
          "JUN": {
            "dataPoints": [
              {
                "value": 3,
                "color": "#3C32BC",
                "label": "ENTERTAINMENT",
                "subLabel": "3%"
              },
              {
                "value": 5,
                "color": "#FCB027",
                "label": "GROCERIES",
                "subLabel": "5%"
              },
              {
                "value": 9,
                "color": "#5A65FB",
                "label": "MORTGAGE",
                "subLabel": "9%"
              }
            ],
            "fullCircleValue": "20",
            "primaryValue": "$33,444",
            "title": "Mortgage"
          },
          "graphType": "pie",
          "size": "large"
        }
      ]
    }
  }
}
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Small Pie Graph with Legend
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a small pie graph with a legend. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396833/23396979.png)
Figure. Simple BPN to Display a Small Pie Graph with a Legend in a Chat Note
Running the simple BPN with the code below will display a small pie graph with a legend in the chat notes area, on the right side of the screen.
![](attachments/23396833/23396980.png)
Figure. Output of a Simple BPN to Display a Small Pie Graph with a Legend in a Chat Note
A BPN Script task will display a pre-populated small pie graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](https://docs.ipsoft.com/display/AmeliaDocsV37/Graphs#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Small Pie Graph Code** Expand source
``` groovy
def smallPieGraph = '''
    {
      "subcomponent": "Markup",
      "markupType": "TimeSelector",
      "label": "Tiny Pie with Time Selector",
      "markupProps": {
        "selected": "APR",
        "hasPieChart": "true",
        "label": "Some total",
        "dates": [
          "APR"
        ],
        "dateStrings": {},
        "subComponents": [
                { 
                "graphType": "metrics",
                "label": "Some total",
                "metricComponents": [
                {
                    "graphType": "metric",
                    "title": "Entertainment",
                    "keyColor": "#3a2741",
                    "dates": {
                        "APR": {
                            "primary": "$100",
                            "secondary": "1%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Groceries",
                    "keyColor": "#ffb317",
                    "dates": {
                        "APR": {
                            "primary": "$300",
                            "secondary": "3%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Preferred Gold Premium",
                    "keyColor": "#e57a96",
                    "dates": {
                        "APR": {
                            "primary": "$400",
                            "secondary": "4%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Platinum Exclusive",
                    "keyColor": "#c9c9c9",
                    "dates": {
                        "APR": {
                            "primary": "$600",
                            "secondary": "6%"
                        }
                    }
                },
                {
                    "graphType": "metric",
                    "title": "Auto",
                    "keyColor": "#1b5176",
                    "dates": {
                        "APR": {
                            "primary": "$400",
                            "secondary": "4%"
                        }
                    }
                }
            ]},
          {
            "title": "Spending",
            "dates": {},
            "dataPoints": [
              {
                "value": 1,
                "color": "#3a2741",
                "label": "ENTERTAINMENT",
                "subLabel": "1%"
              },
              {
                "value": 3,
                "color": "#ffb317",
                "label": "GROCERIES",
                "subLabel": "3%"
              },
              {
                "value": 4,
                "color": "#e57a96",
                "label": "MORTGAGE",
                "subLabel": "4%"
              },
              {
                "value": 5,
                "color": "#c9c9c9",
                "label": "LEISURE",
                "subLabel": "6%"
              },
              {
                "value": 6,
                "color": "#1b5176",
                "label": "AUTO",
                "subLabel": "4%"
              }
          ],
            "primaryValue": "$1,222",
            "label": "Some total",
            "title": "Mortgage",
            "radius": "1",
            "fullCircleValue": "10",
            "primaryValue": "$33,444",
            "graphType": "pie",
            "size": "side"
          }
        ]
      }
    }
    '''
def jsonString = '''
    {
        "action": "addChatNotesIntegration",
        "componentType": "ChatNote",
        "header": "Updated Header",
        "payload": [{
            "component": "ChatNote",
            "title": "Chat Note C",
            "actionProcess": {
                "actionName": "edit-chat-note-B",
                "actionArguments": {
                    "section": "image",
                    "testVar": "some variable"
                },
                "actionMessage": "Edit the section"
            },
            "subcomponents": [''' + smallPieGraph + ''']
        }]
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Small Pie Graph
> [!warning]  
>
> Small pie graphs in the chat notes area must appear in pairs. For example, while one small pie chart cannot display in the chat notes area, a small pie chart and a small timeline can display.
>
> When a single small pie chart is sent to the custom user interface, the error message, "Looks like you are missing a component in your graph group. It should be exactly two of them, not less or more," appears in the chat note.

The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a small pie graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396833/23396977.png)
Figure. Simple BPN to Display a Small Pie Graph and Timeline Graph in a Chat Note
Running the simple BPN with the code below will display a small pie graph and timeline graph in the chat notes area, on the right side of the screen.
![](attachments/23396833/23396982.png)
Figure. Output of a Simple BPN to Display a Small Pie Graph and Timeline Graph in a Chat Note
A BPN Script task will display a pre-populated small pie graph and timeline graph with this example code. Note graphType identifies the definitions for the timeline and pie graphs. In addition, markupProps identifies the start of each definition. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](https://docs.ipsoft.com/display/AmeliaDocsV37/Graphs#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Side Pie Graph Code** Expand source
``` groovy
def smallTimelineMetric = '''
    {
        "subcomponent": "Markup",
        "markupType": "TimeSelectorGroup",
        "label": "Small Timeline & Small Pie",
        "subComponents": [
            {
                "markupProps": {
                    "selected": "1M",
                    "dates": [
                        "1W",
                        "1M",
                        "6M"
                    ],
                    "dateStrings": {
                        "1W": "PAST WEEK",
                        "1M": "PAST MO",
                        "6M": "PAST 6MOS"
                    },
                    "subComponents": [
                        {
                            "dates": {
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
                                }
                            },
                            "graphType": "timeline",
                            "size": "small",
                            "1W": {
                                "sections": [{
                        "dataPoints": [{
                                "x": 5,
                                "y": 12
                            },
                            {
                                "x": 6,
                                "y": 3
                            }
                        ],
                        "lineColor": "blue",
                        "bannerValue": "$19,020.22",
                        "title": "Account Balance"
                    }]
                            },
                            "1M": {
                    "sections": [{
                        "dataPoints": [{
                                "x": 3,
                                "y": 15
                            },
                            {
                                "x": 4,
                                "y": 11
                            },
                            {
                                "x": 5,
                                "y": 12
                            },
                            {
                                "x": 6,
                                "y": 3
                            }
                        ],
                        "lineColor": "blue",
                        "bannerValue": "$11,020.22",
                        "title": "Account Balance"
                    }]
                },
                            "6M": {
                    "sections": [{
                        "dataPoints": [{
                                "x": 1,
                                "y": 10
                            },
                            {
                                "x": 2,
                                "y": 5
                            },
                            {
                                "x": 3,
                                "y": 15
                            },
                            {
                                "x": 4,
                                "y": 11
                            },
                            {
                                "x": 5,
                                "y": 12
                            },
                            {
                                "x": 6,
                                "y": 13
                            },
                            {
                                "x": 7,
                                "y": 4
                            },
                            {
                                "x": 8,
                                "y": 5
                            },
                            {
                                "x": 9,
                                "y": 7
                            },
                            {
                                "x": 10,
                                "y": 2
                            },
                            {
                                "x": 11,
                                "y": 1
                            }
                        ],
                        "lineColor": "blue",
                        "bannerValue": "$18,888.22",
                        "title": "Account Balance"
                    }]
                }
                        }
                    ]
                }
            },
            {
                "markupProps": {
                    "selected": "MAY",
                    "hasPieChart": "true",
                    "dates": [
                        "APR",
                        "MAY",
                        "JUN"
                    ],
                    "dateStrings": {},
                    "subComponents": [
                        {
                            "graphType": "metrics",
                            "metricComponents": [
                            {
                                "graphType": "metric",
                                "title": "Entertainment",
                                "keyColor": "#3C32BC",
                                "dates": {
                                    "APR": {
                                        "primary": "1%",
                                        "secondary": "1%"
                                    },
                                    "MAY": {
                                        "primary": "14%",
                                        "secondary": "14%"
                                    },
                                    "JUN": {
                                        "primary": "3%",
                                        "secondary": "3%"
                                    }
                                }
                            },
                            {
                                "graphType": "metric",
                                "title": "Groceries",
                                "keyColor": "#FCB027",
                                "dates": {
                                    "APR": {
                                        "primary": "3%",
                                        "secondary": "3%"
                                    },
                                    "MAY": {
                                        "primary": "4%",
                                        "secondary": "44%"
                                    },
                                    "JUN": {
                                        "primary": "5%",
                                        "secondary": "5%"
                                    }
                                }
                            },
                            {
                                "graphType": "metric",
                                "title": "Mortgage",
                                "keyColor": "#5A65FB",
                                "dates": {
                                    "APR": {
                                        "primary": "4%",
                                        "secondary": "4%"
                                    },
                                    "MAY": {
                                        "primary": "16%",
                                        "secondary": "16%"
                                    },
                                    "JUN": {
                                        "primary": "9%",
                                        "secondary": "9%"
                                    }
                                }
                            }
                ]
            },
                        {
                        "title": "Spending",
                        "dates": {},
                        "APR": {
                          "dataPoints": [
                            {
                                "value": 1,
                                "color": "#3C32BC",
                                "label": "ENTERTAINMENT",
                                "subLabel": "1%"
                            },
                            {
                                "value": 3,
                                "color": "#FCB027",
                                "label": "GROCERIES",
                                "subLabel": "3%"
                            },
                            {
                                "value": 4,
                                "color": "#5A65FB",
                                "label": "MORTGAGE",
                                "subLabel": "4%"
                            }
                          ],
                          "fullCircleValue": "10",
                          "primaryValue": "$1,222",
                          "title": "Mortgage"
                        },
                        "MAY": {
                          "dataPoints": [
                            {
                                "value": 14,
                                "color": "#3C32BC",
                                "label": "ENTERTAINMENT",
                                "subLabel": "14%"
                            },
                            {
                                "value": 4,
                                "color": "#FCB027",
                                "label": "GROCERIES",
                                "subLabel": "4%"
                            },
                            {
                                "value": 16,
                                "color": "#5A65FB",
                                "label": "MORTGAGE",
                                "subLabel": "16%"
                            }
                          ],
                          "primaryValue": "$1,222",
                          "fullCircleValue": "50",
                          "title": "Mortgage"
                        },
                        "JUN": {
                          "dataPoints": [
                            {
                                "value": 3,
                                "color": "#3C32BC",
                                "label": "ENTERTAINMENT",
                                "subLabel": "3%"
                            },
                            {
                                "value": 5,
                                "color": "#FCB027",
                                "label": "GROCERIES",
                                "subLabel": "5%"
                            },
                            {
                                "value": 9,
                                "color": "#5A65FB",
                                "label": "MORTGAGE",
                                "subLabel": "9%"
                            }
                          ],
                          "primaryValue": "$1,222",
                          "fullCircleValue": "20",
                          "title": "Mortgage"
                        },
                        "graphType": "pie",
                        "size": "small"
                      }
                    ]
                }
            }]
    }
    '''
def jsonString = 
'''
{
    "action":"addChatNotesIntegration",
    "componentType": "ChatNote",
    "header": "Updated Header",
    "payload": [{
      "component": "ChatNote",
      "title": "Chat Note 1",
      "actionProcess": {
        "actionName": "edit-chat-note-B",
        "actionArguments":{
            "section": "image",
            "testVar": "some variable"},
        "actionMessage": "Edit the section"},
      "subcomponents": [''' + smallTimelineMetric +  ''']
  }]}
'''
messageService.sendIntegrationMessage(jsonString)
```
{% /version %}
