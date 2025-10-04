{% version "3.x" %}
This demonstration creates a pie graph of data stored in a Script task and sent as a JSON string for display by Amelia.
![](attachments/11939964/11939966.png)
Figure. doPieGraph BPN
# Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doPieGraph. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Pie Graph

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say this is a large pie graph in chat | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | creates large timeline | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | send the integration message jsonString | Sends the variable jsonString to Amelia's interface for display of interactive calendar |
| 4 | say that was a pie graph |  |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
# A Script to Create a pie graph
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
import groovy.json.JsonOutput
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
execution.setVariable("jsonString", jsonString)
```
# Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doPieGraph workflow by typing this command in the chat interface:
    ``` groovy
    run the workflow doPieGraph
    ```
3.  Amelia displays a pie graph above the input area.  
    ![](attachments/11939964/11939965.png)  
    Figure. Output of doPieGraph BPN  
4.  Amelia displays the the last Say task in the BPN.
{% /version %}
