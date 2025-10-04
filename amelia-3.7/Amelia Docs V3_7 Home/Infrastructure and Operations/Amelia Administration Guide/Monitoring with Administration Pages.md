{% version "3.x" %}
Amelia provides monitoring of conversations and other system behaviors with the Active Conversations, Agent Supervisor, and Metrics pages. The Conversations link is visible from the default chat interface while the Conversations, Supervisor, and Metrics links area available from the administration pages and the Conversations page. Clicking the Admin link at the top right of the default chat interface displays the administration pages.
![](https://docs.ipsoft.com/download/attachments/11940113/amelia-v3-mind-interface-3.7.0.jpg)
Figure. Amelia’s Default Conversation Area
# Active Conversations Page
Amelia allows active conversations to be observed, as well as picked up. Clicking the Conversations link, located at the top right of the conversation area with avatar, displays all active conversations for the Amelia installation with the ability to filter by domains, queues, and agents. A link at the top right of the Active Conversations page also links to a Supervisors page and Metrics page.
![](https://docs.ipsoft.com/download/attachments/11937865/image2019-4-9_16-22-13.png)
Figure. Active Conversations Page
Table. Active Conversation Fields
<table class="relative-table wrapped confluenceTable" style="width: 1022.0px;">
<tbody>
<tr class="header">
<th class="confluenceTh">Field</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Top Navigation</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Domains</p></td>
<td class="confluenceTd"><p>Select a domain to filter active conversation data.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Agent</p></td>
<td class="confluenceTd"><p>Select an agent to filter active conversation data.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Queues</td>
<td class="confluenceTd">Select a queue to filter active conversation data.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Agent</td>
<td class="confluenceTd">Select an agent name to filter active conversation data</td>
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
<td class="confluenceTd"><div class="content-wrapper">
&#10;</div></td>
<td class="confluenceTd">Click to manually refresh data on the Active Conversations page.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Queues Summary</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">Queue</td>
<td class="confluenceTd">The name of each active queue.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Current</td>
<td class="confluenceTd">The number of escalated conversations for a queue.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Queued/Running</td>
<td class="confluenceTd">The number of escalation conversations that are queued and being handled.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Ready Agents</td>
<td class="confluenceTd">The number of agents whose status is set to Ready.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Busy Agents</td>
<td class="confluenceTd">The number of agents whose status has been set to Busy due to handling one or more escalations.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Away Agents</td>
<td class="confluenceTd">The number of agents whose status is set to Away.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Offline Agents</td>
<td class="confluenceTd">The number agents whose status is set to Offline.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Conversation Summary</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>ID</p></td>
<td class="confluenceTd"><p>The conversation ID. If conversation was escalated, click the + (plus) or – (minus) icon to the left of the ID to display or hide information about the escalation queue for the conversation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Domain</p></td>
<td class="confluenceTd"><p>The domain where the conversation happened.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>User</p></td>
<td class="confluenceTd"><p>The person who initiated the conversation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Agent</p></td>
<td class="confluenceTd"><p>The agent assigned to the conversation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Status</p></td>
<td class="confluenceTd"><p>Current status of the escalation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Queue</p></td>
<td class="confluenceTd"><p>If escalated, the escalation queue for the conversation.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Reason</p></td>
<td class="confluenceTd"><p>If escalated, the reason for the escalation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Auto-Refresh</p></td>
<td class="confluenceTd"><p>Select an auto-refresh duration: 30 seconds, 1 Minute, 2 Minutes, 5 Minutes, 10 Minutes.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>My Queues</p></td>
<td class="confluenceTd"><p>Click the toggle to filter active conversations by escalation queues assigned to your login.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">P-SLA</td>
<td class="confluenceTd">The Pickup-Service Level Agreement (P-SLA) is the date and time when escalated conversations must be picked up. The P-SLA is set in the Escalation Queues workspace in the System Settings area of Amelia's administration pages.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Created</p></td>
<td class="confluenceTd"><p>Creation date and time for the conversation.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Queued</p></td>
<td class="confluenceTd"><p>If escalated, whether or not the conversation was escalated.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Queued Time</td>
<td class="confluenceTd">The amount of time a conversation has been in an escalation queue.</td>
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
<td class="confluenceTd"><div class="content-wrapper">
&#10;</div></td>
<td class="confluenceTd">Click to pick up the conversation and respond.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
&#10;</div></td>
<td class="confluenceTd">Click to observe the conversation.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
&#10;</div></td>
<td class="confluenceTd">Click to observe the conversation in 3D view.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
&#10;</div></td>
<td class="confluenceTd">Click to assign the conversation to agents with their status set to Ready.</td>
</tr>
</tbody>
</table>
# Agent Supervisor Page
The Supervisors page, available from the dropdown list at the top right of the page, displays two charts and a Queue Summary table.
-   The Active Escalated Conversations chart displays Active escalated conversations and the Service Level Agreement (SLA) performance by escalation queue.
-   The Hourly Conversations chart displays conversations by hour for the past 24 hours by who handled the conversation.
-   The Queue Summary table displays agent performance, conversation, SLA performance, and other data for each escalation queue.
Figure. Agent Supervisor Page
Table. Agent Supervisor Fields
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Field</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Top Navigation</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Domain</p></td>
<td class="confluenceTd"><p>Select the domain at the top right of this workspace to filter escalation queues by domain.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Show Queue Summary Only</td>
<td class="confluenceTd">Click to toggle the Active Escalated Conversations visible or hidden.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Show Online Agents Only</td>
<td class="confluenceTd">Click to toggle the Agent Summary to display only currently active agents with their status set to READY.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Audio Alerts</td>
<td class="confluenceTd">Click to toggle audio alerts on or off. Select SLA Ok, SLA Warn, and/or SLA Critical.</td>
</tr>
<tr class="even">
<td class="confluenceTd">SLA Ok</td>
<td class="confluenceTd">Click to toggle audio alerts on or off for conversations with SLA Ok.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">SLA Warn</td>
<td class="confluenceTd">Click to toggle audio alerts on or off for conversations with SLA Warn.</td>
</tr>
<tr class="even">
<td class="confluenceTd">SLA Critical</td>
<td class="confluenceTd">Click to toggle audio alerts on or off for conversations with SLA Critical.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Horizontal Panels</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Active Escalated Conversation</p></td>
<td class="confluenceTd"><p>This panel displays graphic data about the escalation queue responses compared to all queues. The chart displays Active, SLA OK, SLA Warn, and SLA Critical data points.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Hourly Conversations</p></td>
<td class="confluenceTd"><p>This panel displays graphic data about the escalation queue responses on an hourly basis. The chart displays Amelia Handled, Amelia Abandoned, Escalate Abandoned, Agent Handled, and Agent Abandoned data points.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Queue Summary</p></td>
<td class="confluenceTd"><p>This panel displays chart data about the escalation queue responses.</p></td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Queue Summary Panel</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
&#10;</div></td>
<td class="confluenceTd">For a queue, click to toggle a summary of data by agent in the Agent Summary section below this panel.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Queue</p></td>
<td class="confluenceTd"><p>The name of the escalation queue.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Code</td>
<td class="confluenceTd">The domain code name</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Current Conversations</p></td>
<td class="confluenceTd"><p>The number of currently active conversations.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Ready Agents</p></td>
<td class="confluenceTd"><p>The number of agents assigned to the escalation queue whose status is Ready.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Busy Agents</p></td>
<td class="confluenceTd"><p>The number of agents assigned to the escalation queue whose status is Busy.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Away Agents</p></td>
<td class="confluenceTd"><p>The number of agents assigned to the escalation queue whose status is Away.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Offline Agents</p></td>
<td class="confluenceTd"><p>The number of agents assigned to the escalation queue whose status is Offline.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Total Conversations</p></td>
<td class="confluenceTd"><p>The total number of conversations the agent has participated in.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>SLA-Violations</p></td>
<td class="confluenceTd"><p>The number of conversations whose pick up time exceeded the SLA agreement time.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Abandoned</p></td>
<td class="confluenceTd"><p>The total number of abandoned conversations.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Max Concurrent</p></td>
<td class="confluenceTd"><p>The number of conversations started for the selected time period.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Avg Answer Speed</p></td>
<td class="confluenceTd"><p>The average time between escalation and agent pick up.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Max Answer Speed</p></td>
<td class="confluenceTd"><p>The maximum time between escalation and agent pick up.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>Avg Handle Time</p></td>
<td class="confluenceTd"><p>The average time between escalation and conversation end.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>Max Handle Time</p></td>
<td class="confluenceTd"><p>The maximum time between escalation and conversation end.</p></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Agent Summary Panel</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Agent</td>
<td class="confluenceTd">The name of an agent assigned to the selected queue.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Status</td>
<td class="confluenceTd">The current status of the agent. Options are OFFLINE, READY, BUSY, AWAY.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Duration</td>
<td class="confluenceTd">Total time agent has spent handling escalations.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Allowed</td>
<td class="confluenceTd">Number of concurrent conversations the agent is assigned to handle. Defined with the Max Concurrent Chats setting in the edit or new user page available by clicking the Systems Settings link in the Admin workspace then clicking the Users link.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Current</td>
<td class="confluenceTd">The number of conversations the agent is currently handling.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Total</td>
<td class="confluenceTd">The total number of conversations the agent has handled.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Abandoned</td>
<td class="confluenceTd">The number of conversations abandoned by the agent.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Max Concurrent</td>
<td class="confluenceTd">The maximum number of conversations the agent has handled concurrently.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Answer Avg</td>
<td class="confluenceTd">The average time to answer for the agent.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Answer Max</td>
<td class="confluenceTd">The maximum time to answer for the agent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Handle Avg</td>
<td class="confluenceTd">The average handle time for the agent.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Handle Max</td>
<td class="confluenceTd">The maximum time handle time for the agent.</td>
</tr>
</tbody>
</table>
To display data for agents assigned to a queue, click the + (plus) or – (minus) sign to the left of the queue name to display or hide agent data. These fields are described below.
Table. Agent Data Fields on the Agent Supervisor Page

| Field | Description |
| ----|----|
| Agent | The name of each agent assigned to the escalation queue. |
| Status | The current status of each agent assigned to the escalation queue. |
| Duration | Time spent in the current status for each agent. |
| Allowed | The maximum number of chat conversations allowed for each agent. |
| Current | The number of currently active conversations for each agent. |
| Total | The total number of conversations for each agent. |
| Abandoned | The total number of abandoned conversations for each agent. |
| Max Concurrent | The number of conversations started by this agent for the selected time period. |
| Answer Avg | The average time between escalation and agent pick up. |
| Answer Max | The maximum time between escalation and agent pick up. |
| Handle Avg | The average time between escalation and conversation end. |
| Handle Max | The maximum time between escalation and agent pick up. |

# Metrics Page
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

# Export Conversations
Conversations can be exported from the Metrics page which is available from the dropdown list at the top right of the page.
1.  Click the Export Conversations tab above the pie chart graphs to display the export form.
2.  Select the date, time, and minute range for conversations to be exported.
3.  Select one or more domains to filter conversations in or out of the exported file.
4.  Click checkboxes to include all domains, transcripts, escalation logs, and escalations not started.
5.  Click the Export button then select where to download the CSV file.
Exports can include up to 2000 conversations in each file. As a date range, domains, and other criteria are selected on the export form, the number of conversations to be exported is displayed below the Export and Reset buttons on the form.
![](attachments/11940300/11940304.png)
Figure. Export Conversations Form
![](attachments/11940300/11940305.png)
Figure. Export Form with Date, Time, Minute Selected
The exported CSV and JSON file output includes these fields below.
## CSV Data Definitions
Table. Metrics Export CSV File Per-Conversation Column Names
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
<td class="confluenceTd">Domain</td>
<td class="confluenceTd">The domain where the conversation happened.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Created</td>
<td class="confluenceTd">Date/Time the conversation started (UTC).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Finished</td>
<td class="confluenceTd">Date/Time the conversation finished (UTC).</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Status</td>
<td class="confluenceTd">Final status of conversation.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Channel</td>
<td class="confluenceTd">Where the conversation originated.</td>
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
<td class="confluenceTd">User Email</td>
<td class="confluenceTd">Any email address for the user captured during the conversation.</td>
</tr>
<tr class="even">
<td class="confluenceTd">User External Uid</td>
<td class="confluenceTd">Any external non-Amelia user ID captured during the conversation.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Custom Metrics</td>
<td class="confluenceTd">A JSON data structure with any custom metrics captured during the conversation.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Escalation Log</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>If included in the export request, a double pipe (||) delimited list of the escalation log entries for escalated conversations. Log entries include escalation type, escalation code, and conversation status.</p>
<p>Example: [04/23/2019 09:40:07 ; NORMAL ; Misunderstanding ; ABANDONED] 04/23/2019 09:40:07 NO_AGENTS_AVAILABLE, , Count: 721||04/23/2019 09:55:08 CONVERSATION_CLOSED, , Count: 0</p>
<p>Format: [ Escalation Time ; Escalation Type ; Escalation Reason ; Escalation Status (ending status) ] LogEntryTime EscalationLogStatus, Escalation Notes, Counter</p>
<div class="table-wrap">
<table class="wrapped confluenceTable">
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Escalation Time</td>
<td class="confluenceTd">Date/Time the escalation started (UTC).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Escalation Type</td>
<td class="confluenceTd"><div class="table-wrap">
<pre class="table"><code>| Element | Description |
| ----|----|
| NORMAL | A normal escalation of the conversation from Amelia to an Agent. |
| ASSIGNED | An escalation that is assigned to a specific agent by another agent/supervisor. The escalation process will direct this escalation at that specific agent and no others, marking it ABANDONED if the targeted agent doesn&#39;t pick up. |
| TRANSFER | An escalation being transferred from one agent to another. The escalation is placed in the escalation queue and the escalation process will determine, and contact, the next available agent. |
| STEAL | An agent or supervisor with the AUTHORITY_CONVERSATION_STEAL authority is stealing an escalation from another agent. |</code></pre>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Escalation Reason</td>
<td class="confluenceTd">Provided by the Escalate Because BPN task or system defaults.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Escalation Status</td>
<td class="confluenceTd"><div class="table-wrap">
<pre class="table"><code>| Element | Description |
| ----|----|
| QUEUED | Escalation is queued for dispatch. |
| RUNNING | Escalation is currently running, sent notifications and waiting for responses. |
| ACCEPTED | Escalation has been accepted by an agent who is in the process of picking up the conversation. |
| ACTIVE | Escalation has been accepted and the conversation picked up by the agent. |
| ABANDONED | Escalation abandoned by the system for some reason. Conversation closed or another escalation was accepted. |</code></pre>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Log Entry Time</td>
<td class="confluenceTd">Date/Time the escalation was logged (UTC).</td>
</tr>
<tr class="even">
<td class="confluenceTd">Escalation Log Status</td>
<td class="confluenceTd"><div class="content-wrapper">
<div class="table-wrap">
<pre class="table"><code>| Element | Description |
| ----|----|
| ASSIGNED_AGENT | Logged when an escalation is manually assigned to an agent by another agent/supervisor |
| AGENT_PICKUP | Logged when the agent has successfully picked up a conversation (either an escalated or non-escalated conversation) |
| MANUAL_PICKUP | Logged when an agent successfully picks up a conversation that has been manually ASSIGNED to them by another agent/supervisor |
| AGENT_PICKUP_TIMEOUT | Logged if the escalation times out when attempting to contact an agent to handle the escalation.; Also logged if an error occurs attempting to contact an agent. |
| AGENT_REJECTED | Logged when an agent manually rejects an escalation request |
| NO_AGENTS_AVAILABLE | Logged when the escalation service cannot find any agents online and available to send an escalation request to |
| CONVERSATION_CLOSED | Logged when the escalation service finds an escalated conversation in the escalation queue but cannot find that conversation in the list of active conversations |</code></pre>
</div>
<blockquote>
<p>[!warning]<br />
</p>
<p>Assigning an escalation to a user is different than transferring a conversation. When assigning an escalation, an agent/supervisor directly chooses which agent should handle the conversation. When transferring a conversation, the agent places the conversation into the escalation queue and the escalation service finds the next available agent. The ASSIGNED_AGENT and MANUAL_PICKUP codes only apply to the assigned scenario, not to the default behavior of the escalation service.</p>
</blockquote>
<p> </p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Escalation Notes</td>
<td class="confluenceTd">Generated by the system and BPN process.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Counter</td>
<td class="confluenceTd"><p>If an event continually occurs successively, a counter is updated instead of writing the same log entry repeatedly. For example, if the escalation process can’t find an available agent for 27 consecutive attempts, instead of storing 27 rows with the status NO_AGENTS_AVAILABLE, the process stores 1 row for NO_AGENTS_AVALABLE and the counter would be incremented for each event, 27 in this case.<br />
<br />
The same event might be logged two or more times if one or more events occurs in the middle, for example you could have a log with events such as:<br />
<br />
escalation_log_status: NO_AGENTS_AVAILABLE, counter: 27,<br />
escalation_log_status: AGENT_PICKUP_TIMEOUT, counter: 12,<br />
escalation_log_status: NO_AGENTS_AVAILABLE, counter: 5,<br />
escalation_log_status: AGENT_PICKUP_TIMEOUT, counter: 15,<br />
escalation_log_status: AGENT_PICKUP, counter: 0,<br />
<br />
So, the counter only applies to consecutive events and is not a cumulative counter for the event.</p></td>
</tr>
</tbody>
</table>
</div>
<p><br />
</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Transcript</td>
<td class="confluenceTd">If included in the export request, a double pipe (||) delimited list of conversation messages for the conversation.</td>
</tr>
</tbody>
</table>
Table. Metrics Export JSON File Per-Conversation Column Names
## JSON Data Definitions
### Key

| Color | Note |
| ----|----|
|  | Denotes new field |
|  | Denotes deprecated field |
|  | Denotes the beginning of a new embedded object |
|  | Denotes a dynamic UUID field within an embedded object |

> [!warning]  
>
> \* **domainCode** field, located in the PRIMARY OBJECT, has been deprecated as of 3.7.x and replaced with the **domains** OBJECT.
>
> \*\* **domainId** field, located in the PRIMARY OBJECT, is a legacy field that is left for backwards compatibility with older Amelia tools.

### Data Dictionary
Table JSON Export File Data Dictionary
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 9%" />
<col style="width: 4%" />
<col style="width: 9%" />
<col style="width: 5%" />
<col style="width: 2%" />
<col style="width: 5%" />
<col style="width: 49%" />
<col style="width: 15%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Field Name</th>
<th class="confluenceTh">Data Type</th>
<th class="confluenceTh">Data Format</th>
<th class="confluenceTh">Field Size</th>
<th class="confluenceTh">PK</th>
<th class="confluenceTh" style="text-align: center;">Value Required or Optional</th>
<th class="confluenceTh">Description</th>
<th class="confluenceTh">Example</th>
</tr>
&#10;<tr class="odd">
<td colspan="8" class="confluenceTd" style="text-align: left;">PRIMARY OBJECT - Objects and Lists of Objects that contain all conversation and metric data.</td>
</tr>
<tr class="even">
<td class="confluenceTd">conversationId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxx-N</td>
<td class="confluenceTd">50</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Unique identifier for the Amelia conversation</td>
<td class="confluenceTd">LGHBWSMJAAIAA-1</td>
</tr>
<tr class="odd">
<td class="confluenceTd">userId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd"><p>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</p></td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID for the <strong>userName</strong> field as exported from the Amelia instance.</td>
<td class="confluenceTd">5d3d4a0f-45f7-4534-bafb-b3f7cd06fc49</td>
</tr>
<tr class="even">
<td class="confluenceTd">userName</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx</td>
<td class="confluenceTd">129</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text user name that represents the logged in USER in the Amelia conversation</td>
<td class="confluenceTd">Patrick Marlow</td>
</tr>
<tr class="odd">
<td class="confluenceTd">anonymous</td>
<td class="confluenceTd">Boolean</td>
<td class="confluenceTd">true || false</td>
<td class="confluenceTd">5</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Meta-field used to identify whether the conversation was initiated from an anonymous domain or not.</td>
<td class="confluenceTd">false</td>
</tr>
<tr class="even">
<td class="confluenceTd">agentId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID for the <strong>agentName</strong> field as exported from the Amelia instance.</td>
<td class="confluenceTd">e62d3ce8-67a7-4d37-91a9-5663b0a39a2a</td>
</tr>
<tr class="odd">
<td class="confluenceTd">finalContextId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID that represents the corresponding context that was active when the conversation ended.</td>
<td class="confluenceTd">b6f676f0-ca29-40cc-946a-73bafe0621b4</td>
</tr>
<tr class="even">
<td class="highlight-green confluenceTd" data-highlight-colour="green">initialChannel</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Denotes the entry point channel of the user to Amelia. Out of the box, default channels are one of webchat_custui, webchat_coreuser, webchat_framed, webchat_coremind, webchat_core3d, js_copilot, java_sdk, js_sdk, go_sdk, voice.  Note, however, client/SDKs can specify any channel they like. </p>
</div></td>
<td class="confluenceTd">webchat_coremind</td>
</tr>
<tr class="odd">
<td class="confluenceTd">conversationCreated</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd"><p>NNNNNNNNNNN.NNN</p>
<p><br />
</p></td>
<td class="confluenceTd">14</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Epoch timestamp (w/ milliseconds) of when the unique Conversation ID was created.</td>
<td class="confluenceTd">1538551862.904</td>
</tr>
<tr class="even">
<td class="confluenceTd">conversationFinished</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Epoch timestamp (w/ milliseconds) of when the unique Conversation ID was closed.</td>
<td class="confluenceTd">1538552018.366</td>
</tr>
<tr class="odd">
<td class="confluenceTd">summaryCreated</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Epoch timestamp (w/ milliseconds) of when the conversation summary was created in the KDB database.</td>
<td class="confluenceTd">1538552018.589</td>
</tr>
<tr class="even">
<td class="confluenceTd">summaryModified</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Epoch timestamp (w/ milliseconds) of when the conversation summary was modified for an reason.</td>
<td class="confluenceTd">1538552018.589</td>
</tr>
<tr class="odd">
<td class="confluenceTd">userEmail</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxx@xxxxxx.xxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text email address of the current logged in user.</td>
<td class="confluenceTd"><a href="mailto:em@il.anon">em@il.anon</a></td>
</tr>
<tr class="even">
<td class="confluenceTd">agentEmail</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxx@xxxxxx.xxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text email address of the current agent handling the user request. By default, this is set to amelia@ipsoft.com but will change if the conversation is escalated.</td>
<td class="confluenceTd"><a href="mailto:amelia@ipsoft.com">amelia@ipsoft.com</a></td>
</tr>
<tr class="odd">
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>domainCode*</del></td>
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>String</del></td>
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>xxxxxxxxxxxxxxxxxx</del></td>
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>50</del></td>
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>N</del></td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red"><del>Required</del></td>
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>Clear text domain code.</del></td>
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>employeeservices</del></td>
</tr>
<tr class="even">
<td class="confluenceTd">domainId**</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd"><p>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</p></td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID for the <strong>domain</strong> field as exported from the Amelia instance.</td>
<td class="confluenceTd">4b639c5e-b323-4fdd-9be3-0220ebbb3f41</td>
</tr>
<tr class="odd">
<td class="highlight-green confluenceTd" data-highlight-colour="green">domains</td>
<td colspan="7" class="highlight-yellow confluenceTd" data-highlight-colour="yellow">DOMAINS OBJECT - List of DOMAIN objects contained within the primary object; Each embedded object contains metadata around specific domains that were triggered during the conversation.</td>
</tr>
<tr class="even">
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">&lt;DOMAIN UUID&gt;</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">String</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">36</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">Y</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">Required</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">UUID that represents a DOMAIN OBJECT for a domain that was filled during a conversation in the PRIMARY OBJECT. DOMAIN OBJECT contains metadata on the unique domain that was active.</td>
<td class="confluenceTd">fbe6165f-5481-4bdf-ac6e-4289eca494aa</td>
</tr>
<tr class="odd">
<td class="confluenceTd">&lt;DOMAIN CODE&gt;</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">50</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text domain code.</td>
<td class="confluenceTd">employeeservices</td>
</tr>
<tr class="even">
<td class="highlight-yellow confluenceTd" data-highlight-colour="yellow">transcript</td>
<td colspan="7" class="highlight-yellow confluenceTd" data-highlight-colour="yellow">TRANSCRIPT OBJECT - List of objects contained within the primary object; Each embedded object is an individual utterance from either AMELIA or USER, with its own set of metadata</td>
</tr>
<tr class="odd">
<td class="confluenceTd">messageId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID for the current utterance.</td>
<td class="confluenceTd">3041c729-7478-4b58-8d64-4208e300f575</td>
</tr>
<tr class="even">
<td class="confluenceTd">contextId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><p>UUID of the conversation context which existed when this message was received or transmitted.</p></td>
<td class="confluenceTd">f9ababeb-2590-4779-a856-d53f8eca327a</td>
</tr>
<tr class="odd">
<td class="confluenceTd">userName</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxx</td>
<td class="confluenceTd">129</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text user name per utterance that represents either Amelia or the logged in User.</td>
<td class="confluenceTd">Amelia || Patrick Marlow</td>
</tr>
<tr class="even">
<td class="confluenceTd">userType</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">AMELIA || USER || END_USER</td>
<td class="confluenceTd">8</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text value per utterance that represents the speaker of the utterance. Can be either AMELIA or USER.</td>
<td class="confluenceTd">AMELIA</td>
</tr>
<tr class="odd">
<td class="confluenceTd">userId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd">UUID of the <strong>userName</strong> per utterance.</td>
<td class="confluenceTd">e62d3ce8-67a7-4d37-91a9-5663b0a39a2a</td>
</tr>
<tr class="even">
<td class="confluenceTd">userEmail</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd"><a href="mailto:xxxxxx@xxxxxx.xxx">xxxxxx@xxxxxx.xxx</a></td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text email per utterance that represents the email address of the current userType.</td>
<td class="confluenceTd"><a href="mailto:amelia@ipsoft.com">amelia@ipsoft.com</a></td>
</tr>
<tr class="odd">
<td class="confluenceTd">source</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Clear text value per utterance that represents the Amelia subsystem that was used to send the utterance.</p>
<p>Examples:</p>
<ul>
<li>If Amelia is responding with a "Say Task" from a BPN, the value will be <strong><em>DefaultBpnEngineDirector<br />
</em></strong></li>
<li>If Amelia is performing a context switch back to a previous BPN, the value will be <strong><em>ContextDialogManagementService</em></strong></li>
<li>If Amelia is responding with Affective system, the value will be <em><strong>InboundPositiveResponseResponder</strong></em></li>
</ul>
<p>List of Sub-System Responders as of 28 Nov 2018 </p>
<div class="table-wrap">
<pre class="table"><code>| Sub-System Common Name | Sub-System Long Name | Description |
| ----|----|----|
| AcknowledgeDefault | AcknowledgeDefaultResponder | If Amelia understands an utterance as a declarative or imperative, not an interrogative or question, and no other module answers, this responder triggers. It uses an entry from the ACKNOWLEDGE response pool. |
| Affective | InboundPositiveResponseResponder | If no more specific module has an answer, this responder allows Amelia to emphasize with users. Amelia will respond to negative statements such as “Traffic was terrible today” and also compliments from user like, “You are doing a great job.”; It uses a variety of response pools for that like COMPLIMENT_REPLY_POSITIVE_INFORMAL. |
| Agent Pickup | AgentPickupHandler |  |
| Agent Transfer | AgentTransferHandler |  |
| AIML | ChitChatResponder | This module has pre-trained chit-chat which is far reaching in English. It is based on pre-loaded AIML files visible in Amelia&#39;s global domain. It will answer personal questions (Who are you?) but can answer a wide range of questions,;depending on AIML training. Amelia choses AIML, when enabled), after more specific use case training with Intents, BPNs, and SemNet. This responder is often turned off because the standard English AIML is far reaching and thus requires a high effort to curate the AIML files. |
| BPN | DefaultBpnEngineDirector | Allows the BPN sub-system module to interact with the user after an intent fires off a BPN. |
| Close Conversation | CloseConversationHandler |  |
| Context Switching | ContextDialogManagementService |  |
| CQA | DefaultCqaResponseService | For Amelia 3.5+, the clarifying question asker (CQA) module asks a clarifying question when there is a possibility of ambiguity in the user&#39;s utterance between two intents. |
| Default Greeting | DefaultStartConversationResponder |  |
| DontKnow | DontKnowDefaultResponder | This responder is chosen if no other responds and if Amelia understands a user utterance is an interrogative, not declarative or imperative. It uses an entry from the DONTKNOW response pool. |
| EpisodicMemory |  | This module answers based on Episodic Memory training. If there is no Episodic Memory training planned, this responder can be disabled. |
| EQA |  | The Elaborate Question Asking (EQA) responder generates a clarifying question in response to an incomplete user utterance. For example, if a user says, &quot;I want,&quot; then Amelia might use the EQA responder to ask, &quot;What do you want?&quot; EQA only responds under very specific conditions. |
| Escalate | EngineEscalationServiceImpl | This responder allows Amelia to escalate a conversation. Should not be turned off in regular Amelia deployments. |
| FAQ |  | The FAQ responder is part of SemNet and can answer based on uploaded FAQ Excel sheets. Answers have a lower priority than intents and, if FAQs and intents overlap to provide a poor response, this responder should be deactivated. |
| IntentFAQ |  | The IntentFAQ responder answers based on trained FAQ intents with an FAQ answer in the intent definition. Intents can be uploaded as an Excel sheet on the SemNet screen |
| LogicNet |  | This responder has the ability to answer simple questions based on inference logic (e.g. deriving facts from statements). This module will play a bigger role in the future and can currently be turned off. |
| SemNet | SemNetResponder | This responder can answer out of the conversation context of a conversation, for example, after an utterance, “The sky is blue,” Amelia might answer with the color of the sky. Because this responder can provide unexpected answers during production, it is recommended to be turned off for production domains. |
| SemNetDoc |  | The SemNet responder can answer with data from uploaded PDFs. Documents must be well curated. The responder may generate unexpected answers and the module should be turned off if this is a problem. |
| SocialTalk |  | This responder is a chit-chat responder like AIML but based on grammar, less encompassing, and uses SOCIALTALK response pools. That can be a simpler way to provide smalltalk capabilities without AIML. |
| Unknown Problem | UnknownProblemDefaultResponder | This responder answers when an utterance is classified as a Request, and if its response is selected, the escalation count is incremented. Thus, this responder should enable more reliable escalations, as it directly &quot;catches&quot; utterances that intent classifiers don&#39;t pick up, but definitely express some sort of request from the user. |</code></pre>
</div>
<p><em><strong>REFERENCE - <a href="https://docs.ipsoft.com/display/AmeliaDocsV35/Domains">https://docs.ipsoft.com/display/AmeliaDocsV35/Domains</a><br />
</strong></em></p>
</div></td>
<td class="confluenceTd">(see embedded table)</td>
</tr>
<tr class="even">
<td class="confluenceTd">understood</td>
<td class="confluenceTd">Boolean</td>
<td class="confluenceTd">true || false</td>
<td class="confluenceTd">5</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Meta-field used to identify whether the utterance was understood or not by a specific Amelia sub-system.</p>
<p><em><strong>The mapping for this value to the utterance it refers to is always 1 utterance behind!</strong></em></p>
<p><strong><em>Example:</em></strong></p>
<div class="table-wrap">
<pre class="table"><code>| User Type | Message | Responder | Value |
| ----|----|----|----|
| AMELIA | Hello! | DefaultStartConversationResponder | true |
| USER | Help me pay my | - | false |
| AMELIA | Sorry, I&#39;m not trained to help with that. | UnknownProblemDefaultResponder | true |</code></pre>
</div>
<p><br />
</p>
<p>Current Sub-System Responder Value Mappings:</p>
<div class="table-wrap">
<pre class="table"><code>| Sub-System Common Name | Sub-System Long Name | Value |
| ----|----|----|
| AcknowledgeDefault | AcknowledgeDefaultResponder | true |
| Affective | InboundPositiveResponseResponder |  |
| Agent Pickup | AgentPickupHandler |  |
| Agent Transfer | AgentTransferHandler |  |
| AIML | ChitChatResponder | false |
| BPN | DefaultBpnEngineDirector | true |
| Close Conversation | CloseConversationHandler | true |
| Context Switching | ContextDialogManagementService |  |
| CQA | DefaultCqaResponseService | true |
| Default Greeting | DefaultStartConversationResponder |  |
| DontKnow | DontKnowDefaultResponder |  |
| EpisodicMemory |  |  |
| EQA |  |  |
| Escalate | EngineEscalationServiceImpl | true |
| FAQ |  |  |
| IntentFAQ |  |  |
| LogicNet |  |  |
| SemNet | SemNetResponder |  |
| SemNetDoc |  |  |
| SocialTalk |  |  |
| Unknown Problem | UnknownProblemDefaultResponder | false |</code></pre>
</div>
<p><br />
</p>
<p><br />
</p>
</div></td>
<td class="confluenceTd">true</td>
</tr>
<tr class="odd">
<td class="confluenceTd">messageText</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">16,777,215</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text utterance from the user or Amelia.</td>
<td class="confluenceTd">I need to take some time off tomorrow.</td>
</tr>
<tr class="even">
<td class="confluenceTd">created</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Epoch timestamp (w/ milliseconds) of when the unique messageId was created.</td>
<td class="confluenceTd">1538551933.579</td>
</tr>
<tr class="odd">
<td class="confluenceTd">slotIds</td>
<td class="confluenceTd">List</td>
<td class="confluenceTd">[x,x...x]</td>
<td class="confluenceTd">16,777,215</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><p>List of Strings of UUIDs that represent the slot(s) that were filled by the current utterance.</p>
<p>Example:</p>
<ul>
<li>In the utterance "I need a flight from LAX to EWR" you might extract 2 entities, <em>origin_airport</em> and destination<em>_airport</em></li>
<li>The corresponding slotIds List for the above utterance would be something like:
<ul>
<li>["c9c600d0-4b26-4a47-ad13-c7b52c79a033","e62d3ce8-67a7-4d37-91a9-5663b0a39a2a"]</li>
</ul></li>
<li>These UUIDs would map to unique clear text values found in the slotsById object (documented below)</li>
</ul></td>
<td class="confluenceTd">["c9c600d0-4b26-4a47-ad13-c7b52c79a033","e62d3ce8-67a7-4d37-91a9-5663b0a39a2a"]</td>
</tr>
<tr class="even">
<td class="confluenceTd">goalIds</td>
<td class="confluenceTd">List</td>
<td class="confluenceTd">[x,x...x]</td>
<td class="confluenceTd">16,777,215</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><p>List of Strings of UUIDs that represent the goal(s) that were filled by the current utterance.</p>
<p>Example:</p>
<ul>
<li>In the utterance "I need a flight from LAX to EWR" you might extract 2 entities, <em>origin_airport</em> and destination<em>_airport</em></li>
<li>The corresponding slotIds List for the above utterance would be something like:
<ul>
<li>["c9c600d0-4b26-4a47-ad13-c7b52c79a033","e62d3ce8-67a7-4d37-91a9-5663b0a39a2a"]</li>
</ul></li>
<li>These UUIDs would map to unique clear text values found in the <strong>goalsById</strong> object (documented below)</li>
</ul></td>
<td class="confluenceTd">["5d3d4a0f-45f7-4534-bafb-b3f7cd06fc49","e62d3ce8-67a7-4d37-91a9-5663b0a39a2a"]</td>
</tr>
<tr class="odd">
<td class="highlight-yellow confluenceTd" data-highlight-colour="yellow">contexts</td>
<td colspan="7" class="highlight-yellow confluenceTd" data-highlight-colour="yellow"><div class="content-wrapper">
<p>CONTEXT OBJECT (OPTIONAL) - List of objects contained within the primary object; Each embedded object contains metadata around specific contexts that were triggered during the conversation.</p>
</div></td>
</tr>
<tr class="even">
<td class="highlight-green confluenceTd" data-highlight-colour="green">bpnProcessInstanceIds</td>
<td class="confluenceTd">OBJECT</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd" style="text-align: center;">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
</tr>
<tr class="odd">
<td class="highlight-green confluenceTd" data-highlight-colour="green">domainId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID of the conversation domain that contains the listed executedBpns</td>
<td class="confluenceTd">fbe6165f-5481-4bdf-ac6e-4289eca494aa</td>
</tr>
<tr class="even">
<td class="confluenceTd">contextId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID of the conversation context that contains the listed executedBpns</td>
<td class="confluenceTd">b8daafa0-9efc-4628-8c7c-aa0cfbd0f838</td>
</tr>
<tr class="odd">
<td class="confluenceTd">goalId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd">UUID of the goal/intent that was triggered in the context of the list of <strong>executedBpns</strong>. This maps back to <strong>goalInstanceId</strong> in the <em><strong>goalsById</strong></em> object.</td>
<td class="confluenceTd">e1cdc6bb-5fc8-4343-b143-3b586dcd1783</td>
</tr>
<tr class="even">
<td class="confluenceTd">executedBpns</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxx,xxxxxxx,xxxxxx</td>
<td class="confluenceTd">16,777,215</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd">Comma delimited list of BPNs that were executed within the specific context.</td>
<td class="confluenceTd">updateInsertDevice,greeting_main,attr</td>
</tr>
<tr class="odd">
<td class="confluenceTd">preferredResponder</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd">Clear text value of the sub-system responder that was triggered during the specific context.</td>
<td class="confluenceTd">Bpn</td>
</tr>
<tr class="even">
<td class="confluenceTd">created</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Epoch timestamp (w/ milliseconds) of when the unique contextId was created.</td>
<td class="confluenceTd">1539767169.911</td>
</tr>
<tr class="odd">
<td class="confluenceTd">analyticOutcomeIds</td>
<td class="confluenceTd">List</td>
<td class="confluenceTd">[x,x...x]</td>
<td class="confluenceTd">16,777,215</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>List of Strings of UUIDs that represent the analytic outcomes that were filled during the current context.</p>
<p><strong>NOTE - To date, this has not been in use, but exists for future deployments in conjunction with the updated Analytics engine. (<a href="http://dtools.ipsoft.com/confluence/display/~pmarlow">Patrick Marlow</a> )</strong></p>
</div></td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="highlight-yellow confluenceTd" data-highlight-colour="yellow">slotsById</td>
<td colspan="7" class="highlight-yellow confluenceTd" data-highlight-colour="yellow">SLOTS OBJECT (OPTIONAL) - Object contained within the primary object; Each embedded object contains metadata on slots that were filled inside individual utterances in the TRANSCRIPT OBJECT.</td>
</tr>
<tr class="odd">
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">&lt;SLOT UUID&gt;</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">String</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">36</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">Y</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">Required</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">UUID that represents a SLOT OBJECT for a slot that was filled in an utterance in the TRANSCRIPT OBJECT. SLOT OBJECT contains metadata on the unique slot that was filled</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">ac58fea9-7f80-4292-acfd-a0a767953f93</td>
</tr>
<tr class="even">
<td class="highlight-green confluenceTd" data-highlight-colour="green">entityModel</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd" style="text-align: center;">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">slotInstanceId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID that represents a slot that was filled in an utterance in the TRANSCRIPT OBJECT. Identical to parent object SLOT UUID.</td>
<td class="confluenceTd">ac58fea9-7f80-4292-acfd-a0a767953f93</td>
</tr>
<tr class="even">
<td class="confluenceTd">messageId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><p>UUID that represents the corresponding utterance where the slot was filled.</p>
<p>Example:</p>
<ul>
<li>If this field contained "f48302bb-9656-46c0-a8a4-c1e5841a2bc1" you would look up to the TRANSCRIPT OBJECT and locate that messageId</li>
<li>Then you would have the clear text messageText to map to the slot</li>
</ul></td>
<td class="confluenceTd">f48302bb-9656-46c0-a8a4-c1e5841a2bc1</td>
</tr>
<tr class="odd">
<td class="confluenceTd">contextId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID that represents the corresponding context that was active while the slot was filled.</td>
<td class="confluenceTd">58cc317f-5e79-410b-ad37-cf600ce4f9ec</td>
</tr>
<tr class="even">
<td class="confluenceTd">sequence</td>
<td class="confluenceTd">Int</td>
<td class="confluenceTd">NNNNNN</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Sequence number indicating the sequence in which the slot instances are extracted.</td>
<td class="confluenceTd">102900</td>
</tr>
<tr class="odd">
<td class="confluenceTd">code</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text value of the <strong>entity name</strong> as it exists in Amelia admin UI or context service.</td>
<td class="confluenceTd">pto_date</td>
</tr>
<tr class="even">
<td class="confluenceTd">value</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><p>Clear text value of the extracted or transformed entity that was captured.</p>
<p>Examples:</p>
<ul>
<li><strong>utterance</strong> = tomorrow; <strong>code</strong> = pto_date; <strong>value</strong> = 10/04/2018</li>
<li><strong>utterance</strong> = one thousand dollars; <strong>code</strong> = dollar_amount; <strong>value</strong> = 1000</li>
</ul></td>
<td class="confluenceTd">10/04/2018</td>
</tr>
<tr class="odd">
<td class="highlight-yellow confluenceTd" data-highlight-colour="yellow">goalsById</td>
<td colspan="7" class="highlight-yellow confluenceTd" data-highlight-colour="yellow">GOALS OBJECT (OPTIONAL) - Object contained within the PRIMARY object; Each embedded object contains metadata on goals that were filled inside individual utterances in the TRANSCRIPT OBJECT.</td>
</tr>
<tr class="even">
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">&lt;GOAL UUID&gt;</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">String</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">36</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">Y</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">Required</td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue"><div class="content-wrapper">
<p>UUID that represents a GOAL OBJECT for a goal that was filled in an utterance in the TRANSCRIPT OBJECT. GOAL OBJECT contains metadata on the unique slot that was filled.</p>
</div></td>
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">c9c600d0-4b26-4a47-ad13-c7b52c79a030</td>
</tr>
<tr class="odd">
<td class="confluenceTd">goalInstanceId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID that represents a goal that was filled in an utterance in the TRANSCRIPT OBJECT. Identical to parent object GOAL UUID.</td>
<td class="confluenceTd">c9c600d0-4b26-4a47-ad13-c7b52c79a030</td>
</tr>
<tr class="even">
<td class="confluenceTd">messageId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><p>UUID that represents the corresponding utterance where the goal was filled.</p>
<p>Example:</p>
<ul>
<li>If this field contained "f48302bb-9656-46c0-a8a4-c1e5841a2bc1" you would look up to the TRANSCRIPT OBJECT and locate that messageId</li>
<li>Then you would have the clear text messageText to map to the goal</li>
</ul></td>
<td class="confluenceTd">f6b50c4c-b4c8-4a37-9a3c-50f112685e94</td>
</tr>
<tr class="odd">
<td class="confluenceTd">code</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text value of the <strong>intent name</strong> as it exists in Amelia admin UI or context service.</td>
<td class="confluenceTd">create_ticket</td>
</tr>
<tr class="even">
<td class="highlight-green confluenceTd" data-highlight-colour="green">domainModel</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd">?</td>
<td class="confluenceTd" style="text-align: center;">???</td>
<td class="confluenceTd">???</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-green confluenceTd" data-highlight-colour="green">intentModel</td>
<td colspan="7" class="highlight-blue confluenceTd" data-highlight-colour="blue">INTENT MODEL OBJECT - Object contained within the GOAL UUID OBJECT; Each embedded object contains metadata on the intent that was triggered inside the GOAL UUID OBJECT</td>
</tr>
<tr class="even">
<td class="highlight-green confluenceTd" data-highlight-colour="green">name</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Clear text name of the intent model that was triggered as it appears on the Amelia Trainer &gt; Dashboard page.</td>
<td class="confluenceTd">esetl_intent_model</td>
</tr>
<tr class="odd">
<td class="highlight-green confluenceTd" data-highlight-colour="green">revisionId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd">Y</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">UUID representing the latest revision ID of the intent.</td>
<td class="confluenceTd">3373381e-cae3-43d2-97a8-3b5059665167</td>
</tr>
<tr class="even">
<td class="highlight-green confluenceTd" data-highlight-colour="green">score</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Value denoting the confidence score of the triggered intent.</td>
<td class="confluenceTd">0.98</td>
</tr>
<tr class="odd">
<td class="highlight-green confluenceTd" data-highlight-colour="green">revisionNumber</td>
<td colspan="7" class="highlight-blue confluenceTd" data-highlight-colour="blue">REVISION NUMBER OBJECT - Object contained within the INTENT MODEL OBJECT; Contains metadata for the major and minor revision number of the intent.</td>
</tr>
<tr class="even">
<td class="highlight-green confluenceTd" data-highlight-colour="green">major</td>
<td class="confluenceTd">Int</td>
<td class="confluenceTd">NNNNNN</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Major revision number of the intent</td>
<td class="confluenceTd">1</td>
</tr>
<tr class="odd">
<td class="highlight-green confluenceTd" data-highlight-colour="green">minor</td>
<td class="confluenceTd">Int</td>
<td class="confluenceTd">NNNNNN</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Minor revision number of the intent</td>
<td class="confluenceTd">2</td>
</tr>
<tr class="even">
<td class="highlight-red confluenceTd" data-highlight-colour="red"><del>analyticOutcomesById</del></td>
<td colspan="7" class="highlight-red confluenceTd" data-highlight-colour="red"><div class="content-wrapper" title="">
<p><del>ANALYTIC OBJECT (OPTIONAL) - NOTE - To date, this has not been in use, but exists for future deployments in conjunction with the updated Analytics engine. (Patrick Marlow )</del></p>
</div></td>
</tr>
<tr class="odd">
<td class="highlight-yellow confluenceTd" data-highlight-colour="yellow">escalations</td>
<td colspan="7" class="highlight-yellow confluenceTd" data-highlight-colour="yellow">ESCALATION OBJECT (OPTIONAL) - List of objects contained within the primary object; Each embedded object contains metadata on escalations that occurred during the conversation</td>
</tr>
<tr class="even">
<td class="confluenceTd">escalationId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">escalationQueueId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">escalationQueueCode</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">conversationId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">agentId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">agentEmail</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxx@xxxxxx.xxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">escalationType</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">escalationStatus</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">escalationReason</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">pickupDate</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd">When present, this value is stored as a Java instant which is serialized as a number. Value is null if the conversation is not picked up.</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">pickupSla</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">handleSla</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">created</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-blue confluenceTd" data-highlight-colour="blue">escalationLog</td>
<td colspan="7" class="highlight-blue confluenceTd" data-highlight-colour="blue">ESCALATION LOG OBJECT - List of objects contained with the escalations object; Each embedded object contains metadata on the specifics of the current escalation</td>
</tr>
<tr class="even">
<td class="confluenceTd">escalationLogId</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
<td class="confluenceTd">36</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">agentId</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">agentEmail</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxx@xxxxxx.xxx</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">escalationLogStatus</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">created</td>
<td class="confluenceTd">Float</td>
<td class="confluenceTd">NNNNNNNNNNN.NNN</td>
<td class="confluenceTd">14</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">notes</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">16,777,215</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Optional</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd">counter</td>
<td class="confluenceTd">Integer</td>
<td class="confluenceTd">NNNNNN</td>
<td class="confluenceTd">255</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-yellow confluenceTd" data-highlight-colour="yellow">metrics</td>
<td colspan="7" class="highlight-yellow confluenceTd" data-highlight-colour="yellow">METRICS OBJECT - List of Objects contained within the primary object; Each embedded object contains metadata on default or custom metrics that were collected or upserted into the METRICS OBJECT.</td>
</tr>
<tr class="even">
<td class="confluenceTd">value</td>
<td class="confluenceTd">Various</td>
<td class="confluenceTd">Various</td>
<td class="confluenceTd">16,777,215</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><p>Clear text value of the metric that was collected.</p>
<p>For <strong>default</strong> metrics, there are various formats that can be exported, including string, int, float, and boolean.<br />
For <strong>custom</strong> metrics upserted from the customMetrics service, only string is allowed at this time.</p>
<div class="table-wrap">
<table class="wrapped confluenceTable">
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="2" class="confluenceTd"><p>Examples of <strong>default</strong> metric <strong>values</strong>:</p></td>
<td colspan="2" class="confluenceTd"><p>Examples of <strong>custom</strong> metric <strong>values</strong>:</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><strong>CODE/NAME</strong></td>
<td class="confluenceTd"><strong>VALUE</strong></td>
<td class="confluenceTd"><strong>CODE/NAME</strong></td>
<td class="confluenceTd"><strong>VALUE</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>user_email</p></td>
<td class="confluenceTd"><a href="mailto:patrick.marlow@ipsoft.com">patrick.marlow@ipsoft.com</a></td>
<td class="confluenceTd"><p>intent_list</p></td>
<td class="confluenceTd">intent1,intent2,intent3</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>agent_email</p></td>
<td class="confluenceTd"><a href="mailto:amelia@ipsoft.com">amelia@ipsoft.com</a></td>
<td class="confluenceTd"><p>trained_optimization</p></td>
<td class="confluenceTd">0</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>user_external_uid</p></td>
<td class="confluenceTd">12345678</td>
<td class="confluenceTd"><p>trained_performance</p></td>
<td class="confluenceTd">3</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>domain</p></td>
<td class="confluenceTd">employeeservices</td>
<td class="confluenceTd"><p>untrained_performance</p></td>
<td class="confluenceTd">1</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>escalated</p></td>
<td class="confluenceTd">false</td>
<td class="confluenceTd"><p>untrained_opportunity</p></td>
<td class="confluenceTd">0</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>executed_bpns</p></td>
<td class="confluenceTd">/Greeting/greetingBPN,/TicketStatus/</td>
<td class="confluenceTd">goals</td>
<td class="confluenceTd">4</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>primary_agent_pickup_sla_violation</p></td>
<td class="confluenceTd">false</td>
<td class="confluenceTd">client_important_metric</td>
<td class="confluenceTd">42</td>
</tr>
<tr class="even">
<td class="confluenceTd">total_handle_time</td>
<td class="confluenceTd">141</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>abandoned</p></td>
<td class="confluenceTd">1</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
</tbody>
</table>
</div></td>
<td class="confluenceTd">(see embedded table)</td>
</tr>
<tr class="odd">
<td class="confluenceTd">code</td>
<td class="confluenceTd">String</td>
<td class="confluenceTd">xxxxxxxxxxxxxxxxxx</td>
<td class="confluenceTd">100</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd"><p>Clear text name of the metric that was collected.</p>
<div class="table-wrap">
<table class="wrapped confluenceTable">
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="2" class="confluenceTd"><p>Examples of <strong>default</strong> metric <strong>names</strong>:</p></td>
<td colspan="2" class="confluenceTd"><p>Examples of <strong>custom</strong> metric <strong>names</strong>:</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><strong>CODE/NAME</strong></td>
<td class="confluenceTd"><strong>VALUE</strong></td>
<td class="confluenceTd"><strong>CODE/NAME</strong></td>
<td class="confluenceTd"><strong>VALUE</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>user_email</p></td>
<td class="confluenceTd"><a href="mailto:patrick.marlow@ipsoft.com">patrick.marlow@ipsoft.com</a></td>
<td class="confluenceTd"><p>intent_list</p></td>
<td class="confluenceTd">intent1,intent2,intent3</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>agent_email</p></td>
<td class="confluenceTd"><a href="mailto:amelia@ipsoft.com">amelia@ipsoft.com</a></td>
<td class="confluenceTd"><p>trained_optimization</p></td>
<td class="confluenceTd">0</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>user_external_uid</p></td>
<td class="confluenceTd">12345678</td>
<td class="confluenceTd"><p>trained_performance</p></td>
<td class="confluenceTd">3</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>domain</p></td>
<td class="confluenceTd">employeeservices</td>
<td class="confluenceTd"><p>untrained_performance</p></td>
<td class="confluenceTd">1</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>escalated</p></td>
<td class="confluenceTd">false</td>
<td class="confluenceTd"><p>untrained_opportunity</p></td>
<td class="confluenceTd">0</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>executed_bpns</p></td>
<td class="confluenceTd">/Greeting/greetingBPN,/TicketStatus/</td>
<td class="confluenceTd">goals</td>
<td class="confluenceTd">4</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>primary_agent_pickup_sla_violation</p></td>
<td class="confluenceTd">false</td>
<td class="confluenceTd">client_important_metric</td>
<td class="confluenceTd">42</td>
</tr>
<tr class="even">
<td class="confluenceTd">total_handle_time</td>
<td class="confluenceTd">141</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd">abandoned</td>
<td class="confluenceTd">1</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
</tbody>
</table>
</div>
<p><br />
</p></td>
<td class="confluenceTd">(see embedded table)</td>
</tr>
<tr class="even">
<td class="confluenceTd">custom</td>
<td class="confluenceTd">Boolean</td>
<td class="confluenceTd">true || false</td>
<td class="confluenceTd">5</td>
<td class="confluenceTd">N</td>
<td class="confluenceTd" style="text-align: center;">Required</td>
<td class="confluenceTd">Meta-field used to identify whether the metric was default or custom.</td>
<td class="confluenceTd">true</td>
</tr>
</tbody>
</table>
{% /version %}
