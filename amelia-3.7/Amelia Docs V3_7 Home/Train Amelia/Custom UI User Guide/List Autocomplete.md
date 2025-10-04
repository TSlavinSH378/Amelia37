{% version "3.x" %}
The custom user interface can present a list of possible responses to a user, as a way to standardize responses and streamline the response process. The list of possible responses is defined in a BPN Script task, with the list contents saved as a variable, then referenced in an Ask task. The contents of the list responses can be defined dynamically or as static code.
# Response Modes
There are two possible ways a user can respond to a pre-populated list of possible responses, submit mode and input mode.
## Submit Mode
The **default submit mode** displays the list of possible responses once Amelia completes the Ask task, asking the question in the conversation area of the custom user interface. When the user starts to type their response, the list is filtered based upon the typed response. The user selects from the list with either their mouse or arrow keys. Once selected, the response appears in the chat input box. The user can confirm the selection before submitting it by clicking the submit button or pressing the Enter key.
In the **auto submit mode**, once a response is selected, the response is sent directly to the conversation area. The response does not appear in the chat input box. The auto response requires configuration by IPsoft staff on request.
## Input Mode
The input mode defines what happens after the selected response is in the chat input box. Input mode only works with the default submit mode described above.
In **strict mode**, the user cannot type anything else in addition to their selected response. The `instructions` property must be set to `strict` in the Script task code.
In **default mode**, the user can type words in addition to the response they selected from the pre-populated list of possible responses. The BPN process must handle cases where a user enters data not on the list.
# Script Task Code
The code example below can be dropped into a Script task in a simple BPN to demonstrate how it works. Once the BPN is saved and deployed, type run the workflow BPNName in the custom user interface chat box, where BPNNameis the name of the simple BPN.
Figure. Simple BPN to Generate a Autocomplete List
A BPN Script task will display a pre-populated list with this example code. Properties are described below the code.
``` groovy
def formInputData = formInputDataBuilder.create()
          .name("locationSelectionForm")
          .allowedUserInputs("both")
          .instructions("strict")
          .addField()
              .name("locationSelectionField")
              .fieldType("AutoComplete")
              .prefixedSelectionUtterance("I select the location", "I select the location")
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
                  .selected(true) // Selected by default
                  .backToField()
              .backToForm()
          .build();
execution.setVariable('formInputData', formInputData.toString())
```
Table. List Autocomplete Properties

| Property | Definition |
| ----|----|
| allowedUserInputs | Set to both |
| instructions | If default submit mode is used, set to strict so;user cannot type anything else in addition to their selected response |
| fieldType | Set to AutoComplete |
| prefixedSelectionUtterance | See descriptions below |

One of three SelectionUtterance fields – postfixed`SelectionUtterance`, prefixed`SelectionUtterance`, or static`SelectionUtterance` – must be present in the form definition code, whether populated or empty. Otherwise, any selection in the custom user interface will return and display the word None.
-   The `prefixedSelectionUtterance("single_select_phrase", "multiple_select_phrase")` property field adds text before the user response. If a button value is `chocolate`, for example, this property can add, "I really like " before the user utterance in the conversation area to display, "I really like chocolate" instead of "chocolate." It's possible to define one response for single choice button and a second response for multiple select buttons.
-   The `postfixedSelectionUtterance("single_select_phrase", "multiple_select_phrase")` property field adds a phrase after the user response, for example, "Chocolate is my favorite food" instead of "Chocolate."
-   And `staticSelectionUtterance("phrase")` adds text to the user selection whether or not the buttons are single or multiple select.
{% /version %}
