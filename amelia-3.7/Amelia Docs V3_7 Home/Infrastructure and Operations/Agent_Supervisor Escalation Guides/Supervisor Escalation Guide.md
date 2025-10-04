{% version "3.x" %}
Supervisors use Amelia administration pages to manage conversations, escalations, assess performance with metrics, and export conversations. In addition, Agent/Supervisor functionality depends on the configuration of users, roles, escalation teams, escalation queues, and other settings. This guide describes how supervisors manage escalated conversations and system configuration.
# Getting Started
Amelia is a cognitive software agent who performs many of the same tasks as human agents. She learns using the same information human agents use to learn. And she can access the same databases and other tools used by humans.
More than a questions and answer chat bot, Amelia understands user requests enough to complete tasks to resolve their issues. She uses conversations to sense the emotions of people as they converse with her and acts accordingly, escalating if needed. She also answers frequently asked questions at any time during a conversation.
## Interfaces
Amelia uses several key interfaces for login, conversation, monitoring her performance, and escalating conversations she can't handle. 
### Login
The login screen is the entry point to access Amelia administration pages.
![](attachments/11940140/11940162.png)
Figure. Login Page
### Conversation Area
Conversations with Amelia happen with different interfaces based on the device used to connect with her. All conversation areas offer the same basic interface design and user experience.
With web pages, for example, Amelia offers users a conversation area with a speaking avatar and a customized user interface (UI) without the avatar but with a wide range of customizations. Conversations with a mobile phone or tablet interface looks similar but is optimized for smaller screens. Both types of conversation areas offer user interaction with buttons, panels, badges, alerts, and other ways to complete tasks in a conversation.
Amelia usually greets people and uses the conversation to manage their interaction. Interactions happen mostly by typing questions and responses in a chat box at the bottom of the conversation area. Amelia displays her responses as a variety of text, buttons, and other elements based on her process and the needs of the conversation. Talking about a car insurance quote, for example, might involve buttons with pictures of different car models and a panel to display information Amelia collects in a conversation.
Every conversation with Amelia has a unique conversation identifier to organize data related to the conversation. When Amelia cannot answer a question, or she senses a person is becoming upset, she will escalate the conversation to the appropriate help desk.
The conversation area with avatar also is the interface used to monitor Amelia's performance and access her administration pages.
![](attachments/11940140/11940634.jpg)
Figure. Conversation Area with Avatar
![](attachments/11940140/11940151.jpg)
Figure. Conversation Area Custom User Interface (Web and Mobile)
### Mind View
The conversation area with avatar includes a Mind link at the top right which, when clicked, displays several panels with different views of Amelia's behavior in real time. Tabs on the right display the different panels. For example, the Process Memory panel displays the BPN process Amelia uses to respond to a user request. The Affective Memory panel shows how Amelia rates the satisfaction of the person engaged in conversation with her.
![](attachments/11940140/11940166.png)
Figure. Mind View
### Process Memory and BPNs
The Process Memory panel in Mind view displays Amelia's progress through a defined Business Process Network (BPN) process. Each process is selected based upon what a person says to Amelia. Each task in a BPN captures or stores data and can access Amelia's subsystems, for example, her affective memory, semantic memory, and analytic memory. BPNs also access third party systems, for example, authenticating users and retrieving their information securely.
![](attachments/11940140/11940165.png)
Figure. Example BPN Process
BPN processes use common elements to define paths through a process, for example, a start and end point. Gateways also manage branching logic based on conversation data.
The primary element of a BPN is a task which can be user tasks, which engage users or further engagement, or script tasks. For example, Request tasks ask users to upload a file while Say tasks direct Amelia to say something to a user. Script tasks can capture and manipulate data which user tasks use to engage people in conversation.
Table. BPN User Task Types

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
Escalate To Because | Transfers the conversation to a pool of agents. Escalate passes the conversation without displaying a reason. Escalate because passes a user-defined comment to display when the escalation is viewed. Escalate to because specifies an escalation queue for the escalation then passes a user-defined comment. |
| Send | Tells Amelia to send a message to the user interface |
| Close the conversation | Allows Amelia to close a conversation with a user |

Some BPN elements and tools are visible only when a BPN task is selected.
![](attachments/11940140/11940164.png)
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

