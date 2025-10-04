{% version "3.x" %}
This demonstration shows how to use a BPN and custom UI to collect information from a person, display their data in a section of the screen, then update their information without leaving the conversation.
To edit a chat note, at least two BPNs are required. One BPN acts as the primary process flow definition. Additional BPNs handle edits to chat notes. The secondary BPNs are referenced in the Script Task code that defines the chat note.
![](attachments/11939940/20809294.png)
Figure. Primary doChatNoteEdit BPN Process
![](attachments/11939940/20809295.png)
Figure. Secondary doChatNoteUpdate BPN Process
In this demonstration, a chat note will display the user’s name in the chat notes area apart from the conversation panel. Clicking the edit link in for the chat note will trigger Amelia to use a secondary BPN to ask for the new name and then update the chat note. The exercise also passes variables along with the name update.
For simplicity and clarity, both BPNs will reuse much of the same script and other tasks.
# Create the Demo
Creating this demonstration involves creating two new BPN models, adding and defining tasks, then conversing with Amelia to interact and see changes made to the chat notes area of the custom user interface.
## Create BPN Tasks
In the Amelia administration pages, use the Process Knowledge tab to create two new BPN models and name one editSection and another editSectionChange. Then create these tasks in the BPN, as described and ordered in Table 7 and Table 8 below.
Table. Primary doChatNoteEdit BPN Specifications

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let's get started | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | ask "What is your name?" | Select this task and click the Properties Panel on the right side. Set Ask behavior (1st pass and subsequent) to Ignore if responded. |
| 3 | create chat note | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code for the doChatNoteEdit BPN into the Script editor. If needed, select Groovy as the language. |
| 4 | say click the edit icon to change your name. Otherwise, can i help with anything else? | Cue user to click edit icon in the chat note |

Table. Secondary doChatNoteUpdate BPN Specifications

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | ask "What is your full name?" | Ask the user for their correct name then wait for a response. |
| 2 | say updating with your new name ${newName} |  |
| 3 | update chat note | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code for the doChatNoteUpdate BPN into the Script editor. If needed, select Groovy as the language. |
| 4 | say i updated your full name. | Confirm the update |
| 5 | say you also passed these variables, var1 ${var1} and var2 ${var2}. can i help with anything else? | Display variables passed along with the chat note update. Exit the BPN workflow. |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Chat Note
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 3 in the table above for the doChatNoteEdit BPN.
The actionProcess code defines what happens when the chat note edit icon is clicked. In this case, the doChatNoteUpdate BPN will be called (actionName), two variables will be passed (var1, var2), and the user will say "I need to change my name" (actionMessage) in the conversation area.
In addition, the component header and title values and the subcomponent label must be the same for the primary BPN chat note and any secondary BPN code to update the chat note.
``` bash
def jsonString = '''
    {
        "action"       : "addChatNotesIntegration",
        "componentType" : "ChatNote",
        "payload"      : [
            {
            "component"    : "ChatNote",
            "header"       : "Personal Details",
            "title"        : "Your Details",
            "actionProcess" : {
                "actionName"      : "doChatNoteUpdate",
                "actionArguments" : {
                    "var1"        : "variable 1",
                    "var2"        : "variable 2"
                },
                "actionMessage" : "I need to change my name"
            },
            "subcomponents" : [
                {
                "subcomponent" : "Markup",
                "markupType"  : "Text",
                "label"       : "Name",
                "value"       : "personName"
                }
            ]
            }
        ]
    }
'''
def personName = execution.getVariable("response")
jsonString = jsonString.replace('personName', personName)
messageService.sendIntegrationMessage(jsonString)
```
## A Script to Update a Chat Note
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 3 in the table above for the doChatNoteUpdate BPN.
The component header and title values and the subcomponent label must be the same for the primary BPN chat note and any secondary BPN code to update the chat note.
``` bash
def jsonString = '''
    {
        "action"       : "addChatNotesIntegration",
        "componentType" : "ChatNote",
        "payload"      : [
            {
            "component"    : "ChatNote",
            "header"       : "Personal Details",
            "title"        : "Your Details",
            "subcomponents" : [
                {
                "subcomponent" : "Markup",
                "markupType"  : "Text",
                "label"       : "Name",
                "value"       : "newName"
                }
            ]
            }
        ]
    }
    '''
def newName = execution.getVariable("response")
jsonString = jsonString.replace('newName', newName)
messageService.sendIntegrationMessage(jsonString)
```
## Interact with Amelia
When the BPN models are built and deployed, as described above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doChatNoteEdit workflow by typing this command in the chat interface:
    
    |  |
    | ----|
    | run the workflow doChatNoteEdit |
    
3.  Type a name when prompted by Amelia.
4.  Amelia displays a chat notes panel on the right side with a chat note that displays the name entered in the conversation area.
5.  Click the edit icon in the chat note on the right side chat note panel. Amelia will respond with the actionMessage from the doChatNoteEdit BPN and then the first task of the secondary doChatNoteUpdate BPN.
6.  Type in a new name. Amelia will update the chat note in the right side chat note panel then display in the conversation area the variables passed with the doChatNoteEdit BPN.
# Deleting Chat Notes
Chat notes can be deleted individually and all available chat notes.
## Delete a Chat Note
``` groovy
import groovy.json.JsonOutput
def jsonString = '{'+
    '"action":"deleteChatNoteIntegration",'+
    '"componentType": "ChatNote",'+
    '"payload": [{'+
      '"component": "ChatNote",'+
      '"title": "Chat Note A"}'+
  ']}'
jsonString = JsonOutput.toJson(jsonString)
execution.setVariable("jsonString", jsonString)
```
## Delete All Chat Notes
This action clears all chat notes, banners, dividers, and other elements on the right side of the custom user interface, also called the right rail.
``` groovy
def deletionPayload =
'''
{
    "action": "clearRightRail",
    "componentType": "ChatNote"
}
'''
execution.setVariable("jsonString", deletionPayload)
```
# Toggle Chat Notes
Chat notes can be toggled open or closed with a BPN Script task.
``` groovy
import groovy.json.JsonOutput
def payload = [
    action       : 'addChatNotesIntegration',
    componentType: 'ChatNote',
    header: 'Welcome to Amelia',
    payload      : [
        [
        component    : 'ChatNote',
        title        : 'Amelia Asks Questions',
        forceOpenState: 'open'
        ],
        [
        component: 'ChatNote',
        title: 'Chat Note A',
        forceOpenState: 'closed'
        ],
        [
        component: 'ChatNote',
        title: 'Chat Note B',
        forceOpenState: 'open'
        ]
    ]
]
def jsonString = JsonOutput.toJson(payload)
execution.setVariable('jsonString',jsonString)
```
# Open Chat Notes
All chat notes on the right side of the custom user interface can be opened at once, for example, to ensure the user sees information.
``` groovy
def openPayload =
'''
{
    "action": "openChatNotes",
    "componentType": "ChatNote"
}
'''
execution.setVariable("jsonString", openPayload)
```
{% /version %}
