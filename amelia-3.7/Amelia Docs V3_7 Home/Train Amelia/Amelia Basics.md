# How to Use Amelia
Amelia has several user interfaces. Most end users will use a customized interface to chat with Amelia. Agents and Supervisors handling escalations of conversations use the basic conversation interface that includes the ability to access conversations and see how Amelia processes conversations to respond to people.
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
### Administration Workspace
Software and knowledge engineers use Amelia's administration pages to configure and train Amelia to handle conversations and tasks. Refer to [Amelia Navigation Links](Amelia%20Navigation%20Links) for details about the main links on the left side of the administration workspace.
![](attachments/11939353/11941028.jpg)
Figure. Amelia's Administration Area
### Amelia Flyout in Administration Workspace
The top right corner of Amelia's administration workspace includes a basic instance of Amelia to test functionality before using the default chat interface or custom user interface. Click the circle to display a chat interface. The chat interface has all the features of the default chat interface and custom user interface, for example, the ability to select a domain, refresh the conversation, and change the conversation language.
![](attachments/11939353/11941339.png)
Figure. Amelia Flyout
# How Amelia Works
Basic ideas and concepts impact how Amelia performs during conversations. Before starting to work with Amelia, it's useful to review how Amelia works in simple terms.
## Who is Amelia?
Amelia is a cognitive software agent who appears as a digital avatar who listens and interacts with people to solve problems. She reads natural language, understands context, applies logic, infers implications, learns through experience and senses emotions. She understands what is meant, not only what a person says. Amelia can take on a wide variety of rote business and engineering tasks.
## How Does Amelia Know What to Say?
When Amelia engages in a conversation, her words are decided based upon a mix of a defined process and careful evaluation of the other person's words, phrasing, and earlier parts of the conversation, as well as Amelia's experiences with similar conversations. For example, she tracks the emotional state of the conversation.
Her defined process workflow uses the Business Process Network (BPN) standard to define a series of tasks, relationships between tasks, and how a conversation flows. Some BPN workflows give Amelia the ability to jump between tasks based on how a conversation progresses. BPN flows also tell Amelia what to say and when, as appropriate. Which BPN Amelia chooses depends on how she is trained and where her knowledge is stored.
![](attachments/11939353/11941029.jpg)
Figure. The Amelia 3.7 BPN Workspace with a Simple BPN
In addition, Amelia has a pool of standard responses to handle routine conversation that might happen. For example, if Amelia doesn't have an answer, she'll say, "I don't know." She also can say thank you different ways, and respond to praise different ways.
Amelia uses intelligent arbitration between the responses from a variety of subsystems to evaluate user utterances and decide how to respond. Each subsystem use different methods to evaluate current and past user utterances. She picks the highest rated response from all subsystems each time she responds.
A team of IPsoft Cognitive engineers and conversation experience designers work with clients to create BPNs and other elements to shape Amelia's responses. 
For details about creating process flows to help Amelia know what to say, refer to the [BPN Getting Started Guide](BPN%20Getting%20Started%20Guide).
## How Is Amelia Trained?
In addition to defining her process flow with BPNs, training Amelia involves preparing data and creating models she uses to process utterances and respond in a helpful way. Amelia only needs one intent model per domain. The model contains interconnected and weighted data about a specific knowledge area, for example, car insurance quotes.
These data types help Amelia understand user utterances in a conversation:
-   **Intents** can connect specific user phrases and responses from Amelia to confirm an intent or call a BPN. For example, "I lost my hotel bill. How can I get a new one?" expresses a goal, retrieve a hotel bill.
-   **Entities** capture key data Amelia needs to complete her tasks and can be referenced in one or more BPNs. For example, to retrieve a hotel bill, Amelia needs to know the person's name, dates for checkin and checkout, and other data stored as entities.
-   Pre-existing chat conversations, classifiers, and other data sources are used to create **annotated models** to train Amelia.
Intents, entities, and annotating data are ways to train Amelia how to process and understand natural language, the natural unconstructed way people talk. This diagram shows the high level conversation flow Amelia uses to process utterances with intents and entities.
![](attachments/11939353/11939358.png)
Figure. Amelia's Conversation Flow
Training Amelia also can include grammars, sets of rewriting rules that represent Natural Language patterns concisely, for example, the unconstructed casual way people talk. Grammars help Amelia use natural language to recognize the user’s intent and data entities needed to address their intent.
Business Process Networks (BPNs) also use grammars to help provide Amelia with structure to follow processes, not only the rote question and answer structure of FAQs but also more complex processes with multiple paths and outcomes.
A team of IPsoft Cognitive engineers, conversation experience designers, and user interface designers work with clients to train Amelia. 
For details about training Amelia, refer to the [Amelia Trainer Guide](Amelia%20Trainer%20Guide).
## How Do Domains Work?
Domains organize Amelia's distinct sets of knowledge, users, groups, roles, escalation teams, and other systems. All Amelia instances begin with the global domain at the top level. The global domain should be the parent to one or more child domains to allow future changes without affecting the global domain settings.
While domains can be organized into parent-child domains, sharing knowledge and systems, no domain can have more than one parent domain. Chats also can use a URL to access a specific domain and its knowledge.
The global domain contains her default personality and chit chat training. Parent and child domains are created below the global domain to segregate knowledge. For example, parent and child domains can hold active responders, greetings, and rote response behaviors before she escalates or closes a conversation. Parent and child domains also can be configured for languages, time zones, default escalation queues, text to speech (TTS), and other functionality.
Intent models, created by training Amelia to determine user intent, are not inherited from parent domains. However, entities, entity models, integrations, BPNs, as well as the content manager, script library, and tabular data capabilities can be inherited from parent domains.
Roles, groups, authorities, and related user functionality also are organized by domain. Users can have access to multiple domains. Because there is no hierarchy for permissions, access to each domain has to be explicitly defined by user groups and roles. User groups should be set up for each distinct set of domains for which a group of users will edit Amelia's knowledge.
> [!warning]  
>
> The global domain can access child domains and their entities, entity models, intents, intent models, content manager, script libraries, tabular data, integrations, and BPNs (using a Run the Workflow task).
>
> The closest element has the highest priority in cases where a parent or child domain has the same name for an integration flow or other element. For example, if the global, parent, and current domains each have an integration flow named Weather, a BPN in the current domain will call the Weather flow from the current domain. If there is no Weather flow in the current domain, the BPN in the current domain would call the Weather flow defined in the parent domain.

