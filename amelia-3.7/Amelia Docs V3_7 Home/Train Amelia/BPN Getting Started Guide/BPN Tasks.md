Steps in Amelia's conversations are mapped to individual tasks in a Business Process Network (BPN) model. Results from these tasks determine the flow to other tasks. Tasks tell Amelia what to ask or say, as well as run other BPNs, set and unset variables, escalate conversations to human agents, and other tasks.
The outbound flow from a task and inbound flow into a task are called edges. Conditions that regulate whether or not the conversation continues past a task edge are written with edge notation.
In addition, all BPN model tasks have access to any variables captured and set during the conversation process, as well as the conversation history. This thread of execution scope also is available to any sub BPNs called with a Run the Workflow task and their output also is available to tasks within the calling wrapper BPN.
For clarity, use lower case letters in all task text except where sense is altered. Amelia also will capitalize the first letter of a sentence in English.
# BPN Basics
In addition to different task types, Amelia includes improvements to BPN process and task creation, for example, autocomplete for tasks and some Properties Panel settings, as well as easier to read notation to test for conditions for data flowing from the edge of a task.
## Autocomplete
Autocomplete for tasks and some settings in the Properties Panel helps to create BPNs more quickly and accurately. Typing more slowly and stopping in the middle of a statement or phrase triggers this functionality.
To access all possible autocomplete options for a blank task, first type a task type, for example, *ask*, then backspace to erase the text. Autocomplete will display a list of all options for all tasks.
![](attachments/11939422/11941408.png)
Figure. Autocomplete for Ask Task
## Types of BPN Tasks
Amelia includes a number of tasks to organize conversations and engage customers.
Table. BPN Task Types

| Task Type | Description |
| ----|----|
| Ask | Instructs Amelia to ask the user a question |
| Say | Tells Amelia what to say to the user |
| Set the Variable | Defines the value of a variable available within the conversation and BPN model scope |
| Unset the Variable | Removes a variable from the conversation and BPN model scope |
| Run the Workflow | Instructs Amelia to continue the current activity thread into another workflow |
| Run the Integration Flow | Tells Amelia to connect to a backend system using a defined flow |
| Run the rpa bot | Tells Amelia to run a pre-configured 1RPA bot by name;(available with version 3.7.26+) |
| Request | Asks the user to upload a file |
| Present | Provides the user with a link to a file or an image |
| EscalateEscalate Because | Transfers the conversation to a pool of agents. Escalate passes the conversation without displaying a reason. Escalate because passes a user-defined comment to display when the escalation is viewed. |
| Send | Tells Amelia to send a message to the user interface |
| Close the conversation | Allows Amelia to close a conversation with a user |

