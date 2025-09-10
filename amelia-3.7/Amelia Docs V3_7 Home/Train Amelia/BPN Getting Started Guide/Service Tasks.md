Service BPN tasks create custom UI interfaces with clicks and light typing instead of typing code in a Script task. Service and Script tasks both use Amelia services. However, a Service task offers a code free way to access different services.
# Creating a Service Task
To create a Service task, click a BPN task to display the option icons. Then click the ![](attachments/28476460/28476473.png)wrench icon once to display a dropdown list of BPN types. Select Service Task from the dropdown list.
![](attachments/28476460/28476464.png)
Figure. Select Service Task
The BPN task will display two gear icons at the top left of the BPN task to indicate this is a Service task. To select a widget to customize the custom UI, click the BPN again to display the option icons. Then click the ![](attachments/28476460/28476474.png)notepad icon to display the Widget Helper.
![](attachments/28476460/28476466.png)
Figure. Select Notepad Icon to Display Widget Helper Popup
The Widget Helper popup displays a list available widgets used to define the Service task.
![](attachments/28476460/28476467.png)
Figure. Widget Helper Popup with Service Task Widgets
# Service Task Widgets
Service task widgets provide an easy way to create elements for a custom UI to support Amelia's conversation as she collects data and interacts with people.
## Form Input
There are two form-related buttons that can be created with widgets, a single select button and multi select button.
### Single Select Button
The Single Select button creates one or more buttons to display in the custom UI. Click the ![](attachments/28476460/28476475.png) circle plus button to create additional buttons. Each button appears in the right side of the workspace and updates as changes are made.
![](attachments/28476460/28476468.png)
Figure. Form Input Single Select Button
Table. Form Input Single Select Button Elements
<table class="wrapped confluenceTable" style="width: 1016.0px;">
<tbody>
<tr class="header">
<th class="confluenceTh" style="width: 120.0px">Element</th>
<th class="confluenceTh" style="width: 896.0px">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd" style="width: 120.0px">Target Variable</td>
<td class="confluenceTd" style="width: 896.0px"><div class="content-wrapper">
<p>Accept or define the variable name to contain the value of the button. Click the <img src="attachments/28476460/28476477.png" />gear icon to edit and change the target variable name.</p>
</div></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd" style="width: 1016.0px"><strong>Options</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 120.0px">Button Name</td>
<td class="confluenceTd" style="width: 896.0px">Type the name for the button</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 120.0px">Button Value</td>
<td class="confluenceTd" style="width: 896.0px">Type the value for the button</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 120.0px">Disable</td>
<td class="confluenceTd" style="width: 896.0px">Click to disable the button</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 120.0px">Hidden</td>
<td class="confluenceTd" style="width: 896.0px">Click to hide the button</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 120.0px">Selected</td>
<td class="confluenceTd" style="width: 896.0px">Click to select the button by default</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 120.0px">Drop an Image</td>
<td class="confluenceTd" style="width: 896.0px">Drag and drop an image to appear as a button. Or click the target area to open a file explorer popup then select a file on the local computer.</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 120.0px"><div class="content-wrapper">
<p><img src="attachments/28476460/28476476.png" /></p>
</div></td>
<td class="confluenceTd" style="width: 896.0px">Click to create a new button set with target variable and options.</td>
</tr>
</tbody>
</table>
### Multi Select Button
The Single Select button creates one or more buttons to display in the custom UI. Click the ![](attachments/28476460/28476475.png) circle plus button to create additional buttons. Each button appears in the right side of the workspace and updates as changes are made.
![](attachments/28476460/28476469.png)
Figure. Form Input Multi Select Button
Table. Form Input Multi Select Button Elements
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Target Variable</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Accept or define the variable name to contain the value of the button. Click the <img src="attachments/28476460/28476477.png" />gear icon to edit and change the target variable name.</p>
</div></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Options</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Button Name</td>
<td class="confluenceTd">Type the name for the button</td>
</tr>
<tr class="even">
<td class="confluenceTd">Button Value</td>
<td class="confluenceTd">Type the value for the button</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Disable</td>
<td class="confluenceTd">Click to disable the button</td>
</tr>
<tr class="even">
<td class="confluenceTd">Hidden</td>
<td class="confluenceTd">Click to hide the button</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Selected</td>
<td class="confluenceTd">Click to select the button by default</td>
</tr>
<tr class="even">
<td class="confluenceTd">Drop an Image</td>
<td class="confluenceTd">Drop an ImageDrag and drop an image to appear as a button. Or click the target area to open a file explorer popup then select a file on the local computer.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/28476460/28476476.png" /></p>
</div></td>
<td class="confluenceTd">Click to create a new button set with target variable and options</td>
</tr>
</tbody>
</table>
## Integration
There are two integration-related widgets, a chat note alert and a calendar people can use to select dates.
### Chat Note Alert Option
Alerts convey important information for people to know as Amelia works with them during a conversation. Changes made on the left side of the workspace will be reflected on the right side.
![](attachments/28476460/28476472.png)
Figure. Chat Note Alert
Table. Chat Note Alert Elements
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Target Variable</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Accept or define the variable name to contain the value of the alert. Click the <img src="attachments/28476460/28476477.png" />gear icon to edit and change the target variable name.</p>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">Select Alert Name</td>
<td class="confluenceTd">Select the alert name. Info Banner, Warning Banner, Error Banner, and Success Banner are options. Info Banner is the default.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Alert Type</td>
<td class="confluenceTd">Select Alert Type. Text Dismiss is the default.
<div class="table-wrap">
<pre class="table"><code>| Alert Type | Description |
| ----|----|
| Text |  |
| Text Dismiss |  |
| Text Action |  |
| Text Multi |  |</code></pre>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">Info Message</td>
<td class="confluenceTd">Type the message for the alert</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Send Message</td>
<td class="confluenceTd">Click to select and send a message</td>
</tr>
</tbody>
</table>
### Form Input Calendar
The calendar widget lets people select either a specific data or date range with the ability to limit dates to today and future dates. Changes made on the left side of the workspace will be reflected on the right side.
![](attachments/28476460/28476471.png)
Figure. Form Input Calendar Range
Table. Form Input Calendar Range Elements

