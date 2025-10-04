{% version "3.x" %}
Amelia's Process Memory interfaces provides tools to define Business Process Networks to map how Amelia responds to user interactions. The BPN interface has these components to build process flows:
-   **Workspace** to create, edit, approve, and script BPN process flows
-   **Tool Bar** to drag and drop elements to build process flows
-   **Task Tools** to define what happens at decision points within the process flow
-   **Flow Line Tools** to create links between events and other BPN elements, as well as define responses to Tasks
-   **Script Library** holds scripts shared across multiple BPN models
-   **Tabular Data** and **Resource Objects** store commonly used data for one or more BPN models
-   **Buckets** contain stored files available to BPN models and Present tasks
To access the BPN workspace, click the Process Memory heading, located near the top left of the Amelia chat interface, then click the Process Knowledge link that appears immediately below the heading. The BPN workspace appears, with a list of BPNs on the left side and a blank workspace on the right side.
# Process Knowledge Workspace
BPNs can be created with a drag and drop workspace with a variety of configuration settings. Properties Panel settings are discussed in detail later in the [BPN Tasks](BPN%20Tasks) page.
![](attachments/11939361/11941342.jpg)
Figure. BPN Editor Workspace
## Top Navigation
Table. BPN Workspace Top Navigation
<table class="wrapped relative-table confluenceTable" style="width: 72.1649%;">
<colgroup>
<col style="width: 20%" />
<col style="width: 79%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">BPN Editor Top Navigation Tabs</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Save</td>
<td class="confluenceTd">Click to save the open BPN workspace</td>
</tr>
<tr class="even">
<td class="confluenceTd">Deploy</td>
<td class="confluenceTd">Approve BPN and load into Amelia's system for processing and evaluation</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Undeploy</td>
<td class="confluenceTd">Remove the BPN from Amelia's memory. Any dependent sub-flow BPNs will be undeployed at the same time as the main BPN.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><div class="content-wrapper">
<p><strong>Settings (<img src="attachments/11939361/11941344.png" />)</strong></p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Amelia Trainer &gt; Intents</td>
<td class="confluenceTd">Click to open a popup window to create and manage intents</td>
</tr>
<tr class="even">
<td class="confluenceTd">Amelia Trainer &gt; Entities</td>
<td class="confluenceTd">Click to open a popup window to create and manage entities</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Export</td>
<td class="confluenceTd">Export the open BPN workspace as an XML .bpmn file or PDF</td>
</tr>
<tr class="even">
<td class="confluenceTd">Import</td>
<td class="confluenceTd">Import saved BPN files in XML .bpmn file format</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Right Side Icons</strong> (with Properties Panel toggled closed)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939361/11941345.png" /></p>
</div></td>
<td class="confluenceTd">Click to select a version of the BPN to display in the workspace.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939361/11941346.png" /></p>
</div></td>
<td class="confluenceTd">Click to display a popup with versions of the BPN to manage.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939361/11941347.png" /></p>
</div></td>
<td class="confluenceTd">Click to display the BPN workspace full screen. Press ESC key to return to normal viewing mode.</td>
</tr>
</tbody>
</table>
## Panels
The BPN workspace has a Process Tree area and a Properties Panel. Both can be toggled to become visible or closed.
Table. BPN Workspace Panels

| Panel | Description |
| ----|----|
| Properties Panel | After a task, flow, gateway, or BPN model workspace is selected, click the Properties Panel to display any options for a selected item. Click the Properties Panel title to toggle the panel open or closed. |
| BPN List | Displays the folders and BPN models. Double-click a folder or model name to display folders and models. Click the Process Tree title to toggle the area open or closed. Search BPN model or folder names with the Search box at the top of this area. |

## Tool Bar
The BPN tool bar on the left side of the BPN workspace makes it easy to drag and drop to define process flows.
Table. BPN Workspace Tool Bar Icons

| BPN Tool Icon | Description |
| ----|----|
|  | Click this lasso icon then drag to select parts of the BPN process diagram, as a way to manage large BPNs with many tasks and other elements |
|  | Click to activate the space/remove tool then click and drag to create or remove vertical or horizontal space between elements in a BPN process diagram. It is a way to manage large BPNs with many tasks and other elements. |
|  | Click create a Start event then drag into position and click to set down |
|  | Click to create an End event then drag into position and click to set down |
|  | Click to create a Gateway event then drag into position and click to set down |
|  | Click to create a Task then drag into position and click to set down |

## Task Tools
Click once on a task to display a set of task tools.
![](attachments/11939361/11941348.png)
Figure. BPN Task Object Tool Icons for Ask and Script Tasks
The icons that appear to the right of a task provide configuration options when you click once on any task. Some icons appear only for specific task types.
Table. BPN Task Object Tool Icons

