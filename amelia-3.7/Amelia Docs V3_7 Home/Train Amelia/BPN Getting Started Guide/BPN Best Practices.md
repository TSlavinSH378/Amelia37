BPN processes help determine how Amelia behaves during a conversation. Careful planning and thought is required to help Amelia converse in a natural human way and for her processes to be easy to create and maintain.
# Creating Conversations
The ability to converse with humans using natural language is Amelia's greatest strength. However, this is not easy to accomplish. In the same way people would notice and become annoyed if a person talked to us as if they were filling out a form, conversations with Amelia need to include basic human elements.
For example, all conversations have check-in points where we confirm what we've heard or correct what someone thinks we've said. Amelia's conversations follow a straight path but they also need check-in points and other features.
With the latest version of Amelia, this is especially important as Amelia now can jump from process to process based on conversation flow with the ability to return to the person's primary goal process. The process to configure Amelia must identify opportunities to make her conversation natural, as well as help create the shortest path to meet the person's needs. This will impact BPN Ask and Say tasks, in particular, but also configuration of her humanization features.
Amelia's conversations also include a happy path to follow if the user answers as expected. The path is defined by architect and client process diagrams.
## Qualities of a Good Conversation
In conversation, Amelia acts as a person would, in addition to her role as a customer support representative. Both qualities need to be included in a successful implementation of Amelia's conversations. In interactions with end users, her success largely depends on her ability to be like a human — moreover, one who is informed, educated, helpful, direct, down-to-earth, pleasant, and easy to understand.
On a deeper level, Amelia should be empathetic and responsive to a user’s emotional state. As Amelia converses, her language must become more and more authentic, nuanced, dynamic, and insightful. Conversations should elicit delight on the part of the user. Like a human agent, she should continually strive to build rapport. And when she does, she’ll become both functional and memorable.
This section contains a working list of best practices used to determine whether Amelia is indeed ready to be deployed and interact with real-world users. It is divided into two sections. The first section addresses best practices for Amelia’s interactions with end users and the second addresses best practices related to the language itself. More details are in a document available from the Linguistics group within the IPsoft Cognitive team.
## Best Practices to Work with Customers
The best customer service agents are efficient, personable, attentive to details, and proactive. They make things pleasant and more convenient, which has a positive effect on any customer.
These are some of the best practices for any agent, human or virtual.
-   Greet customers with enthusiasm
-   Set expectations up front
-   Start by listening
-   Be attentive to details
-   Anticipate questions and responses
-   Empathize with the customer
-   Respect the customer's time by being efficient
-   Prefer natural responses – for example, free text – over button selections
-   Advocate for the brand and its product or service
-   Have personality.
For example, one way for Amelia to set expectations up front is to explicitly state at the start of a chat what she can help with:
*Hello, my name is Amelia and I can help you with inquiries about your account.*
Better yet, the goal can be explicit before users even open the chat. The call to action that pushes the user toward an engagement with Amelia can be written in such a way that they know what Amelia can assist them with:
*Click here to get a car insurance quote from Amelia.*
## Best Practices for Amelia's Language
Before Amelia can be deployed, she must have a strong command of the language she’s meant to use in each use case. When Amelia communicates effectively and eloquently, she begins to resemble the very best human agents — and the customer’s experience will be better for it.
-   Every word, phrase, and sentence Amelia says must be crystal clear
-   Amelia needs to be thorough without overloading people with too much information too quickly
-   She should sound natural and plainspoken like a real person, not repetitive
-   Her utterances must be proofread to remove typos and other silly errors
-   Amelia must be consistent in her word choices and how she describes parts of the conversation
For example, to help Amelia be clear in her conversations, her utterances must mean what is intended and phrased in ways to make meaning clear. Sometimes, this is as easy as rearranging the clauses and/or phrases in a sentence.
*Unclear: You must first add your dependent daughter to pay your first month’s premium.*
*Better: To pay your first month’s premium, you must first add your dependent daughter.*
# General BPN Design
In general, when designing BPNs keep in mind two main principles, modularity and readability. Both principles should be considered when writing up BPNs. In general, a BPN that gets kicked off from an intent should give the reader an overview of the entire journey for that intent. The IPsoft Experience Design team will create their conversation flows this way to be picked up and filled in by engineers. Some parts of that BPN may then be abstracted to shared components like Script libraries or other BPNs.
## GDPR Compliance
> [!warning]  
>
> Conversations with Amelia can involve personal user data. Any information related to a natural person/data subject that can directly or indirectly identify that person is personal data. Personal data includes name, email, street address, phone number, bank details, medical information, and personal information, for example, gender preference, sexual orientation, and racial identity.
>
> Personal data must be anonymized, or excluded if possible, when creating BPNs and training Amelia. While Amelia instances can be configured to anonymize personal user data, BPNs and other artifacts should be constructed with privacy in mind. Personal data should only be collected and used for purposes that are legitimate, narrowly specified, and defined explicitly.
>
> Government regulations control the use and storage of personal data. For consumer data, follow the “[Principles relating to processing of personal data](http://www.privacy-regulation.eu/en/5.htm)” European Union GDPR article and other sources.

BPNs should not display any personal information back to a user, unless in an authenticated session with explicit sign-off from the client that displaying personal information should be part of the process. The same rule applies to any logging or variables that get stored. Do not use this information unless absolutely necessary with client permission. If needed, for Ask tasks in the BPN, use the Secure user input setting in the Properties Panel when asking for personal information:
![](attachments/11939398/11941315.jpg)
Figure. Secure user input Setting in Ask Task Properties Panel
## Naming Conventions
There are a number of possible naming conventions for BPNs and BPN folders. Consistent application of the convention is more important than the convention. When choosing a naming convention, apply it consistently across a particular project. Do not mix conventions within a project.
Since Groovy is the preferred language for BPN scripts, BPN and BPN folder naming conventions should ideally be consistent with Groovy naming conventions (`lowercase` for package names, `TitleCase` for class names, and `camelCase` for methods and variables). Therefore, since packages are represented by folders on the filesystem, and classes are files within those folders, these are the suggested naming conventions:
-   Use `lowercase` for BPN folder names. Since this corresponds to the Groovy (Java) package naming convention, also strive to keep folder names short (with no specific limit defined).
-   Use `TitleCase` for BPN names. This corresponds to the Groovy (Java) class naming convention.
## Modularity
Design BPNs with a clear name and purpose, the same as creating classes or functions in software development. This encourages reuse of existing work so BPNs can be extended and used in other areas without base modifications.
### BPN Wrapper
BPN Wrappers are commonly used when two distinct requests are spoken by a user in a similar way. The wrapper BPN must disambiguate by asking questions then route the user to an appropriate BPN process. Entities should be created to help clarify intent, where if the entity is filled, the wrapper BPN proceeds down the correct path. In cases where the user says something with no distinction, however, the wrapper BPN has to ask for clarification. For example, with the utterance "I want to add a person to my account" for Insurance, the wrapper BPN needs to ask, "Are you a new customer or existing customer" to route the user to the correct BPN.
### Ask Tasks & Context Switching
In programming, Ask tasks are akin to a "read line" function where we are asking for input from the user. At this point, the person may answer the question but also with the ability to Context Switch.
Context Switching is a key feature of Amelia. Settings in the Ask task Properties Panel enable or disable response subsystems on Imperative, Interrogative, and Declarative utterances, as well as enable or disable Intent switching.
Intent switching should be disabled only where context switching is definitely not wanted or it is a problem. For example, if the user is asked to describe something, their description should not trigger a context switch. Or during a key question, for example, "Do you want to finalize your payment?"). Disable intent switching only if there is no other option.
## Readability
As with code, other people will see your BPN. They should be able to easily read through it to determine the possible conversation paths. There are several best practices to encourage readability.
### Clean and Clear Routing
BPNs should always read from left to right. When branches in the flow occur they should go above or below the main BPN path and eventually rejoin the main path if necessary. 
![](attachments/11939398/11941316.png)
Figure. DO NOT DO THIS: A BPN With Unclear Routing  
![](attachments/11939398/11941317.png)
Figure. A BPN With Clean Clear Routing
### Logical Branching
When you need to create a logical branch in a BPN, this can be done directly off of a User or Script task. These are evaluated the same way as an exclusive gateway (so stop using exclusive gateways to avoid clutter).
![](attachments/11939398/11941318.png)
Figure. A BPN With Poor Logical Branching
![](attachments/11939398/11941319.png)
Figure. A BPN With Good Logical Branching
### Task Consolidation
Fewer tasks means less clutter, which means better readability. Dialogue tasks like say and ask will often be dictated by the Experience Design team, but should often be grouped where appropriate. There should almost never be a need for subsequent script tasks, they can probably be combined or examined as to why they are separate.
![](attachments/11939398/11941320.png)
Figure. A BPN With Poor Task Consolidation (Too Many Consecutive Script Tasks)
![](attachments/11939398/11941321.png)
Figure. A BPN With Good Task Consolidation (A Single Combined Script Task)
### BPN Comments
Use the TextAnnotation task in the BPN designer to create comments.
![](attachments/11939398/11941322.png)
Figure. A BPN With TextAnnotation Tasks
### Script Task Names
A traditional camel case script name should be used on script tasks to identify what they do. For more complex scripts, a longer description may be used combined with a name
![](attachments/11939398/11941323.png)
Figure. Use Camel Case Descriptions for Script Tasks
### Entire Say/Ask Task Variable-ized -* aka say ${this}*
Not only hard to read, but the output is not parsed. Try to only put in variables what needs to change - if largely different, BPN flow should be added to handle the different path.
![](attachments/11939398/11941324.png)
Figure. Include Context with Say/Ask Task that Use Variables
### JEXL Default Values
Any JEXL expression should have a default value. This is done using the ternary operator, for example: say ${var ? var : default}. If var has a value Amelia will say it, otherwise if var is null or otherwise evaluated to false, she will say default.
![](attachments/11939398/11941325.png)
Figure. JEXL Expressions Should Have a Default Value
# BPN Sub-Flows
A BPN has the ability to execute another BPN that exists in the same or parent domain of the active BPN. This is done using the "run the workflow ..." task, and allows the BPN designer to create parts of the workflow, that may be reused by other BPNs, in their own BPN and executed.
## Variable Propagation
BPN sub-flows can send and receive variables relative to the process flow that executes it. The Run the Workflow task that calls a sub-flow includes a Variable Propagation setting on its Properties Panel. This setting defines how variables propagate between the wrapper BPN and the sub-flow BPN.
![](attachments/11939398/11941326.png)
Figure. Variable Propagation for Run the Workflow Tasks
Table. Variable Propagation Options for Run the Workflow Tasks

