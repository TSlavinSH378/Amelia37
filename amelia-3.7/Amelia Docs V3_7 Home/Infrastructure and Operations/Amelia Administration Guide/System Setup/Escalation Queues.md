Once a conversation is escalated, it will be placed in one of the existing queues defined for the conversation domain. The module in Amelia that escalates the conversation, for example, a BPN, will specify the queue where the conversation should be placed. If no queue is specified, conversations will be queued on the domain's default queue.
To create and modify escalation queues, users must have their access privileges include these authorities:
AUTHORITY_ADMIN_ESCALATION_QUEUE_VIEW  
AUTHORITY_ADMIN_ESCALATION_QUEUE_EDIT
## The Escalation Queues Interface
To edit or add an escalation queue, log in to Amelia's administration pages and select System Settings then Escalation Queues from the left side navigation links. The Escalation Queues workspace appears with a New Escalation Queue button at the top right.
The default Escalation Queues workspace includes a search box to find existing teams within a domain. To edit an existing team, click the notepad edit icon to the left of the name. Click the New Escalation Queue button to add a team.
![](https://docs.ipsoft.com/download/attachments/11937818/image2018-11-20_12-55-34.png)
Figure. Escalation Queues Form
The fields in the Escalation Queue form are described below.
Table. Escalation Queue Form Fields
|                                           |                                                                                                                                  |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| Field                                     | Description                                                                                                                      |
| Basics                                    |                                                                                                                                  |
| Name                                      | Type the name of the queue                                                                                                       |
| Code                                      | Type a code name for the queue, usually the Name without spaces or hyphens                                                       |
| Domain                                    | Select the domain used with this escalation queue                                                                                |
| Escalation notification timeout (seconds) | Click or type time in seconds                                                                                                    |
| Max consecutive timeouts                  | Click or type maximum number of consecutive timeouts allowed. When set to 0, agent status will not be set to Away automatically. |
| Queue Enabled?                            | Select or deselect to enable this escalation queue                                                                               |
| SLAs                                      |                                                                                                                                  |
| Pickup Time SLA (seconds)                 | Click or type time in seconds                                                                                                    |
| Pickup Warning (seconds)                  | Click or type time in seconds                                                                                                    |
| Handle Time SLA (seconds)                 | Click or type time in seconds                                                                                                    |
| Handle Warning (seconds)                  | Click or type time in seconds                                                                                                    |
| Escalation Teams                          |                                                                                                                                  |
| Search                                    | Type name of escalation team then click the Add button                                                                           |
| Add Button                                | Click to add name in Search field                                                                                                |
| Current                                   | This column lists existing escalation teams assigned to this queue                                                               |
| Add                                       | This column lists recently added escalation teams assigned to this queue                                                         |
| Removed                                   | This column lists recently removed escalation teams assigned to this queue                                                       |
## Create and Update an Escalation Queue
The Escalation Queues workspace is available by clicking the System Settings heading then the Escalation Queues link on Amelia's left side administration pages navigation. The default Escalation Queues workspace will appear with a list of existing queues, if any.
1.  Click the Systems Settings heading then click the Escalation Queue link.  
    To edit an existing queue, click the notepad edit icon to the left of a name. The queue edit form appears.  
    To add a new queue, click the New Escalation Queue button at the top right of the Escalation Queues workspace. The New Queue form appears.
2.  Complete the queue edit form that appears on the right side of the interface.
A default escalation queue must be configured for escalations to work. If an escalation queue has not been set for the domain, it needs to be configured.
To configure the default escalation queue for a domain, on the left side of the administration page, click the System Settings heading then the Domains link to display the Domains workspace. Find then click the notepad icon to the left of the domain name for this escalation queue. On the domain edit form, select the escalation queue as the default queue for the domain. 
## Delete an Escalation Queue
The Escalation Queues workspace is available by clicking the System Settings heading then the Escalation Queues link on Amelia's left side administration pages navigation. The default Escalation Queues workspace will appear with a list of existing queues.
The default Escalation Queues workspace includes a search box to find existing queues. To edit an existing queue, click the notepad edit icon to the left of the name.
> [!info]  
>
> Only delete if there is no alternative. Do NOT delete any default item or item critical to Amelia’s operation. For example, do not delete the initial Escalation Queue created and configured during setup installation.

1.  Click the Systems Settings heading then click the Escalation Queues link.
2.  If appropriate, use the search box to find a queue name. Click the notepad edit icon to the left of the name. The queue edit form appears.
3.  Click the Delete button at the top right of the workspace.
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
![](images/icons/bullet_blue.gif) [image2018-3-22_9-28-54.png](attachments/11940267/11940268.png) (image/png)  
