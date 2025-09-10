Domains and users in Amelia are associated with an authentication policy. The [Authentication Policy](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions#AccessandPermissions-AuthPolicies) part of the [Access and Permissions](https://docs.ipsoft.com/display/AmeliaDocsV3/Access+and+Permissions) page has more technical details.
## The Authentication Policy Interface
To edit or add an authentication policy, log in to Amelia's administration pages and select System Settings then Authentication Policies from the left side navigation links. The Authentication Policies workspace appears with a New Authentication Policy button at the top right.
The default Authentication Policies workspace includes a search box to find existing policies within a domain. To edit an existing policy, click the notepad edit icon to the left of the name. Click the New Authentication Policy button to add a policy.
Figure. Authentication Policies Form
The fields in the Authentication Policies form are described below.
Table Authentication Policies Form Fields

| Field | Description |
| ----|----|
| Name | Type the name of the authentication policy |
| Password Complexity Rules | Type a regular expression evaluation for user passwords. [a-z]::1::[A-Z]::1::[\d]::1::[^a-zA-Z0-9]::1 is the default. |
| Password Rejection Rules | Type a regular expression evaluation to reject user passwords. [\s]::1::(?i)${email}::1::(?i)${firstName}::1::(?i)${lastName}::1 is the default. |
| Password Complexity Description | Type in guidelines for user to create their passwords with this policy |
| Authentication System | Select the authentication system to use for this policy. Internal and Deny All are defaults. |
| Password Change Allowed? | Select or deselect the ability for users to change their passwords |
| Forgot Password Allowed? | Select or deselect the ability for users to reset their passwords |
| Minimum Password Complexity Matches | The minimum number of matches that must be made when evaluated by the password complexity rules |
| Minimum;Password Length | Type a number for the minimum characters allowed for passwords |
| Maximum;Password Length | Type a number for the maximum characters allowed for passwords |
| Past Password Retention | Type the number days to retain the user's prior password data |
| Password Expiration Days | Type the number of days to force a user to reset their password |
| Password Expiration Warning Days | Type the number of days to warn the user to reset their password before it expires |
| Minimum Password Age | Type the number of times a password can be reused |
| Maximum Login Attempts | Type the number of login attempts before the user is locked out |
| Lockout Duration Minutes | Type the number of minutes the user must wait after they are locked out due to too many login attempts before they can try to login again |
| Inactivity Expiration Days | Type the number of days of no user logins before their password and account are locked |

## Create and Update an Authentication Policy
The Authentication Policies workspace is available by clicking the System Settings heading then the Authentication Policies link on Amelia's left side administration pages navigation. The default Authentication Policies workspace will appear with a list of existing policies, if any.
1.  Click the Systems Settings heading then click the Authentication Policies link.  
    To edit an existing policy, click the notepad edit icon to the left of the policy name. The authentication policy edit form appears.  
    To add a new policy, click the New Authentication Policy button at the top right of the Authentication Policies workspace. The New Authentication Policy form appears.
2.  Complete the authentication policy edit form that appears on the right side of the interface.
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
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-3-20_15-45-27.png](attachments/11940263/11940264.png) (image/png)  