| Option | Description |
| ----|----|
| Bidirectional | Process variables will be copied into the sub flow and back out to the executing flow |
| Push only | Process variables from the executing flow will be copied into the sub flow, but not back out |
| Pull only | Process variables from the executing flow will not be copied into the sub flow, but any process variables created in the sub flow will be copied back to the executing flow |
| None | No variables will be passed in or out of the sub flow |

The Variable Propagation setting impacts the performance of large interconnected BPN flows. A large amount of process variables calling several sub flows will be read or written to the database every time a new process instance starts or resumes. Limit the amount and propagation direction of process variables to avoid performance issues.
## Escalations
Escalations from Amelia to a human is a common use case. The Escalate task has two components, an escalation queue and an escalation reason. It is best practice to use both of these components, to reference and escalation queue and reason.
![](attachments/11939398/11941327.jpg)
Figure. Escalate Options
> [!warning]  
>
> Before Amelia 3.4.0, not using the full escalation syntax caused a failed escalation or missing information in the Conversations page used to manage escalations.

### Assign an Escalation Queue
If a queue is not defined in the Escalate task, a BPN will attempt to escalate to the default queue set for the BPN. To set the default queue for a BPN, click anywhere in the BPN background then open the Properties Panel and select the queue from the Default escalation queue setting.
![](attachments/11939398/11941328.png)
Figure. Set Default Escalation Queue for a BPN
If the BPN default escalation queue is not set, the BPN will escalate to the default queue set for the current domain. The Escalations setting on a detail page for a domain is available by clicking the System Settings link on the left side of Amelia's administration pages then clicking the Domains link that appears. Find the domain listed in the Domains workspace and click to open the detail page for the domain.
![](attachments/11939398/11941329.png)
Figure. Escalations Setting on a Domain Detail Page
### Provide an Escalation Reason
The escalation reason should be a short description of why the conversation is being escalated to an agent, something that will give an Agent context when picking up the conversation, but also something that can be useful for post chat analysis.
![](attachments/11939398/11941330.jpg)
Figure. BPN Escalation Reason Displays on Active Conversations Page
## Conversation Event Processes
Each domain can have BPNs assigned to handle conversation events, for example, a process to run before escalation and another process to run after a conversation is closed. The Conversation Event Processes settings on a detail page for a domain are available by clicking the System Settings link on the left side of Amelia's administration pages then clicking the Domains link that appears. Find the domain listed in the Domains workspace and click to open the detail page for the domain.
![](attachments/11939398/11941331.png)
Figure. Select BPNs for Conversation Event Processes
### Pre-Escalation BPNs
For each domain, a pre-escalate BPN can be specified to run before the conversation is escalated to an Agent.
A pre-escalation BPN performs any action that needs to take place when Amelia finished interacting with a user. Updating a ticketing system may be a common task performed in a pre-escalate BPN. Keep in mind the pre-escalation BPN isn't the end of a conversation. The Agent should continue to resolve the conversation.
> [!info]  
>
> Do not put an Escalate task in a pre-escalation BPN. This creates an infinite loop.

