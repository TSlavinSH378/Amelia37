Vertical bar graphs can be displayed in Amelia's conversation in the custom user interface. Data is sent with an integration message from a BPN Script task to the interface.
# Chat Log
Single series and multiple series vertical bar graphs can display in the chat log conversation area, as part of the conversation.
## Large Single Series Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large single series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/20809656/23396517.png)
Figure. Simple BPN to Display a Single Series Vertical Bar Graph in the Chat Log
Running the simple BPN with the code below will display a vertical bar graph in the chat notes area, on the right side of the screen.
![](attachments/20809656/23396518.png)
Figure. Output of a Simple BPN to Display a Single Series Vertical Bar Graph in the Chat Log
A BPN Script task will display a pre-populated graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Single Series Vertical Bar Graph Code** Expand source
``` groovy
def jsonString = '''
    {
        "action": "addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "TimeSelector",
            "subComponentProps": {
                "hasLargeBarGraph": "true",
                "vertical": "true",
                "selected": "JUN",
                "dates": [
                    "JUN",
                    "JUL",
                    "AUG",
                    "SEP",
                    "OCT",
                    "NOV"
                ],
                "dateStrings": {},
                "subComponents": [
                    {
                        "graphType": "metric",
                        "title": "Account Balance",
                        "bannerValue": "$19,020.22",
                        "timePeriod": "PAST MO",
                        "dates": {
                                "JUN": {
                                    "balance": "$4,777.00",
                                    "primary": "$+1,777.00",
                                    "secondary": "+2.75%"
                                },
                                "JUL": {
                                    "balance": "$9,990.00",
                                    "primary": "$+5,220.00",
                                    "secondary": "+10.5%"
                                },
                                "AUG": {
                                    "balance": "$12,870.00",
                                    "primary": "$+2,880.00",
                                    "secondary": "+45%"
                                },
                                "SEP": {
                                    "balance": "$10,870.00",
                                    "primary": "$-2,000.00",
                                    "secondary": "+32%"
                                },
                                "OCT": {
                                    "balance": "$11,890.00",
                                    "primary": "$+1,020.00",
                                    "secondary": "-23%"
                                },
                                "NOV": {
                                    "balance": "$12,610.00",
                                    "primary": "$+720.22",
                                    "secondary": "25%"
                                }
                            }
                    },
                    {
                        "graphType": "bar",
                        "dataPoints": [
                            [{
                                    "x": "JUN",
                                    "y": 1777,
                                    "color": "#5764FC"
                                },
                                {
                                    "x": "JUL",
                                    "y": 5220
                                },
                                {
                                    "x": "AUG",
                                    "y": 2880
                                },
                                {
                                    "x": "SEP",
                                    "y": 2000
                                },
                                {
                                    "x": "OCT",
                                    "y": 1020
                                },
                                {
                                    "x": "NOV",
                                    "y": 720
                                }
                            ]
                        ]
                    }
                ]
            }
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Large Multiple Series Graph
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large multiple series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/20809656/23396932.png)
Figure. Simple BPN to Display a Multiple Series Vertical Bar Graph in the Chat Log
Running the simple BPN with the code below will display a vertical bar graph in the chat notes area, on the right side of the screen.
![](attachments/20809656/20809657.png)
Figure. Output of a Simple BPN to Display a Multiple Series Vertical Bar Graph in the Chat Log
A BPN Script task will display a pre-populated graph with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Multiple Series Vertical Bar Graph Code** Expand source
``` groovy
def jsonString = '''
    {
        "action": "addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "TimeSelector",
            "subComponentProps": {
                "hasLargeBarGraph": "true",
                "vertical": "true",
                "selected": "JUN",
                "dates": [
                    "JUN",
                    "JUL",
                    "AUG",
                    "SEP",
                    "OCT",
                    "NOV"
                ],
                "dateStrings": {},
                "subComponents": [
                    {
                        "graphType": "metrics",
                        "metricComponents": [
                        {
                            "graphType": "metric",
                            "title": "Income",
                            "keyColor": "#5764FC",
                            "dates": {
                                "JUN": {
                                    "primary": "+$1,777.00",
                                    "secondary": "+2.75%"
                                },
                                "JUL": {
                                    "primary": "+$5,220.00",
                                    "secondary": "+10.5%"
                                },
                                "AUG": {
                                    "primary": "+$2,880.00",
                                    "secondary": "+45%"
                                },
                                "SEP": {
                                    "primary": "$2,000.00",
                                    "secondary": "+32%"
                                },
                                "OCT": {
                                    "primary": "-$1,020.00",
                                    "secondary": "-23%"
                                },
                                "NOV": {
                                    "primary": "$720.22",
                                    "secondary": "25%"
                                }
                            }
                        },
                        {
                            "graphType": "metric",
                            "title": "Spending",
                            "keyColor": "#392BBB",
                            "dates": {
                                "JUN": {
                                    "primary": "$627.00",
                                    "secondary": "-1.0%"
                                },
                                "JUL": {
                                    "primary": "-$2,008.00",
                                    "secondary": "-4.75%"
                                },
                                "AUG": {
                                    "primary": "-$14,258.00",
                                    "secondary": "-24.45%"
                                },
                                "SEP": {
                                    "primary": "+$1,002.25",
                                    "secondary": "12.2%"
                                },
                                "OCT": {
                                    "primary": "+$72.00",
                                    "secondary": "1%"
                                },
                                "NOV": {
                                    "primary": "+$333",
                                    "secondary": "8%"
                                }
                            }
                        },
                        {
                            "graphType": "metric",
                            "title": "Savings",
                            "keyColor": "#FEB42E",
                            "dates": {
                                "JUN": {
                                    "primary": "-$627.00",
                                    "secondary": "-1.0%"
                                },
                                "JUL": {
                                    "primary": "-$2,008.00",
                                    "secondary": "-4.75%"
                                },
                                "AUG": {
                                    "primary": "-$4,258.00",
                                    "secondary": "-24.45%"
                                },
                                "SEP": {
                                    "primary": "+$4,000.00",
                                    "secondary": "14%"
                                },
                                "OCT": {
                                    "primary": "+$2,543.12",
                                    "secondary": "4%"
                                },
                                "NOV": {
                                    "primary": "+$1,700.52",
                                    "secondary": "3.2%"
                                }
                            }
                        }
                    ]},
                    {
                        "graphType": "bar",
                        "dataPoints": [
                            [{
                                    "x": "JUN",
                                    "y": 1777,
                                    "color": "#5764FC"
                                },
                                {
                                    "x": "JUL",
                                    "y": 5220
                                },
                                {
                                    "x": "AUG",
                                    "y": 2880
                                },
                                {
                                    "x": "SEP",
                                    "y": 2000
                                },
                                {
                                    "x": "OCT",
                                    "y": 1020
                                },
                                {
                                    "x": "NOV",
                                    "y": 720
                                }
                            ],
                            [{
                                    "x": "JUN",
                                    "y": 627,
                                    "color": "#3B2CB7"
                                },
                                {
                                    "x": "JUL",
                                    "y": 2008
                                },
                                {
                                    "x": "AUG",
                                    "y": 1258
                                },
                                {
                                    "x": "SEP",
                                    "y": 1002
                                },
                                {
                                    "x": "OCT",
                                    "y": 720
                                },
                                {
                                    "x": "NOV",
                                    "y": 333
                                }
                            ],
                            [{
                                    "x": "JUN",
                                    "y": 627,
                                    "color": "#FEB52B"
                                },
                                {
                                    "x": "JUL",
                                    "y": 2008
                                },
                                {
                                    "x": "AUG",
                                    "y": 1258
                                },
                                {
                                    "x": "SEP",
                                    "y": 4000
                                },
                                {
                                    "x": "OCT",
                                    "y": 2543
                                },
                                {
                                    "x": "NOV",
                                    "y": 1700
                                }
                            ]
                        ]
                    }
                ]
            }
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
# Chat Notes
Single series and multiple series vertical bar graphs can display in the chat note area on the right side next to the conversation area.
## Large Vertical Bar Graphs
The code examples below can be dropped into a Script task in a simple BPN to demonstrate how they work. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/20809656/23396545.png)
Figure. Simple BPN to Display Large Vertical Bar Graph in Chat Notes
Running the simple BPN with the code below will display a large vertical bar graph in the chat notes area, on the right side of the screen.
![](attachments/20809656/23396544.png)
Figure. Output of a Simple BPN to Display Large Vertical Bar Graph in Chat Notes
A BPN Script task will display a pre-populated graph with this example code. Note it displays two notes, one with a large vertical bar graph and a second note with a small vertical bar graph, each defined with a component name and a subcomponent object definition. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Large Vertical Bar Graph Code for Chat Note** Expand source
``` groovy
def jsonString = '''
    {
        "action": "addChatNotesIntegration",
        "componentType": "ChatNote",
        "header": "Updated Header",
        "payload": [
        {
           "component": "ChatNote",
           "title": "Small Vertical Bar Graph",
           "subcomponents": [
           {
               "subcomponent": "Markup",
                "markupType": "TimeSelector",
                "label": "Metric",
                "markupProps": {
                    "hasSmallBarGraph": "true",
                    "selected": "JUN",
                    "vertical": "true",
                    "dates": [
                        "JUN",
                        "JUL",
                        "AUG"
                    ],
                    "dateStrings": {},
                    "subComponents": [
                        {
                            "graphType": "metrics",
                            "size": "small",
                            "metricComponents": [
                            {
                                "graphType": "metric",
                                "title": "Income",
                                "dates": {
                                    "JUN": {
                                        "primary": "+$1,777.00",
                                        "secondary": "+2.75%"
                                    },
                                    "JUL": {
                                        "primary": "+$5,220.00",
                                        "secondary": "+10.5%"
                                    },
                                    "AUG": {
                                        "primary": "+$2,880.00",
                                        "secondary": "+45%"
                                    }
                                }
                            }
                            ]},
                        {
                            "graphType": "bar",
                            "dataPoints": [
                                [{
                                        "x": "JUN",
                                        "y": 1777,
                                        "color": "#5764FC"
                                    },
                                    {
                                        "x": "JUL",
                                        "y": 5220
                                    },
                                    {
                                        "x": "AUG",
                                        "y": 2880
                                    }
                                ]]
                        }
                    ]
                }
           }]
        }]
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Small Vertical Bar Graphs
The code examples below can be dropped into a Script task in a simple BPN to demonstrate how they work. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/20809656/23396940.png)
Figure. Simple BPN to Display Small Vertical Bar Graph in Chat Notes
Running the simple BPN with the code below will display a small vertical bar graph in the chat notes area, on the right side of the screen.
![](attachments/20809656/23396939.png)
Figure. Output of a Simple BPN to Display Small Vertical Bar Graph in Chat Notes
A BPN Script task will display a pre-populated graph with this example code. Toggle the Expand Source link to display code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Small Vertical Bar Graph Code** Expand source
``` groovy
def jsonString = '''
    {
        "action": "addChatNotesIntegration",
        "componentType": "ChatNote",
        "header": "Updated Header",
        "payload": [
        {
           "component": "ChatNote",
           "title": "Small Vertical Bar Graph",
           "subcomponents": [
           {
               "subcomponent": "Markup",
                "markupType": "TimeSelector",
                "label": "Metric",
                "markupProps": {
                    "hasSmallBarGraph": "true",
                    "selected": "JUN",
                    "vertical": "true",
                    "dates": [
                        "JUN",
                        "JUL",
                        "AUG"
                    ],
                    "dateStrings": {},
                    "subComponents": [
                        {
                            "graphType": "metrics",
                            "size": "small",
                            "metricComponents": [
                            {
                                "graphType": "metric",
                                "title": "Income",
                                "dates": {
                                    "JUN": {
                                        "primary": "+$1,777.00",
                                        "secondary": "+2.75%"
                                    },
                                    "JUL": {
                                        "primary": "+$5,220.00",
                                        "secondary": "+10.5%"
                                    },
                                    "AUG": {
                                        "primary": "+$2,880.00",
                                        "secondary": "+45%"
                                    }
                                }
                            }
                            ]},
                        {
                            "graphType": "bar",
                            "dataPoints": [
                                [{
                                        "x": "JUN",
                                        "y": 1777,
                                        "color": "#5764FC"
                                    },
                                    {
                                        "x": "JUL",
                                        "y": 5220
                                    },
                                    {
                                        "x": "AUG",
                                        "y": 2880
                                    }
                                ]]
                        }
                    ]
                }
           }]
        }]
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-7-30_14-55-22.png](attachments/20809656/20809657.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-30_14-59-4.png](attachments/20809656/20809658.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-30_14-28-44.png](attachments/20809656/20809659.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-30_14-26-8.png](attachments/20809656/20809660.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-7_14-30-6.png](attachments/20809656/23396517.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-7_14-34-10.png](attachments/20809656/23396518.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-8_10-58-20.png](attachments/20809656/23396544.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-8_11-0-20.png](attachments/20809656/23396545.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-20_12-50-2.png](attachments/20809656/23396932.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-20_13-9-47.png](attachments/20809656/23396934.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-20_13-14-26.png](attachments/20809656/23396939.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-20_13-15-36.png](attachments/20809656/23396940.png) (image/png)  
