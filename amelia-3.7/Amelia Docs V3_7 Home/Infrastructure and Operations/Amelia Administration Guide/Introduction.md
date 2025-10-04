{% version "3.x" %}
This Amelia Administration guide provides detailed instructions about how to setup and manage Amelia's software system, for example, backups, setting up access authentication, creating user groups, and more.
# Amelia's Systems
An Amelia instance includes a mix of components used to build an interconnected set of domains, users, authentication policies, roles, and other elements. What is used depends on the needs of the setup.
### Access System
Users, groups, roles, and authorities in Amelia control what users can do.
#### Users
While users can be added to groups, they cannot be added to roles.
#### Groups
Groups collect many users and one or more roles and authorities. Membership in a group shares with many users the role access rights and authorities needed to perform specific tasks. Groups belong to one domain only.
#### Roles
Roles organize all the authorities needed to perform specific tasks. Authorities are granted to users upon login based on their group memberships.
#### Authorities
An authority represents the ability to perform an action or view a something within Amelia. The set of authorities is fixed and not configurable. 
### Escalation System
Amelia instances can include the ability to escalate her interactions to human agents for complex questions. Escalation teams and queues build on the basic foundation of users, groups, and roles.
Escalation teams are a set of users that can handle escalations for one or more queues. Conversations are escalated exclusively to members of the team(s) assigned to the queue, regardless of their roles or user group memberships.
Once Amelia escalates a conversation, it will be placed in one of the existing queues defined for the domain. The module in Amelia that escalates the conversation, for example, a BPN, will specify the queue where the conversation should be placed. If no queue is specified, conversations will be queued on the domain's default queue.
An agent can belong to more than one queue (and team) and a queue can be monitored by more than one team. In this example, the IT Helpdesk Queue is monitored by two teams, Workplace Support and Application Support, and Agent 006 part of both teams.
Figure. Integration with Teams, Groups, and Queues
Configuration of escalation functionality is handled through the System Settings link at the bottom left side of Amelia's administration pages. Typically, once at least one domain is created, Amelia is configured in a specific order to handle escalated conversations.
1.  Create users
2.  Create an agent group and assign it the Agent role
3.  Assign users to the agent group
4.  Create an escalation team and add users
5.  Create an escalation queue and add escalation teams
6.  Assign an escalation queue to a domain
### Authentication and Third-Party Integrations
Many installations will include connections to authentication systems and other third-party tools to include in Amelia's interactions. For example, Amelia might provide insurance quotes and, as a result, be connected to quote engine software to pass data back and forth during a conversation. Amelia also integrates with LDAP, AD, SAML2, facial recognition, and other authentication systems to provide access.
### Domains
Amelia's domains organize knowledge, users, roles, groups, and other elements. Domain knowledge is shared by any child or grandchild domains set up with a parent domain. If Amelia cannot find information in the local domain, she looks at any parent domain then the global domain for an answer. Therefore, while Amelia includes a global domain, the best practice is to create a new domain to hold any globally shared knowledge. Then share the knowledge with child domains. Over time, this arrangement is easier to change how domains interact than if the global domain is populated with data.
# Interfaces
In addition to Amelia’s chat interface, administration pages are available with workspaces to add and edit data Amelia uses to interact with people. These interfaces are described in this section.
Administration pages are available with a direct https://hostname/Amelia/admin/ URL or by clicking the Admin link in the top right of Amelia's basic chat interface. Amelia's custom user interface (UI) does not include a link to administration pages.
The basic chat interface has a set of links at the top right which includes an Admin link to access the administration pages.
![](attachments/11940183/11940186.jpg)
Figure. Admin Link in Amelia's Basic Chat Interface
The default Amelia administration pages include three distinct groups of links.
-   System settings and modules to configure Amelia's responses
-   Jump links to quickly access key administration functionality
-   Links from the basic chat interface as well as agent and supervisor role links
![](attachments/11940183/28480858.jpg)
Figure. Amelia's Administration Default Home Page
## System Settings and Modules Navigation
The left side of Amelia's administration pages include links to setup and manage Amelia. Clicking the small arrow near the top of these links toggles the display of icons only and icons with links. When toggled closed, hovering the mouse displays flyout menus with links. When toggled open, clicking the module name or Systems Settings labels displays any secondary links.
These settings administration pages are described in detail in this document. Other documents describe how to configure Amelia's modules
![](attachments/11940183/28480859.png)
Figure. System Settings and Modules Navigation Links
Table. System Settings and Modules Navigation Links
|                         |                                                                                                        |
|-------------------------|--------------------------------------------------------------------------------------------------------|
| Module/Link Name        | Description                                                                                            |
| Process Memory          | see [BPN Getting Started Guide](BPN%20Getting%20Started%20Guide)                                       |
| Episodic Memory         | [see Episodic Memory Guide](Episodic%20Memory%20Guide)                                                 |
| Semantic Memory         | [see Semantic Memory Guide](Semantic%20Memory%20Guide)                                                 |
| Analytic Memory         | [see Analytic Memory Guide](Analytic%20Memory%20Journey%20Graph)                                       |
| Affective Memory        | [see Affective Memory](Affective%20Memory)                                                             |
| Amelia Trainer          | [see Amelia Trainer Guide](Amelia%20Trainer%20Guide)                                                   |
| Integrations            | [see Integrations Guide](Integrations%20Guide)                                                         |
| System Settings         |                                                                                                        |
| Authentication Systems  | Each domain in Amelia is associated with an authentication policy                                      |
| Authentication Policies | Authentication systems in Amelia define where and how to store user credentials and how to verify them |
| Escalation Teams        | Create and edit teams of users to manage escalations based on day and time ranges                      |
| Escalation Queues       | Create and edit queues used to organize escalations from Amelia                                        |
| Domains                 | Create domains to organize distinct knowledge sets individually or as parent child domains             |
| Groups                  | User groups in Amelia are the intersection of Users, Roles, Domains, and Authorities                   |
| Users                   | See all the users by Domain and, given appropriate permissions, create a new user                      |
| Roles                   | Roles allow defining collections of authorities and reusing these across multiple user groups          |
| UI Bundles              | Install and modify custom user interface (UI) file bundles                                             |
| Audit Log               | Search and view activity organized into 69 Amelia event types                                          |
| 1Desk Instances         | Connect Amelia with one or more 1Desk instances                                                        |
| 1RPA Instances          | Connect Amelia with one or more 1RPA instances                                                         |
| Copilot Phrases         | Create and edit snippets used with the Copilot user interface                                          |
## Jump Links
These links are located at the top right of Amelia's administration pages. Clicking the thunderbolt icon displays a small set of useful links to jump immediately to key administration tasks, for example, to create a new user or entity.
![](attachments/11940183/11940191.png)
Figure. Jump Links
Table. Jump Links

