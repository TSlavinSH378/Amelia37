-   [The Domain Interface](#Domains-TheDomainInterface)
    -   [Basics](#Domains-Basics)
    -   [Domain Switching](#Domains-DomainSwitching)
    -   [Anonymous Access](#Domains-AnonymousAccess)
    -   [Conversation Event Processes](#Domains-ConversationEventProcesses)
    -   [Escalations](#Domains-Escalations)
    -   [New Conversation User Create](#Domains-NewConversationUserCreate)
    -   [Subsystem Responders](#Domains-SubsystemRespondersSubsystemResponders)
        -   [AcknowledgeDefault](#Domains-AcknowledgeDefault)
        -   [Affective](#Domains-Affective)
        -   [AIML](#Domains-AIML)
        -   [BPN](#Domains-BPN)
        -   [CQA](#Domains-CQA)
        -   [Dontknow](#Domains-Dontknow)
        -   [EpisodicMemory](#Domains-EpisodicMemory)
        -   [EQA](#Domains-EQA)
        -   [Escalate](#Domains-Escalate)
        -   [FAQ](#Domains-FAQ)
        -   [IntentFAQ](#Domains-IntentFAQ)
        -   [SemNet](#Domains-SemNet)
        -   [SemNetDoc](#Domains-SemNetDoc)
        -   [SocialTalk](#Domains-SocialTalk)
        -   [UnknownProblem](#Domains-UnknownProblem)
    -   [User Message Content Masks](#Domains-UserMessageContentMasks)
    -   [1Desk](#Domains-1Desk)
    -   [1RPA](#Domains-1RPA)
    -   [Bean Mappings](#Domains-BeanMappings)
-   [Create and Update a Domain](#Domains-CreateandUpdateaDomain)
-   [Filter Incoming Messages](#Domains-FilterIncomingMessages)
-   [Filter Transcript Data](#Domains-FilterTranscriptData)
Domains organize distinct sets of knowledge, users, groups, roles, escalation teams, and other systems.  The global domain should be the parent to one or more child domains to allow future changes without affecting the global domain settings.
While domains can be organized into parent-child domains, sharing knowledge and systems, no domain can have more than one parent domain. Chats also can use a URL to access a specific domain and its knowledge.
The global domain contains Amelia's default personality and chit chat training. Parent and child domains are created below the global domain to segregate knowledge. For example, parent and child domains can hold active responders, greetings, and rote response behaviors before she escalates or closes a conversation. Parent and child domains also can be configured for languages, time zones, default escalation queues, text to speech (TTS), and other functionality.
Intent models, created by training Amelia to determine user intent, are not inherited from parent domains. However, entities, entity models, integrations, BPNs, as well as the content manager, script library, and tabular data capabilities can be inherited from parent domains.
Roles, groups, authorities, and related functionality also are organized by domain. Users can have access to multiple domains. Because there is no hierarchy for permissions, access to each domain has to be explicitly defined by user groups and roles. User groups should be set up for each distinct set of domains for which a group of users will edit Amelia's knowledge.
> [!warning]  
>
> The global domain can access child domains and their entities, entity models, intents, intent models, content manager, script libraries, tabular data, integrations, and BPNs (using a Run the Workflow task).
>
> The closest element has the highest priority in cases where a parent or child domain has the same name for an integration flow or other element. For example, if the global, parent, and current domains each have an integration flow named Weather, a BPN in the current domain will call the Weather flow from the current domain. If there is no Weather flow in the current domain, the BPN in the current domain would call the Weather flow defined in the parent domain.

# The Domain Interface
To edit or add a domain, log in to Amelia's administration pages and select System Settings then Domains from the left side navigation links. The Domains workspace appears with a New Domain button at the top right.
The default Domains workspace includes a search box to find existing domains. To edit an existing domain, click the notepad edit icon to the left of the name. Click the New Domain button to add a domain.
![](attachments/11940269/25462287.png)
Figure. New Domain Form
The fields in the Domains workspace are described below.
Table. New Domain Form Fields
<table class="relative-table wrapped confluenceTable" style="width: 86.8421%;">
<colgroup>
<col style="width: 17%" />
<col style="width: 82%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Field</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd"><h4 id="Domains-Basics"><strong>Basics</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd">Name</td>
<td class="confluenceTd">The unique name of the domain</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Code</td>
<td class="confluenceTd">Type a code name for the domain, usually the Name without spaces</td>
</tr>
<tr class="even">
<td class="confluenceTd">Enabled</td>
<td class="confluenceTd">Select whether or not the domain is enabled and active</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Hidden</td>
<td class="confluenceTd"><p>Select whether or not the domain is visible only to users with global access permissions.</p>
<p>Selecting this setting hides the domain name on any user selection screen. However, conversations are allowed if the Allow Conversations setting is selected and the domain is directly referenced with a URL querystring or custom user interface settings.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow Conversations</td>
<td class="confluenceTd">Select whether or not to allow conversations for this domain</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Allow 'run the workflow'?</td>
<td class="confluenceTd">Select whether or not to allow BPN processes in the domain can use a Run the Workflow task to run additional BPN processes from within a BPN</td>
</tr>
<tr class="even">
<td class="confluenceTd">Parent Domain</td>
<td class="confluenceTd">If appropriate, select the parent domain</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Authentication Policy</td>
<td class="confluenceTd">Displays a dropdown list of active authentication policies</td>
</tr>
<tr class="even">
<td class="confluenceTd">Locale</td>
<td class="confluenceTd">Select the geographic location and language</td>
</tr>
<tr class="odd">
<td class="confluenceTd">TimeZone</td>
<td class="confluenceTd">Displays a dropdown list of world time zones</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Avatar</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Voice</td>
<td class="confluenceTd"><p>Type in the name of Amelia's text to speech (TTS) voice. For English, the voice is VW Julie.</p>
<p>TTS settings require a TTS server be configured and available with the appropriate voices installed. IPsoft has TTS servers in place for IPsoft hosted instances. Amelia instances not hosted by IPsoft need the appropriate separate TTS setup for settings to work properly.</p>
<div class="table-wrap">
<pre class="table"><code>| Language | Voice Name |
| ----|----|
| English (American) | VW Julie |
| Japanese | VW Misaki |
| Chinese (Mandarin) | VW Hui |
| Korean | VW Yumi |
| French | Florence |
| Swedish | Astrid |
| Norwegian | Vilde |
| Spanish | Ximena |
| Danish | Frida |
| Arabic | Laila |
| Russian | Olga |
| Dutch | Lotte |
| Italian | Silvana |
| Turkish | Zeynep |
| Polish | Zoisa |
| Portuguese | Amalia |
| German | Marlene |
| Romanian | Ioana |</code></pre>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">WebGI Enabled</td>
<td class="confluenceTd">Select or deselect WebGI</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Image Enabled</td>
<td class="confluenceTd">Select or deselect Image</td>
</tr>
<tr class="even">
<td class="confluenceTd">Avatar Image</td>
<td class="confluenceTd">Click the folder icon to upload an avatar image</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Branding Image</td>
<td class="confluenceTd">Click the folder icon to upload a logo</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Translation</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">User Translation Enabled</td>
<td class="confluenceTd">Select to enable or deselect to disable user's ability to select a language for their conversation</td>
</tr>
<tr class="even">
<td class="confluenceTd">Agent Translation Enabled</td>
<td class="confluenceTd">Select to enable or deselect to disable agent's ability to select a language for their conversation</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><h4 id="Domains-DomainSwitching"><strong>Domain Switching</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow Switch In</td>
<td class="confluenceTd">Select to allow Amelia to switch into this domain based upon the current context in a conversation</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Allow Switch Out</td>
<td class="confluenceTd">Select to allow Amelia to switch out of this domain based upon the current context in a conversation</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><h4 id="Domains-AnonymousAccess"><strong>Anonymous Access</strong></h4></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Allow Anonymous?</td>
<td class="confluenceTd">Select or deselect allowing anonymous access to interact with Amelia</td>
</tr>
<tr class="even">
<td class="confluenceTd">Allow Anonymous View?</td>
<td class="confluenceTd">Select or deselect allowing anonymous viewing of Amelia or require authentication to see Amelia</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><h4 id="Domains-ConversationEventProcesses"><strong>Conversation Event Processes</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd">Greeting Intent</td>
<td class="confluenceTd">Select an intent from a list of active intents to associate with the greeting process</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Greeting Process</td>
<td class="confluenceTd">Select from a list of active BPNs to instruct Amelia's greeting process</td>
</tr>
<tr class="even">
<td class="confluenceTd">Pre-Escalation Process</td>
<td class="confluenceTd">Select from a list of active BPNs to direct Amelia's actions prior to an escalation</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Run on Transfer?</td>
<td class="confluenceTd">Select to run the pre-escalation process when a conversation is transferred to another domain</td>
</tr>
<tr class="even">
<td class="confluenceTd">Pre-Close Process</td>
<td class="confluenceTd">Select from a list of active BPNs to instruct Amelia's interactions prior to closing a conversation</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><h4 id="Domains-Escalations"><strong>Escalations</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd">Default Queue</td>
<td class="confluenceTd">Select from a list of configured escalation queues created with the Escalation Queues tab on left side of Amelia's administration pages. Note a default escalation queue must be selected for escalation to work.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><h4 id="Domains-NewConversationUserCreate"><strong>New Conversation User Create</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd">Group</td>
<td class="confluenceTd">Select the group to assign new conversations for this domain</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><div class="content-wrapper">
<h4 id="Domains-SubsystemRespondersSubsystemResponders"><strong>Subsystem Responders</strong></h4>
</div></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><p>Click the Enabled check box to the right of a responder to toggle enable or disable the responder for this domain. To evaluate utterances, Amelia calls responders in a set order of priority, from first to last:</p>
<ul>
<li>Escalate </li>
<li>Bpn</li>
<li>Cqa</li>
<li>EpisodicMemory</li>
<li>IntentFAQ</li>
<li>FAQ</li>
<li>Semnet</li>
<li>SemnetDoc</li>
<li>EQA</li>
<li>Affective</li>
<li>AIML</li>
<li>SocialTalk</li>
<li>UnknownProblem</li>
<li>AcknowledgeDefault</li>
<li>DontKnow</li>
</ul>
<p><br />
</p>
<p>Amelia predicts two classes for user utterances: Request and Generic Problem.</p>
<p><strong>Request</strong> corresponds to utterances from the user that express problems or requests, for example,"Can/could you", "I want/need", and all imperative sentences. It introduces a new subsystem responder UnknownProblem. This responder answers when an utterance is classified as a Request, and if its response is selected, the escalation count is incremented. Thus, this responder should enable more reliable escalations, as it directly "catches" utterances that intent classifiers don't pick up, but definitely express some sort of request from the user.</p>
<p><strong>Generic Problem</strong> corresponds to incomplete or introductory problem statements from the user, like "I have a question" or "I have a problem". If this is identified, Amelia will ask an elaborating question via the EQA (elaborating question asking) responder.</p>
<p>The new responder is enabled by default, and EQA will be triggered by Generic Problem without any configuration or changes. The UknownProblem and EQA responders are returned if they score highest in priority compared to the other responders.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-AcknowledgeDefault">AcknowledgeDefault</h5></td>
<td class="confluenceTd">If Amelia understands an utterance as a declarative or imperative, not an interrogative or question, and no other module answers, this responder triggers. It uses an entry from the ACKNOWLEDGE response pool.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="Domains-Affective">Affective</h5></td>
<td class="confluenceTd">If no more specific module has an answer, this responder allows Amelia to emphasize with users. Amelia will respond to negative statements such as “Traffic was terrible today” and also compliments from user like, “You are doing a great job.”  It uses a variety of response pools for that like COMPLIMENT_REPLY_POSITIVE_INFORMAL.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-AIML">AIML</h5></td>
<td class="confluenceTd">This module has pre-trained chit-chat which is far reaching in English. It is based on pre-loaded AIML files visible in Amelia's global domain. It will answer personal questions (Who are you?) but can answer a wide range of questions, depending on AIML training. Amelia choses AIML, when enabled), after more specific use case training with Intents, BPNs, and SemNet. This responder is often turned off because the standard English AIML is far reaching and thus requires a high effort to curate the AIML files.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="Domains-BPN">BPN</h5></td>
<td class="confluenceTd">Allows the BPN sub-system module to interact with the user after an intent fires off a BPN.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-CQA">CQA</h5></td>
<td class="confluenceTd">For Amelia 3.5+, the clarifying question asker (CQA) module asks a clarifying question when there is a possibility of ambiguity in the user's utterance between two intents.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="Domains-Dontknow">Dontknow</h5></td>
<td class="confluenceTd">This responder is chosen if no other responds and f Amelia understands a user utterance is an interrogative, not declarative or imperative. It uses an entry from the DONTKNOW response pool.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-EpisodicMemory">EpisodicMemory</h5></td>
<td class="confluenceTd">This module answers based on Episodic Memory training. If there is no Episodic Memory training planned, this responder can be disabled.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="Domains-EQA">EQA</h5></td>
<td class="confluenceTd"><p>The Elaborate Question Asking (EQA) responder generates a clarifying question in response to an incomplete user utterance. For example, if a user says, "I want," then Amelia might use the EQA responder to ask, "What do you want?" EQA only responds under very specific conditions.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-Escalate">Escalate</h5></td>
<td class="confluenceTd">This responder allows Amelia to escalate a conversation. Should not be turned off in regular Amelia deployments.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="Domains-FAQ">FAQ</h5></td>
<td class="confluenceTd">The FAQ responder is part of SemNet and can answer based on uploaded FAQ Excel sheets. Answers have a lower priority than intents and, if FAQs and intents overlap to provide a poor response, this responder should be deactivated.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-IntentFAQ">IntentFAQ</h5></td>
<td class="confluenceTd">The IntentFAQ responder answers based on trained FAQ intents with an FAQ answer in the intent definition. Intents can be uploaded as an Excel sheet on the SemNet screen.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="Domains-SemNet">SemNet</h5></td>
<td class="confluenceTd">This responder can answer out of the conversation context of a conversation, for example, after an utterance, “The sky is blue,” Amelia might answer with the color of the sky. Because this responder can provide unexpected answers during production, it is recommended to be turned off for production domains.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-SemNetDoc">SemNetDoc</h5></td>
<td class="confluenceTd">The SemNet responder can answer with data from uploaded PDFs. Documents must be well curated. The responder may generate unexpected answers and the module should be turned off if this is a problem.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="Domains-SocialTalk">SocialTalk</h5></td>
<td class="confluenceTd">This responder is a chit-chat responder like AIML but based on grammar, less encompassing, and uses SOCIALTALK response pools. That can be a simpler way to provide smalltalk capabilities without AIML.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="Domains-UnknownProblem">UnknownProblem</h5></td>
<td class="confluenceTd">This responder answers when an utterance is classified as a Request, and if its response is selected, the escalation count is incremented. Thus, this responder should enable more reliable escalations, as it directly "catches" utterances that intent classifiers don't pick up, but definitely express some sort of request from the user.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Transcripts</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Anonymize User</td>
<td class="confluenceTd"><p>Select to replace first name, last name, and email addresses with configurable mask values. The values are set in these settings with default values Firstname, Lastname, and em@il.anon:</p>
<p>amelia.transcripts.anonymous-first-name=Firstname<br />
amelia.transcripts.anonymous-last-name=Lastname<br />
amelia.transcripts.anonymous-email=em@il.anon</p>
<p>These settings are in the application.properties file located in the amelia-engine-service folder.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Add</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Click the  button to add a mask pattern to match and content to replace.</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Delete</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Click the button to the right of a match/replace entry to delete the entry.</p>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">Auto-Cleanup Days Retained</td>
<td class="confluenceTd">Default is 60 days. See Filter Transcript Data section below for details.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><h4 id="Domains-UserMessageContentMasks"><strong>User Message Content Masks</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd">Add</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Click the  button to add a mask pattern to match and content to replace. See Filter Incoming Messages section below for details.</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Delete</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Click the  button to the right of a match/replace entry to delete the entry</p>
</div></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Amelia Settings</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Amelia User</td>
<td class="confluenceTd">Select user account to have Amelia use a name other than Amelia. To change Amelia's name, first create a user account with the System Settings &gt; Users workspace. Then select the new user account with this dropdown list.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><h4 id="Domains-1Desk"><strong>1Desk</strong></h4></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Instance</td>
<td class="confluenceTd">Select the instance Amelia will use for conversations in this domain</td>
</tr>
<tr class="even">
<td class="confluenceTd">Client Code</td>
<td class="confluenceTd">Type the 1Desk client code to use for this domain. Multiple Amelia domains may map to the same client in 1Desk.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Default User Domain?</td>
<td class="confluenceTd">When automatically creating users, use this domain as their primary domain for users on the 1Desk side in the configured client.  For example, if there is an Acme Client in 1Desk and two domains – Acme HR and Acme IT in Amelia, the domain with this checkbox checked is where Acme users will be created in Amelia.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><h4 id="Domains-1RPA"><strong>1RPA</strong></h4></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Instance</td>
<td class="confluenceTd">Select the instance Amelia will use for conversations in this domain</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><h4 id="Domains-BeanMappings"><strong>Bean Mappings</strong></h4></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Add</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Click the <img src="attachments/11940269/25462292.png" /> button to add a Spring Bean mapping then click the Save button at the top of the form</p>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">Delete</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Click the  button to the right of a bean mapping Property Name and Value then click the Save button at the top of the form</p>
</div></td>
</tr>
</tbody>
</table>
# Create and Update a Domain
The Domains workspace is available by clicking the System Settings heading then the Domains link on Amelia's left side administration pages navigation. The Domains workspace will appear with a list of existing domains, if any.
1.  Click the Systems Settings heading then click the Domains link.  
    To edit an existing domain, click the notepad edit icon to the left of the domain name. The Domain edit form appears.  
    To add a new domain, click the New Button button at the top right of the Domains workspace. The New Domain form appears.
2.  Complete the Domains edit form that appears on the right side of the interface.
# Filter Incoming Messages
The Domains form includes the ability to mask user data before the data appears on screen for the user and any agent. Data patterns and masks can be set for a domain with the User Message Content Masks panel. Once the user or agent types data that matches a pattern, Amelia applies a mask.
> [!warning]  
>
> This feature masks data in real time once a pattern is matched. The Transcripts panel of the Domains form masks data as it is stored in databases.

To set mask patterns for secure data, for example, Social Security Numbers or credit card numbers, in the Amelia administration pages click System Settings link on the left side then click the Domains link. The Domains page will appear with a list of domains. Click the notepad icon to the left of a domain name to display the properties page for the domain. Then scroll down to the User Message Content Masks section.
Click the green plus (+) icon to the right of the Match / Replace heading to display a form. Type the regular expression pattern in the Match field and the mask to use if a match happens, for example, `\d(3)-\d(2)-\d(4)` for a Match, and `###-##-####` for the replacement mask would anonymize any Social Security numbers.
![](attachments/11940269/11940271.png)
Figure. User Message Content Masks Panel
# Filter Transcript Data
To mask first name, last name, and email address information in log files, three settings have been added with a check box on the form used to create and edit domains in Amelia.
These settings, with default mask values `Firstname`, `Lastname`, and `em@il.anon`, are located in the application.properties file in the amelia-engine-service folder:
``` groovy
amelia.transcripts.anonymous-first-name=Firstname
amelia.transcripts.anonymous-last-name=Lastname
amelia.transcripts.anonymous-email=em@il.anon
```
The Domains form used to create and edit domains in Amelia also has been updated to add a Transcripts panel with a single check box, Anonymize. Selecting the check box activates masking of first name, last name, and email addresses in Amelia’s log files for the domain. The Transcripts panel also includes the ability to create matches and patterns to anonymize specific data patterns, for example, credit card numbers.
Click the green plus (+) icon to the right of the Match / Replace heading to display a form. Type the regular expression pattern in the Match field and the mask to use if a match happens, for example, `\d(3)-\d(2)-\d(4)` for a Match, and `###-##-####` for the replacement mask would anonymize any Social Security numbers.
![](attachments/11940269/11940270.png)
Figure. Transcripts Panel in Domain Form
Table. Transcripts Panel Elements

| Element | Description |
| ----|----|
| Anonymize User | When selected, activates masking of first name, last name, and email addresses in Amelia’s log files for the domain. |
| Match | A regular expression that matches sensitive data to be masked. |
| Replace | A pattern to replace and mask sensitive data. |
| Auto-Cleanup Days Retained | Number of days to retain log data before recycling the log file. Default is 90 days. Amelia audit logs are retained for 90 days instead of 60 days, the prior default setting. Retention time can be configured with the amelia.job.audit-cleanup-keep-past.days application property.The property is set in the /apps/IPsoft/amelia/amelia-common-config/application.properties file:
amelia.job.audit-cleanup-keep-past.days = 90

\|
**More System Settings**
-   [Authentication Systems](Authentication%20Systems)
-   [Authentication Policies](Authentication%20Policies)
-   [Escalation Teams](Escalation%20Teams)
-   [Escalation Queues](Escalation%20Queues)
-   [Domains](Domains)
-   [Groups](Groups)
-   [Users](Users)
-   [Roles](Roles)
-   [Custom UI Bundles](Custom%20UI%20Bundles)
-   [Audit Log](Audit%20Log)
-   [Facial Recognition](Facial%20Recognition)
-   [Response Pools](Response%20Pools)
-   [1Rpa Instances](1Rpa%20Instances)
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-11-19_11-18-24.png](attachments/11940269/11940270.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-19_11-16-43.png](attachments/11940269/11940271.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-6-5_9-38-6.png](attachments/11940269/11940272.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-3-20_12-27-19.png](attachments/11940269/11940273.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-4-9_11-44-43.png](attachments/11940269/11944113.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-4-9_11-45-19.png](attachments/11940269/11944114.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-29_15-46-22.png](attachments/11940269/25462287.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-29_15-56-18.png](attachments/11940269/25462292.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-29_15-57-11.png](attachments/11940269/25462293.png) (image/png)  