### Active Conversation Page
For Supervisors and Agents, clicking the Conversations link, located at the top right of the conversation area with avatar, displays all active conversations for the Amelia installation with the ability to filter by domains, queues, and agents. A link at the top right of the Active Conversations page also links to a Supervisors page and Metrics page.
![](attachments/11940140/11943505.jpg)
Figure. Active Conversations Page
Table. Active Conversation Fields
|                               |                                                                                                                                                                                                                                   |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Field                         | Description                                                                                                                                                                                                                       |
| Domains                       | Select a domain to filter active conversation data.                                                                                                                                                                               |
| Queues                        | Select an escalation queue to filter active conversation data.                                                                                                                                                                    |
| Agent                         | Select an agent to filter active conversation data.                                                                                                                                                                               |
| Auto-Refresh                  | Select an auto-refresh duration: 30 seconds, 1 Minute, 2 Minutes, 5 Minutes, 10 Minutes.                                                                                                                                          |
| My Queues                     | Click the toggle to filter active conversations by escalation queues assigned to your login.                                                                                                                                      |
| Conversations                 |                                                                                                                                                                                                                                   |
| ID                            | The conversation ID. If conversation was escalated, click the + (plus) or – (minus) icon to the left of the ID to display or hide information about the escalation queue for the conversation.                                    |
| Domain                        | The domain where the conversation happened.                                                                                                                                                                                       |
| User                          | The person who initiated the conversation.                                                                                                                                                                                        |
| Agent                         | The agent assigned to the conversation.                                                                                                                                                                                           |
| Escalation Status             | Current status of the escalation.                                                                                                                                                                                                 |
| Escalation Queue              | If escalated, the escalation queue for the conversation.                                                                                                                                                                          |
| Escalation Reason             | If escalated, the reason for the escalation.                                                                                                                                                                                      |
| P-SLA                         | The Pickup-Service Level Agreement (P-SLA) is the date and time when escalated conversations must be picked up. The P-SLA is set in the Escalation Queues workspace in the System Settings area of Amelia's administration pages. |
| Created                       | Creation date for the conversation.                                                                                                                                                                                               |
| Queued                        | If escalated, whether or not the conversation was escalated.                                                                                                                                                                      |
| Answer Speed                  | If escalated, the time required to answer the escalation.                                                                                                                                                                         |
| Handle Time                   | If escalated, the time required to respond and resolve the conversation.                                                                                                                                                          |
| Actions: Pickup Conversation  | Click the black speech bubble icon to pick up the conversation and respond.                                                                                                                                                       |
| Actions: Observe Conversation | Click the eye icon to observe the conversation.                                                                                                                                                                                   |
### Agent Supervisor Page
The Supervisors page, available from the dropdown list at the top right of the page, displays two charts and a Queue Summary table.
-   The Active Escalated Conversations chart displays Active escalated conversations and the Service Level Agreement (SLA) performance by escalation queue.
-   The Hourly Conversations chart displays conversations by hour for the past 24 hours by who handled the conversation.
-   The Queue Summary table displays agent performance, conversation, SLA performance, and other data for each escalation queue.
Fields for this page are described below in the Operations section.
![](attachments/11940140/11940170.png)
Figure. Agent Supervisor Page
### Metrics Page
The Metrics page, available from the dropdown list at the top right of the page, displays pie charts with conversations by domain, escalation queue, agent, BPN model, and BPN folder, as well as a summary table each of these filters. Conversations also can be exported using the Metrics page.
Fields for this page are described below in the Operations section.
![](attachments/11940140/11940171.png)
Figure. Metrics Page
### End User
When a conversation is picked up by an agent, the customer will see a series of messages to indicate conversation control has passed from Amelia to an agent. The agent will see the same conversation with a Close button to close the conversation when appropriate.
![](attachments/11940140/11940150.jpg)
Figure. End User View of Picked Up Conversation
When a conversation is observed, the customer does not see any indication the conversation is viewed. For agents and supervisors, the observed conversation is the same as a picked up conversation except for the Close button which does not appear and the Send button which is deactivated.
## Escalations and Notifications
Amelia escalates a conversation when:
-   A BPN process includes an Escalate task for part of the process Amelia is not being trained to complete.
-   Amelia's emotional quotient shows the person she's conversing with is upset or close to upset.
-   Any misunderstanding where Amelia expects one type of answer and receives another, for example, a noun when she expects a date or number.
Agents engage with escalation through a notification (push) or by picking up conversations on the Active Conversations page (pull). Supervisors can assign escalation requests to an agent which generates a push notification. Agents see a push notification as a popup they can click to accept the escalation request.
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
## Confirm Escalation Team is Connected
To handle escalations, agents must log in to Amelia and set their status to Ready to handle conversations. The test BPN, described at the end of this guide, can help generate escalated conversations to test the conversation is routed to the correct escalation queue, any SLA warnings are triggered, agents are available to handle escalated conversations, assign and pickup conversations, and so on.
The first step is to confirm agents are logged in and have their status set to Ready. The status dropdown is at the top right of the Amelia conversation screen and administration pages.
Refer to the Configuration section below for any issues encountered beyond agents not being logged in or their status not set to Ready.
# Conversations
Active conversations can be displayed by clicking the Conversations link at the top right of the Amelia chat interface with an avatar or clicking the links at the top right of Amelia's administration pages. The Active Conversations page will display. Escalated conversations display a set of three buttons – Pickup, Observe, and Assign -- to the far right of the row. Conversations not escalated only display the Pickup and Observe buttons. Click the plus sign to the left of a conversation to view any escalation for the conversation.
![](attachments/11940140/11943506.jpg)
Figure. Active Conversations with Escalated Conversation
![](attachments/11940140/11940160.jpg)
Figure. Three Escalation Action Buttons: Pickup, Observe, Assign
## Assign Conversations
Escalated conversations are automatically routed in a round robin process to available agents logged in with their status set to Ready, as described in the Escalations and Notifications section above. Escalated conversations also can be assigned using the Active Conversations page. This page is available by clicking the Conversations link at the top right of Amelia's conversation area or selecting Conversations from Amelia's administration pages.
To assign a conversation, click the escalation action button with two horizontal arrows at the far right of an escalation listing row. The Assign Conversation popup will appear with a list of available agents and their current active conversations. Click the radio button next to a name then click the Assign button to assign the escalated conversation and close the popup.
![](attachments/11940140/11940145.jpg)
Figure. Assign Conversation Popup
## Observe Conversations
To observe a conversation, click the eye action button at the far right of an escalation listing row.
## Pick Up Conversations
To pick up a conversation, click the speech bubble action button at the far right of an escalation listing row.
## View Conversation Escalation Logs
To view the escalation log for an escalated conversation, click the View Logs icon to the far right of the escalation details row underneath a conversation row.
![](attachments/11940140/11940148.jpg)
Figure. View Logs Icon
![](attachments/11940140/11940147.jpg)
Figure. Escalation Logs Popup
## SLA Warnings
When an escalated conversation listed on the Active Conversations page is close to violating the Pickup Service Level Agreement (P-SLA) for its queue, the row background will turn yellow and the text red. The P-SLA setting is set in the Escalation Queues workspace in the System Settings area of Amelia's administration pages.
## SLA Violations
When an escalated conversation listed on the Active Conversations page is exceeds (violates) the Pickup Service Level Agreement (P-SLA) for its queue, the row background will turn light red and the text red. The P-SLA is set in the Escalation Queues workspace in the System Settings area of Amelia's administration pages.
# Operations
In addition to managing escalated conversations, supervisors can view metrics for all conversations and export conversations. Metrics are displayed on the Supervisors and Metrics pages, both available through the dropdown list at the top right of the page. Conversations also can be exported from the Metrics page.
## Supervisors
The Supervisors page, available from the dropdown list at the top right of the page, displays two charts and a Queue Summary table.
-   The Active Escalated Conversations chart displays Active escalated conversations and the Service Level Agreement (SLA) performance by escalation queue.
-   The Hourly Conversations chart displays conversations by hour for the past 24 hours by who handled the conversation.
-   The Queue Summary table displays agent performance, conversation, SLA performance, and other data for each escalation queue.
![](attachments/11940140/11940170.png)
Figure. Agent Supervisor Page
Table. Agent Supervisor Fields

