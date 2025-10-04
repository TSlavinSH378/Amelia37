{% version "3.x" %}
All the authorities needed to perform specific tasks are grouped into roles. For example, a Power User in the Amelia environment is an enhanced User. They can see everything, more than Users, but what they can do is limited. To demonstrate a chat session with Amelia and show which BPN is triggered, a user would need to be assigned the Power User role (to see everything) and an Agent role (to run a chat session).
More information about roles is found in the [R](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-UserGroupDefs)[oles](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-RoleDefs) and [Authorities](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-AuthorityDefs) parts of the [Access and Permissions](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions) section.
## Default Roles
The default roles in an Amelia system include these roles. See [R](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-UserGroupDefs)[oles](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-RoleDefs) and [Authorities](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-AuthorityDefs) sections for authorities assigned to each role.
Table: Default Roles

| Role Name | Description |
| ----|----|
| End User | Engage Amelia in conversation. |
| Power User | Read only access to the system without the ability to change anything. |
| Agent | Observe and pick up active conversations with Amelia. |
| Knowledge Designer | Edit FAQs, Grammars, BPNs, and modify response pool entries. |
| Integration Designer | Edit Create and delete new and existing integrations. Because integrations are global and not specific to a domain, the Global Integration Designer role should be assigned when setting up a user account. |
| Administrator | Modify data on the domain level, as well as authentication systems, policies, and roles. |
| Agent Supervisor | Assign conversations to agents, see Agent Supervisor Dashboard with conversation data. |
| RBAC Administrator | Create and modify users, groups, and roles. |

## The Roles Interface
To edit or add a role, log in to Amelia's administration pages and select System Settings then Roles from the left side navigation links. The Roles workspace appears with a New Role button at the top right.
The default Roles workspace includes a search box to find existing roles within a domain. To edit an existing role, click the notepad edit icon to the left of the name. Click the New Role button to add a role.
Figure. Roles Workspace
The fields in the Roles workspace are described below.
Table. Roles Workspace Fields
|                       |                                                                                                                                                                              |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Field                 | Description                                                                                                                                                                  |
| Name                  | Type the name of the role                                                                                                                                                    |
| Authority Edit        |                                                                                                                                                                              |
| Available Authorities | A list of available authorities within the Amelia system. Click available authorities on the left side list then drag to the right and drop on the Selected Authorities box. |
| Selected Authorities  | A list of authorities selected for the role. Click authority on the right side Selected Authorities list then drag to the left and drop on the Unused Authorities box.       |
## Create and Update Roles
The Roles workspace is available by clicking the System Settings heading then the Roles link on Amelia's left side administration pages navigation. The default Roles workspace will appear with a list of existing roles, if any.
1.  Click the Systems Settings heading then click the Roles link.  
    To edit an existing role, click the notepad edit icon to the left of the group name. The group edit form appears.  
    To add a new role, click the New Role button at the top right of the Roles workspace. The New Role form appears.
2.  Complete the Roles edit form that appears on the right side of the interface.
## Delete a Role
The Roles workspace is available by clicking the System Settings heading then the Roles link on Amelia's left side administration pages navigation. The default Roles workspace will appear with a list of existing roles, if any.
The default Roles workspace includes a search box to find existing roles within a domain. To edit an existing role, click the notepad edit icon to the left of the name.
Only delete if there is no alternative. Do NOT delete any default item or item critical to Amelia’s operation. For example, do not delete the initial Escalation Queue created and configured during setup installation.
1.  Click the Systems Settings heading then click the Roles link.
2.  If appropriate, use the search box to find a role name. Click the notepad edit icon to the left of the name. The role edit form appears.
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
{% /version %}
