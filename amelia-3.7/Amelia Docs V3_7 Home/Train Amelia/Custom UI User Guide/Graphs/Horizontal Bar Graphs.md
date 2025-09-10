> [!info]  
>
> This graph only displays in the chat note area.

Multimedia content – video, images, documents, links, and data in table format – can be displayed in Amelia's conversation in the custom user interface. Data is sent with an integration message from a BPN Script task to the interface.
The code examples below can be dropped into a Script task in a simple BPN to demonstrate how they work. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/20809652/20809654.png)
Figure. Simple BPN to Display Horizontal Bar Graph in Chat Notes
Running the simple BPN with the code below will display a horizontal bar graph in the chat notes area, on the right side of the screen.
![](attachments/20809652/20809653.png)
Figure. Output of a Simple BPN to Display Horizontal Bar Graph in Chat Notes
A BPN Script task will display a pre-populated horizontal bar graph with this example code. Click the Expand Source link below to toggle display of the example code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Horizontal Bar Chart Code** Expand source
``` groovy
def jsonString = '''
    {
        "action": "addChatNotesIntegration",
        "componentType": "ChatNote",
        "header": "Updated Header",
        "payload": [
        {
           "component": "ChatNote",
           "title": "Small Horizontal Bar Graph",
           "subcomponents": [
           {
               "subcomponent": "Markup",
                "markupType": "TimeSelector",
                "label": "Metric",
                "markupProps": {
                    "hasSmallBarGraph": "true",
                "horizontal": "true",
                "selected": "JUN",
                "dates": [
                    "JUN",
                    "JUL",
                    "AUG"
                ],
                "dateStrings": {},
                "subComponents": [
                    {
                        "graphType": "metrics",
                        "metricComponents": [
                         {
                         "graphType": "metric",
                            "title": "AUG",
                            "keyColor": "#F4B644",
                            "dates": {
                                "JUN": {
                                    "primary": "+$2,880.00",
                                    "secondary": "+45%"
                                }
                            }
                        },
                        {
                            "graphType": "metric",
                            "title": "JUL",
                            "keyColor": "#CEC6BD",
                            "dates": {
                                "JUN": {
                                    "primary": "+$5,220.00",
                                    "secondary": "+10.5%"
                                }
                            }
                        },
                        {
                            "graphType": "metric",
                            "title": "JUN",
                            "keyColor": "#37283F",
                            "dates": {
                                "JUN": {
                                    "primary": "+$1,777.00",
                                    "secondary": "+2.75%"
                                }
                            }
                        }
                        ]},
                    {
                        "graphType": "bar",
                        "orientation": "horizontal",
                        "colors": [
                           "#37283F",
                           "#CEC6BD",
                           "#F4B644"
                        ],
                        "dataPoints": [
                            {
                                    "x": 1777,
                                    "y": "JUN",
                                    "color": 0
                                },
                                {
                                    "x": 5220,
                                    "y": "JUL",
                                    "color": 1
                                },
                                {
                                    "x": 2880,
                                    "y": "AUG",
                                    "color": 2
                                }
                            ]
                    }
                ]
                }
           }]
        }
        ]
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