| Field | Description |
| ----|----|
| Domain | Select the domain at the top right of this workspace to filter escalation queues by domain. |
| Active Escalated Conversation | This panel displays graphic data about the escalation queue responses compared to all queues. The chart displays Active, SLA OK, SLA Warn, and SLA Critical data points.Click the repeating circle icon at the far right of this header to refresh data. |
| Hourly Conversations | This panel displays graphic data about the escalation queue responses on an hourly basis. The chart displays Amelia Handled, Amelia Abandoned, Escalate Abandoned, Agent Handled, and Agent Abandoned data points.Click the repeating circle icon at the far right of this header to refresh data. |
| Queue Summary | This panel displays chart data about the escalation queue responses.Click the repeating circle icon at the far right of this header to refresh data. |
| Queue | The name of the escalation queue. |
| Code | The domain code name |
| Current Conversations | The number of currently active conversations. |
| Ready Agents | The number of agents assigned to the escalation queue whose status is Ready. |
| Busy Agents | The number of agents assigned to the escalation queue whose status is Busy. |
| Away Agents | The number of agents assigned to the escalation queue whose status is Away. |
| Offline Agents | The number of agents assigned to the escalation queue whose status is Offline. |
| Total Conversations | The total number of conversations. |
| SLA-V | The number of conversations whose pick up time exceeded the SLA agreement time. |
| Abandoned | The total number of abandoned conversations. |
| Max Concurrent | The number of conversations started today. |
| Avg Answer Speed | The average time between escalation and agent pick up. |
| Max Answer Speed | The maximum time between escalation and agent pick up. |
| Avg Handle Time | The average time between escalation and conversation end. |
| Max Handle Time | The maximum time between escalation and agent pick up. |

