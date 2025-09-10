-   [Chat Log Tables](#TableCharts-ChatLogTables)
    -   [Basic Version](#TableCharts-BasicVersion)
    -   [Popup Version](#TableCharts-PopupVersion)
-   [Chat Notes Table](#TableCharts-ChatNotesTable)
> [!info]  
>
> Table charts can appear in either the chat log or a chat note.

Table charts can be displayed in Amelia's conversation in the custom user interface. Data is sent with an integration message from a BPN Script task to the interface.
# Chat Log Tables
Two possible types of table charts can be displayed in the chat log area. The basic table displays data with the ability to sort by table heading. The popup table displays a portion of the table in the chat log. When the table is clicked, a popup displays the full table
## Basic Version
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a large single series graph. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396837/23396902.png)
Figure. Simple Example to Display a Basic Table Chart in the Chat Log Area
Running the simple BPN with the code below will display a table chart in the chat notes area, on the right side of the screen.
![](attachments/23396837/23396905.png)
Figure. Output of a Simple BPN to Display a Basic Table Chart in the Chat Log Area
A BPN Script task will display a basic chart in the chat log area with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Chat Log Table - Basic** Expand source
``` groovy
def jsonString = '''
{
    "action": "addChatMessage",
    "payload": {
        "componentType": "MessageIntegration",
        "subComponentType": "TableGraph",
        "src": {
            "title": "Account Balance",
            "columns": ["month", "income", "spending", "saving"],
            "rows": [
                [{
                    "name": "Mar",
                    "value": "03"
                }, {
                    "name": "$5,423",
                    "value": "5423"
                }, {
                    "name": "$489",
                    "value": "489"
                }, {
                    "name": "$932",
                    "value": "932"
                }],
                [{
                    "name": "Feb",
                    "value": "02"
                }, {
                    "name": "$3,123",
                    "value": "3123"
                }, {
                    "name": "$889",
                    "value": "889"
                }, {
                    "name": "$402",
                    "value": "402"
                }],
                [{
                    "name": "Apr",
                    "value": "04"
                }, {
                    "name": "$6,423",
                    "value": "6423"
                }, {
                    "name": "$789",
                    "value": "789"
                }, {
                    "name": "$32",
                    "value": "32"
                }],
                [{
                    "name": "May",
                    "value": "05"
                }, {
                    "name": "$6,423",
                    "value": "6423"
                }, {
                    "name": "$789",
                    "value": "789"
                }, {
                    "name": "$902",
                    "value": "902"
                }],
                [{
                    "name": "Jun",
                    "value": "06"
                }, {
                    "name": "$6,423",
                    "value": "6423"
                }, {
                    "name": "$789",
                    "value": "789"
                }, {
                    "name": "$902",
                    "value": "902"
                }]
            ]
        }
    }
}
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Popup Version
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a table in the chat log area that displays the full chart in a popup when clicked. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396837/23396901.png)
Figure. Simple BPN to Display a Popup Table Chart in the Chat Log Area
Running the simple BPN with the code below will display a popup table chart in the chat log.
![](attachments/23396837/23396908.png)
Figure. Output of a Simple BPN to Display a Popup Table Chart in the Chat Log Area
A BPN Script task will display a pre-populated popup table with this example code. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Chat Log Table - Popup** Expand source
``` groovy
def jsonString = '''
{
    "action": "addChatMessage",
    "payload": {
        "componentType": "MessageIntegration",
        "subComponentType": "TableData",
        "title": "Account Balance",
        "descr": "Access all awards in this handy table with links.",
        "rows": [
            [
                "Above & Beyond",
                "Recognizes co-workers for demonstrating clinic values"
            ],
            [
                "Anniversary List",
                "Years of service at 5-year increments<br/><a href='https://www.wikipedia.org/'>Monthly List</a>"
            ],
            [
                "Argent Society",
                "Recognition of allied health status service<br/><a href='#'>Argent Society - RST</a><br/><a href='#'>Argent Society - ARZ, FLA</a>"
            ],
            [
                "Associate Appointment",
                "Recognizes individuals , not consulting or adminstrative staff who contribute on a continuing basis in unusually important ways to the practice, research and educational activities<br/><a href='#'>Info/Nominate</a>"
            ],
            [
                "E-cards",
                "Recognizes co-workers with an electronic greeting card<br/><a href='#'>E-cards</a>"
            ],
            [
                "Excellence Awards",
                "Mayo clinic fosters recognition of its staff through the Awards for Excellence program. Award recipients are dedicated individuals who exemplify the values of excellence for which Mayo is known<br/><a href='#'>Info/Nominate</a><br/><a href='#'>Recipients 2017</a><br/><a href='#'>Recipients 2016</a>"
            ],
            [
                "Manager Recognition Tools",
                "Manager guide to employee recognition<br/><a href='#'>Giving Employee Recognition</a>"
            ],
            [
                "Recognition Events",
                "Special events held throughout the year to show appreciation to Mayo employees, volunteers, students and retirees<br/><a href='#'>Event Info</a>"
            ],
            [
                "Recognition / Hospitality Funds",
                "Institutional funds for each department to be used for expenses associated with recognition of individual or team performance, group hospitality and social activities<br/><a href='#'>Funds Info</a>"
            ],
            [
                "Retirements",
                "Recognizes retiring employees meeting Mayo Clinic’s criteria of age and continuous years of service in a benefit eligible position<br/><a href='#'>Reception Planning List</a><br/><a href='#'>Monthly YTD List</a>"
            ],
            [
                "Years of Service Recognition - Allied Health Staff",
                "Recognizes employees for years of service at 5 year intervals, beginning with completion of 5 years of service.<br/><a href='#'>Info</a><br/><a href='#'>Award Redemption</a>"
            ]
        ]
    }
}
    '''
messageService.sendIntegrationMessage(jsonString)
```
# Chat Notes Table
The code example below can be dropped into a Script task in a simple BPN to demonstrate how to display a basic table in a chat note. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/23396837/23396900.png)
Figure. Simple BPN Example to Display a Table Chart in a Chat Note
Running the simple BPN with the code below will display a basic table in the chat notes area, on the right side of the screen.
![](attachments/23396837/23396907.png)
Figure. Output of a Simple BPN to Display a Table Chart in a Chat Note
A BPN Script task will display a pre-populated table with this example code. Note this code defines the subcomponent as a single variable called within the jsonString variable at the bottom of the example. Toggle the Expand Source link to view code.
> [!info]  
>
> Refer to [Code Structure for Graphs](Graphs_20809637.html#Graphs-CodeStructure) for details about common JSON name:value pair definitions used in the code examples below. Many of these definitions also are easy to understand by reading the code. 

**Chat Notes Table** Expand source
``` groovy
def tableGraph = '''
{
    "subcomponent": "Markup",
    "markupType": "TableGraph",
    "label": "Table Graph",
    "src": {
        "title": "Account Balance",
        "columns": ["month", "income", "spending", "saving"],
        "rows": [
            [{
                "name": "Mar",
                "value": "03"
            }, {
                "name": "$5,423",
                "value": "5423"
            }, {
                "name": "$489",
                "value": "489"
            }, {
                "name": "$932",
                "value": "932"
            }],
            [{
                "name": "Feb",
                "value": "02"
            }, {
                "name": "$3,123",
                "value": "3123"
            }, {
                "name": "$889",
                "value": "889"
            }, {
                "name": "$402",
                "value": "402"
            }],
            [{
                "name": "Apr",
                "value": "04"
            }, {
                "name": "$6,423",
                "value": "6423"
            }, {
                "name": "$789",
                "value": "789"
            }, {
                "name": "$32",
                "value": "32"
            }],
            [{
                "name": "May",
                "value": "05"
            }, {
                "name": "$6,423",
                "value": "6423"
            }, {
                "name": "$789",
                "value": "789"
            }, {
                "name": "$902",
                "value": "902"
            }],
            [{
                "name": "Jun",
                "value": "06"
            }, {
                "name": "$6,423",
                "value": "6423"
            }, {
                "name": "$789",
                "value": "789"
            }, {
                "name": "$902",
                "value": "902"
            }]
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
        "title": "Chat Note A",
        "actionProcess": {
            "actionName": "edit-chat-note-B",
            "actionArguments": {
                "section": "image",
                "testVar": "some variable"
            },
            "actionMessage": "Edit the section"
        },
        "subcomponents": [''' + tableGraph + ''']
    }]
}
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-8-19_14-47-40.png](attachments/23396837/23396900.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_14-49-1.png](attachments/23396837/23396901.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_14-49-55.png](attachments/23396837/23396902.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_15-16-13.png](attachments/23396837/23396905.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_15-17-22.png](attachments/23396837/23396906.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_15-29-54.png](attachments/23396837/23396907.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_15-44-11.png](attachments/23396837/23396908.png) (image/png)  