## Outgoing Edge Transitions
Because Ask tasks generate responses from the user, the outbound flow from an Ask task uses edge notation to define any conditions. For example, if the question requires a yes or no answer, the task will have at least two edges, one for yes and one for no, that flow out to different tasks. One edge flow condition will test for cases where the user answers *yes*. The second edge flow condition will test for answers that are *no*.
In this example, the Expression value refers to the response object with the simple syntax of `response:yes()` with `yes()` a function calling the standard classifier with many different ways to say yes. The no outgoing flow line uses `response:no()` for its expression value. The `response:yes()` syntax uses a `service:function()` structure with *response* as one of several services which have one or more functions. These are described in more detail in the [Edge Notation](Process-Flows-and-Edge-Notation_11939503.html#ProcessFlowsandEdgeNotation-EdgeNotationFlows) section of the [Process Flows](Process%20Flows%20and%20Edge%20Notation) page.
The user response to an Ask task is captured in a response object available to tasks within the BPN model. The response can be used to test conditions on the outbound edge of an Ask task.
Edge notation is placed in the Properties Panel for the outbound flow line from an Ask task. Edge notation uses a Name which appears above or to the side of a flow line and an Expression used by the BPN model but not visible. This makes it easier to read a BPN process.
![](attachments/11939422/11941411.png)
Figure. Flow Line Properties Panel from an Ask task Edge
> [!warning]  
>
> Ask task and Gateway edges operate differently. Because Ask tasks capture user input from a conversation with Amelia, they have a wider range of dialogue-related context available than gateways. For example, the outbound process flow from an Ask task can evaluate the slot code retrieved by the Ask task. A gateway evaluating the same slot code would be out of context.

## BPN Variables
When a BPN model runs, two sets of variables are stored inside the BPN runtime process instance. These variables capture data needed for BPN operation and to complete any tasks. Variables are available through Script tasks.

| Variable | Description |
| ----|----|
| bpnVariableService | Available in Script tasks as an execution objectPersistent storage serviceSupports primitive types and serializable objects (boolean, char, short, int, long, Double, byte array, serializable objects). Only serializable map is supported. Each entry value must be serializable. |
| transientVariableService | Available in Script tasks with transientVariableServiceNon-persistent memory storageUsed for custom UI variables and sensitive data variables for security reasons, for example, Social Security NumbersSupports all types of variablesNot necessary to serialize for object |

## Domain Switching
In some cases, Amelia is configured with multiple domains to handle multiple possible conversation topics. One domain might be configured for insurance quotes and another domain to handle credit card applications. Amelia can switch between these topics and their domains as a conversation unfolds. The Predict workspace link, available by clicking the Amelia Trainer link on the left side of Amelia's administration pages, provides insight into which domains are triggered by different utterances.
In addition to creating domains and populating them with data, Ask tasks within a BPN need to have their Allow domain switch property set to Yes.
## Context Switching
Amelia can switch contexts in a single conversation, for example, switching to a car insurance process if the user suddenly asks for car insurance help in a conversation about home insurance. Amelia switches back to the original conversation intent and context, home insurance, when the user completes their second intent, signing up for car insurance.
Designing a BPN process with Ask and Say tasks plus context switching requires careful analysis and planning. When a context switch to another BPN occurs then completes, Amelia moves back to the previous BPN task. If the previous task is null, Amelia will resume at a StartEvent task. Otherwise, she resumes the earlier process with one move forward from the task where the switch happened. If she resumes on a Say or Ask task, however, the task Amelia resumes on isn't spoken again because Amelia has consumed the message earlier in the first pass through the process before the context switch.
This can lead a BPN to work on a first pass, switch context, and then return to the original BPN process, only to fail on the second pass if Amelia resumes on an Ask task or flow line that requires a condition to proceed. Because Amelia has processed the Ask task in the first pass through, she won't speak the task she lands on. The user won't know what Amelia expects.
To avoid this second pass problem, analyze the BPN process flow to add a Say task or an Ask task – accessible without conditions – immediately after the task where the context switch happens.
![](attachments/11939422/25462611.png)
Figure. Sample BPN to Demonstrate Intent Switching
The sample BPN above demonstrates how Amelia handles context switching when the conversation, on the left, determines what happens within the two BPNs on the right side Process Memory workspace.
1.  The conversation is partially complete. Amelia asks a question from the Ask task marked C.
2.  The user responds with a "no" which triggers the BPN conditional flow C1.
3.  Amelia responds by asking again the question from Ask task B.
4.  The user responds with a non sequitur, "Let's go see a panda," which has nothing to do with favorite colors (Ask task B) or email addresses (Ask task C).
5.  Amelia responds by switching context at Ask task B to the Say task 1 in the second BPN.
6.  When the second BPN completes, after speaking the Say task, Amelia moves to the next task after the task that triggered the context switch. Since the context switched with Ask task B, Amelia tries to move to Ask task C through the C1 condition. Amelia does not move from left to right from Ask task B to Ask task C.
7.  Because Amelia cannot reach Ask task C she does nothing. The user provokes her by answering with their favorite color.
8.  Amelia responds by describing her problem indirectly: she's trying to get to Ask task C through the C1 flow but cannot get through the flow. She responds that she's looking for a no (C1) or yes (C2).
One possible solution to this problem is to have the C1 flow terminate in a Say task that says, "Let's try this again" and connect that Say task to Ask task B without conditions. When context shifts back to the first BPN, dropping in at the context switch point at Ask task B, Amelia will choose the Say task, "Let's try this again" then move to Ask task B. Amelia will not speak the "Let's try this again" Say task because she has already processed and spoke the task before the context switch. Instead, Amelia will process then speak Ask task B.
![](attachments/11939422/25462714.png)
Figure. Sample BPN with Possible Context Switching Solution
# Ask Task
The Ask task instructs Amelia to ask questions and request entity slot names.
## Ask Task Syntax
The Ask task instructs Amelia to ask the user a question. Questions are placed between double quotes, for example, *ask "what is your first name?"* to prompt the person's first name. 
To ask for an entity slot name defined with the Entities link and workspace visible by clicking the Amelia Trainer link, the syntax is *ask for the slot \<slot_code\>* with no quotes where slot_code is the Code value set in the Entities workspace.
![](attachments/11939422/11941671.png)
Figure. Two Ask task Syntax Examples
> [!warning]  
>
> The best way to capture and use user input is to use slot entities in a Say task and edge notation with [Service prefixes](Service%20Prefixes), for example, `say `` ${ctx:latestSlot('slot_name_here").value()}` or `slot:value.matches('red')` for a flow line. While a Say task or edge notation using `${response}` will display the correct user response in most cases, slot entities ensure accurate display and evaluation with edge notation.

## Ask Task Properties Panel
The Ask task Properties Panel has settings used to configure its behavior. To display the properties panel, select or create an Ask task then click the Properties Panel rectangle at the right edge of the Process Knowledge workspace.
![](attachments/11939422/11941048.png)
Figure. BPN Ask task Properties Panel
Table. BPN Ask task Properties Panel Elements
<table class="wrapped relative-table confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 15%" />
<col style="width: 84%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Ask task Property</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Name</td>
<td class="confluenceTd">This field contains the text input into the user task.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Question</td>
<td class="confluenceTd">This dropdown list only appears when the Ask task requests an entity slot. The elements in the dropdown list are defined in the Amelia Trainer administration pages, the Entity List section, when editing an entity. Questions are added at the bottom left of an edit entity page.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Question Selection Policy</td>
<td class="confluenceTd">This setting is for entity slots defined with multiple questions for Amelia to ask. Fixed will use only the question selected in the Question setting above. Round-robin will select a question in the order they're listed in the entity slot definition page. Random will select a question randomly.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow others to respond on dialog act(s)</td>
<td class="confluenceTd"><p>When a user utterance should not trigger a BPN action – for example, the user says, "Hold on" or "Sounds good" – none, one, some, or all possible dialog acts can be set to trigger instead of the BPN. Control is passed back to the BPN after the dialog act responds and the Ask task repeats its statement or question. There are dialog acts that can be activated or disabled.</p>
<p><strong>Apology</strong> – apologies ("Sorry", "I apologize", "My mistake")<br />
<strong>Auto feedback negative</strong> – user doesn't understand Amelia ("I don't understand")<br />
<strong>Downplay</strong> – responses to apologies ("No problem", "It was nothing", "Don't worry about it")<br />
Greeting - user greets Amelia ("Hello!")<br />
<strong>Pause</strong> – pause the conversation ("Hold on", "One minute while I check on that")<br />
<strong>Thanking</strong> – a thank you ("Thanks so much", "I appreciate it")<br />
<strong>Thanking Reply</strong> – response to a thanking ("You're welcome")</p>
<p>To test this feature, select the Semantic Memory tab of the Mind view when conversing with Amelia in the standard chat interface. Any triggered Dialog Act will display at the top right of the Semantic Memory panel.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">If imperative allow others to respond</td>
<td class="confluenceTd">If set to Yes, allow other subsystems to respond if user response is a command or request. Can trigger Amelia to escalate if she can't understand or answer. Selecting No overrides this behavior.</td>
</tr>
<tr class="even">
<td class="confluenceTd">If interrogative allow others to respond</td>
<td class="confluenceTd">If set to Yes, allow other subsystems to respond if user response is a question. Can trigger Amelia to escalate if she can't understand or answer. Selecting No overrides this behavior.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">If declarative allow others to respond</td>
<td class="confluenceTd">If set to Yes, allow other subsystems to respond if user response is a declarative statement. Can trigger Amelia to escalate if she can't understand or answer. Selecting No overrides this behavior.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow intent switch</td>
<td class="confluenceTd">If set to yes, allow Amelia to switch intents as she works through a conversation. The Intents Settings workspace for an intent includes the ability to define what Amelia says when she switches back to the intent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Allow domain switch</td>
<td class="confluenceTd">If set to Yes, allow Amelia to switch to this BPN if a conversation results in her switching to this domain and BPN. The likelihood of domain switching can be determined in the Predict workspace link visible by clicking the Amelia Trainer navigation link on the left side of Amelia's administration pages. Yes is the default.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow cancel dialog act</td>
<td class="confluenceTd">If set to yes, if the user responds with the word cancel or similar cancel dialogue act, Amelia will stop processing the user response. If no, Amelia will handle the user response if the user responds with a cancel dialogue act. Yes is the default.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Ask Behavior (1st pass)</td>
<td class="confluenceTd">The options for this drop-down are Confirm (default), Always Ask, and Ignore if Responded. This will guide Amelia as to how she should ask the question to the user if she already has data for this question in her Neural Ontology (NONT). For example, with the ask task of "ask what is the user's invoice number", and existing data in the NONT of "invoice number -&gt; 123456", Amelia will ask the user "Is your invoice number 123456?" if "Confirm" is selected in the drop-down. With "Always Ask", Amelia would ask "What is your invoice number?" With "Ignore if Responded," Amelia will simply not ask a question.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Ask Behavior (subsequent)</td>
<td class="confluenceTd">This field is similar to the above Ask Behavior, except it determines the Ask Behavior for subsequent uses of the ask user task. This is useful if you would like to change Amelia's Ask Behavior for use during loops.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Confirmation question</td>
<td class="confluenceTd">Question to be asked when the slot associated with the Ask task is already filled and the selected behavior is Confirm.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Maximum consecutive attempts</td>
<td class="confluenceTd">The maximum number of attempts at executing an Ask task back-to-back. Consecutive task executions occur when the user utterance does not satisfy any of the task conditions, and the task is re-executed. The value for this property may be 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, or infinity. The default value for this property is 2. Once the number of consecutive attempts to execute an ask task surpasses the value configured for the task, the conversation gets escalated immediately.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Choice Similarity Algorithm</td>
<td class="confluenceTd"><p>Select an algorithm used to generate a dialog around the available choices stemming from an Ask task, to guide the user to one choice. The options for this drop-down are the search matching algorithms Fuzzy (default), Levenshtein Distance, Cosine Distance, Entailment, and Word Mover's Distance.</p>
<p>There are two categories of similarity algorithm, edit distance (Fuzzy, Levenshtein distance, and Cosine Distance) and semantic similarity (entailment and Word Mover’s distance). Edit distance algorithms provide good string matching capabilities but lack semantic awareness. Semantic similarity algorithms have a better grasp on semantics. They can tell "My name is John" is equivalent to "John is my name," a connection some edit distance algorithms cannot identify. However, semantic similarity algorithms are dependent on data used to train them.</p>
<div class="table-wrap">
<pre class="table"><code>| Algorithm | Description |
| ----|----|
| Fuzzy | The most common application of approximate matches until recently has been;spell checking |
| Levenshtein Distance | In approximate string matching, the objective is to find matches for short strings in many longer texts, in situations where a small number of differences is to be expected. The short strings could come from a dictionary, for instance. Here, one of the strings is typically short, while the other is arbitrarily long. This has a wide range of applications, for instance,;spell checker.The Levenshtein distance can also be computed between two longer strings, but the cost to compute it, which is roughly proportional to the product of the two string lengths, makes this impractical. |
| Cosine Distance | Computes the dot product of two nonzero vectors |
| Entailment | Entailment measures, if one sentence can be inferred from the other. It;estimates the strength of the semantic relationship between units of language, concepts or instances, through a numerical description obtained according to the comparison of information supporting their meaning or describing their nature. |
| Word Mover&#39;s Distance | Word embeddings that learn semantically meaningful representations for words from local cooccurrences in sentences. The WMD distance measures the dissimilarity between two text documents as the minimum amount of distance that the embedded words of one document need to “travel” to reach the embedded words of another document. |</code></pre>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">Form data variable</td>
<td class="confluenceTd">The form data variable connects a variable defined in a Script task task to data captured by an Ask task that follows. For example, a Script task could define a section to display in the Amelia chat interface that builds then displays a data set needed to create a car insurance quote. To capture car model information, the Script task would create a variable to store car model data then the BPN model would match the variable name in the script to an Ask task that collects car model data as a form data variable from the user response.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Allow for intent detection in form input</td>
<td class="confluenceTd">If set to yes, intent detection would be enabled for the option selection on the form.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow outbound backjumps</td>
<td class="confluenceTd">If set to Yes, this property indicates backjumps from this task will always be allowed. Yes is the default.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Outbound backjump strategy</td>
<td class="confluenceTd"><p>Backjumping is a search for an Ask task whose slot was modified by the user’s response to the current Ask task. Two search strategies accommodate the most common use cases:</p>
<ul>
<li>Nearest affected task – searches for the nearest modified (affected) task in the execution path.</li>
<li>Farthest affected task – searches for the farthest modified (affected) task in the execution path.</li>
</ul>
<p>Unlike the stochastic BPN algorithm in earlier versions of Amelia, these algorithms perform searches intra and inter-process. Nearest affected task is the default.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow inbound backjumps</td>
<td class="confluenceTd">If set to Yes, this property indicates backjumps landing on this task will always be allowed. Yes is the default.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Object names</td>
<td class="confluenceTd">This option is deprecated in V3. Refers to an object name dictionary containing all possible object names (nouns).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Hint Text</td>
<td class="confluenceTd">Text that appears in the chat interface to help define what user response is expected for the Ask task.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Secure user input</td>
<td class="confluenceTd">Indicates whether or not the response to the Ask task contains secure information or not, for example, social security numbers.</td>
</tr>
</tbody>
</table>
## Entities and Ask Tasks
Entities are data used to resolve user intent or goal in a conversation. For example, a street address is an entity needed to ship goods. Amelia makes it easier to connect entities with BPNs using an Ask task. In addition, one or more questions can be predefined as part of the entity definition. While the Train Amelia guide has more details about [working with entities](Entities%20List), connecting an entity to an Ask task is not complicated.
In the Amelia administration pages, click the Amelia Trainer navigation link on the left side then click the Entities link. Click the Add Entities tab at the far right of the Entities workspace to display a form to add entities. Type the Name, Code, Datum Type, and Description. The Code field is the name used in a BPN Ask task. To save, click the Add button. Or alternately, click the upload button or drop a file on the Upload Entities area to add a CSV file of questions and/or answers.
![](attachments/11939422/11939424.png)
Figure. Add Entities Tab for Use in Ask Tasks
Once the entity is added, click the name or Pencil icon to the right of its name in the list on the Entities workspace. The Entity Settings page appears. Scroll down to the Question area at the bottom of the form and enter one or more questions Amelia should ask in a conversation to retrieve the entity information.
![](attachments/11939422/11939423.png)
Figure. Add Questions to Entity for Use in Ask Tasks
These questions appear in the Ask task property panel as a Question dropdown list when the Ask task is selected and the property panel toggled open.
![](attachments/11939422/11939468.png)
Figure. Entity Questions Linked to Ask Task Property Panel
Once an entity is linked to an Ask task, the next step is to capture the entity value when the person responds to Amelia's question asking for it. The most direct way is to use the context service prefix, ctx, and specify the entity slot as the value to capture the user response, then assign the value to a variable. For example, this Say task text:
``` bash
say your first name is ${ctx:slot("full_name").value().firstName()}
```
![](attachments/11939422/11939443.png)
Figure. Entity Captured in an Ask Task and Expressed in a Say Task
Once saved and deployed, from the Amelia chat window, run the workflow and provide a name with three words, for example, Jane Emily Doe. Amelia will respond with the first word as your first name using the `${ctx:slot("full_name").value().firstName()}` notation in the Say task.
The context service prefix syntax also could be used to define a flow with edge notation, in the Expression field of the Properties Panel for the flow. The [Process Flows page](Process%20Flows%20and%20Edge%20Notation) describes edge notation in more detail.
Script tasks also can be used to capture an entity slot value for use elsewhere in the BPN process.
Refer to the [Amelia Trainer Guide](Amelia%20Trainer%20Guide) for more details about how to create entities, including using them to create conceptual models for Amelia to use in conversations.
## Backjumps to Handle Conversation Changes
Until this version of Amelia software, stochastic BPNs have been used to manage jumps in a conversation when users changed the subject. Stochastic BPNs had multiple paths to handle multiple possible jumps for a topic.
With Amelia 3.7, the dynamic functionality of stochastic BPNs has been transferred to Ask tasks. These tasks can be set to handle jumps caused when users change a conversation topic. Amelia evaluates all Ask tasks as a conversation progresses and decides which Ask task is appropriate based on the latest user utterance. This approach avoids unpredictability caused using spread activation logic to determine landing points in a BPN.
The ability to jump around a BPN is defined with three backjump settings for Ask tasks. The settings determine whether or not a jump can be made from an Ask task, to an Ask task, and the overall strategy for Amelia to use when determining how to handle conversation changes. The stochastic BPN type is no longer available.
![](attachments/11939422/11941742.png)
Figure. Ask Task Backjump Property Settings
Table. Ask Task Backjump Property Setting Definitions

| Ask Task Property | Description |
| ----|----|
| Allow outbound backjumps | If set to Yes, this property indicates backjumps from this task will always be allowed. Yes is the default. |
| Outbound backjump strategy | Backjumping is a search for an Ask task whose slot was modified by the user’s response to the current Ask task. Two search strategies accommodate the most common use cases:Nearest affected task – searches for the nearest modified (affected) task in the execution path.Farthest affected task – searches for the farthest modified (affected) task in the execution path.Unlike the stochastic BPN algorithm in earlier versions of Amelia, these algorithms perform searches intra and inter-process. Nearest affected task is the default. |
| Allow inbound backjumps | If set to Yes, this property indicates backjumps landing on this task will always be allowed. Yes is the default. |

# Say Task
Say tasks are used by Amelia to share information in a conversation. Simple statements can be placed in double quotes while longer statements can be included either in a variable in a preceding script task or placed as text between quotes. Variables in a script task also can be used to output data as an HTML table, list, or other useful format.
**![](attachments/11939422/11939456.png)  
**
Figure. Three Examples of Say tasks
If Amelia spells out bits of data, for example, a Vehicle Identification Number (VIN) for a car, the VIN is surrounded by open and closed \<spell\>1234567890\</spell\> tags. Currently, Amelia will display the open and close spell tags within the conversation area.
SAPI XML TTS Tags can also be used to control how Amelia pronounces the text in the Say task. This link is for an XML TTS tutorial: <https://msdn.microsoft.com/en-us/library/ms717077(v=vs.85).aspx>.
# Set the Variable Task
The Set the Variable task stores a value in the variable specified for the scope of the current BPN execution. Variables also are set with Script tasks. Variables can store custom values, the results of calculations and/or integrations, and user utterances captured as slot entities.
![](attachments/11939422/11939447.png)
Figure. Two Examples of Set the Variable tasks
# Unset the Variable Task
The Unset the variable task deletes the variable specified in the scope of the current BPN execution.
![](attachments/11939422/11939455.png)
Figure. Example of Unset the Variable Task task
# Run the Workflow Task
The Run the Workflow task continues the current thread of execution in a different workflow. This separate workflow, or sub-BPN workflow, is executed in the manner of a subroutine. When the sub-BPN workflow execution is run to completion, the flow will continue from the Run the Workflow task in the parent wrapper BPN. The sub-BPN workflow referred to must be an approved and deployed workflow located in the same Amelia environment and domain as the parent.
This example shows a sub-BPN called doSubBPNChild run from a wrapper parent workflow. The sub-BPN also sets a variable *success* which is available to the wrapper BPN.
![](attachments/11939422/11939454.png)
Figure. Example of Run the Workflow task Parent Tasks
![](attachments/11939422/11939453.png)
Figure. Example of Run the Workflow task doSubBPNChild Tasks
# Run the Integration Flow Task
Amelia V3 has an integration framework allowing full flexibility to orchestrate and control external systems via APIs and Web services. Integration involves using the Apache Camel standard to create an integration flow in the Integrations section of Amelia's administration pages, calling the integration flow name from a BPN task, parsing the output with a Script task, and then referencing the flow and its output(s) in one or more BPN tasks.
While the Integration guide describes the integration process in detail, this example shows Run the Integration Flow task, Script task, and a task to output results. The integration uses the Yahoo weather API. The step by step instructions for this integration are described in [the Integrations Guide](Integrations%20Guide).
![](attachments/11939422/11939441.png)
Figure. Example of Run the Integration Workflow task
> [!warning]  
>
> Script tasks also can use the [Integration Service](Integration%20Service) to interact with integration flows, in some cases, removing the need for the Run the Integration Flow task.

# Run the rpa bot Task
With the release of Amelia 3.7.26, 1RPA bots can be called by Amelia within a BPN. The syntax is `run the rpa bot bot_name` where `bot_name` is the name of a bot in a 1RPA instance configured for the Amelia instance. When this task is run by Amelia, she waits until the 1RPA bot returns a SUCCESS or FAIL status.
1RPA instances are configured with the 1RPA Instances workspace found by clicking the System Settings link, on the left side of Amelia's administration pages, then clicking the 1Rpa Instances link. See [1Rpa Instances](1Rpa%20Instances) for configuration details.
# Request Task
The Request task allows people to upload files during a conversation with Amelia. Files are uploaded to an existing bucket created with the Content Manager link that appears after clicking the Process Memory link in Amelia's administration page.
## Syntax 
There are two possible syntax structures for the Request task. One syntax structure identifies a variable name to use with the uploaded file. A second structure does not assign a variable name and uses instead the original variable name used by Request tasks, uploaded_resources. The third structure allows uploads for a variety of resource file types.
-   request \[a\|an\|one\] \<resource_type\> and store into\|in \<bucket_name\>
-   request \[a\|an\|one\] \<resource_type\> identified by \<variable_name\> and store into\|in \<bucket_name\>
-   request \[a\] resource\[s\] with extension \[identified by \] and store into\|to
> [!warning]  
>
> The `resource` type allows Amelia to request file uploads of a variety of file types independent of file type. For example, the Request task syntax `request resources with extension xls, bmp, pdf` would allow users to upload files of only these specified file types.
>
> When typing the Request task syntax, type a space then press the Ctrl/Control and space bar to display options, for example, all possible resource file types.

Table. Syntax Examples for Multiple File Uploads

| Syntax Element | Description |
| ----|----|
| resource_type | A type of resource(s) to upload. There are several supported resource types:audio;-  wav, mp3, ac3, oggbinary - any file extensiondocument  - doc, docx, odt, pdf, rtf, ps, epsexcel - xls, xlsxhtml - html, htm, xhtmlimage - jpeg, jpg, png, gif, tif, tiff, svg, emf, bmp, wmf, ps, epsoffice - xls, xlsx, ods, doc, docx, odt, rtf, pps, ppt, ppsx, pptx, keypresentation -  pps, ppt, ppsx, pptx, keyspreadsheet - xls, xlsx, odstext - txt, csv, md, rtfvideo - mov, mpeg, mpg, mp4, ogv, ogg, m4v, 3gp, flvword - doc, docx |
| bucket_name | A name of the bucket where resource(s) will be stored |
| variable_name | A variable name to store information;pertaining to the uploaded resources for future use.Whether or not a variable name is provided, the uploaded resource information will be stored in a variable named uploaded_resources |

## Single and Multiple File Syntax
Use of the *a* or *an* or *one* article syntax limits the file upload to a single file. To allow multiple file upload do not use the article before resource type.
Table. Syntax Examples for Multiple File Uploads

| Example | Syntax |
| ----|----|
| Upload single document and save it into "docs" bucket | request a document and store into docs |
| Upload multiple documents and save it into "docs" bucket. Also create "files" variable. | request documents identified by files and store into docs |
| Upload multiple presentations and save them into "user.docs" bucket | request presentations and store into user.docs |
| Upload Excel file, create "user_doc" variable and save it into "user.doc" bucket | request an excel identified by user_doc and store into user.doc |
| Upload single resource with some file extensions and save it into "images" bucket | request a resource with extension jpg, pdf and store into docs |
| Upload multiple resources with some file extensions and save it into "images" bucket. Also create "files" variable. | request resources with extension jpg, pdf identified by files and store into docs |

## Request Properties Panel
The Request task properties panel has an option to provide a Cancel button as part of the file upload overlay that appears in the conversation area. Set the Cancellable setting to Yes to add a Cancel button. The panel also includes the ability to provide hint text, for example, to indicate what file types are acceptable.
In addition, there should be two outgoing edges from a Request task, one default edge to handle upload failures and a second edge to test for upload success. Both edges should lead to tasks that convey the status of the upload.
![](attachments/11939422/11939469.png)
Figure. Example of Request Task Edge Properties
## Service Prefix and Functions
The Request task includes a service prefix and functions which can be used in edge notation, for example, to take one flow path if the file uploaded successfully and a second flow path if the file upload was canceled. These are set in the flow properties panel as appropriate, as described in the Process Flow section.
Table. Service Prefix:Function() for Request Tasks

| Prefix:Function() | Description |
| ----|----|
| upload:succeeded() | evaluates to true if the resources have been successfully uploaded |
| upload:canceled() | evaluates to true if the resource upload has been canceled |

> [!info]  
>
> All Request tasks should include a success flow and a cancel flow from their edges. Otherwise, Amelia may not deploy the BPN.

## Variable Properties
A stored variable from a Request task represents an array of objects containing metadata about a bucket and uploaded file. Several properties of uploaded objects are available to scripts, tasks, and flows within a BPN model. Whether or not a variable is defined in a Request task, metadata is available with the uploaded_resources variable.
Table. Uploaded Object Properties for Request Tasks

| Property | Description |
| ----|----|
| bucketId | bucket ID |
| bucketName | bucket Name |
| objectId | uploaded resource metadata ID |
| objectName | uploaded resource name |
| contentType | resource content type |
| contentLength | resource length |
| contentDisposition | resource content disposition |
| contentMd5 | resource MD5 |
| httpContentDisposition | content disposition mappable to;RFC 2616 ("INLINE" or "ATTACHMENT") |
| scope | scope to which an object is associated ("CONVERSATION" or "SYSTEM") |
| url | URL to get direct access to the resource |

Table. Uploaded Object Properties Examples for Request Tasks

| Example | Syntax |
| ----|----|
| Get a number of uploaded resources | <variable_name>.length |
| Get bucket name of an uploaded resource | <variable_name>[0].bucketName() |

## Request Task Example
This BPN example includes elements described above in this section.
Figure. Request Task 
This BPN example also uses Groovy code for the Script task. Replace test_var with uploaded_resources to confirm both the defined variable test_var and the default variable uploaded_resources contain the same information.
``` groovy
//replace domain-path-to-amelia-instance with base URL (e.g. https://site.com/Amelia)
def baseURL = "domain-path-to-amelia-instance";
resources = execution.getVariable('test_var');
cmObjectMetadataId = resources[0].objectId;
url = cmService.getResourceUrl(cmObjectMetadataId);
fullURL = baseURL + url;
execution.setVariable('url', url);
execution.setVariable('full_url', fullURL);
```
This example is described as a step by step tutorial at the bottom of Content Management Service.
## File Upload Limitations
The application.properties files used by Amelia include two settings that limit the size of files uploaded with a Request task:
-   amelia.file.maxsize
-   amelia.file.maxsize.allowed
Both settings default to 20MB unless set to lower values. The amelia.file.maxsize setting limits the size of individual files uploaded in the chat box. The amelia.file.maxsize.allowed setting limits the size of files uploaded anywhere in the Amelia system. The amelia.file.maxsize.allowed setting always overrides the amelia.file.maxsize setting if, for example, the limit for chat box uploads (amelia.file.maxsize) is greater than the amelia.file.maxsize.allowed limit.
## Media File URLs
While using a Script task to capture the full media URL then copy/pasting the URL in a web browser will display the uploaded image, the image will not appear in the Buckets workspace. Amelia V3 has two scopes for multimedia files, system and conversation. System scope includes files uploaded and created in the Buckets workspace. Conversation scope includes files uploaded and managed as part of a conversation controlled by a BPN process. BPNs look for multimedia files first in the conversation scope and, if not found, search the system Buckets.
# Content Manager Buckets and File Storage
Files uploaded with the Request task and downloaded with the Present task are both stored by Amelia in Buckets. These are locations created to store files. Buckets are found in Amelia's administration pages, under the Process Memory left side navigation link and its Content Manager secondary link.
> [!warning]  
>
> In cases where a resource with the same name resides in buckets with the same name both on the admin portal and in the conversation, the resource from the conversation bucket would hold precedence.

1.  Click the Process Memory and Content Manager links to display the Buckets workspace.
2.  To create a bucket, click the Create plus button near the top left of the workspace. A Create New Bucket popup appears. Type a name then click the Create button to save.
    1.  Bucket names can be between 3 and 63 characters long and contain only lower-case characters, numbers, periods, and dashes
    2.  Each name must start with a lowercase letter or a number
    3.  Names cannot contain underscores, end with a dash, have consecutive periods, or use dashes adjacent to periods
    4.  An IP address (e.g. 1.1.1.1) cannot be used as a name
3.  Click the new bucket name to open a Resources page for the bucket.
4.  To upload a file into the new bucket, click the Upload button at the top left of the workspace.  
    To create an HTML document in the new bucket, click the Create Document link above the list of resources. A Create New Document popup appears. Type a resource name for the new file. The file displays in the bucket. Click the file resource name to open an HTML editor to enter content. HTML file names must include the extension in the name, for example, htmlDoc.html for an HTML file name.  
    To Update a file or Rename a file, click the stacked three dot icon at the far right side of a row to display a menu.
To delete a bucket, first click the name from the list on the Bucket workspace to open it. Delete all files within the bucket. Return to the Bucket workspace and select the check box to the left of the bucket name. A Delete link appears next to the Create link directly above the list of bucket names. Click the Delete link to delete the empty bucket.
Resources also can be renamed and a static URL for the resource can be copied, as described in the table below.
![](attachments/11939422/11942876.png)
Figure. Content Manager Buckets Workspace to Store Files for Request and Present Tasks
Table. Content Manager File Options

| Option | Description |
| ----|----|
| Update | Click to update an existing resource by uploading a new file to overwrite the existing file. |
| Rename | Click to rename the resource file. |
| Copy admin URL | Click to copy to the clipboard a URL to a resource that uses the Amelia admin environment. To use this URL, the person must have access to the administration pages. |
| Copy conversation URL | Click to copy to the clipboard a URL to a resource that uses a generic Amelia file path available to anyone during a conversation with Amelia. The URL can be included in Script tasks and other elements used to create her conversations. |

![](attachments/11939422/11939431.png)
Figure. Content Manager Bucket Resources Page with HTML Editor
# Present Task
The Present task lets Amelia to display a mix of file, popup, and link to share resources to people during a conversation. Resources can be downloaded in some cases. Display of resources can be configured different ways. Resources are stored in the Content Manager area of Amelia's administration pages, as described immediately above in [Content Manager Buckets and File Storage](https://docs.ipsoft.com/display/AmeliaDocsV3/BPN+Tasks#BPNTasks-BucketsandFileStorage) for the Request task.
## Syntax
The Present task syntax is straightforward:
`present from `
Table. Present Task Syntax

| Syntax Element | Description |
| ----|----|
| resource_name | These media types are currently preview-able:IMAGE/JPEGIMAGE/GIFIMAGE/SVGIMAGE/BMPIMAGE/PNGDOCUMENT/PDFTEXT/HTMLTEXT/XHTMLOther media types can only be downloaded |
| bucket_name | The name of the bucket the resource is stored in. Files must be in the specified bucket, either prior to the conversation or earlier in a conversation. |

![](attachments/11939422/11939466.png)
Figure. Example of Present Task Syntax and Properties Panel Settings
## Present Properties Panel
Properties Panel settings for the Present task sets display options, for example, whether or not to display the file name and size.
Table. Properties Panel Options for Present Task

| Property Setting | Option Description |
| ----|----|
| Name | Text in the BPN task. The syntax is present <resource_name> from <bucket_name>. |
| Display file name | Display the file name underneath the resource. Options are Yes or No. |
| Display file size | Display the file size details underneath the resource. Options are Yes or No. |
| Aspect Ratio | The aspect ratio to use to display the video. Options are auto (default), 16:9, 4:3, 21:9, 14:10, and 19:10. |
| Mute | Play the audio or video file with sound muted. Options are Yes or No. |
| Title | Title of the resource being presented. |
| Description | Description of the resource being presented. |

# Escalate and Escalate Because Task
The Escalate and Escalate Because tasks end the BPN flow and transfer the conversation with the end user to a pool of agents. These tasks should be used in cases where it is known that Amelia will not be able to solve the user's problem without human intervention. The Escalate Because task provides some context to the agent for the reason that Amelia escalated the conversation. The text following Escalate Because should be enclosed in double quotes. Variables may be used in the text to provide a dynamic context to the agent.
**Example 1: **escalate
**Example 2:** escalate because "the webservice for looking up invoices timed out when using the input invoice ${invoice_number}"
It is also possible to specify the code of the queue the conversation should be escalated to. The syntax is "escalate to \<queue_code\>", which may be combined with the warm handover syntax.
> [!warning]  
>
> The queue name does not need to be enclosed in quotes, since queue codes do not contain spaces. Also, if a queue matching the specified code cannot be found, the escalation will be directed to the *default queue* (associated with the user's domain(s)).

**Example 3:** escalate to L3-main
**Example 4:** escalate to L2-main because "A manual status check is needed for account ${account_number}"
As of Amelia 3.4.21, basic HTML tags can be included in the text following the because part of the Escalate Because task. The allowed HTML elements are a, b, blockquote, br, cite, code, dd, dl, dt, em, i, li, ol, p, pre, q, small, strike, strong, sub, sup, u, ul , and appropriate attributes. Links (a elements) can point to http, https, ftp, mailto, and have an enforced rel=nofollow attribute. The target=”\_blank” attribute for links is enforced to ensure clicks open content in a new browser window. The img element and its attributes are not allowed.
# Trigger the Intent Task
This task allows an intent to be triggered in a new context. This task overrides any conclusions Amelia has arrived at about the context and intent of a conversation. The task has two syntaxes to invoke an intent:
`trigger the intent <intent_code>`
`trigger the intent <intent_code> in <domain_code>`
# Complete the Context Task
This task closes the current context. All intent, entity, BPN process instance, and variables used to track Amelia's state will be preserved. Closing the context returns control to the parent context.
> [!info]  
>
> When a conversation opens, Amelia's current context is empty. As entities are filled, they are added to the current context. If an intent triggers, it creates a child context and any identified extractable entities are added to that child context.
>
> This task closes the current context, usually a child context, which may contain an intent and entities. If an intent has not triggered, this task closes the empty root context.

# Complete all Contexts Task
This task closes all contexts. All intent, entity, BPN process instance, and variables used to track Amelia's state will be preserved. Closing all contexts returns control to the root context.
> [!info]  
>
> When a conversation opens, Amelia's current context is empty. As entities are filled, they are added to the current context. If an intent triggers, it creates a child context and any identified extractable entities are added to that child context.
>
> This task recursively closes all child contexts until the empty root context is reached. Any entities extracted in the closed contexts will be ignored at the root context.

# Send Task
The send task tells Amelia to send a message to the UI. Currently, two types of message are supported, Integration and Form Data Input. As of Amelia V3.6.x, Script tasks also can send integration messages. See [Send Integration Messages with a Script Task](https://docs.ipsoft.com/display/AmeliaDocsV36/Script+Tasks#ScriptTasks-SendIntegrationMessageswithaScriptTask) for more details.
Table. Message Types for Send Task

| Send task Property | Description |
| ----|----|
| Integration Messages | Messages aimed at the UI, which can only be understood by a customer-specific user interface. Although JSON is highly recommended, any string-based payload may be conveyed by integration messages.Syntax:;send the integration message var_name, where var_name is the name of a BPN variable (execution or transient) whose value will be passed as the integration message's payload. |
| Form Input Data Messages | These messages are also sent to the UI, but have a more specific role, they are mainly used by the customer-specific UI to build interactive widgets, which send utterances on behalf of Amelia. These utterance messages may also include additional attributes that will be passed back to the process in execution.Syntax:;send form for var_name, where var_name is the name of a BPN variable (execution or transient) whose value will be passed as the form input data message's payload. |

# Close the Conversation Task
The Close the conversation task allow the current conversation to be closed by Amelia during the execution of a BPN. Once the execution flow hits the Close the Conversation task, the conversation will be closed and the subsequent tasks (if existing) will be ignored. The thread of execution is stopped and all variables and other context are not available.
**Example: **close the conversation
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-9-26_15-9-21.png](attachments/11939422/11939423.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-7-57.png](attachments/11939422/11939424.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-3-44.png](attachments/11939422/11939425.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-entities-workspace-3.6.jpg](attachments/11939422/11939426.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-4-20_15-6-22.png](attachments/11939422/11939427.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-20_12-40-32.png](attachments/11939422/11939428.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-20_10-42-53.png](attachments/11939422/11939429.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-20_10-14-11.png](attachments/11939422/11939430.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_17-9-5.png](attachments/11939422/11939431.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_17-7-47.png](attachments/11939422/11939432.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_16-48-44.png](attachments/11939422/11939433.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_16-47-39.png](attachments/11939422/11939434.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_16-45-11.png](attachments/11939422/11939435.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-3_13-6-2.png](attachments/11939422/11939436.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-3_13-5-10.png](attachments/11939422/11939437.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-3_13-4-4.png](attachments/11939422/11939438.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-3_12-57-41.png](attachments/11939422/11939439.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-6_14-55-30.png](attachments/11939422/11939440.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-13_10-26-24.png](attachments/11939422/11939441.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-19_14-22-45.png](attachments/11939422/11939442.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_12-48-0.png](attachments/11939422/11939443.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_12-47-8.png](attachments/11939422/11939444.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_12-45-44.png](attachments/11939422/11939445.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_12-45-22.png](attachments/11939422/11939446.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-26_15-2-1.png](attachments/11939422/11939447.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-40-25.png](attachments/11939422/11939448.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-40-3.png](attachments/11939422/11939449.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-39-49.png](attachments/11939422/11939450.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-39-22.png](attachments/11939422/11939451.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-39-1.png](attachments/11939422/11939452.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-38-37.png](attachments/11939422/11939453.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-38-15.png](attachments/11939422/11939454.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-37-53.png](attachments/11939422/11939455.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-37-19.png](attachments/11939422/11939456.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-36-57.png](attachments/11939422/11939457.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-36-34.png](attachments/11939422/11939458.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-35-39.png](attachments/11939422/11939459.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-35-10.png](attachments/11939422/11939460.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-34-38.png](attachments/11939422/11939461.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-34-9.png](attachments/11939422/11939462.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-33-22.png](attachments/11939422/11939463.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-33-1.png](attachments/11939422/11939464.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-9_10-45-41.png](attachments/11939422/11939465.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-9_10-41-18.png](attachments/11939422/11939466.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_16-15-56.png](attachments/11939422/11939467.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-53-31.png](attachments/11939422/11939468.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-52-48.png](attachments/11939422/11939469.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-52-1.png](attachments/11939422/11939470.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-46-36.png](attachments/11939422/11939471.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-44-14.png](attachments/11939422/11939472.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-43-37.png](attachments/11939422/11939473.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-41-56.png](attachments/11939422/11939474.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-19-28.png](attachments/11939422/11939475.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_15-14-41.png](attachments/11939422/11939476.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-16_13-16-53.png](attachments/11939422/11941048.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_14-9-25.png](attachments/11939422/11941141.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_14-10-55.png](attachments/11939422/11941142.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_14-22-31.png](attachments/11939422/11941143.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_14-31-56.png](attachments/11939422/11941144.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_14-33-21.png](attachments/11939422/11941145.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_15-33-15.png](attachments/11939422/11941151.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_16-24-52.png](attachments/11939422/11941152.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-17_16-37-9.png](attachments/11939422/11941153.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-25_14-59-12.png](attachments/11939422/11941408.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-25_15-56-22.png](attachments/11939422/11941411.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-2-4_16-38-47.png](attachments/11939422/11941671.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-2-6_9-58-22.png](attachments/11939422/11941742.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_10-32-37.png](attachments/11939422/11942870.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_11-2-20.png](attachments/11939422/11942874.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_11-4-15.png](attachments/11939422/11942876.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-13_14-2-34.png](attachments/11939422/25462611.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-13_14-20-21.png](attachments/11939422/25462612.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-13_14-31-55.png](attachments/11939422/25462614.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-13_14-45-56.png](attachments/11939422/25462618.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-18_16-23-54.png](attachments/11939422/25462714.png) (image/png)  