| Link | Description |
| ----|----|
| Intent | Displays the Intents workspace |
| Entity | Displays the Entities workspace |
| Integration Flow | Displays a blank New Integration Service form |
| Semantic Data | Displays the Import workspace to upload and define semantic data |
| Tabular Data | Displays the Import Tabular Data workspace to upload and define a tabular data file |
| New User | Displays the New User form to add an access record |

## Chat and Role Links
Located at the top right corner of Amelia's administration pages, these links replicate links that appear at the top right of her basic chat interface. In addition, the supervisor role pages are linked.
![](attachments/11940183/28480860.png)
Figure. Chat and Role Links
Table. Chat and Role Links

| Link | Description |
| ----|----|
| User | Displays Amelia's basic chat interface |
| Mind | Displays the basic chat interface with panels to explore how Amelia's modules work to guide her behaviors |
| 3D | Displays the Mind interface as three-dimensional models |
| Admin | Displays the default home page for Amelia's administration pages |
| Conversations | Displays the current active conversations for use by Agents and Supervisors on escalation teams |
| Supervisors | Displays conversation and Agent data for use by Supervisors of escalation teams |
| Metrics | Displays conversation and Agent data for use by Supervisors of escalation teams |
| Sign Out | Logs out of Amelia's administration pages and basic chat interface |

## Status and Sign Out Links
Availability for escalation can be set by clicking the dot next to the user name at the top left of Amelia's administration pages. The same dropdown menu includes the ability to sign out.
![](attachments/11940183/28480861.png)
Figure. Status and Sign Out Links
{% /version %}
