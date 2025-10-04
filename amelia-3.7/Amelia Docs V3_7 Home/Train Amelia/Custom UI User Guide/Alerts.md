{% version "3.x" %}
Alerts display small pieces of information to users in the form of a banner that appears above the chat input box or in the conversation flow. A Script task defines the alert then sends the data to the custom user interface.
The code example below can be dropped into a Script task in a simple BPN to demonstrate how they work. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName `is the name of the simple BPN.
![](attachments/20809561/20809562.png)
Figure. Basic BPN to Display an Alert
The define alert Script task above displays an alert. In this example, the alert color is custom, the alert disappears only when the user clicks the alert or the X to the right. And the run doAlertWarning would trigger a BPN process called doAlertWarning.
![](attachments/20809561/20809564.png)
Figure. Alert Display
Alert priority and types can be mixed different ways.
![](attachments/20809561/20809584.png)
Figure. Alert Priorities and Types
# The Script Task
To display an alert above the conversation chat input box, a BPN Script task defines JSON output then sends an integration message to the custom user interface for display.
A Script task will display an alert with this example code. Properties are defined below.
``` groovy
def jsonString = """
    {
        "action": "addChatInputBanner",
        "componentType": "ChatInputBanner",
        "payload": {
            "inputBannerType": "InfoBanner",
            "text": "This is the content for my info banner",
            "customStyle": {
                "backgroundColor": "#E1CAD1",
                "color": "#433c3e"
            },
            "contentType": "textMulti",
            "actionText": "Display an alert warning",
            "action": "doAlertWarning",
            "actionMessage": "I want a warning alert!"
        }
    }
    """
messageService.sendIntegrationMessage(jsonString)
```
The alert JSON payload has a number of properties. The action property also is used different ways, as shown above.
Table. Alert Properties
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Property</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">action</td>
<td class="confluenceTd">The first definition of the JSON payload. Options are addChatInputBanner to open an alert or closeChatInputBanner to close an alert.</td>
</tr>
<tr class="even">
<td class="confluenceTd">inputBannerType</td>
<td class="confluenceTd"><p>Defines the type of alert to display</p>
<div class="table-wrap">
<pre class="table"><code>| Type | Description |
| ----|----|
| InfoBanner | Grey banner for information |
| SuccessBanner | Blue banner to indicate success |
| WarningBanner | Orange banner to warn users |
| DangerBanner | Red banner to warn users of a problem or error |</code></pre>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">text</td>
<td class="confluenceTd">Text used in the alert</td>
</tr>
<tr class="even">
<td class="confluenceTd">customStyle</td>
<td class="confluenceTd">Optional. backgroundColor defines the background color for the alert while color defines the text color.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">contentType</td>
<td class="confluenceTd"><p>Each content type has four possible format options which can be combined with inputBannerType, for example, a multiple line SuccessBanner</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| text | Displays text and disappears after three seconds |
| textDismiss | Displays text but user has to click alert for alert to disappear |
| textAction | Displays text with a hyperlink which can trigger a BPN process. User has to click alert for alert to disappear. Link is right aligned in alert. |
| textMulti | Same functionality as textAction but with a maximum of three lines of text. Link is bottom left aligned in alert. |</code></pre>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">actionText</td>
<td class="confluenceTd">Optional for text and textDismiss content types. The text link label that triggers a BPN process or other action when clicked.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">action</td>
<td class="confluenceTd">Optional for all content types. The name of the BPN process triggered by clicking the actionText link.</td>
</tr>
<tr class="even">
<td class="confluenceTd">actionMessage</td>
<td class="confluenceTd">For textAction and textMulti content types. When the actionText is clicked, submits a pre-defined message as a user utterance in the conversation area. If blank, the default message is, "I invoked an action."</td>
</tr>
</tbody>
</table>
# Examples
Alert properties can be combined in different ways to achieve different effects.
## Simple Text Alert with No Dismiss Option
Replace the payload JSON object above with this basic payload definition.
``` groovy
    "payload": {
        "inputBannerType": "InfoBanner",
        "text": "This is the content for my info banner",
        "contentType": "text"
    }
```
This payload displays a simple alert which disappears after three seconds elapse.
![](attachments/20809561/20809586.png)
Figure. Output for Simple Text Alert
## Warning Text Alert with Dismiss Option
To display a warning alert with the ability to click and dismiss the alert, replace the payload JSON object above with this payload definition.
``` groovy
    "payload": {
      "inputBannerType": "WarningBanner",
      "text": "This is the content for my warning banner",
      "contentType": "textDismiss"
    }
```
This payload displays a warning alert with the ability to click the alert to dismiss it.
![](attachments/20809561/20809587.png)
Figure. Warning Text Alert with Dismiss Option
## Success Text Alert with Dismiss Option
To display a success alert with the ability to click and dismiss the alert, replace the payload JSON object above with this payload definition.
``` groovy
        "payload": {
            "inputBannerType": "SuccessBanner",
            "text": "This is the content for my success banner.",
            "contentType": "textDismiss"
        }
```
This payload displays a success alert with the ability to click the alert to dismiss it.
![](attachments/20809561/20809627.png)
Figure. Success Text Alert with Dismiss Option
## Danger/Error Alert with Action Link
To display a danger alert with an action link and multiple text lines, replace the payload JSON object above with this payload definition.
``` groovy
    "payload": {
        "inputBannerType": "ErrorBanner",
        "text": "This is the content for my error banner",
        "contentType": "textAction",
        "actionText": "Run Single Select",
        "actionMessage": "Optional single-select Utterance",
        "action": "single-select"
    }
```
The payload displays a danger or error alert with an action link and multiple lines of text.
![](attachments/20809561/20809588.png)
Figure. Danger or Error Action Alert
## Close an Alert
Alerts can be closed by sending the following payload in a Script task.
``` groovy
def jsonString = """
    {
        "action": "closeChatInputBanner",
        "componentType": "ChatInputBanner",
        "payload": {
            "inputBannerType": "ChatInputBanner"
        }
    }
    """
messageService.sendIntegrationMessage(jsonString)
```
{% /version %}
