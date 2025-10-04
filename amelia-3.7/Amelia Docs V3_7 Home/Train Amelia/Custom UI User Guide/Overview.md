{% version "3.x" %}
When Amelia talks with people through a chat interface, her conversation can include different ways to interact in addition to text. She also can collect, organize, and present artifacts from the conversation. For example, a car insurance quote can include a photo of the vehicle plus financial details used to generate a quote. Or Amelia can include a map to help customers find a local store. Amelia also can ask a person to click to select from button options instead of typing text.
This enhanced chat interface is called a custom user interface, or custom UI. Within the chat conversation, Amelia can present single and multiple choice buttons to collect data. Chat notes appear in a panel that slides into view from the right edge of the chat interface. Within the chat notes panel, one or more chat notes can present a mix of text, images, video, HTML tables, and maps as needed. The chat notes panel also can include a banner fixed at the top.
Currently, chat notes and a banner are the two components of Amelia's custom UI. These two components each have a set of subcomponents, for example, text, value, fontSize, and so on.
The primary difference between the Amelia V2 custom UI and the new V3 custom UI is the use of JSON to organize a data payload for Amelia to display. The updated custom UI also includes the ability to control font size and weight, for example, to provide a large type for the banner heading.
# Chat Interface
Amelia's custom UI chat interface is an efficient set of sliding panels to hold the conversation, display data and other artifacts from a conversation, and manage a conversation, for example, to reset it or request a live agent.
![](attachments/11939917/11939918.jpg)
Figure. Custom UI Interface
Table. Elements of the Custom UI

| Element | Description |
| ----|----|
| Text Input | Enter text to respond and engage Amelia in conversation |
| Conversation Area | A transcript of text and other interactions with Amelia |
| Chat Notes Panel | A fly out panel that holds chat notes and banners |
| Menu | Click to reset the conversation, logout, or contact a live agent |