## Metrics
The Metrics page, available from the dropdown list at the top right of administration pages, displays pie charts with conversations by domain, escalation queue, agent, BPN model, and BPN folder, as well as a summary table for each of these filters. Conversations also can be exported using the Export Conversations tab on the Metrics page.
Conversation data can be sorted by domain, escalation queue, agent, BPN model, and BPN folder with tabs near the top of the page. In addition, conversations can be filtered by domain and date with the two dropdowns at the top right of the Metrics page. Selecting a domain and date then clicking the Export button will download a CSV file with the filtered data for the current Metrics page tab and its displayed data.
> [!warning]  
>
> Hover the computer mouse over a pie chart to see the data source and data.

![](attachments/11940300/11940303.png)
Figure. Metrics Page
Export files for Domain, Escalation Queue, Agent, BPN Model, and BPN Folder tabs include column headings both unique and shared. Descriptions for all possible column headings are in the table below.
Table. Metric Page Column Headings

| Heading | Description |
| ----|----|
| Total | Total conversations by selected element: domain, escalation queue, agent, BPN model, or BPN folder |
| Amelia Handled | Total conversations handled completely by Amelia |
| Agent Handled | Total conversations handled by an agent |
| Escalated | Total number of escalated conversations |
| Max Concurrent | Maximum concurrent conversations for the selected time period |
| SLA Violations | The number of conversations whose pick up time exceeded (violated) the SLA agreement time. |
| Abandoned Total | Total abandoned conversations |
| Abandoned Amelia | Total conversations abandoned by Amelia |
| Abandoned Escalate | Total abandoned escalated conversations |
| Abandoned Agent | The total number of abandoned conversations by agents |
| Avg Answer Speed | The average time between escalation and agent pick up |
| Max Answer Speed | The maximum time between escalation and agent pick up |
| Avg Handle Time | The average time between escalation and conversation end |
| Max Handle Time | The maximum time between escalation and conversation end |

