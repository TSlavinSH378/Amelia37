{% version "3.x" %}
This page describes the RBAC functionality of Conductor including managing users, roles, authorities, and groups.
# Authorities
The following authorities exist in Conductor:

| Name | Description |
| ----|----|
| ADMIN_CLIENT_READ | Allows the user to view ALL client details. |
| ADMIN_CLIENT_WRITE | Allows the user to create and edit ALL client details. |
| ADMIN_INSTANCE_READ | Allows the user to view instance details. |
| ADMIN_INSTANCE_WRITE | Allows the user to create and edit instances. |
| ADMIN_RBAC_READ | Allows the user to view other user details. |
| ADMIN_RBAC_WRITE | Allows the user to create and edit other users. |
| USER_MIGRATION_READ | Allows the user to view migrations and requests. |
| USER_MIGRATION_WRITE | Allows the user to create and edit migrations and requests. |
| USER_MIGRATION_RUN | Allows the user to submit migration requests. |

The above authorities are defined in the application code and cannot be changed, however custom roles can be created with any combination of the above authorities.
# Roles
The following roles are created in Conductor by default:
|                     |                      |
|---------------------|----------------------|
| Role                | Authorities          |
| ROLE_ADMIN_CLIENT   | ADMIN_CLIENT_READ    |
|                     | ADMIN_CLIENT_WRITE   |
| ROLE_ADMIN_INSTANCE | ADMIN_INSTANCE_READ  |
|                     | ADMIN_INSTANCE_WRITE |
| ROLE_ADMIN_RBAC     | ADMIN_RBAC_READ      |
|                     | ADMIN_RBAC_WRITE     |
| ROLE_USER           | USER_MIGRATION_READ  |
|                     | USER_MIGRATION_WRITE |
|                     | USER_MIGRATION_RUN   |
The authorities included in these roles can be changed or removed and new roles can be created with different authorities as required. To create or update roles, go to the Roles screen under the Configuration menu.
![](attachments/32510217/32510218.png)
Figure. List of Roles Workspace
To change the authorities in a role, move them between the two lists in the edit modal.
![](attachments/32510217/32510219.png)
Figure. Move Roles Between Lists
# Users
By default, an admin and user test account is created in Conductor. These can be deleted or disabled if desired once other admin accounts have been added. Adding a user requires a first name, last name, email address, and password. Any number of roles can be assigned to a user, authorities cannot be assigned directly to a user.
![](attachments/32510217/32510220.png)
Figure. List of Users Workspace
A user can be assigned roles with the dropdown in the edit modal.
![](attachments/32510217/32510221.png)
Figure. Create New User Workspace
# Groups
A group is simply a list of users that are associated with a [Client](Client%20Guide). Users in a group will have access to all instances associated with the client, and thus all migrations for those instances.
Two groups will exist by default for IPsoft Admins and Users.
![](attachments/32510217/32510222.png)
Figure. List of User Groups
To change the members in a group, move the users between the two lists in the edit modal.
![](attachments/32510217/32510223.png)
Figure. Update Group Workspace
{% /version %}