### Pre-Close BPNs
A pre-close BPN should be used for actions that need to take place when a conversation closes, for example, scripts to log information or integrations to update external systems.
Pre-close BPNs should be defined as headless with no dialogue or interaction with the user. To set the type of BPN, click anywhere in the BPN background then open the Properties Panel and select Headless from the Type setting.
![](attachments/11939398/11941332.jpg)
Figure. Set BPN Type to Headless
When monitoring a conversation with the Process Memory pane of the Mind view, visible with the default Amelia chat interface, the pre-close BPN will not display as part of the BPN. However, the pre-close BPN will run. Based on actions the pre-close BPN performs, check the log files or external systems to confirm results.
> [!info]  
>
> Do not put a Close the Conversation task in a pre-close BPN. This creates an infinite loop.

# BPN Variable Scopes
Variables can be kept in two different scopes in the context of a conversation. The transient scope exists for the entire conversation and will be accessible by all processes until the conversation is closed. The execution scope is specific to one process instance. Currently, only process variables can be used on edge expressions or in task names. 
## Transient Variables
The [Transient Variable Service](#) allows for the creation and recovery of transient variables longer than 64kB. Script tasks can use `transientVariableService` to access these variables. Transient variables are accessible across all processes executed during a conversation. They are removed once the conversation is closed by the user or due to timeout.
## Process Variables
Script tasks and libraries can use `execution` to access process variables using the [Execution Object](#). The execution object provides access to a variety of process instance elements as variables, for example, to get the value of variables captured by Amelia, user information, and unique identifiers for conversation, status, and processes.
# Script Libraries to Reuse Code
[Script libraries](#) share code between BPNs with similar needs and functions, for example, creating custom UI components, preparing integration request payloads, and any repeatable code used by multiple scripts in a BPN or several BPNs.
# Tabular Data
[Tabular data](#) is a structured data file used to read static data without an external Camel integration. Tabular data tables are only for reading data. Data cannot programmatically update.
# Multimedia Content Manager
The [Content Manager](#) can be used to store multimedia files that will be presented to the user during a conversation. The [Present task](#) displays data stored in the content manager while the [Request task](#) collects data files and stores them in the content manager.
While using a Script task to capture the full media URL then copy/pasting the URL in a web browser will display the uploaded image, the image will not appear in the Buckets workspace. Amelia V3 has two scopes for multimedia files, system and conversation. System scope includes files uploaded and created in the Buckets workspace. Conversation scope includes files uploaded and managed as part of a conversation controlled by a BPN process. BPNs look for multimedia files first in the conversation scope and, if not found, search the system Buckets.