## Export Conversations
Conversations can be exported from the Metrics page, available from the dropdown list at the top right of the page.
1.  Click the Export Conversations tab above the pie chart graphs to display the export form.
2.  Select the date, time, and minute range for conversations to be exported.
3.  Select domains to filter conversations in or out of the exported file.
4.  Click checkboxes to include all domains, transcripts, escalation logs, and escalations not started.
5.  Click the Export button then select where to download the CSV file.
Exports can include up to 2000 conversations in each file. As a date range, domains, and other criteria are selected on the export form, the number of conversations to be exported is displayed below the Export and Reset buttons on the form.
![](attachments/11940140/11940158.png)
Figure. Export Conversations Form
![](attachments/11940140/11940156.png)
Figure. Export Form with Date, Time, Minute Selected
The exported file output includes these fields below.
Table. Metrics Export File Per-Conversation Column Names
<table class="relative-table wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Column Name</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Conversation Id</td>
<td class="confluenceTd">The internal ID of the conversation.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Created</td>
<td class="confluenceTd">Date/Time the conversation started (UTC).</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Finished</td>
<td class="confluenceTd">Date/Time the conversation finished (UTC).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Status</td>
<td class="confluenceTd">Final status of conversation.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Primary Agent Email</td>
<td class="confluenceTd">Email of the agent (besides Amelia) who communicated most with the user, if any.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Primary Agent Handle Time</td>
<td class="confluenceTd">Duration from pickup to time of last utterance from the user or agent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Primary Agent Answer Speed</td>
<td class="confluenceTd">Duration between escalation creation and time of pickup.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Pickup SLA Violation</td>
<td class="confluenceTd">Whether the pickup SLA was violated on the escalation.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Escalated</td>
<td class="confluenceTd">Whether or not an escalation happened, TRUE or FALSE.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Escalation Queue</td>
<td class="confluenceTd">If the conversation was escalated, the code of the escalation queue of the first escalation</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Escalation Reason</td>
<td class="confluenceTd">The reason for the escalation if the conversation was escalated, blank otherwise.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Abandoned</td>
<td class="confluenceTd"><p>Four possible values:</p>
<div class="table-wrap">
<pre class="table"><code>|  |  |
| ----|----|
| 0 | The conversation was not abandoned. Default. |
| 1 | Amelia was the agent and the conversation ends in a non-default context (BPN, SLU). A completed BPN does not count as abandoned. A partially completed BPN, however, does count as abandoned. |
| 2 | The conversation was escalated and never picked up. |
| 3 | The conversation was abandoned while the agent was not Amelia and the user did not say anything after the escalation. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Amelia Handled</td>
<td class="confluenceTd">Derived from the escalated and abandoned metrics (!escalated &amp;&amp; abandoned == 0).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Amelia Abandoned</td>
<td class="confluenceTd">Derived from the escalated and abandoned metrics (!escalated &amp;&amp; abandoned == 1).</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Agent Handled</td>
<td class="confluenceTd">Derived from the escalated and abandoned metrics (escalated &amp;&amp; abandoned == 0).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Agent Abandoned</td>
<td class="confluenceTd">Derived from the escalated and abandoned metrics (escalated &amp;&amp; (abandoned == 1) || (abandoned == 3)).</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Escalate Abandoned</td>
<td class="confluenceTd">Derived from the abandoned metric (abandoned == 2).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Total Handle Time</td>
<td class="confluenceTd">Duration between start of conversation and last utterance from the user or agent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Executed BPNs</td>
<td class="confluenceTd">A comma delimited list of all BPNs executed in the conversation.</td>
</tr>
<tr class="even">
<td class="confluenceTd">User Name</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Name of the user in the conversation (defaults to Anonymous for anonymous users). If the domain Transcripts setting is set to Anonymize, the user name will be the first name and last name masks set in the application.properties file in the amelia-engine-service folder:</p>
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb2" data-syntaxhighlighter-params="brush: groovy; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: groovy; gutter: false; theme: Confluence"><pre class="sourceCode groovy"><code class="sourceCode groovy"><span id="cb2-1"><a href="#cb2-1" aria-hidden="true" tabindex="-1"></a>amelia<span class="op">.</span>transcripts<span class="op">.</span>anonymous<span class="op">-</span>first<span class="op">-</span>name<span class="op">=</span>Firstname</span>
<span id="cb2-2"><a href="#cb2-2" aria-hidden="true" tabindex="-1"></a>amelia<span class="op">.</span>transcripts<span class="op">.</span>anonymous<span class="op">-</span>last<span class="op">-</span>name<span class="op">=</span>Lastname</span></code></pre></div>
</div>
</div>
<p><br />
</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Escalation Log</td>
<td class="confluenceTd">If included in the export request, a double pipe (||) delimited list of the escalation log entries for escalated conversations.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Transcript</td>
<td class="confluenceTd">If included in the export request, a double pipe (||) delimited list of conversation messages for the conversation.</td>
</tr>
</tbody>
</table>
# Configuration
Agent/Supervisor functionality requires configuration of users, roles, escalation teams, escalation queues, and other settings. While supervisors sometimes perform these tasks, IPsoft staff often do the work when the Amelia instance is set up. Contact IPsoft if you have any questions or need support with setup and modifications.
An agent can belong to more than one queue (and team) and a queue can be monitored by more than one team. In this example, the IT Helpdesk Queue is monitored by two teams, Workplace Support and Application Support, and Agent 006 part of both teams.
![](attachments/11940140/28480742.png)
Figure. Integration with Teams, Groups, and Queues
Configuration is handled through the System Settings link at the bottom left side of Amelia's administration pages. Typically, once at least one domain is created, Amelia is configured in a specific order to handle escalated conversations.
1.  Create users
2.  Create an agent group and assign it the Agent role
3.  Assign users to the agent group
4.  Create an escalation team and add users
5.  Create an escalation queue and add escalation teams
6.  Assign an escalation queue to a domain
## Create Groups
To create a group for agents to handle escalation events, click the System Settings link on the left side of Amelia's administration pages then click the Groups link to display a searchable list of groups. Click the New Group button at the top right of the Groups page to display the New Group workspace.
The New Group workspace is available by clicking the System Settings then Groups links in Amelia's administration pages.
1.  Select the domain for the group or click the Global check box to make the group available to all domains.
2.  Click the Users tab in the middle of the workspace and add users by typing a name then clicking the Add button.
3.  Click the Roles tab in the middle of the workspace, click to select Agent on the left side and drag it to the right and drop on the Selected Roles box.
4.  Click the Save button at the top right of the New User workspace to save changes.
![](attachments/11940140/28480801.png)
Figure. New Group Form
Table. Group Form Fields
|                      |                                                                                                                                                                                                                                                |
|------------|------------------------------------------------------------|
| Field                | Description                                                                                                                                                                                                                                    |
| User Group Details   |                                                                                                                                                                                                                                                |
| Domain               | Select a specific domain, if applicable                                                                                                                                                                                                        |
| Name                 | Type the name of the group                                                                                                                                                                                                                     |
| Global               | Select or deselect to make the group available globally to all domains                                                                                                                                                                         |
| Users                |                                                                                                                                                                                                                                                |
| Search               | Click the Search box then type in partial or complete User name into the Search field                                                                                                                                                          |
| Add                  | When a user name appears in the search field, click to add the user to this group definition. The new user name appears in the Added box. To delete a user, click the x to the right of any name in the Existing, Added, or Deleted boxes.     |
| Member Groups        |                                                                                                                                                                                                                                                |
| Search               | Click the Search box then type in partial or complete group name into the Search field                                                                                                                                                         |
| Add                  | When a group name appears in the search field, click to add the group to this group definition. The new group name appears in the Added box. To delete a group, click the x to the right of any name in the Existing, Added, or Deleted boxes. |
| Roles                |                                                                                                                                                                                                                                                |
| Unused Roles         | Click available roles on the left side list then drag to the right and drop on the Selected Roles box.                                                                                                                                         |
| Selected Roles       | Click role on the right side list then drag to the left and drop on the Unused Roles box.                                                                                                                                                      |
| Authorities          |                                                                                                                                                                                                                                                |
| Unused Authorities   | Click available authorities on the left side list then drag to the right and drop on the Selected Authorities box.                                                                                                                             |
| Selected Authorities | Click authority on the right side list then drag to the left and drop on the Unused Authorities box.                                                                                                                                           |
## Create Users
To create a user access record for an agent, click the System Settings link on the left side of Amelia's administration pages then click the Users link to display a searchable list of users. Click the New User button at the top right of the Users page to display the New User workspace.
> [!warning]  
>
> By default, agents can observe and pickup conversations only for their assigned queue. In contrast, the current CONVERSATION_OBSERVE_AUTHORITY and CONVERSATION_PICKUP_AUTHORITY apply to all conversations within a domain.
>
> If an agent is not assigned one or both of these authorities, they can observe and pickup conversations only in their assigned queue(s). While they can see all conversations listed on the main Conversations page, names are blanked out for conversations not in their queue. And clicking on a conversation not in their queue will not display the conversation. This limits access to personal information (PI) and personally identifiable information (PII) to comply with GDPR regulations.
>
> This change affects customers who use these two authorities to manage access to conversations in queues. Agents and supervisors who need access to all conversations can use these authorities.

