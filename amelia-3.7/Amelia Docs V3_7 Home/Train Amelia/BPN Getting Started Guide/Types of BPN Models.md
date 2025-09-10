The first step creating a BPN involves the choice of BPN model type. There are three different types with Amelia V3, each with their own positives and negatives.
# BPN Model Types
There are several possible types of BPN models.
-   **Deterministic** — A BPN model whose tasks are executed sequentially. Its elements may perform dialog management and branching logic such as ad-hoc forks, joins, and gateways.
-   **Headless** —  A BPN model whose tasks don’t use conversation, for example, the Ask or Say tasks. Script, Set, Unset tasks are allowed, as well as forking, join, and gateways.
The model type is set in the Properties Panel of a BPN model by clicking a blank area of the workspace, opening the panel, then selecting Type.
> [!warning]  
>
> Amelia 3.7 no longer includes a stochastic BPN model type to be executed dynamically based on the current context in an active conversation. Instead, Ask tasks include property settings to define what happens when a conversation jumps back to an earlier part of a BPN process. See [Backjumps to Handle Conversation Changes](BPN-Tasks_11939422.html#BPNTasks-Backjumps) in the BPN Tasks section.

# BPN Model Properties
The BPN model types have common properties.
![](attachments/11939405/11941385.png)
Figure. BPN Model Properties Panel Settings
Table. BPN Model Property Panel Settings

| Setting | Description |
| ----|----|
| Name | The name of the model |
| Type | Deterministic, Headless |
| Documentation | Any notes about the model |
| Default escalation queue | If appropriate, select a queue to handle escalations |
| Escalation variables | Click the + icon to display a field and enter a variable to attach to an escalation request. Variables are created in Script tasks within the BPN, a Set the Variable task, or passed along with an Escalate Because task. |

## Attachments:
![](images/icons/bullet_blue.gif) [image2017-9-22_16-31-53.png](attachments/11939405/11939406.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_13-5-36.png](attachments/11939405/11939407.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_13-4-59.png](attachments/11939405/11939408.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-25_12-2-46.png](attachments/11939405/11941384.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-25_12-3-50.png](attachments/11939405/11941385.png) (image/png)  
