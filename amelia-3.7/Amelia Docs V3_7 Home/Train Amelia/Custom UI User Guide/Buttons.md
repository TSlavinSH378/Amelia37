{% version "3.x" %}
Amelia can display single or multiple-choice buttons with user selection used to direct the future conversation flow, as well as present data in one or more chat notes.
![](attachments/11939928/20808262.png)
Figure. Example Multiple Choice Buttons
# Button Types
There are four types of button and all buttons are single select or multiple select.
![](attachments/11939928/28475525.png)
Figure. Button Options with Active and Selected States
Table. Button Options

| Button Type | Available Property Fields | Description |
| ----|----|----|
| Small | .name(), .value() | A simple text button |
| Medium | .name(), .value(), .imageBase64() | Image with a title acts as a button |
| Large | .name(), .value(), .imageBase64(), .imageAltText(), .fieldType("singleSelectionImageDescr"),;.fieldType("multipleSelectionImageDescr") | Image with a title and description text acts as a button |
| X-Large | .name(), .value(), .imageBase64(), .imageAltText(), .valueForDisplay(), .fieldType("singleSelectionImageDescrOptions"), .fieldType("multipleSelectionImageDescrOptions") | Image with a title, description, and up to two call to action buttons |

Buttons are created with an Ask task using the `Form data variable` property in the task Properties panel which is set to `formInputData`.
The `showSelectButtonsinChatLog` property field set to `true` limits buttons to be available only in the chat input box. When set to `false`, buttons will appear in the chat conversation.
One of these three SelectionUtterance fields – postfixed`SelectionUtterance`, prefixed`SelectionUtterance`, or static`SelectionUtterance` – must be present in the form definition code, whether populated or empty. Otherwise, any selection in the custom user interface will return and display the word None.
-   The `prefixedSelectionUtterance("single_select_phrase", "multiple_select_phrase")` property field adds text before the user response. If a button value is `chocolate`, for example, this property can add, "I really like " before the user utterance in the conversation area to display, "I really like chocolate" instead of "chocolate." It's possible to define one response for single choice button and a second response for multiple select buttons.
-   The `postfixedSelectionUtterance("single_select_phrase", "multiple_select_phrase")` property field adds a phrase after the user response, for example, "Chocolate is my favorite food" instead of "Chocolate."
-   And `staticSelectionUtterance("phrase")` adds text to the user selection whether or not the buttons are single or multiple select.
## Small Buttons
### Single Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("singleSelection")
                    .postfixedSelectionUtterance("", "")
                    .addOption()
                        .name("Lamborghini Aventador ü 2016")
                        .value("la2016")
                        .backToField()
                    .addOption()
                        .name("VW Beetle Å1971")
                        .value("vb1971")
                        .backToField()
                    .addOption()
                        .name("Aventador")
                        .value("la2020")
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputDataString)
```
### Multiple Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("multipleSelection")
                    .postfixedSelectionUtterance("I select the vehicle", "I select the vehicles")
                    .addOption()
                        .name("Lamborghini Aventador 2016")
                        .value("la2016")
                        .selected(true)
                        .backToField()
                    .addOption()
                        .name("VW Beetle 1971")
                        .value("vb1971")
                        .selected(false)
                        .backToField()
                    .addOption()
                        .name("VW Brasilia 1977")
                        .value("vr1977")
                        .selected(true)
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
## Medium Buttons
To use buttons with images, the property field `imageBase64()` must be specified.
The property field `fieldType()` must be either "singleSelectionImage" or "multipleSelectionImage."
### Single Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("singleSelectionImage")
                    .postfixedSelectionUtterance("", "")
                    .addOption()
                        .name("Lamborghini Aventador ü 2016")
                        .value("la2016")
                        .imageBase64("https://image-example.png")
                        .backToField()
                    .addOption()
                        .name("VW Beetle Å1971")
                        .value("vb1971")
                        .imageBase64("https://image-example.png")
                        .backToField()
                    .addOption()
                        .name("Aventador")
                        .value("la2020")
                        .imageBase64("https://image-example.png")
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
### Multiple Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("multipleSelectionImage")
                    .postfixedSelectionUtterance("I select the vehicle", "I select the vehicles")
                    .addOption()
                        .name("Lamborghini Aventador 2016")
                        .value("la2016")
                        .imageBase64("https://image-example.png")
                        .selected(true)
                        .backToField()
                    .addOption()
                        .name("VW Beetle 1971")
                        .value("vb1971")
                        .imageBase64("https://image-example.png")
                        .selected(false)
                        .backToField()
                    .addOption()
                        .name("VW Brasilia 1977")
                        .value("vr1977")
                        .imageBase64("https://image-example.png")
                        .selected(true)
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
## Large Buttons
Property fields `.imageBase64()` and `.imageAltText()` must be specified to use the large size button.
The property field `fieldType()` also must be equal to "singleSelectionImageDescr" or "multipleSelectionImageDescr."
### Single Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("singleSelectionImageDescr")
                    .postfixedSelectionUtterance("", "")
                    .addOption()
                        .name("Lamborghini Aventador ü 2016")
                        .value("la2016")
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("VW Beetle Å1971")
                        .value("vb1971")
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("Aventador")
                        .value("la2020")
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
### Multiple Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("multipleSelectionImageDescr")
                    .postfixedSelectionUtterance("I select the vehicle", "I select the vehicles")
                    .addOption()
                        .name("Lamborghini Aventador 2016")
                        .value("la2016")
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .selected(true)
                        .backToField()
                    .addOption()
                        .name("VW Beetle 1971")
                        .value("vb1971")
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .selected(false)
                        .backToField()
                    .addOption()
                        .name("VW Brasilia 1977")
                        .value("vr1977")
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .selected(true)
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
## X-Large Buttons
Every call to action button is an option – the `addOption()` property field – grouped into a separate X-Large button only in the case when `name()`, `imageBase64()` and `imageAltText()` are the same. Use different `value()` and `valueForDisplay()` values for each option. The  `valueForDisplay()` property field is used to name a call to action button label – "Select Option" or "Select for Later."
The property field `fieldType()` must equal either `"singleSelectionImageDescrOptions"` or `"multipleSelectionImageDescrOptions`*.*
### Single Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("singleSelectionImageDescrOptions")
                    .postfixedSelectionUtterance("", "")
                    .addOption()
                        .name("Lamborghini Aventador 2016")
                        .value("la2016")
                        .valueForDisplay('Select Option')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("Lamborghini Aventador 2016")
                        .value("la2016later")
                        .valueForDisplay('Select for Later')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("VW Beetle 1971")
                        .value("vb1971")
                        .valueForDisplay('Select Option')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("VW Beetle 1971")
                        .value("vb1971later")
                        .valueForDisplay('Select for Later')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