The New User workspace is available by clicking the System Settings then Users links in Amelia's administration pages.
1.  Click the Users link on the left side of the administration page to display a list of Users.
2.  To edit an existing user, search for the name and click the notepad edit icon to the left of their name.  
    To add a new user, click the New Users button at the top of the Users list page.
3.  Complete the New Users form that appears.
4.  Click the Save button at the top right of the New User workspace to save changes.
![](attachments/11940140/11940155.png)
Figure. New User Form
Table. User Form Fields
|                          |                                                                                                                                                              |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Field                    | Description                                                                                                                                                  |
| User Details             |                                                                                                                                                              |
| Domain                   | Select a domain for the user                                                                                                                                 |
| First Name               | Type user's first name                                                                                                                                       |
| Last Name                | Type user's last name                                                                                                                                        |
| Email                    | Type user's email address                                                                                                                                    |
| External UID             | Optional. Type user's external UID                                                                                                                           |
| Authentication Policy    | Select the authentication policy for user to use for login                                                                                                   |
| Locale                   | Select location for language                                                                                                                                 |
| Time Zone                | Select global time zone for user                                                                                                                             |
| Maximum Concurrent Chats | Type in a number or click to increase or decrease a number. Users who are part of an escalation team must have this value set greater than the default of 0. |
| Enabled                  | Select or deselect to enable the user's access                                                                                                               |
| Exclude From Metrics     | Select or deselect to exclude this user's activity from metrics                                                                                              |
| Password                 |                                                                                                                                                              |
| Change Password?         | For existing users, select or deselect to force user to change password                                                                                      |
| Password                 | If Change Password? is selected, and if needed on the new user form, type the user's password                                                                |
| Confirm Password         | If Change Password? is selected, and if needed on the new user form, retype the user's password                                                              |
| Last Updated             | For existing users, displays the date and time of last password change                                                                                       |
| Groups                   |                                                                                                                                                              |
| Search                   | Type in partial or complete User name into the Search field then click the Add button                                                                        |
| Add Button               | When a group name appears in the search field, click to add the group to this group definition                                                               |
| Existing                 | List of existing groups for the user record                                                                                                                  |
| Added                    | List of recently added groups for the user record                                                                                                            |
| Removed                  | List of recently removed groups for the user record                                                                                                          |
| Effective Authorities    |                                                                                                                                                              |
| List                     | Lists all authorities assigned to the user record                                                                                                            |
## Create Escalation Teams
To create an escalation team to organize users, click the System Settings link on the left side of Amelia's administration pages then click the Escalation Team link to display a searchable list of teams. Click the New Escalation Team button at the top right of the Escalation Team page to display the New Team workspace.
The New Team workspace is available by clicking the System Settings then Escalation Team links in Amelia's administration pages.
1.  Click the dropdown list at the top left of Amelia's chat interface. Select Admin. The administration pages display.
2.  Click the Escalation Teams tab on the left side of the administration page to display the Escalation Teams control panel.  
    To edit an existing team, click twice on a team name listed in the control panel.  
    To add a new team, click the New button at the top of the Escalation Teams control panel.
