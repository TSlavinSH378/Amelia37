{% version "3.x" %}
Escalation teams are collections of users and must be created before creating one or more escalation queues.
An escalation team is a set of agents (team members) that can handle escalations for one or more queues. Conversations are escalated exclusively to members of the team(s) assigned to the queue, regardless of their roles or user group memberships.
Every team member also must be able to accept chats from Amelia and their user record must have *Max active chats (agent)* setting be greater than 0. User records are created and updated by clicking the Users tab on the left side of the administration page. The *Max active chats (agent)* setting is in the Basics area in the Users workspace that appears on the right side of the screen when a new record is created or an existing record is opened by double-clicking a user name in the Users Control Panel.
To create and modify escalation teams, users must have their access privileges include these authorities:
AUTHORITY_ADMIN_ESCALATION_QUEUE_VIEW  
AUTHORITY_ADMIN_ESCALATION_QUEUE_EDIT
## The Escalation Teams Interface
To edit or add an escalation team, log in to Amelia's administration pages and select System Settings then Escalation Teams from the left side navigation links. The Escalation Teams workspace appears with a New Escalation Team button at the top right.
The default Escalation Teams workspace includes a search box to find existing teams within a domain. To edit an existing team, click the notepad edit icon to the left of the name. Click the New Escalation Team button to add a team.
![](attachments/11940265/11940266.png)
Figure. Escalation Team Form
The fields in the Escalation Teams form are described below.
Table. Escalation Team Form Fields
|                  |                                                                                                                                                                                                                                |
|------------|------------------------------------------------------------|
| Field            | Description                                                                                                                                                                                                                    |
| Basics           |                                                                                                                                                                                                                                |
| Name             | Type the name of the escalation team                                                                                                                                                                                           |
| Enabled          | Select or deselect to enable the team and make it active                                                                                                                                                                       |
| Custom Schedule? | Select or deselect to configure a custom day time schedule. If selected, the Week Schedule section will appear.                                                                                                                |
| Week Schedule    |                                                                                                                                                                                                                                |
| Start            | For each day of the week, select a start time                                                                                                                                                                                  |
| End              | For each day of the week, select an end time                                                                                                                                                                                   |
| TimeZone         | Select a time zone for the escalation team                                                                                                                                                                                     |
| Team Members     |                                                                                                                                                                                                                                |
| Search           | Click the Search box then type in partial or complete user name into the Search field                                                                                                                                          |
| Add              | When a user name appears in the search field, click to add the user to this team. The new user name appears in the Added box. To delete a user, click the x to the right of any name in the Existing, Added, or Deleted boxes. |
## Create and Update Escalation Teams
The Escalation Teams workspace is available by clicking the System Settings heading then the Escalation Teams link on Amelia's left side administration pages navigation. The default Escalation Teams workspace will appear with a list of existing teams, if any.
1.  Click the Systems Settings heading then click the Escalation Teams link.  
    To edit an existing team, click the notepad edit icon to the left of a name. The team edit form appears.  
    To add a new team, click the New Escalation Team button at the top right of the Escalation Teams workspace. The New Team form appears.
2.  Complete the team edit form that appears on the right side of the interface.
## Delete an Escalation Team
The Escalation Teams workspace is available by clicking the System Settings heading then the Escalation Teams link on Amelia's left side administration pages navigation. The default Escalation Teams workspace will appear with a list of existing teams.
The default Escalation Teams workspace includes a search box to find existing teams. To edit an existing team, click the notepad edit icon to the left of the name.
> [!info]  
>
> Only delete if there is no alternative. Do NOT delete any default item or item critical to Amelia’s operation. For example, do not delete the initial Escalation Queue created and configured during setup installation.

1.  Click the Systems Settings heading then click the Escalation Teams link.
2.  If appropriate, use the search box to find a team name. Click the notepad edit icon to the left of the name. The team edit form appears.
3.  Click the Delete button at the top right of the workspace.
**  
**
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
{% /version %}
