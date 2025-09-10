Access to Amelia is provided through authentication systems. Amelia includes a set of default systems. The [A](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-AuthPolicies)[uthentication System](https://docs.ipsoft.com/display/AmeliaDocsV37/Access+and+Permissions#AccessandPermissions-AuthSystems) part of the [Access and Permissions](https://docs.ipsoft.com/display/AmeliaDocsV37/Access+and+Permissions) page has more technical details.
## The Authentication Systems Interface
To edit or add an authentication policy, log in to Amelia's administration pages and select System Settings then Authentication Systems from the left side navigation links. The Authentication Systems workspace appears with a New Authentication System button at the top right.
The default Authentication Systems workspace includes a search box to find existing systems within a domain. To edit an existing system, click the notepad edit icon to the left of the name. Click the New Authentication System button to add a system.
Figure. Authentication System Form
The fields in the Authentication Systems form are described below.
Table Authentication System Form

| Field | Description |
| ----|----|
| Name | Type the name of the new authentication system |
| Code | Type the code of the system, usually the Name lower case with no spaces or separators |
| Description | Type a description for the authentication system |
| Authentication System Type | DENY_ALL, INTERNAL, LDAP, SAML2, FACIAL_RECOGNITION are defaults. Selecting some options displays a customization form below the Authentication System Basics form, for example, AD, SAML2, LDAP, and WS_FEDERATION. |
| Disabled? | Select or deselect whether or not this system is disabled |
| Immediate? | Select or deselect whether or not this authentication system is immediately available |
| Display on Login Window? | Select or deselect to display this authentication system in the login window |
| Login Window Order | If displaying the system in the login window, type a number for the order the system should appear when multiple systems are visible in the login window |

In some cases, selecting the Type on the Authentication System workspace will display an additional form below the Basics form. For example, selecting LDAP as the authentication system type will display a form to enter LDAP integration details.
## Create and Update Authentication Systems
The Authentication Systems workspace is available by clicking the System Settings heading then the Authentication Systems link on Amelia's left side administration pages navigation. The default Authentication Systems workspace will appear with a list of existing systems.
1.  Click the Systems Settings heading then click the Authentication Systems link.  
    To edit an existing system, click the notepad edit icon to the left of the system name. The authentication system edit form appears.  
    To add a new system, click the New Authentication System button at the top right of the Authentication Systems workspace. The New Authentication System form appears.
2.  Complete the authentication system edit form that appears on the right side of the interface.
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
