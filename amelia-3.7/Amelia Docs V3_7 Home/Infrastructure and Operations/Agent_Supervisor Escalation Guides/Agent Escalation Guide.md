# Getting Started
Amelia is a cognitive software agent who performs many of the same tasks as human agents. She learns using the same information human agents use to learn. And she can access the same databases and other tools used by humans.
More than a questions and answer chat bot, Amelia understands user requests enough to complete tasks to resolve their issues. She uses conversations to sense the emotions of people as they converse with her and acts accordingly, escalating if needed. She also answers frequently asked questions at any time during a conversation.
## Interfaces
Amelia uses several key interfaces for login, conversation, monitoring her performance, and escalating conversations she can't handle.
### Login
The login screen is the entry point to access Amelia administration pages.
![](attachments/11940113/11940123.png)
Figure. Login Page
### Conversation Area
Conversations with Amelia happen with different interfaces based on the device used to connect with her. All conversation areas offer the same basic interface design and user experience.
With web pages, for example, Amelia offers users a conversation area with a speaking avatar and a customized user interface (UI) without the avatar but with a wide range of customizations. Conversations with a mobile phone or tablet interface looks similar but is optimized for smaller screens. Both types of conversation areas offer user interaction with buttons, panels, badges, alerts, and other ways to complete tasks in a conversation.
Amelia usually greets people and uses the conversation to manage their interaction. Interactions happen mostly by typing questions and responses in a chat box at the bottom of the conversation area. Amelia displays her responses as a variety of text, buttons, and other elements based on her process and the needs of the conversation. Talking about a car insurance quote, for example, might involve buttons with pictures of different car models and a panel to display information Amelia collects in a conversation.
Every conversation with Amelia has a unique conversation identifier to organize data related to the conversation. When Amelia cannot answer a question, or she senses a person is becoming upset, she will escalate the conversation to the appropriate help desk.
The conversation area with avatar also is the interface used to monitor Amelia's performance and access her administration pages.
![](attachments/11940113/11940631.jpg)
Figure. Conversation Area with Avatar
![](attachments/11940113/11940119.jpg)
Figure. Conversation Area Custom User Interface (Web and Mobile)
### Mind View
The conversation area with avatar includes a Mind link at the top right which, when clicked, displays several panels with different views of Amelia's behavior in real time. Tabs on the right display the different panels. For example, the Process Memory panel displays the BPN process Amelia uses to respond to a user request. The Affective Memory panel shows how Amelia rates the satisfaction of the person engaged in conversation with her.
![](attachments/11940113/11940126.png)
Figure. Mind View
### Process Memory and BPNs
The Process Memory panel in Mind view displays Amelia's progress through a defined Business Process Network (BPN) process. Each process is selected based upon what a person says to Amelia. Each task in a BPN captures or stores data and can access Amelia's subsystems, for example, her affective memory, semantic memory, and analytic memory. BPNs also access third party systems, for example, authenticating users and retrieving their information securely.
![](attachments/11940113/11940127.png)
Figure. Example BPN Process
BPN processes use common elements to define paths through a process, for example, a start and end point. Gateways also manage branching logic based on conversation data.
The primary element of a BPN is a task which can be user tasks, which engage users or further engagement, or script tasks. Request tasks ask users to upload a file while Say tasks direct Amelia to say something. Script tasks can capture and manipulate data which user tasks use to engage people in conversation.
Table. BPN Task Types

| Task Type | Description |
| ----|----|
| Ask | Instructs Amelia to ask the user a question |
| Say | Tells Amelia what to say to the user |
| Set the Variable | Defines the value of a variable available within the conversation and BPN model scope |
| Unset the Variable | Removes a variable from the conversation and BPN model scope |
| Run the Workflow | Instructs Amelia to continue the current activity thread into another workflow |
| Run the Integration Flow | Tells Amelia to connect to a backend system using a defined flow |
| Request | Asks the user to upload a file |
| Present | Provides the user with a link to a file or an image |
| EscalateEscalate Because
Escalate To Because | Transfers the conversation to a pool of agents. Escalate passes the conversation without displaying a reason. Escalate because passes a user-defined comment to display when the escalation is viewed. Escalate to because specifies an escalation queue for the escalation then;passes a user-defined comment. |
| Send | Tells Amelia to send a message to the user interface |
| Close the conversation | Allows Amelia to close a conversation with a user |

