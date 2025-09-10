.
In Amelia's custom user interface, a banner is a standalone component like chat notes that appears fixed at the top of the chat notes panel. A banner is the simplest component of the custom UI and, therefore, a good place to start learning about how to use the interface. The banner background color is defined when Amelia is installed.
![](attachments/11939923/11945102.png)
Figure. Banner on Desktop and Mobile
# Create a Basic Banner
To explore how to create a banner, create a BPN to generate a banner with different font sizes and weights.
Figure. doBanner BPN
## Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doBanner. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Banner

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | define banner | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | send the integration message jsonString | Sends the variable jsonString to Amelia's interface for display |
| 4 | say integration message sent | Exit the BPN |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Banner
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above. The elements used to build the banner are described in the next section.
``` bash
import groovy.json.JsonOutput
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
execution.setVariable("jsonString", jsonString)
```
## Interact with Amelia
When the BPN model is built and approved, as described above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doBanner workflow by typing this command in the chat interface:
    
    |  |
    | ----|
    | run the workflow doBanner |
    
3.  Amelia displays a chat notes panel on the right side with a banner fixed at the top.
# Additional Banners
## Banner with Buttons
![](attachments/11939923/11945103.png)
Figure. Banner with Buttons
``` groovy
{
    "component": "Banner",
    "title": "My Banner",
    "subcomponents": [{
            "subcomponent": "Markup",
            "markupType": "Default",
            "value": "Congratulations!",
            "fontSize": "title",
            "fontWeight": "bold"
        },
        {
            "subcomponent": "Markup",
            "markupType": "Default",
            "value": "Your quote is complete",
            "fontSize": "title",
            "fontWeight": "normal"
        },
        {
            "subcomponent": "Markup",
            "markupType": "Default",
            "value": "12-month policy",
            "fontSize": "body",
            "fontWeight": "normal"
        },
        {
            "subcomponent": "Markup",
            "markupType": "Default",
            "value": "$89 / month",
            "fontSize": "display",
            "fontWeight": "bold"
        },
        {
            "subcomponent": "Markup",
            "markupType": "Buttons",
            "buttons": [{
                "label": "View Summary",
                "value": "summary",
                "link": {
                    "href": "https://google.com",
                    "target": "top"
                }
            }, {
                "label": "Purchase Now",
                "value": "purchase",
                "actionProcess": {
                    "actionName": "gif",
                    "actionArguments": {
                        "section": "image",
                        "driver": "driver"
                    },
                    "actionMessage": "Edit the section"
                }
            }]
        },
        {
            "subcomponent": "Markup",
            "markupType": "Text",
            "value": "<a href=\'https://www.google.com\' target=\'_blank\'>View PDF</a>",
            "fontSize": "body",
            "fontWeight": "normal"
        }
    ]
}
```
## Banner with Image Background
![](attachments/11939923/11945104.png)
Figure. Banner with Background Image on Desktop and Mobile
``` groovy
import groovy.json.JsonOutput
def jsonString = '''
{
    "action": "addChatNotesIntegration",
    "componentType": "ChatNote",
    "payload": [{
        "component": "Banner",
        "title": "My Banner",
        "styles": {
            "backgroundImage": "url(https://ui-amelia-dev.ipsoft.com/Amelia/getFile?fileId=1468)", <------ This image must be from the content manager of your instance
            "backgroundSize": "100%",
            "height": "100%",
            "backgroundRepeat": "no-repeat",
            "backgroundPosition": "center"
        },
        "subcomponents": []
    }]
}
'''
execution.setVariable("jsonString", jsonString)
```
# Banner Elements
In addition to the common code structure used to build a JSON string to send to Amelia's interface, banners have specific elements, settings, and values.
Table. Banner Elements

| Element | Description |
| ----|----|
| component | Either ChatNote or Banner, the two components currently available |
| title | Unique because titles are used to identify chat notes when adding and deleting chat notes |
| subcomponent | Current value is Markup |
| markupType | Banners use Default as markupType. Other options are Text and Buttons which are described in the tables below. |

## Default and Text Elements
The Default and Text markupType elements include font size and other settings.
Table. Default and Text Settings
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Default/Text Settings</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">value</td>
<td class="confluenceTd">Text to display in the chat notes panel. If markupType is Text, basic HTML can be included.</td>
</tr>
<tr class="even">
<td class="confluenceTd">fontSize</td>
<td class="confluenceTd"><p>Possible predefined options are small, caption, body, subhead, title, headline, and display.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Font Size Pts | Line Height Pts | Font Size Ems |
| ----|----|----|----|
| small | 10 | 16 | .625 |
| caption | 12 | 16 | .75 |
| body | 16 | 24 | 1 |
| subhead | 20 | 24 | 1.25 |
| title | 24 | 32 | 1.5 |
| headline | 32 | 40 | 2 |
| display | 40 | 56 | 2.5 |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">fontWeight</td>
<td class="confluenceTd">regular and bold are the possible options</td>
</tr>
</tbody>
</table>
## Button Settings
Banners can include buttons with their own settings and options. Buttons are either links to a new web page or call a BPN.
Table. Button Settings

| Button Settings | Description |
| ----|----|
| label | Text that appears within the button |
| value | Not currently used. |
| link | The destination URL includes two additional settings and values. A button definition uses either link or actionProcess.href – The destination link. If no https, https, ftp, mailto, or other protocol is specified, the URL will treated as relative to the current URL.target – Where to display the link. _blank opens a new browser window. _top opens in the full body of the browser window. |
| actionProcess | For chat notes, defines what data to pass to a specific BPN when editing with the Edit button. Has additional settings and values. If actionProcess is not present in the code, the Edit button will not appear. A button definition uses either actionProcess or link.actionName – The name of the BPN to call when the Edit link is clickedactionArguments – Additional data to pass to the BPN when the Edit link is clicked. Values are passed as keys and values in a single object.
actionMessage – Custom message output as the user's utterance in the conversation area, for example, "I want to edit my address." If value is empty, the default utterance is, "I have invoked an action." |

