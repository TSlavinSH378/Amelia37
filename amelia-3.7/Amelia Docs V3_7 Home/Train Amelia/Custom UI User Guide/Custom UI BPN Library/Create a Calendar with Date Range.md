-   [Create the BPN](#CreateaCalendarwithDateRange-CreatetheBPN)
-   [A Script to Create a Calendar](#CreateaCalendarwithDateRange-AScripttoCreateaCalendar)
-   [Interact with Amelia](#CreateaCalendarwithDateRange-InteractwithAmelia)
This demonstration creates a calendar with a date range to appear in the conversation area.
![](attachments/11939961/11939963.png)
Figure. doCalendarDteRange BPN
## Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doCalendarDteRange. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Calendar with a Date Range

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say this is a test of a calendar accepts a date range | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | creates calendar with blocked start date | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language.In the code, set the two blockedDays dates to the current date and a future date to see these dates cannot be selected for a start date or end date. |
| 3 | send the integration message jsonString | Sends the variable jsonString to Amelia's interface for display of interactive calendar |
| 4 | say when would you like to attend? |  |
| 5 | say this produces a calendar that takes a date range with specific blocked dates |  |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Calendar
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
// Date Range with specific blocked dates
import groovy.json.JsonOutput
def payload = [
    action: 'addChatInputIntegrationMessage',
    payload: [
        componentType: 'MessageIntegration',
        subComponentType: 'DatePicker',
        formMessageType: 'datePicker',
        data: [
            datePickerType: 'dateRange',
            dateFormat: 'DD-MM-YYYY',
            blockedDays: [
                '2018-03-02',
                '2018-03-03'
            ]
        ]
    ]
]
def jsonString = JsonOutput.toJson(payload)
execution.setVariable('jsonString',jsonString)
```
## Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doCalendarDteRange workflow by typing this command in the chat interface:
    ``` groovy
    run the workflow doCalendarDteRange
    ```
3.  Amelia displays a calendar in the conversation flow with two months displayed. Click a start and end date. A blue up arrow appears at the bottom right of the calendar.  
    ![](attachments/11939961/11939962.png)  
    Figure. Output of doCalendarDteRange BPN  
4.  Click the blue up arrow at the bottom right of the calendar to submit the calendar data.
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-8-23_11-7-32.png](attachments/11939961/11939962.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-8-20_15-39-23.png](attachments/11939961/11939963.png) (image/png)  