| Task Object Icon | Description |
| ----|----|
|  | Create an end event connected to the selected task by a process flow line |
|  | Create a gateway connected to the selected task by a process flow line. The default setting is exclusive but can be changed. |
|  | Create a new task connected to the selected task by a process flow line |
|  | Add a non-functional comment or note for the selected task |
|  | Modifies the active task or flow behavior. Script tasks allow processes to execute during BPN execution outside the natural language processing of tasks, for example, to display data to the user. The User, Manual Task, and Service Task selection options are not used.The top of the popup menu includes three additional options:Parallel Multi Instance (three vertical bars icon) – 
Sequential Multi Instance (three horizontal bars icon) – 
Loop (circle arrow icon) – |
|  | Click to delete the selected task |
|  | For script tasks, click to open script dialog for editing. Available only for script tasks. |
|  | Click to attach a Flow line arrow from the selected task to anywhere in the BPN |
|  | Task icons for the Run the Workflow and the Run the Integration Flow tasks now include an eye icon that, when clicked, opens the BPN workspace or integration flow referenced in the tasks. Clicking the browser back arrow returns to the BPN process workspace. |

The easiest way to create tasks is to click once on an task to display the task tool icons and select the square task icon in the top right:
![](attachments/11939361/11941349.jpg)
Figure. BPN Task Object Tools: Create a Task Step 1
Clicking the square task icon creates a new task attached or appended to your mouse. Move your mouse to position the new task then click to place and open it.
![](attachments/11939361/11941350.jpg)
Figure. BPN Task Object Tools: Create a Task Step 2
A flow line arrow is created automatically to connect the original task and new task. Repeat this process to create tasks needed for a BPN.
Double-click on an task to edit and configure the task, for example, to add text.
## BPN Revisions
Versions of BPNs, and the ability to switch to an earlier or later version of a BPN, is available with the Process Knowledge workspace which is part of the Process Memory part of Amelia’s administration pages.
BPN version numbers appear at the top right of the workspace with the current active version in bold. Click a version number to display the selected version. A revision popup also helps manage prior versions.
![](attachments/11939361/11941351.jpg)
Figure. BPN Revision Management User Interface
When a non-active version is displayed in the BPN workspace, the Deploy button near the top left of the workspace becomes active. Clicking the active Deploy tab changes the active BPN version and number.
To filter prior revisions, click the revision popup icon at the top right of the BPN workspace, to the right of the listed version numbers. The revisions popup appears. Filter revisions by BPN type or status.
![](attachments/11939361/11941352.png)
Figure. BPN Revisions Popup
## Move BPNs
BPN models can be dragged from one folder to another folder in the Processes workspace in the Process Knowledge area of Amelia’s administration pages.
BPN models can be moved with a right mouse-click over the name of a BPN model listed on the left side of the Processes workspace. Select Move from the popup menu to display the Move BPN Model popup box. If needed, select the correct domain from the top left dropdown list in the popup. Then select the folder where to move the model. Click Submit to move the model.
![](attachments/11939361/11941353.png)
Figure. Right Click Mouse to Move BPN Model
![](attachments/11939361/11941371.png)
Figure. Select Domain and Folder in the Move BPN Model Popup
# Flow Line Edit Tools
Hover over the left or right of straight process flow line (not corners) until yellow dots appear. Double-click the dot on a line to add or edit text.
![](attachments/11939361/11941372.jpg)
Figure. BPN Flow Line Edit Tools: Enter Text
Hover over the center of a straight process flow line to drag and position the line up or down when a yellow rectangle appears. Click and hold any dot to drag the flow line into position.
![](attachments/11939361/11941373.jpg)
Figure. BPN Flow Line Edit Tools: Shape Lines
# Script Library Workspace
Amelia V3 includes the ability to share scripts used by script tasks in multiple BPN models within a domain. To access the script library workspace, click the Process Memory link on the left side of Amelia administration pages then click Script Library.
![](attachments/11939361/11941374.jpg)
Figure. Script Library Workspace
Table. Script Library Workspace Elements

| Script Library Workspace Element | Description |
| ----|----|
| Top Navigation | Click tabs to Save a script or Check Syntax of a script and display results in Console below. Scripts also can be imported from files or exported as files. |
| Language | Groovy is the default language. |
| Import User Libraries | Click to display then select from a dropdown list of shared scripts. |
| Code Editor | Includes syntax highlighting and line numbers. |
| Console | Check Syntax results display here. |
| Script Tree | Displays the folders and scripts. Double-click a folder or script name to display folders and models. Click the Script Tree title to toggle the area open or closed. Search script or folder names with the Search box at the top of this area. |

# Tabular Data
BPN models can use different assets for data retrieval. Tabular data can be accessed through BPN Script tasks while the Content Manager stores files shown to users with the BPN Present task and collected with the Request task.
CSV files can be uploaded and made available to BPN tasks to query and retrieve data used to complete a conversation. For example, a CSV file with geolocation information might provide office locations to be queried based on the location of the user. Tabular data provides database features without cluttering Amelia's database. Refer to the [Tabular Data Sources](Script-Tasks_11939477.html#ScriptTasks-TabularData) section of the [Script Tasks](Script%20Tasks) page of this guide.
![](attachments/11939361/11941379.png)
Figure. Tabular Data Workspace
# Content Manager
The Content Manager includes buckets as a folder to hold files displayed to users in a conversation with the Present task, as well as a location to upload files collected from users. Refer to the [Content Manager Buckets and File Storage](BPN-Tasks_11939422.html#BPNTasks-ContentManager) section in the [BPN Tasks](BPN%20Tasks) page for more details.
![](attachments/11939361/11941380.png)
Figure. Buckets Workspace
{% /version %}
