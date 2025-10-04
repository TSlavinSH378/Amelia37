{% version "3.x" %}
This demonstration creates a calendar with a single date selection to appear in the conversation area.
![](attachments/11939957/11939958.png)
Figure. doCalendarSingleDte BPN
## Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doCalendarSingleDte. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Calendar with a Date Range

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say this is a calendar that accepts a single date | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | creates single date calendar | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | send the integration message jsonString | Sends the variable jsonString to Amelia's interface for display of interactive calendar |
| 4 | ask "When would you like to attend?" |  |
| 5 | say this produces a calendar that takes a single date |  |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Calendar
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
import groovy.json.JsonOutput
def payload = [
    action: "addChatInputIntegrationMessage",
    payload: [
        componentType: "MessageIntegration",
        subComponentType: "DatePicker",
        formMessageType: 'datePicker',
    data: [
            datePickerType: "dateSingle",
            dateFormat: "DD-MM-YYYY"
        ]
    ]
]
def jsonString = JsonOutput.toJson(payload)
execution.setVariable('jsonString',jsonString)
```
## Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doCalendarSingleDte workflow by typing this command in the chat interface:
    ``` groovy
    run the workflow doCalendarSingleDte
    ```
3.  Amelia displays a calendar in the conversation flow with two months displayed. Click a single date. A green up arrow appears at the bottom right of the calendar.  
    ![](attachments/11939957/11939959.png)  
    Figure. Output of doCalendarSingleDte BPN  
4.  Click the green up arrow at the bottom right of the calendar to submit the calendar data.
{% /version %}