### Multiple Select Code Example
``` groovy
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("multipleSelectionImageDescrOptions")
                    .postfixedSelectionUtterance("I select the vehicle", "I select the vehicles")
                    .addOption()
                        .name("Lamborghini Aventador 2016")
                        .value("la2016")
                        .valueForDisplay('Select Option')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("Lamborghini Aventador 2016")
                        .value("la2016later")
                        .valueForDisplay('Select for Later')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("VW Beetle 1971")
                        .value("vb1971")
                        .valueForDisplay('Select Option')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .addOption()
                        .name("VW Beetle 1971")
                        .value("vb1971later")
                        .valueForDisplay('Select for Later')
                        .imageBase64("https://image-example.png")
                        .imageAltText("text description")
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
# Create a Multiple Choice Button
This demonstration creates a multiple choice button to appear in the conversation area of the custom user interface.
![](attachments/11939928/20808261.png)
Figure. doMultiButtons BPN
## Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doMultiButtons. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Multiple Choice Button

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | define multiple choice buttons | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | ask "What are your favorite flavors of ice cream?" | Select this task and click the Properties Panel on the right side. Set Ask behavior (1st pass and subsequent) to Always ask.Then set Form data variable to multiChoiceButton. The Form data variable name must match the variable used in the last line of the code from Task 2 to display buttons. |
| 4 | say ${response} tastes good. | Select the flow line from Task 3 to this task then click the Properties Panel on the right side. Type 1 flavor in the Name field and response:value().matches('(?i)(chocolate|vanilla)') in the Expression field. |
| 5 | say ${response} is an interesting choice | Select the flow line from Task 3 to this task then click the Properties Panel on the right side. Type 2+ flavors in the Name field.Select the flow line from Task 3 to this task and right mouse-click to view the wrench icon then select Default Flow. |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Multiple Choice Button
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above. Note the `multiChoiceButton` variable name set in the last line in this script must be the same name set in the Form data variable setting in the Ask task Properties Panel described in Task 3 above.
``` groovy
def multiChoiceButton = formInputDataBuilder.create()
          .name("flavorSelection")
          .nameForDisplay("Ice Cream Flavor Form")
          .formType("sampleForm")
          .staticSelectionUtterance("")
          .allowedUserInputs("form_only")
          .addField()
              .name("flavorSelectionField")
              .fieldType("multipleSelection")
              .postfixedSelectionUtterance("", "")
              .addOption()
                  .name("Chocolate")
                  .value("chocolate")
                  .backToField()
              .addOption()
                  .name("Vanilla")
                  .value("vanilla")
                  .backToField()
              .addOption()
                  .name("Strawberry")
                  .value("strawberry")
                  .selected(true) // Selected by default
                  .backToField()
              .backToForm()
                .addField()
                .name("cancel")
                .fieldType("cancelButton")
                .staticSelectionUtterance("Continue")
                .backToForm()
          .build();