IPsoft Cognitive engineers work with clients to design and configure Amelia's domains, user accounts, and other administrative details. 
For information about how to configure domains, refer to the [Administration Guide](Domains) and the [Domains](Domains) section.
## Does Amelia Work with Other Computer Systems?
If needed, Amelia connects with other computer systems within tasks as part of a BPN process flow. She can cancel credit cards, for example, or retrieve paid time off balances as part of a conversation.
Amelia's integration service runs separately from Amelia, possibly located on another host or hosts, and allows her to interact with external systems. Integration flows are Apache Camel contexts created with Amelia V3 administration tools and deployed to these remote processes with gRPC, a universal remote procedure call standard.
The integration service unpacks the data received from an external system and deploys it in a Spring application separate from the parent context and any other flows running on the service. The integration service relies on Spring integration to handle RPC-style calls over RabbitMQ message broker and then internally hands off to Apache Camel to execute a request.
IPsoft Cognitive engineers work with clients to integrate Amelia with external computer systems.
For information about how to configure integrations, refer to the [Integrations Guide](Integrations%20Guide).
## Is Amelia's Interface Adaptable?
Amelia has several interfaces. How people interact with Amelia determines which interface works best. The default administration interface, for example, includes tools to view how her subsystems respond in real time. She can appear as a small custom overlay floating above a web page or in a chat interface with data from the conversation displayed on the right side of the screen. Amelia also can appear on phones and tablets or devices like intelligent home speakers.
IPsoft Cognitive engineers work with clients to design and deploy an appropriate interface for Amelia.
For information about Amelia's interfaces, refer to the [Amelia Custom UI Guide](https://docs.amelia.com/display/COGVODAFONE/Amelia+Custom+UI+Guide) and the [Amelia's Interfaces](Amelia's%20Interfaces) page.
## Learn More
Also be sure to read [Getting Started with Training Amelia](Getting%20Started) for more details about the training process.