3.  Complete the Escalation Teams form that appears on the right side of the interface.
![](attachments/11940140/28480802.png)
Figure. New Escalation Team Form
Table. Escalation Team Form Fields
|                                                |                                                                                                          |
|------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Field                                          | Description                                                                                              |
| Basics                                         |                                                                                                          |
| Name                                           | Type the name of the escalation team                                                                     |
| Enabled                                        | Select or deselect to enable the team and make it active                                                 |
| Custom Schedule?                               | Select or deselect to configure a custom day time schedule                                               |
| Week Schedule (if Custom Schedule is selected) |                                                                                                          |
| Start                                          | For each day of the week, select a start time                                                            |
| End                                            | For each day of the week, select an end time                                                             |
| TimeZone                                       | Select a time zone for the escalation team                                                               |
| Team Members / Users Edit                      |                                                                                                          |
| Search                                         | Type name of a user then click the Add Button                                                            |
| Add Button                                     | Click to add a user found with the Search field                                                          |
| Added                                          | For each user added, lists the email address, first name, last name, and their assigned Amelia domain(s) |
## Create Escalation Queue
Once a conversation is escalated, it will be placed in one of the existing queues defined for the conversation domain. The module in Amelia that escalates the conversation, for example, a BPN, will specify the queue where the conversation should be placed. If no queue is specified, conversations will be queued on the domain's default queue.
To create and modify escalation queues, users must have their access privileges include these authorities:
AUTHORITY_ADMIN_ESCALATION_QUEUE_VIEW  
AUTHORITY_ADMIN_ESCALATION_QUEUE_EDIT
To create an escalation queue to organize users, click the System Settings link on the left side of Amelia's administration pages then click the Escalation Queue link to display a searchable list of queues. Click the New Escalation Queue button at the top right of the Escalation Queues page to display the New Queue workspace.
The New Queue workspace is available by clicking the System Settings then Escalation Team links in Amelia's administration pages.
1.  Click the dropdown list at the top left of Amelia's chat interface. Select Admin. The administration pages display.
2.  Click the Escalation Queues tab on the left side of the administration page to display the Escalation Queues control panel.  
    To edit an existing queue, click twice on a queue name listed in the control panel.  
    To add a new queue, click the New button at the top of the Escalation Queues control panel.