| Element | Description |
| ----|----|
| Target Variable | Accept or define the variable name to contain the value of the calendar. Click the;gear icon to edit and change the target variable name. |
| Select Title | Type a name for the calendar |
| Select Type | Select calendar type. Range Date Picker and Single Date Picker are options |
| Create a Range for Users to Select Within | Appears only if Range Date Picker is selected as calendar type |
| Do Not Allow Dates Before Today | Select to prevent people from selecting past dates. Only today and future dates are available for selection. |
| Send Message | Click to select and send a message |

## Chat Notes
There is a widget that can create a chat note. Changes to the chat note definition on the left of the workspace will be reflected in the Preview area on the right side.
![](attachments/28476460/28476470.png)
Figure. Chat Note Create Workspace
Table. Chat Note Create Elements
<table class="wrapped confluenceTable" style="width: 1050.0px;">
<tbody>
<tr class="header">
<th class="confluenceTh" style="width: 147.0px">Element</th>
<th class="confluenceTh" style="width: 903.0px">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Target Variable</td>
<td class="confluenceTd" style="width: 903.0px"><div class="content-wrapper">
<p>Accept or define the variable name to contain the value of the chat note. Click the <img src="attachments/28476460/28476477.png" />gear icon to edit and change the target variable name.</p>
</div></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd" style="width: 1050.0px"><strong>Chat Note</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Title</td>
<td class="confluenceTd" style="width: 903.0px"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Sub-Component(s)</td>
<td class="confluenceTd" style="width: 903.0px">Define the sub-component(s). Click the X to delete a sub-component definition.
<div class="table-wrap">
<pre class="table"><code>| Element | Description |
| ----|----|
| label |  |
| value |  |
| Type |  |
| Title |  |</code></pre>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px"><div class="content-wrapper">
<p><img src="attachments/28476460/28476476.png" /></p>
</div></td>
<td class="confluenceTd" style="width: 903.0px">Click to create a new chat note with target variable and sub-components.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Send Message</td>
<td class="confluenceTd" style="width: 903.0px">Click to select and send a message</td>
</tr>
</tbody>
</table>
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-12-20_14-17-13.png](attachments/28476460/28476463.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-19-27.png](attachments/28476460/28476464.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-20-13.png](attachments/28476460/28476465.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-21-3.png](attachments/28476460/28476466.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-22-8.png](attachments/28476460/28476467.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-23-30.png](attachments/28476460/28476468.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-24-25.png](attachments/28476460/28476469.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-27-46.png](attachments/28476460/28476470.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-28-30.png](attachments/28476460/28476471.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-29-16.png](attachments/28476460/28476472.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-34-20.png](attachments/28476460/28476473.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-34-53.png](attachments/28476460/28476474.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-45-36.png](attachments/28476460/28476475.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-47-58.png](attachments/28476460/28476476.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-20_14-50-49.png](attachments/28476460/28476477.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-1-15_15-20-51.png](attachments/28476460/28477252.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-1-15_15-23-45.png](attachments/28476460/28477253.png) (image/png)  
