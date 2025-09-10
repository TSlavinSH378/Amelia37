This demonstration displays a simple rating survey coded in a Script task and sent as a JSON string for display by Amelia.
![](attachments/11939973/11939975.png)
Figure. doSurvey BPN
# Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doSurvey. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Survey

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say tests the survey using stars | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | creates stars survey | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language.In the script code, the surveyType setting can be stars, numbers, or emojis. If numbers, the label and value setting pairs are bad (value: 1), ok (2), good (3), better (4), great (5). If emojis, the label and value setting pairs are devastated, sad, neutral, and excited, for example, label: "devastated", value: "devastated". |
| 3 | send the integration message jsonString | Sends the variable jsonString to Amelia's interface for display of interactive calendar |
| 4 | ask "Please let us know how satisfied you are with your experience." |  |
| 5 | say thank you |  |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
# A Script to Create a survey
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
import groovy.json.JsonOutput
def payload = [
  action: "addChatInputIntegrationMessage",
  payload: [
    componentType: "MessageIntegration",
    subComponentType: "Survey",
    formMessageType: "survey",
    data: [
      surveyType: "stars",
      surveyData: [
        [
          label: "1",
          value: 1
        ],
        [
          label: "2",
          value: 2
        ],
        [
          label: "3",
          value: 3
        ],
        [
          label: "4",
          value: 4
        ],
        [
          label: "5",
          value: 5
        ],
        [label: "6",
          value: 6]
      ]
    ]
  ]
]
def jsonString = JsonOutput.toJson(payload)
execution.setVariable("jsonString", jsonString)
```
# Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doSurvey workflow by typing this command in the chat interface:
    ``` groovy
    run the workflow doSurvey
    ```
3.  Amelia displays a survey above the input area. Click the stars and a green up arrow appears at the bottom right of the input area.  
    ![](attachments/11939973/11939974.png)  
    Figure. Output of doSurvey BPN  
4.  Click the green up arrow to submit the survey. Amelia displays the the last Say task in the BPN.