3.  Complete the Escalation Queues form that appears on the right side of the interface.
If appropriate, on the left side of the administration page, click the Domains tab and double-click the appropriate domain(s). Then select the appropriate values for Default Queue in the Escalations area. A default escalation queue must be configured for escalations to work.
![](attachments/11940140/28480803.png)
Figure. Escalation Queue Form
Table. Escalation Queue Form Fields
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh" style="text-align: left;">Field</th>
<th class="confluenceTh" style="text-align: left;">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd" style="text-align: left;"><strong>Basics</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Name</td>
<td class="confluenceTd" style="text-align: left;">Type the name of the queue</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Code</td>
<td class="confluenceTd" style="text-align: left;">Type a code name for the queue, usually the Name without spaces or hyphens</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Domain</td>
<td class="confluenceTd" style="text-align: left;">Select the domain used with this escalation queue</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Escalation notification timeout (seconds)</td>
<td class="confluenceTd" style="text-align: left;">Click or type time in seconds</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Max consecutive timeouts</td>
<td class="confluenceTd" style="text-align: left;">Click or type maximum number of consecutive timeouts allowed. When set to 0, agent status will not be set to Away automatically.</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Queue Enabled?</td>
<td class="confluenceTd" style="text-align: left;">Select or deselect to enable this escalation queue</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd" style="text-align: left;"><strong>Pre-Escalation Process</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Pre-Escalation Process</td>
<td class="confluenceTd" style="text-align: left;">Select a BPN process to use in a pre-escalation process</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Run on Transfer?</td>
<td class="confluenceTd" style="text-align: left;">Select to run the pre-escalation process on transfer into an escalation queue</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd" style="text-align: left;"><strong>SLAs</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Pickup Time SLA (seconds)</td>
<td class="confluenceTd" style="text-align: left;">Click or type time in seconds</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Pickup Warning (seconds)</td>
<td class="confluenceTd" style="text-align: left;">Click or type time in seconds</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Handle Time SLA (seconds)</td>
<td class="confluenceTd" style="text-align: left;">Click or type time in seconds</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Handle Warning (seconds)</td>
<td class="confluenceTd" style="text-align: left;">Click or type time in seconds</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;"><strong>Exclusive Supervisor Group</strong></td>
<td class="confluenceTd" style="text-align: left;"><br />
</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd" style="text-align: left;"><strong>Escalation Teams</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Search</td>
<td class="confluenceTd" style="text-align: left;">Type name of escalation team then click the Add button</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Add Button</td>
<td class="confluenceTd" style="text-align: left;">Click to add name in Search field</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Current</td>
<td class="confluenceTd" style="text-align: left;">This column lists existing escalation teams assigned to this queue</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left;">Add</td>
<td class="confluenceTd" style="text-align: left;">This column lists recently added escalation teams assigned to this queue</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left;">Remove</td>
<td class="confluenceTd" style="text-align: left;">This column lists recently removed escalation teams assigned to this queue</td>
</tr>
</tbody>
</table>
## Set Default Escalation Queue for a Domain
Once an escalation queue is created, the queue can be assigned to a domain. To set the default escalation queue for a domain, log in to Amelia's administration pages then select System Settings and Domains from the left side navigation links.
1.  Type the domain name in the search box at the top of the Domains list page to display the domain name.
2.  Click the notepad edit icon to the left of the domain name. The Domain edit page appears.
3.  Find the Escalations box and dropdown list then select a queue name from the dropdown list.
4.  Click the Save button at the top of the domain edit page to save changes.
![](attachments/11940140/11940149.png)
Figure. Escalations Box and Dropdown to Set Default Escalation Queue
## Set Maximum Active Chats for Agents
The maximum active chats setting for an agent determines their availability to be assigned an escalated conversation. To increase or decrease this setting, log in to Amelia's administration pages then select the System Settings link then the Users from the left side navigation.
1.  Type the name in the search box at the top of the Users list page to display the user name.
2.  Click the notepad edit icon to the left of the user name. The user's edit page appears.
3.  Find the Max Concurrent Chats setting then click or type in a new number.
4.  Click the Save button at the top of the user's edit page to save changes.
## Configure Maximum Allowed Agent Wait Time to Join Escalated Chat
Amelia by default waits 30 seconds after sending an escalation alert to an agent before she re-queues the escalation alert to another agent. The wait time is configurable with an amelia-escalation-service property.
``` groovy
amelia.escalation.service.join-wait-period.seconds=30
```
## Create an Escalation Training BPN
A training BPN process file is a simple way to test configurations and gain experience with Amelia's escalation functionality. Calling a single task BPN from a chat session with Amelia can escalate the conversation for a specific reason and to a specific escalation queue. This BPN is called escalate.
![](attachments/11940140/28480804.png)
Figure. A Single Task Escalation BPN
### Build the BPN
Table. BPN Specifications to Escalate a Conversation

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | escalate to globalqueue because "This is a test. Please ignore." | Replace globalqueue with the appropriate queue code name. Note the code name doesn't use hyphens or spaces. |

Once the BPN task is built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
### Run the Workflow and Escalate a Conversation
When the BPN model is built and deployed, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the right edge of the Mind panel.
1.  Click the web browser reload button to refresh the conversation page and clear any earlier interactions.
2.  Ask Amelia to run the escalate workflow by typing this command in the chat interface:
    
    |  |
    | ----|
    | run the workflow escalate |
    
3.  Click the Conversations link at the top of the conversation area to see the escalated conversation listed on the Active Conversations page.
{% /version %}