execution.setVariable("multiChoiceButton", multiChoiceButton.toString())
```
## Interact with Amelia
When the BPN model is built and approved, as described above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the new workflow by typing this command in the chat interface:
    
    |  |
    | ----|
    | run the workflow doMultiButtons |
    
3.  Amelia displays buttons in the conversation area. Click buttons to make a selection and click a selected button to deselect it.
4.  Click the Submit button.
# Create a Single Choice Button
This demonstration creates a choice choice button to appear in the conversation area of the custom user interface.
![](attachments/11939928/20808267.png)
Figure. doSingleButton BPN
## Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doSingleButton. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Single Choice Button

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | create single button | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | ask "Which color do you like?" | Select this task and click the Properties Panel on the right side. Set Ask behavior (1st pass and subsequent) to Always ask.Then set Form data variable to singleChoiceButton. The Form data variable name must match the variable used in the last line of the code from Task 2 to display buttons. |
| 4 | say like a ${response} ribbon | Select the flow line from Task 3 to this task then click the Properties Panel on the right side. Type Red in the Name field and response:value().matches('Red') in the Expression field. |
| 5 | say like the ${response} sky | Select the flow line from Task 3 to this task then click the Properties Panel on the right side. Type Blue in the Name field and response:value().matches('Blue') in the Expression field. |
| 6 | say like the ${response} sun | Select the flow line from Task 3 to this task then click the Properties Panel on the right side. Type Yellow in the Name field and response:value().matches('Yellow') in the Expression field. |
| 7 | say it's okay to not pick a color. | Select the flow line from Task 3 to this task then click the Properties Panel on the right side. Type cancel in the Name field and leave the Expression field blank. |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Single Choice Button
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above. Note the singleChoiceButton variable name set in the last line in this script must be the same name set in the Form data variable setting in the Ask task Properties Panel described in Task 3 above.
``` groovy
def options = ['color1': 'Red',
            'color2': 'Blue',
            'color3': 'Yellow',
            'cancel': 'Cancel']
execution.setVariable('options', options);
def fieldBuilder = formInputDataBuilder.create()
      .name("singleChoiceButton")
      .nameForDisplay("Single Choice Button")
      .formType("sampleForm")
      .staticSelectionUtterance("")
      .allowedUserInputs("form_only")
      .addField()
        .name("SomeChoice")
        .fieldType("singleSelection")
        .postfixedSelectionUtterance("", "")
options.each {
      fieldBuilder = fieldBuilder.addOption()
        .value(it.key)
        .name(it.value)
        .backToField()
}
def singleChoiceButton = fieldBuilder.backToForm()
    .build()
execution.setVariable('singleChoiceButton', singleChoiceButton.toString())
```
## Interact with Amelia
When the BPN model is built and approved, as described above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the new workflow by typing this command in the chat interface:
    
    |  |
    | ----|
    | run the workflow doSingleButton |
    
3.  Amelia displays buttons in the conversation area. Click and unclick buttons to make a selection before clicking the Submit button.
{% /version %}
