{% version "3.x" %}
This demonstration creates suggested responses to appear above the chat input in the conversation area.
![](attachments/11939970/11939971.png)
Figure. doSuggestedResponses BPN
# Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doSuggestedResponses. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create Suggested Responses

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say we have several locations to pick from | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | suggest response | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language.The setting .allowedUserInputs should be set to both.The setting .instructions can be set to strict to prevent user input in the text field after they select a suggested response. |
| 3 | ask "Where would you like to go?" | The formInputData value from the Task 2 script is attached to this Ask task for display. |
| 4 | say ${response} is an excellent choice | Amelia displays the response value captured with the Ask task in Task 3. |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
# A Script to Create Suggested Responses
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
def formInputData = formInputDataBuilder.create()
          .name("locationSelectionForm")
          .allowedUserInputs("both")
          .instructions("strict")
          .addField()
              .name("locationSelectionField")
              .fieldType("AutoComplete")
              .postfixedSelectionUtterance("I select the location", "I select the location")
              .addOption()
                  .name("Franklin Lakes")
                  .nameForDisplay("Ohio")
                  .value("flakes")
                  .backToField()
              .addOption()
                  .name("Franklin Stakes")
                  .nameForDisplay("Ohio")
                  .value("flakes")
                  .backToField()
              .addOption()
                  .name("University of Maryland")
                  .nameForDisplay("Maryland")
                  .value("uni")
                  .backToField()
              .addOption()
                  .name("University of New York")
                  .nameForDisplay("New York")
                  .value("uni")
                  .backToField()
              .addOption()
                  .name("Colorado Rocks")
                  .nameForDisplay("Colorado")
                  .value("rocks")
                  .backToField()
              .addOption()
                  .name("Colorado State")
                  .nameForDisplay("Colorado")
                  .value("rocks")
                  .backToField()
              .addOption()
                  .name("Hollywood Heights")
                  .nameForDisplay("CA")
                  .value("heights")
                  .backToField()
              .addOption()
                  .name("Mountain Heights")
                  .nameForDisplay("GA")
                  .value("heights")
                  .backToField()
              .addOption()
                  .name("Mount Rainier")
                  .nameForDisplay("Seattle")
                  .value("rainier")
                  .backToField()
              .addOption()
                  .name("Washington DC")
                  .value("capitol")
                  .backToField()
              .addOption()
                  .name("Washington Street")
                  .value("capitol")
                  .backToField()
              .addOption()
                  .name("New York City")
                  .nameForDisplay("New York")
                  .value("nyc")
                  .backToField()
              .backToForm()
          .build();
execution.setVariable('formInputData', formInputData.toString())
```
# Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doSuggestedResponses workflow by typing this command in the chat interface:
    ``` groovy
    run the workflow doSuggestedResponses
    ```
3.  Amelia displays a list of suggested responses above the input area. Type characters to filter the list then select an option. A green up arrow appears at the bottom right of the input area.  
    ![](attachments/11939970/11939972.png)  
    Figure. Output of doSuggestedResponses BPN  
4.  Click the green up arrow to submit it as a response. Amelia displays the response from the last Say task in the BPN.
{% /version %}
