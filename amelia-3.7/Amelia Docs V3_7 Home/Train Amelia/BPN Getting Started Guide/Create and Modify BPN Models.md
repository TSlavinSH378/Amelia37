{% version "3.x" %}
The BPN creation process involves opening a model followed by layout of different elements to document one or more process flows. Models are submitted for approval and become active within Amelia upon approval.
![](attachments/11939409/11941390.jpg)
Figure. Process Memory BPN Editor Workspace
# Create a BPN Model
BPNs are available on Amelia's administration pages.
1.  On the administration page, scroll down the left navigation links and click Process Memory link then the Process Knowledge link that appears.
2.  Right mouse click over the top folder in the BPN list and select Add Folder from a popup, type the name of the folder in the Create New Folder popup, then click the Create button. Alternately, type a folder name in the Search text field then press Enter to search. A folder will appear below the search field.
3.  Select a folder and right mouse-click to display a popup and select Add Process. The Create New Process popup will appear.
4.  Type a Process Name. The name must be unique within the current selected domain.
5.  Click the Create button to create a new BPN. A blank BPN workspace with a Start task will appear in the right side workspace.
6.  Click the Save button near the top left of the BPN workspace to finish creation of the BPN.
7.  Click anywhere on the workspace background then click the Properties Panel into view. Set the model Type to Deterministic or Headless. See the [Types of BPN Models](Types%20of%20BPN%20Models) page for details.
To build out a BPN, use the Tool Bar to create the tasks, flows, gateways, and other elements of the larger process flow, as described in [Process Memory Interfaces](Process%20Memory%20Interfaces), [BPN Tasks](BPN%20Tasks), and [Script Tasks](Script%20Tasks).
> [!warning]  
>
> Names for BPNs must be unique within each domain. BPNs also are accessible to parent and child domains.
>
> The closest BPN has the highest priority in cases where a parent or child domain has the same name for a BPN. For example, if the global, parent, and current domains each have a BPN named Weather, a BPN in the current domain will call the Weather BPN from the current domain. If there is no Weather BPN in the current domain, the BPN in the current domain would call the Weather BPN defined in the parent domain.

# Save and Deploy a BPN
BPN models must be deployed for Amelia to be able to use them in a conversation.
1.  Click the Save button near the top left of the BPN workspace.
2.  Click the Deploy button, to the right of the Save button.
# Test BPN Model Workflows
Amelia’s administration pages allow testing of the BPN process workflow. One approach uses the Amelia instance built into the administration pages while the other approach uses the default chat interface which includes several diagnostic tools.
## Test with Built In Amelia Interface
Every workspace in Amelia's administration pages includes a circle at the top right. When clicked, this opens a chat window to converse with Amelia. All active intents, entities, models, and other materials in a selected domain are available to this version of Amelia. The built in chat interface provides a quick way to test progress while optimizing an instance of Amelia for a domain.
## Test with Default Chat Interface
Amelia's default chat interface includes a range of diagnostic tools to observe and evaluate her performance handling a conversation. In the top right of the administration workspaces, click the Secondary Links dropdown and select Mind to display the default chat interface in a new browser tab with the Mind interface selected. Click the Process Ontology tab at the top right edge of the Mind workspace.
1.  From the Amelia administration pages, select Mind from the secondary navigation links at the top right of the administration pages. If needed, select the domain to use to chat with Amelia.  
    ![](attachments/11939409/11941397.png)  
    Figure. Select Mind from Secondary Navigation Links  
2.  With the Mind interface on the right side of the window and Amelia's chat interface on the left, click the Process Memory tab on the right side of the Mind interface.
3.  In Amelia's chat interface, type *run the workflow BPN_Name* where BPN_Name is the name of the BPN model. The Mind interface will show the BPN in the Process Memory panel. Amelia will perform the first task in the BPN.  
    ![](attachments/11939409/11941398.jpg)  
    Figure. Mind Interface and Process Memory Tab Selected
# Debug BPN Model Workflows
Common reasons BPNs fail to trigger during a conversation are several:
-   Names misspelled or not included in the correct spot, for example, an Ask task connected to an entity needs to use the correct entity name and select a question for the Question dropdown in the Ask task Properties Panel.
-   Configuration errors caused by tasks, script tasks, classifiers, entities, and other elements.
-   Entity and intent utterances, FAQs, models, and other elements that conflict with other utterances set up with Amelia.
-   Request tasks missing a Cancel flow path, as described in [Service Prefix and Functions](BPN-Tasks_11939422.html#BPNTasks-ServicePrefixFunctions) in the [Request Task](BPN-Tasks_11939422.html#BPNTasks-RequestTask) documentation.
## Basic Debugging
-   Double check the usage of all tasks according to the [BPN Tasks](BPN%20Tasks) and [Script Tasks](Script%20Tasks) documentation.
-   For any [Script Tasks](Script%20Tasks), run the script through an online or local tester for the language used.
-   Find the error in the log file located on the server under** /apps/IPsoft/amelia/\*/var/log/amelia-engine.log**
-   Ensure your latest changes to the BPN(s) being executed have been deployed in the Process Memory workspace.
## Integration Errors
-   Double check the usage of the [Run the Integration Flow task](BPN-Tasks_11939422.html#BPNTasks-RunIntegrationFlow) is correct according to the documentation in the [Integration Guide](Integrations%20Guide).
-   Ensure the integration flow is [deployed](Create-an-Integration-Flow_11939847.html#CreateanIntegrationFlow-DeployIntegrationService).
-   Ensure that all the input variables used in the integration flow are available to BPN script tasks according to the [Integration Guide](Integrations%20Guide) and as demonstrated in the [Create a BPN Process Flow](Create%20a%20BPN%20Process%20Flow) section of the guide.
# Copy, Import, and Export BPNs
BPNs can be copied from one to another through export then import of a BPN into a new model. Click the Export or Import button at the top of the Process Memory BPN workspace. BPNs can be exported in XML (.bpnm) format or PDF.
Importing a BPN into a BPN model will overwrite existing tasks and other elements in the destination model. It also is possible to use the Lasso tool from the BPN tool bar to select one or more elements of a BPN model then use Ctrl+C/Command+C to copy the elements and Ctrl+V/Command+V to paste the elements elsewhere in the model. It is not currently possible to copy and paste model elements from one model to another.
{% /version %}
