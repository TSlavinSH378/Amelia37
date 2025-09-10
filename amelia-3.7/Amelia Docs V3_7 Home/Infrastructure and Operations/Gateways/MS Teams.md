The Amelia MS Teams Gateway allows users to have a conversation with Amelia through the MS Teams chat software.  
# Text Messages
Normal text message conversation is supported.
# Present Task (Images Only)
Amelia has the ability to present images to the user with the supported image files using a Present task in a BPN.
![](attachments/25461075/28477686.png)
Figure. Use a BPN Present Task to Display Images
# Forms
**Forms by default delete themselves after the submit button has been hit**.
If you keep the form available the user can repeatedly submit the form (sending the value to amelia) repeatedly even after the bpn has moved on in context.  
There is an application property that allows the form to persist after being submitted.
**Forms echo the submitted response upon submit**
Because the value of the form is submitted to Amelia, the user can't confirm by the chat the value that was submitted; especially if the bpn does not echo the value back  
There is an application property to enable and configure the statement.
(e.g. {"The following value(s) have been selected: "} + {value})
![](attachments/25461075/28477688.png)
Figure. Echo Submitted Responses Example
## Quick Reply Buttons / Dropdown Selection
Quick reply buttons can be generated in the BPN using FormInputData.
> [!warning]  
>
> Clicking the button return the value associated with the button rather than the name. Similarly, dropdowns also return the value rather than name when the submit button is selected


| Button | Dropdown |
| ----|----|
| Figure. Buttons with Response Echo | Figure. Dropdown with Response Echo |

buttons.bpmndropdown.bpmn
## Multi-line Input
General Text, Date (YYYY-MM-DD), and Number format constraints are available.
There is currently no gateway side validation of the data.
Hitting submit returns a json value based on the field name and the input to Amelia.
![](attachments/25461075/28477697.png)  
(\*\*Developer Sample Image to display the return json value to Amelia\*\*)
Figure. Multi-line Input with Response Echo
The JSON value is formatted in the echo message to be more presentable.
![](attachments/25461075/28477698.png)
Figure. Multi-line Input with Response Echo Formatted
If the user does not fill out all information, the form will return empty string. The exception being the date field. Teams will not send the JSON key back in the activity; hence there's nothing to display and echo back.
![](attachments/25461075/28477699.png)
Figure. Multi-line Input with Response Echo Blank and Date Excluded
Note the missing date field in the echo.
multiline.bpmn
