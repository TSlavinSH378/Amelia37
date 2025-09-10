-   [The User Interface](#Users-TheUserInterface)
-   [Create and Update Users](#Users-CreateandUpdateUsers)
-   [Add User Attributes](#Users-AddUserAttributesAddUserAttributes)
Users within the Amelia system are provided access to a mix of groups, roles, authorities, and domains.
## The User Interface
To edit or add a user, log in to Amelia's administration pages and select System Settings then Users from the left side navigation links. The Users workspace appears with a New User button at the top right.
The default Users workspace includes a search box to find existing users within a domain. To edit an existing user, click the notepad edit icon to the left of the name. Click the New User button to add a user.
![](attachments/11940276/11941432.png)
Figure. New User Page Form
The fields in the Users form are described below.
Table. User Form Fields
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Field</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>User Details</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">Domain</td>
<td class="confluenceTd">Select a domain for the user</td>
</tr>
<tr class="odd">
<td class="confluenceTd">First Name</td>
<td class="confluenceTd">Type user's first name</td>
</tr>
<tr class="even">
<td class="confluenceTd">Last Name</td>
<td class="confluenceTd">Type user's last name</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Email</td>
<td class="confluenceTd">Type user's email address</td>
</tr>
<tr class="even">
<td class="confluenceTd">External UID</td>
<td class="confluenceTd">Optional. Type user's external UID</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Authentication Policy</td>
<td class="confluenceTd">Select the authentication policy for user to use for login</td>
</tr>
<tr class="even">
<td class="confluenceTd">Locale</td>
<td class="confluenceTd">Select location for language</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Time Zone</td>
<td class="confluenceTd">Select global time zone for user</td>
</tr>
<tr class="even">
<td class="confluenceTd">Maximum Concurrent Chats</td>
<td class="confluenceTd"><p>Type in a number or click to increase or decrease a number. Users who are part of an escalation team must have this value set greater than the default of 0.</p>
<p>Max number of concurrent chats is the number of chats an agent will be pushed through dispatch but does not limit the number of chats an agent can pick up manually.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Enabled</td>
<td class="confluenceTd">Select or deselect to enable the user's access</td>
</tr>
<tr class="even">
<td class="confluenceTd">Exclude From Metrics</td>
<td class="confluenceTd">Select or deselect to exclude this user's activity from metrics</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Password</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">Change Password?</td>
<td class="confluenceTd">For existing users, select or deselect to force user to change password</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Password</td>
<td class="confluenceTd">If Change Password? is selected, and if needed on the new user form, type the user's password</td>
</tr>
<tr class="even">
<td class="confluenceTd">Confirm Password</td>
<td class="confluenceTd">If Change Password? is selected, and if needed on the new user form, retype the user's password</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Last Updated</td>
<td class="confluenceTd">For existing users, displays the date and time of last password change</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Groups</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Search</td>
<td class="confluenceTd">Type in partial or complete User name into the Search field then click the Add button</td>
</tr>
<tr class="even">
<td class="confluenceTd">Add Button</td>
<td class="confluenceTd">When a group name appears in the search field, click to add the group to this group definition</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Existing</td>
<td class="confluenceTd">List of existing groups for the user record</td>
</tr>
<tr class="even">
<td class="confluenceTd">Added</td>
<td class="confluenceTd">List of recently added groups for the user record</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Removed</td>
<td class="confluenceTd">List of recently removed groups for the user record</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Effective Authorities</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">List</td>
<td class="confluenceTd">Lists all authorities assigned to the user record</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Attributes</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Name</td>
<td class="confluenceTd">Type the attribute name to be stored then retrieved in a BPN script.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Value</td>
<td class="confluenceTd">Type the value assigned to the name to be stored then retrieved in a BPN script.</td>
</tr>
</tbody>
</table>
## Create and Update Users
The Users workspace is available by clicking the System Settings heading then the Users link on Amelia's left side administration pages navigation. The default Users workspace will appear with a list of existing users.
1.  Click the Systems Settings heading then click the Users link.  
    To edit an existing user record, click the notepad edit icon to the left of a user name. The user edit form appears.  
    To add a new user record, click the New User button at the top right of the Users workspace. The New User form appears.
2.  Complete the user edit form that appears on the right side of the interface.
## Add User Attributes
The Attributes tab at the bottom of the user detail page, when clicked, displays a green plus ( + ) button at the top right of the Attributes form. User attributes can be added and retrieved with Script tasks in a BPN.
1.  Click the green plus button to display a row with blank Name and Value fields.
2.  Type a name as a common key to retrieve a value.
3.  Type a value to be retrieved with the name key.
4.  Click the Save button at the top of the user detail page.
![](attachments/11940276/11941440.png)
Figure. Attributes Form
A BPN Script task can use the userService to use the name as a key to retrieve a value for the user, for example, their date of birth. The Script task also can add a key name and value to the attributes map within the user object which also creates a Name and Value entry in the Attributes tab on the User detail page form.
``` groovy
//grab user object then retrieve attribute
def user = userService.getUser()
def dob = user.attributes().get("user_dob")
//add sttribute then update user object
user.attributes().put("user_code", "userxyz")
userService.updateUser(user)
```
> [!warning]  
>
> All attribute values are set and returned as strings. To parse attribute values as non-string types, string values must be set to a different type before parsing. For example, to extract the year value from the string 01/01/1900, the string must be converted to a date format before the year value can be extracted.

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
![](images/icons/bullet_blue.gif) [image2018-3-20_16-40-47.png](attachments/11940276/11940277.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-28_14-8-55.png](attachments/11940276/11941432.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-28_16-21-44.png](attachments/11940276/11941440.png) (image/png)  
