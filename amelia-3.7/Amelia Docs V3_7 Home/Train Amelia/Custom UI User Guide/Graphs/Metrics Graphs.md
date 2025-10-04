{% version "3.x" %}
Metric graphs can be displayed in Amelia's conversation in the custom user interface. Data is sent with an integration message from a BPN Script task to the interface.
# Chat Log and Chat Notes
Large metric graphs can display in the chat log conversation area, as part of the conversation, or in a chat note on the right side of the screen.
## Large Metric Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large multiple series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396835/23396945.png)
Figure. Simple  BPN to Display a Large Metric Graph in the Chat Log
Running the simple BPN with the code below will display a metrics graph in the chat log area.
![](attachments/23396835/23396944.png)
Figure. Output of a Simple BPN to Display a Large Metric Graph in the Chat Log
A BPN Script task will display a pre-populated metrics graph in the chat log with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](https://docs.ipsoft.com/display/AmeliaDocsV37/Graphs#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large Metric Graph Code** Expand source
``` groovy
def jsonString = '''
    {
        "action": "addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "Metric",
            "subComponentProps": {
                "title": "Account Balance",
                "bannerValue": "$19,020.22",
                "primary": "+2,000",
                "secondary": "10.5%",
                "timePeriod": "PAST MO"
            }
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
# Chat Notes
Large and small metrics graphs can display in the chat note area on the right side next to the conversation area. The example below displays both in one code block.
## Small and Large Metric Graphs
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large multiple series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396835/23396949.png)
Figure. Simple BPN to Display Small and Large Metric Graphs in a Chat Note
Running the simple BPN with the code below will display large and small metrics graphs in the chat notes area, on the right side of the screen.
![](attachments/23396835/23396948.png)
Figure. Output of a Simple BPN to Display Small and Large Metric Graphs in a Chat Note
A BPN Script task will display a pre-populated metrics graphs with this example code. Search the code for Metric, Small Metric, Income, Expense, and other terms displayed in the chat note to see how these elements are defined. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](https://docs.ipsoft.com/display/AmeliaDocsV37/Graphs#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Small Metric Graph Code** Expand source
``` groovy
def jsonString = '''
    {
        "action": "addChatNotesIntegration",
        "componentType": "ChatNote",
        "header": "Angry Bird 1",
        "payload": [{
            "component": "ChatNote",
            "title": "Chat Note A",
            "styles": {
                "labelSize": "subhead",
                "labelWeight": "regular"
            },
            "actionProcess": {
                "actionName": "edit-chat-note",
                "actionLabel": "Update my personal information",
                "actionArguments": {
                    "section": "image",
                    "testVar": "' + testVar + '"
                },
                "actionMessage": "Edit the section"
            },
            "subcomponents": [
                {
                "subcomponent": "Markup",
                "markupType": "TimeSelector",
                "label": "Metric",
                "markupProps":
                    {
                        "selected": "1M",
                        "dates": ["1W", "1M", "6M"],
                        "dateStrings": {
                            "1W": "PAST WEEK",
                            "1M": "PAST MO",
                            "6M": "PAST 6MOS"
                        },
                        "subComponents": [
                            {
                            "graphType": "metric",
                            "title": "Account Balance",
                            "bannerValue": "$19,020.22",
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
                            }
                        }]
                    }
                },
                {
                "subcomponent": "Markup",
                "markupType": "TimeSelectorGroup",
                "label": "Small Metrics",
                "subComponents": [
                    {"markupProps":
                        {
                        "selected": "1M",
                        "dates": ["1W", "1M", "6M"],
                        "dateStrings": {
                            "1W": "PAST WEEK",
                            "1M": "PAST MO",
                            "6M": "PAST 6MOS"
                        },
                        "subComponents": [
                            {
                            "graphType": "metric",
                            "title": "Income",
                            "size": "small",
                            "dates": {
                                "1W": {
                                    "primary": "$1,777.00",
                                    "secondary": "+2.75%"
                                },
                                "1M": {
                                    "primary": "$5,220.00",
                                    "secondary": "+10.5%"
                                },
                                "6M": {
                                    "primary": "$20,880.00",
                                    "secondary": "+45%"
                                    }
                                }
                            }
                        ]
                    }
                    },
                    {
                       "markupProps":
                       {
                        "selected": "1M",
                        "dates": ["1W", "1M", "6M"],
                        "dateStrings": {
                            "1W": "PAST WEEK",
                            "1M": "PAST MO",
                            "6M": "PAST 6MOS"
                        },
                        "subComponents": [
                            {
                            "graphType": "metric",
                            "title": "Expenses",
                            "size": "small",
                            "dates": {
                                "1W": {
                                    "primary": "$627.00",
                                    "secondary": "-1.0%"
                                },
                                "1M": {
                                    "primary": "$2,008.00",
                                    "secondary": "-4.75%"
                                },
                                "6M": {
                                    "primary": "$14,258.00",
                                    "secondary": "-24.45%"
                                    }
                                }
                            }
                        ]
                    }
                }]
                }
            ]
        }]
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
{% /version %}