# BPN Integration
The custom UI is activated with BPN tasks through scripts and property panel settings used to define process flows for Amelia to follow in her conversations. Editing chat notes also trigger additional BPN processes to make any changes to the note.
## Process Flow
This process flow shows at a high level how BPN tasks and flows for custom UI interactions might be described. Actual BPN tasks and flows depend on each process to be modeled.
![](attachments/11939917/11939922.png)
Figure. High Level Example of BPN Process Flow with Custom UI
## Tasks
BPN models can be created and edited in Amelia’s administration pages. Each BPN defines an interaction step by step for Amelia to perform one or more tasks. See the [Amelia V3 BPN Getting Started Guide](BPN%20Getting%20Started%20Guide) for more details about BPNs.
Within the BPN workspace, the custom UI can be configured by creating Script Tasks and updating the property panels for each task. Click once on a Task to display the task tool icons, as shown below.
![](https://docs.ipsoft.com/download/attachments/11939477/amelia-script-task-tools-3.7.37.jpg)
Figure. Basic BPN Task Tools to Create Scripts and Set Properties
The Change Task Type wrench icon sets the type, Task or Script. The Edit Script document icon opens an editor where scripts can be written in Groovy or JavaScript. When a Task is selected, the Properties panel displays configuration options based on the task type. Refer to the [BPN Tasks](BPN%20Tasks) page for details about BPN tasks which is part of the [BPN Getting Started Guide](BPN%20Getting%20Started%20Guide).
## Edge Notation
The direction of a BPN process can be controlled by notation between the edges of a task. For example, clicking a yes or no button can determine two different paths in the process flow. The notation is based on basic Java notation.
Flow lines can include conditions to determine whether or not they should be followed. The Properties Panel for flow lines includes both Name and Expression fields. The Name appears near the flow line while the Expression is the condition to be met in order for the flow line to be followed during a BPN process.
Edges and gateways with flow lines that have edge notation also must include either a default flow line or specify an otherwise condition with bpn:otherwise() edge notation for one flow line. To set a default flow line, select a flow near its end points to display the wrench and garbage can icons. Click the wrench icon and select Default Flow from the popup. Refer to the [BPN Tasks](BPN%20Tasks) page for details about outgoing edge transitions which is part of the [BPN Getting Started Guide](BPN%20Getting%20Started%20Guide).
Figure. Flow Line Edge Notation Properties
## Implementation Steps
For each update sent to the custom UI, the following steps are performed to generate then present data with the custom UI. 
Data is generated in BPN
-   A BPN Script Task — written in Groovy — creates a JSON string and an object variable.
-   To control the chat note panel and chat note, the Script task also sends an integration message to the custom UI for display. To control single and multiple choice buttons, a *fieldBuilder* object is created to pass the button definition to the custom UI.
Presenting the document section
-   The client-specific UI is tailored to understand and render the data sent by BPN as the payload of an integration message.
-   Standard navigation mechanisms, such as the ability to direct the conversation flow to another BPN, is supported with the Run the Workflow BPN task.
# Code Structure
For Amelia's custom user interface, features are displayed either in the conversation area with the *fieldBuilder* object or in the chat notes panel that slides into view from the right edge of the chat interface and displays using a JSON payload object.
## Chat Notes
Each chat note and banner that appears in a chat notes panel generates a JSON key:value string to be passed to Amelia's chat interface. The code structure includes calling a JSON library, setting up a payload, defining components and subcomponents, create the JSON string, and finally set a variable equal to the JSON string.
This example code includes the most common shared code structure elements for custom UI features displayed in chat notes.
``` bash
def jsonString = '''
    {
        "action": "addChatNotesIntegration",
        "componentType": "ChatNote",
        "payload": [{
            "component": "Banner",
            "title": "My Banner",
            "styles": {
                "height": "100%",
                "color": "#fff",
                "backgroundColor": "#4d5aff"
            },
            "subcomponents": [{
                    "subcomponent": "Markup",
                    "markupType": "Text",
                    "value": "Welcome to SSMC Chat Support",
                    "fontSize": "headline",
                    "fontWeight": "bold"
                },
                {
                    "subcomponent": "Markup",
                    "markupType": "Text",
                    "value": "Chat with Amelia, our Virtual SSMC Desk Representative, to help you:",
                    "fontSize": "title",
                    "fontWeight": "regular"
                },
                {
                    "subcomponent": "Markup",
                    "markupType": "Text",
                    "value": "<br/><br/><ul><li>Create a ticket</li><li>Update a ticket</li><li>Check ticket status</li></ul>",
                    "fontSize": "subhead",
                    "fontWeight": "normal"
                }
            ]
        }]
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
These elements are described below. The rest of this document describes these elements in detail while building banners and chat notes.
Table. Chat Notes Code Structure

| Element | Description |
| ----|----|
| def jsonString | Define a variable payload as a JSON object that contain key:value definitions Amelia uses to display chat notes and banner in the chat note panel |
| action | addChatNotesIntegration creates a new chat note if no other chat note with the same title exists. If another chat note with the same title exists, content will be replaced with the latest data provided.deleteChatNoteIntegration deletes a chat note based on the title. If no chat note exists with the same title, the action does not execute. |
| componentType | ChatNote is the only current value available |
| payload | Contains the JSON definition with component and subscomponents |
| component | Either ChatNote or Banner, the two components currently available |
| title | Unique because titles are used to identify chat notes when adding and deleting chat notes |
| subcomponent | An additional set of elements based on the type of component and subcomponent. |
| messageService | The messageService is used to send the jsonString variable value in an integration message to the custom UI for display |

## Conversation Area
This example includes the most common shared code structure elements for custom UI features displayed in the chat conversation area. It's optimized for the Groovy language.
``` groovy
def fieldBuilder = formInputDataBuilder.create()
      .name("singleChoiceButton")
      .nameForDisplay("Single Choice Button")
      .formType("sampleForm")
      .staticSelectionUtterance("")
      .allowedUserInputs("both")
      .addField()
        .name("someChoice")
        .fieldType("singleSelection")
        .postfixedSelectionUtterance("", "")
                .addOption()
                  .name("Rare")
                  .value("Rare")
                  .backToField()
                .addOption()
                  .name("Medium Rare")
                  .value("Medium Rare")
                  .backToField()
                .addOption()
                  .name("Medium")
                  .value("Medium")
                  .backToField()
                .addOption()
                  .name("Medium Well")
                  .value("Medium Well")
                  .backToField()
                .addOption()
                  .name("Well Done")
                  .value("Well Done")
                  .backToField()
            .backToForm()
          .build()
execution.setVariable('singleChoiceButton', fieldBuilder.toString())
```
These code elements are described below. The rest of this document describes these elements in detail.
Table. Conversation Area Code Structure

| Element | Description |
| ----|----|
| def fieldBuilder | Define a variable fieldBuilder to pass to the custom user interface |
| name | Mandatory internal name, must be unique across sections |
| nameForDisplay | Name visible on the UI (optional) |
| formType | Type of the form data being sent. Used for gross determinations by the client. For choice buttons use sampleForm, otherwise booleanForm. |
| staticSelectionUtterance | Adds text to user’s selection when Amelia displays the user response. For example:.staticSelectionUtterance(“Edit the first vehicle”)Whether the user selects one or many elements, the utterance will be, "Edit the vehicle".One of the three SelectionUtterance fields – postfixedSelectionUtterance, prefixedSelectionUtterance, or staticSelectionUtterance – must be present in the form definition code, whether populated or not. Otherwise, any selection in the custom user interface will return and display the word None. |
| allowedUserInputs | Which inputs should be enabled when the form is displayed on the UI. Valid choices are:bothform_onlychat_only |
| addField | Define a unique field made of unique options |
| name | Internal name for the unique field |
| fieldType | Custom section title, e.g., multi-selection-field. May be used to provide rendering and behavior hints to the custom UI. Possible values are singleSelection, multipleSelection, multipleSelectionImage, carousel, autoComplete, cancelButton |
| postfixedSelectionUtterance | Adds text to user’s selection when Amelia displays the user response. For example:.postfixedSelectionUtterance(“I have selected this”, “I have selected”)For single choice buttons, the first argument is used, “I have selected this “ + button label.For a multiple select form, the second argument is used, “I have selected” + button 1 label + button 3 label, etc.One of the three SelectionUtterance fields – postfixedSelectionUtterance, prefixedSelectionUtterance, or staticSelectionUtterance – must be present in the form definition code, whether populated or not. Otherwise, any selection in the custom user interface will return and display the word None. |
| addOption | Define a unique option |
| name | Displayed name for the unique option |
| value | Internal field value for the unique option |
| backToField | Marks the end of the unique option definition |
| backToForm | Defines the end of the unique field definition |

{% /version %}