Some BPN elements and tools are visible only when a BPN task is selected.
![](attachments/11940113/11940128.png)
Figure. BPN Task Object Tool Icons (Script Task)
Table. BPN Elements and Task Tools

| BPN Element/Tool | Description |
| ----|----|
|  | Click create a Start event then drag into position and click to set down |
|  | Create an end event connected to the selected task by a process flow line |
|  | Create a gateway connected to the selected task by a process flow line. The default setting is exclusive but can be changed. |
|  | Create a new task connected to the selected task by a process flow line |
|  | Add a non-functional comment or note for the selected task |
|  | Modifies the active task or flow behavior. Script tasks allow processes to execute during BPN execution outside the natural language processing of tasks, for example, to display data to the user. The User, Manual Task, and Service Task selection options are not used. |
|  | Click to delete the selected task |
|  | For script tasks, click to open script dialog for editing. Available only for script tasks. |
|  | Click to attach a Flow line arrow from the selected task to anywhere in the BPN |

### Active Conversations
For Agents, clicking the Conversations link, located at the top right of the conversation area with avatar, displays all active conversations for the Amelia installation with the ability to filter by domains, queues, and agents.
![](attachments/11940113/11940122.jpg)
Figure. Active Conversations Page
Table. Active Conversation Fields
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Field</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd"><p>Domains</p></td>
<td class="confluenceTd"><p>Select a domain to filter active conversation data.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Queues</p></td>
<td class="confluenceTd"><p>Select an escalation queue to filter active conversation data.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Agent</p></td>
<td class="confluenceTd"><p>Select an agent to filter active conversation data.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Auto-Refresh</p></td>
<td class="confluenceTd"><p>Select an auto-refresh duration: 30 seconds, 1 Minute, 2 Minutes, 5 Minutes, 10 Minutes.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>My Queues</p></td>
<td class="confluenceTd"><p>Click the toggle to filter active conversations by escalation queues assigned to your login.</p></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><p>Conversations</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>ID</p></td>
<td class="confluenceTd"><p>The conversation ID. If conversation was escalated, click the + (plus) or – (minus) icon to the left of the ID to display or hide information about the escalation queue for the conversation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Domain</p></td>
<td class="confluenceTd"><p>The domain where the conversation happened.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>User</p></td>
<td class="confluenceTd"><p>The person who initiated the conversation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Agent</p></td>
<td class="confluenceTd"><p>The agent assigned to the conversation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Escalation Status</p></td>
<td class="confluenceTd"><p>Current status of the escalation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Escalation Queue</p></td>
<td class="confluenceTd"><p>If escalated, the escalation queue for the conversation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Escalation Reason</p></td>
<td class="confluenceTd"><p>If escalated, the reason for the escalation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">P-SLA</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Created</p></td>
<td class="confluenceTd"><p>Creation date for the conversation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Queued</p></td>
<td class="confluenceTd"><p>If escalated, whether or not the conversation was escalated.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Answer Speed</p></td>
<td class="confluenceTd"><p>If escalated, the time required to answer the escalation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Handle Time</p></td>
<td class="confluenceTd"><p>If escalated, the time required to respond and resolve the conversation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Actions: Pickup Conversation</p></td>
<td class="confluenceTd"><p>Click the black speech bubble icon to pick up the conversation and respond.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Actions: Observe Conversation</p></td>
<td class="confluenceTd"><p>Click the eye icon to observe the conversation.</p></td>
</tr>
</tbody>
</table>
### End User
When a conversation is picked up by an agent, the customer will see a series of messages to indicate conversation control has passed from Amelia to an agent. The agent will see the same conversation with a Close button to close the conversation when appropriate.
![](attachments/11940113/11940118.jpg)
Figure. End User View of Picked Up Conversation
When a conversation is observed, the customer does not see any indication the conversation is viewed. For agents and supervisors, the observed conversation is the same as a picked up conversation except for the Close button which does not appear and the Send button which is deactivated.
## Escalations and Notifications
Amelia escalates a conversation when:
-   A BPN process includes an Escalate task for part of the process Amelia is not being trained to complete.
-   Amelia's emotional quotient shows the person she's conversing with is upset or close to upset.
-   Any misunderstanding where Amelia expects one type of answer and receives another, for example, a noun when she expects a date or number.
Agents engage with escalation through a notification (push) or by picking up conversations on the Active Conversations page (pull). Supervisors can assign escalation requests to a queue or agent which generates a push notification.
Escalated conversations are assigned to a team and agent with a defined process. For each escalated conversation queued up:
1.  Select all teams assigned to that escalation queue
2.  Filter out teams with a non-matching schedule
Within the escalation teams with a matching schedule:
1.  Filter out users with status set to Away or Offline
2.  Filter out users whose number of active chats equals their maximum concurrent chats setting
3.  Ranks users by availability, specifically, count (active sessions)/max AgentActiveChats
4.  Route escalated conversation to agent with least number of tickets handled based on total number of handled escalations
5.  If more than one agent, randomly select agent from the list of candidates and assign to an agent
Amelia then repeats this process as needed, looking up the next escalated conversation for assignment and selecting all teams assigned to the conversation's escalation queue.
## Set Agent Status
To handle escalations, agents must log in to Amelia and set their status to Ready to handle conversations. Status is set at the top right of Amelia's conversation area. Click the current status icon to display the dropdown list of options.
![](attachments/11940113/11940117.jpg)
Figure. Status Dropdown
# Conversations
Active conversations can be displayed by clicking the Conversations link at the top right of the Amelia chat interface with an avatar or clicking the links at the top right of Amelia's administration pages. The Active Conversations page will display. Escalated conversations display a set of two buttons – Pickup and Observe -- to the far right of the row. Conversations not escalated only display the Pickup and Observe buttons. Click the plus sign to the left of a conversation to view any escalation for the conversation.
![](attachments/11940113/11940121.jpg)
Figure. Active Conversations with Escalated Conversation
![](attachments/11940113/11940120.png)
Figure. Escalation Action Buttons: Pickup, Observe
## Observe Conversations
To observe a conversation, click the eye action button at the far right of an escalation listing row.
## Pick Up Conversations
To pick up a conversation, click the speech bubble action button at the far right of an escalation listing row.
## Steal Conversations
Agents with the AUTHORITY_CONVERSATION_STEAL authority assigned to their user account have the ability to pick up (steal) chats currently assigned and handled by another agent. This authority is not granted as part of any role. This authority must be manually added to a user account.
When an agent with the authority to steal a conversation chooses to pick up an assigned conversation listed in the Conversations page, a popup warning appears to report the conversation is being handled by another agent. The popup warning includes options to observe, pickup, or cancel the conversation pick up.
![](attachments/11940113/11940115.png)
Figure. Conversation Assigned Popup Warning with Steal Option
When the agent clicks the Steal button in the popup warning, the conversation is transferred to them and away from the current agent. The current agent will be set to observation mode with no ability to chat. Amelia’s log file will state the current agent has left and the new agent has entered the conversation.
## SLA Warnings
When an escalated conversation listed on the Active Conversations page is close to violating the Pickup Service Level Agreement (P-SLA) for its queue, the row background will turn yellow and the text red. The P-SLA setting is set in the Escalation Queues workspace in the System Settings area of Amelia's administration pages.
## SLA Violations
When an escalated conversation listed on the Active Conversations page is exceeds (violates) the Pickup Service Level Agreement (P-SLA) for its queue, the row background will turn light red and the text red. The P-SLA is set in the Escalation Queues workspace in the System Settings area of Amelia's administration pages.
## Alerts
In addition to picking up conversations with the Active Conversations page, agents who are logged in with their status set to Ready will see a popup appear when an escalated conversation has been assigned to them automatically through a round robin process. The popup includes buttons to Accept or Reject the escalation.
Clicking the Accept button opens a new browser window to display the current conversation, the same as when a conversation is picked up from the Active Conversations page.
> [!warning]  
>
> The web browser may display an alert requesting permissions to display alert popups from Amelia. If this happens, allow popups to display for Amelia.

![](attachments/11940113/11940116.jpg)
Figure. Escalation Alert Popup
