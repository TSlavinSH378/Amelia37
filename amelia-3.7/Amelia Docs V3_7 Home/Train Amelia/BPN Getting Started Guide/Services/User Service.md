-   [Methods](#UserService-Methods)
    -   [getUser](#UserService-getUser)
    -   [registerUser](#UserService-registerUser)
    -   [updateUser](#UserService-updateUser)
    -   [userExistsWithName](#UserService-userExistsWithName)
    -   [userExistsWithEmail](#UserService-userExistsWithEmail)
-   [BpnUser Data Structure](#UserService-BpnUserDataStructure)
-   [Display User Data](#UserService-DisplayUserData)
    -   [Create a BPN](#UserService-CreateaBPN)
    -   [A Script to User Data](#UserService-AScripttoUserData)
    -   [Interact with Amelia](#UserService-InteractwithAmelia)
# Methods
## getUser
    BpnUser getUser()
Get the user data associated with the current conversation.
## registerUser
    BpnUser registerUser(BpnUser bpnUser, String userGroupName)
Register a new user.
## updateUser
    BpnUser updateUser(BpnUser existingUser)
Update the user associated with the given conversation.
## userExistsWithName
    boolean userExistsWithName(String name)
Returns true if a user already exists with the given name.
## userExistsWithEmail
    boolean userExistsWithEmail(String email)
Returns true if a user already exists with the given email.
# BpnUser Data Structure
Simplified representation of an Amelia user.

| Name | Data type | Accessor | Mutator |
| ----|----|----|----|
| userId | String | userId()

\|
    N/A (defaults to null)
\| \| anonymous \| boolean \|
    anonymous()
\|
    N/A (defaults to false)
\| \| firstName \| String \|
    firstName()
\|
    firstName(String s)
\| \| lastName \| String \|
    lastName()
\|
    lastName(String s)
\| \| email \| String \|
    email()
\|
    email(String s)
\| \| attributes \| Map\<String,;String\> \|
    attributes()
\|
    attributes(Map<String, String> m)
\|
# Display User Data
This demonstration extracts user data associated with the current conversation and displays it within a conversation with Amelia.
![](attachments/11939543/11939544.png)
Figure. showUserData BPN
## Create a BPN
In the Amelia administration pages, use the Process Knowledge tab to create a new BPN model and name it showUserData. Save the new model then build each of the BPN tasks as described below. Create these Tasks in a BPN, as described and ordered in the table below.
Table. BPN Specifications to Extract User Data

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let's get started | Initialize Amelia and let the person know the conversation has started |
| 2 | get user first and last name | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | say ${firstName} | Display output of firstName extracted from user data in Task 2 above |
| 4 | say ${lastName} | Display output of lastName extracted from user data in Task 2 above |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save button
-   Click the Deploy button
These steps load the BPN model into Amelia’s memory.
## A Script to User Data
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` bash
def user = userService.getUser()
def firstName = user.firstName()
def lastName = user.lastName()
execution.setVariable("firstName", firstName)
execution.setVariable("lastName", lastName)
```
## Interact with Amelia
When the BPN models are built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the right edge of the Mind panel..
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the testQuantity workflow by typing this command in the chat interface:
    ``` bash
    run the workflow showUserData
    ```
3.  Amelia displays the first and last name extracted from the user data associated with the current conversation.
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-1-5_11-41-52.png](attachments/11939543/11939544.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-5_11-40-54.png](attachments/11939543/11939545.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-15_12-48-59.png](attachments/11939543/11939546.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-15_12-43-48.png](attachments/11939543/11939547.png) (image/png)  
