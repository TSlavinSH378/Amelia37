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

