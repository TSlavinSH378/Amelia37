-   [Methods](#ConversationService-Methods)
    -   [getTranscriptUtterances](#ConversationService-getTranscriptUtterances)
    -   [getTranscript()](#ConversationService-getTranscript())
    -   [getEmotionalSatisfactionScore()](#ConversationService-getEmotionalSatisfactionScore())
    -   [escalationInfo() (new in 3.6.x)](#ConversationService-escalationInfo()(newin3.6.x))
-   [Retrieve Conversation Example](#ConversationService-RetrieveConversationExample)
    -   [Create a BPN](#ConversationService-CreateaBPN)
    -   [A Script to Extract Datum Information](#ConversationService-AScripttoExtractDatumInformation)
    -   [Interact with Amelia](#ConversationService-InteractwithAmelia)
Within a BPN process, the conversation can be captured and parsed as needed with the Conversation Service.
# Methods
## getTranscriptUtterances
> [!warning]  
>
> When migrating from 3.7.x versions below 3.7.12 to version 3.7.12 and above, to call this method directly or with a wildcard, the Conversation Service package name in Script tasks and the Script Library scripts must be updated to change the scripting element of the package name to script.
>
> Releases prior to 3.7.12:
>
>     import net.ipsoft.ameliav3.bpn.scripting.service.conversation.*
>
>     import net.ipsoft.ameliav3.bpn.scripting.service.conversation.getTranscriptUtterances()
>
> Releases 3.7.12 and above:
>
>     import net.ipsoft.ameliav3.bpn.script.service.conversation.*
>
>     import net.ipsoft.ameliav3.bpn.script.service.conversation.getTranscriptUtterances()

    conversation.getTranscriptUtterances()
Retrieves an object with the entire conversation which can be iterated through for evaluation. During iteration, additional methods are available for each part of the conversation.

| Method | Description |
| ----|----|
| sequenceId() | The number position of the utterance within the conversation |
| utterance() | The utterance spoken by Amelia or the user |
| sessionId() | A unique ID assigned to each participant within a conversation session and used only within the conversation. Closing a conversation destroys the sessionId value. |
| dateTime() | YYYY-MM-DD HH:MM:SS.SSS format |
| sessionMode() | AGENT or USER with Amelia as AGENT by default |
| userId() | A unique ID assigned to each participant within a conversation and used only within the conversation. The userId value is unique to each user across conversations. |
| username() | The full name of the user, typically FirstName LastName |
| userFirstName() | The first name of the user |
| userLastName() | The last name of the user |

## getTranscript()
Retrieves a full transcript of the conversation as a string object.
## getEmotionalSatisfactionScore()
Amelia's affective memory estimates a user's emotional satisfaction score at every turn in her conversations. There are no pre-defined boundaries to determine whether or not a person is happy or upset, these scores are considered reasonable:
-   A low satisfaction score is equal to or less than -0.5
-   A neutral satisfaction score ranges between -0.2 to 0.2
-   A high satisfaction score is equal to or greater than 0.5
The emotional satisfaction score can be captured and used in a BPN to steer the conversation.
``` groovy
def score = conversationService.getEmotionalSatisfactionScore();
execution.setVariable("userSatisfactionScore", score);
execution.setVariable("isLowSatisfactionScore", score <= -0.5);
execution.setVariable("isHighSatisfactionScore", score >= 0.5);
```
## escalationInfo() (new in 3.6.x)
> [!warning]  
>
> When migrating from 3.7.x versions below 3.7.12 to version 3.7.12 and above, to call this method directly or with a wildcard, the Conversation Service package name in Script tasks and the Script Library scripts must be updated to change the scripting element of the package name to script.
>
> Releases prior to 3.7.12:
>
>     import net.ipsoft.ameliav3.bpn.scripting.service.conversation.*
>
>     import net.ipsoft.ameliav3.bpn.scripting.service.conversation.escalationInfo()
>
> Releases 3.7.12 and above:
>
>     import net.ipsoft.ameliav3.bpn.script.service.conversation.*
>
>     import net.ipsoft.ameliav3.bpn.script.service.conversation.escalationInfo()

    BpnEscalationDto escalationInfo()
Includes the ability to capture escalation reasons in pre-escalation BPNs. The `escalateInfo` method has a number of accessors included that capture escalation data. BPN Script tasks can be used to call the escalateInfo method then use the accessors to set variables.
``` groovy
def info = conversationService.escalationInfo();
execution.setVariable('reason', info.reason());
execution.setVariable('source', info.escalationSourceType());
execution.setVariable('responder', info.responder());
```
Table. escalationInfo Accessor Methods

| BpnEscalationDto | Accessor | Data Type | Description | Nullable |
| ----|----|----|----|----|
| escalationQueueCode() | String | The escalation queue if specified | yes | "globalqueue" |
| reason() | String | The escalation reason if specified | yes | E.g., "Misunderstanding", "An error has occurred", "Explicitly escalated from the BPN model 'normal_escalate'", "Direct escalation." |
| escalationSourceType() | String | The escalation source type (IMPLICIT, EXPLICIT, DIRECT) | no | EXPLICIT: Explicit escalations from a responder. E.g., "escalate lemma".IMPLICIT: Implicit escalations from the system (due to errors or conflicting states).DIRECT: Direct escalations from the user. |
| responder() | String | The responder that caused the escalation, (Bpn, AIML, etc) | yes | AcknowledgeDefaultAffectiveAIMLBpnCqaDontKnowEpisodicMemoryEQAEscalateFAQIntentFAQSemnetSemnetDocSocialTalkUnknownProblem |

# Retrieve Conversation Example
This demonstration creates then retrieves a short conversation divided into its parts.
![](attachments/11939528/11939529.png)
Figure. BPN to Retrieve a Conversation
## Create a BPN
In the Amelia administration pages, use the Process Knowledge tab to create a new BPN model and name it testConvoSvc. Save the new model then build each of the BPN tasks as described below.
Create these Tasks in a BPN, as described and ordered in the table below.
Table. BPN Specifications to Create then Retrieve a Conversation

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let's get started | Initialize Amelia and let the person know the conversation has started |
| 2 | ask "where are you working today?" | Prompt the user for a responseFor this demonstration, click the Properties Panel tab on the right side of the workspace and set Ask behavior (1st pass) and Ask behavior (subsequent) to Ignore if responded. |
| 3 | parse conversation | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 4 | say ${conv} | Display output of conversation extracted from utterance from Tasks 1 and 2 above |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save button
-   Click the Deploy button
These steps load the BPN model into Amelia’s memory.
## A Script to Extract Datum Information
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 3 in the table above.
> [!warning]  
>
> When migrating from 3.7.x versions below 3.7.12 to version 3.7.12 and above, to call this method directly or with a wildcard, the Conversation Service package name in Script tasks and the Script Library scripts must be updated to change the scripting element of the package name to script.
>
> Releases prior to 3.7.12:
>
>     import net.ipsoft.ameliav3.bpn.scripting.service.conversation.*
>
>     import net.ipsoft.ameliav3.bpn.scripting.service.conversation.getTranscriptUtterances()
>
> Releases 3.7.12 and above:
>
>     import net.ipsoft.ameliav3.bpn.script.service.conversation.*
>
>     import net.ipsoft.ameliav3.bpn.script.service.conversation.getTranscriptUtterances()

``` bash
import net.ipsoft.ameliav3.bpn.script.service.conversation.*;
def extractConversation = conversationService.getTranscriptUtterances();
StringBuilder sb = new StringBuilder();
for(net.ipsoft.ameliav3.bpn.script.service.conversation.TranscriptUtterance tu : extractConversation) {
  if (tu.username.equalsIgnoreCase('Amelia')){
      sb.append("A: " + tu.utterance + " "+tu.userFirstName()+" "+tu.userLastName()+" "+tu.sequenceId()+" "+tu.sessionId()+" "+tu.dateTime()+" "+tu.sessionMode()+" "+tu.userId()+" "+tu.username());
  } else {
      sb.append("U: " + tu.utterance + " "+tu.userFirstName()+" "+tu.userLastName()+" "+tu.sequenceId()+" "+tu.sessionId()+" "+tu.dateTime()+" "+tu.sessionMode()+" "+tu.userId()+" "+tu.username());
  }
}
execution.setVariable("conv", sb);
```
## Interact with Amelia
When the BPN models are built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the right edge of the Mind panel..
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the testConvoSvc workflow by typing this command in the chat interface:
    ``` bash
    run the workflow testConvoSvc
    ```
3.  Type in a response to Amelia's question about your location.
4.  Amelia displays the conversation broken into these parts:  
    Utterance  
    userFirstName  
    userLastName  
    SeqID  
    SessID  
    DateTime  
    SessMode  
    UserID  
    Username
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-1-5_11-25-55.png](attachments/11939528/11939529.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-20_16-43-51.png](attachments/11939528/11939530.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-20_16-40-48.png](attachments/11939528/11939531.png) (image/png)  
