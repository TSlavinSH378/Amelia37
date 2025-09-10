Amelia V3 has two interfaces available to chat with people. The traditional chat interface includes an avatar and, in some cases, the ability to see details about the BPN process, affective memory, and other factors she uses to respond in conversations. There's also a custom user interface that allows Amelia to present data collected during a conversation, for example, to build an insurance quote. Both interfaces allow images, buttons, and other types of interactive content to appear in the conversation flow.
The Amelia V3 administration pages include the ability to deploy custom user interfaces (UIs) for a variety of situations, for example, different Amelia environments for different products and services. User interfaces are configured as bundles then uploaded and deployed in Amelia instances.
UI bundles can be deployed by customers as well as IPsoft technical staff. Configuring UI bundles is done by IPsoft staff in consultation with clients.
Creating and configuring a new UI bundle requires importing a configurator BPN, if needed, then creating the UI bundle with the UI Bundles workspace.
## Import the Configurator BPN
The Configurator BPN (Business Process Network) is available from the IPsoft repository and available on request. The BPN is imported into a blank BPN to enable a domain to run the Configurator.
Once created, a configurator BPN should not require updates. The BPN has four tasks, a Say tasks at the start and end with a Script task to call internal Amelia functions and a Send the Integration Message task Amelia uses to display the chat note panel with the Configurator in the custom user interface.
If a configurator BPN is needed or has to be updated, on the left side of the Amelia V3 administration pages, click the Process Memory link and the Process Knowledge link when it appears. The Processes workspace appears.
1.  Click a folder and right mouse-click to select Add Process. If needed, first click the top level root folder then right mouse-click and select Add Folder.
2.  Enter the name *configurator* in the Create New Process popup that appears. Click the Create button to save. A blank BPN workspace appears.
3.  Click the wrench ![](attachments/11939949/20807931.png) icon at the top left of the workspace to display a submenu, click the Import link, then select the configurator.bpmn file downloaded from the IPsoft repository. For updates to this BPN, first delete all tasks then import the configurator.bpmn file into the empty BPN workspace.
4.  Click the Save tab above the workspace to save the BPN then click the Deploy tab to deploy the configurator BPN.
![](attachments/11939949/20807932.png)
Figure. Tasks in the Configurator BPN
The next step is to create a UI bundle with the UI Bundles workspace.
## UI Bundles Workspace
The UI Bundles workspace organizes the creation, updates, deployment, and publishing of custom user interfaces. 
The Amelia V3 administration pages includes a UI Bundlesworkspace to manage the deployment of UI bundles. Click the Systems Settings link in the administration pages then click the UI Bundles link to display the workspace.
Each custom user interface is deployed with a unique code used to display the interface with a URL. For example, a UI bundles with the code */product* would use the URL */Amelia/ui/product* to display the custom user interface.
![](attachments/11939949/11942688.jpg)
Figure. UI Bundles Workspace
Table. UI Bundles Workspace Elements

| Element | Description |
| ----|----|
| New Bundle | Displays a blank New Bundle workspace |
| Notepad Icon | Located to the left of a UI bundle name, click the icon to edit a UI bundle |
| Code | Added to /Amelia/ui/ URL path, for example, /Amelia/ui/code |
| Latest Published Version | For each UI bundle, the version number of the most recently published bundle. Creating a new version increments the version number by one. Saving a version also increments the version number by one. |
| Latest Deployed Version | The most recently deployed version of the bundle. Deployed versions display at the URL path with the version number, for example, /Amelia/ui/code/2 for the second version. |
| Default Deployed Version | The bundle to display at the specified URL path for the bundle. Bundles can be published and deployed but not display at the specified URL path until they are set as the Default Displayed Version.On the UI bundle edit page shown below, clicking the Default for Bundle? toggle setting for a UI bundle defines the default user interface displayed when the base URL path is used, for example, /Amelia/ui/code/. |
| Global Default? | If selected, displays the bundle at the /Amelia URL path. Setting a UI bundle as global default replaces the default builtin UI, the traditional chat interface with an avatar. |
| Administrator Group | Select a group who can edit and publish the UI bundle. Groups are created in the Groups workspace, available by clicking the System Settings link on the left side of Amelia's administration pages then clicking the Groups link. |
| Current Global Bundle | Displays a link to the UI bundle defined for the Global domain |
| Force Reset Global to builtin | Click to force the UI bundle for the Global domain to be the default builtin bundle |

## Assign Edit Capability
Individual UI bundles can be edited and published solely by administrators or the members of an assigned administrator group. For example, different teams can be given access to different user interfaces without any team having administrative privileges for all UI bundles.
To assign the ability to edit and publish a UI bundle, click the Administrator Group dropdown list to the far right of a bundle list entry then select the appropriate group.
To create a group, click the Systems Settings link on the left side of Amelia's administration page then click the Groups link to display the Groups workspace.
## Create a New UI Bundle
Creating a UI bundle requires a set of files which use the Amelia V3 UI Bundles administration pages. Files are available from IPsoft Cognitive staff.
-   amelia-customui-x.x.x.zip (where x.x.x is the current version number) contains the default custom UI elements, for example, logos, Amelia avatar, and color definitions
-   config.json defines the default custom UI elements in a JSON structure
On the left side of the Amelia V3 administration pages, click the System Settings link and the UI Bundles link when it appears. The UI Bundles workspace appears, as shown below.
1.  Click the New Bundle link at the top right of the workspace. The New Bundle page appears.
2.  Type the Code to use in the URL file path, for example, the code *test* would have the URL */Amelia/ui/test*. Type the Revision Name for the bundle.
3.  Open the config.json file downloaded from the IPsoft repo then copy and paste its contents into the Config Json field on the New Bundle page.
4.  Click the folder icon next to the UI Zip Bundle field and select then upload the amelia-custom.x.x.x.zip file (where x.x.x is the current version number) with the New Bundle page.
5.  If appropriate, add Content Security Policy (CSP) header information and notes.
6.  Click the Save button at the top right of the New Bundle page to save and create the new UI bundle. The edit page for the UI bundle will appear. In the Current Revisions section of the edit page, the Published? toggle is switched on.
> [!warning]  
>
> Clicking the Configurator Create New UI Bundle button multiple times saves a new version of the UI bundle each time whether or not any details have changed. Each version has a unique version ID and URL path. Version IDs and URL paths are available in the UI Bundle edit workspace where they can be set as the new default user interface.

![](attachments/11939949/11942691.png)
Figure. New UI Bundle Edit Workspace
![](attachments/11939949/11942692.png)
Figure. UI Bundle Edit Workspace
## Deploy and Publish a UI Bundle
Once a bundle is created and saved and the edit page displays, as shown above, the Current Revisions section of the page will show the Published? toggle as active. Alternately for UI bundles listed in the UI Bundles workspace, click the notepad icon to the left of any bundle name to display the edit page.
1.  Click the Deployed? toggle in the Current Revisions section for the selected revision. The linked URL path for the deployed version appears to the right of the active Deployed? toggle.
2.  Click the Default for Bundle? toggle in the Current Revisions section to make the revision the default user interface when the base URL path is used.
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
