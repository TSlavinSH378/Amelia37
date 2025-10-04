{% version "3.x" %}
This demonstration creates an alert created in a Script task and sent as a JSON string for display by Amelia.
![](attachments/11939954/11939956.png)
Figure. doAlert BPN
# Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doAlert. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create Suggested Responses

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say this is a test of alerts | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | creates alert | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | send the integration message jsonString | Sends the variable jsonString to Amelia's interface for display of interactive calendar |
| 4 | say this was just an alert |  |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
# A Script to Create an Alert
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
import groovy.json.JsonOutput
def payload = [
    action:'addChatInputBanner',
    componentType: 'ChatInputBanner',
    payload:[
        inputBannerType: 'ErrorBanner',
        text: 'This is the content for my error banner',
        contentType: 'textAction',
        actionText: 'click this for help',
        action: 'alertSubFlowTester'
        ]
    ]
def jsonString = JsonOutput.toJson(payload)
execution.setVariable("jsonString", jsonString)
```
# Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doAlert workflow by typing this command in the chat interface:
    ``` groovy
    run the workflow doAlert
    ```
3.  Amelia displays an alert above the input area.  
    ![](attachments/11939954/11939955.png)  
    Figure. Output of doAlert BPN  
4.  Amelia displays the the last Say task in the BPN.
{% /version %}
