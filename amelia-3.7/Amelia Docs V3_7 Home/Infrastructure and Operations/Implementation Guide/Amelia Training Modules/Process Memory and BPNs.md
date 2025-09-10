With Amelia V3, the use of Business Process Networks (BPNs) to manage conversations has been refined.
-   A new edge notation (service prefixes) for transitions specifies conditions with less complexity and code
-   Additional property settings for Ask tasks, for example, choice display behavior and subsequent ask behavior
-   Ask tasks are two types, questions or request an entity value
-   Entities (formerly slot grammars) and classifiers can be connected to ask lemma tasks
-   BPN model property types have expanded to include headless, stochastic, and composite entity elicitor types in addition to deterministic
-   Dynamic stochastic BPNs allow Amelia to jump around the BPN based on the conversation progress
-   A Tabular Data service has been added to provide data to be used by BPNs
-   Scripts can be stored in a library and used by multiple BPNs
The process to create BPNs and process flows in Amelia V3 is similar to V2 but with a slightly different workspace interface and tools, for example, edge notation and precondition tasks. The Amelia V3 [BPN Getting Started Guide](BPN%20Getting%20Started%20Guide) has extensive details about how to create BPN models. Links to specific related topics are at the bottom of this page.
# Process Memory Workspace
The workspace includes a list of folders and BPNs on the left, workspace in the middle, and a slide out properties panel on the right side.
![](attachments/11940402/11940431.jpg)
# BPN Model Types
In Amelia Version 3, BPNs have several possible types.
-   **Deterministic** — A BPN model whose tasks are executed sequentially. Its elements may perform dialog management and branching logic such as ad-hoc forks, joins, and gateways.
-   **Stochastic** —  A dynamic BPN model to be executed based on the current context in an active conversation. A spread activation algorithm evaluates all tasks in a model and decides which task is most appropriate to execute next. Tasks can be set as preconditions, requiring Amelia to process them ahead of others, for example, to collect data needed by the most appropriate task. Stochastic models work best for wrapper BPNs with Ask and Say tasks that also run sub BPNs that contain Script tasks to request and process user data.
-   **Headless** —  A BPN model whose tasks don’t use conversation, for example, the Ask or Say tasks. Script, Set, Unset tasks are allowed, as well as forking, join, and gateways. Headless BPNs are under development.
The model type is set in the Properties Panel of a BPN model by clicking a blank area of the workspace, opening the panel, then selecting Type.
# Create a Basic BPN
Business Process Network (BPN) diagrams are easy to create with the Amelia V3 Process Memory section. Click the Process Memory link on the left side of the administration pages then click the Process Knowledge link under it.
The exercise shows uses the Process Knowledge workspace to create a simple BPN with four tasks that splits into two flows.
![](attachments/11940402/11940430.png)
## Define the BPN
The simple BPN includes four tasks that splits into two flows.

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | ask "What's your favorite color?" | This task primes Amelia to collect a response from the user |
| 3 | say red | Amelia only processes this task if you answer red |
| 4 | say blue | Amelia only processes this task if you answer blue |

The thin line circle at the beginning of the BPN is the Start Event while the thick line circle at the End Event. All BPNs have one Start Event and at least one End Event.
The flow lines between the BPN tasks can be used to set up conditions that must be met for the flow to continue in a direction. In addition, the slash on the flow line to the *say red* task indicates it is the default flow.
All these points will be presented in detail as the BPN is built.
## Build the BPN
This exercise introduces Say and Ask tasks, two common tasks used in BPN models, as well as edge notation, flow line manipulation, default flows, and limited use of variables in a Say task.
The Save tab at the top right of the BPN model should be clicked periodically to save your work.
1.  If necessary, right mouse-click over the Root folder and click the Add Folder popup to create a new folder. Then right mouse-click over a folder to contain the BPN model and select Add Process from the popup menu.  
    ![](attachments/11940402/11940410.png)  
2.  Type the name of the BPN model, in this case, simpleBPN.  
    ![](attachments/11940402/11940412.png)  
3.  The new BPN Model appears with one thin circle Start Event. Click the Start Event and select the square Append Task icon, at top right of the set of icons, to add a task. The task appears to the right of the Start Event. Move the task to the right then click to place it.  
    ![](attachments/11940402/11940407.png)  
4.  With the task placed and clicked open, type *say let's get started*. Then click anywhere on the BPN model to deselect the new task.  
    ![](attachments/11940402/11940406.png)  
5.  Click the new Say task and select the Append Task icon. The task appears to the right of the first Say task. Move the new task to the right then click to place it.  
    ![](attachments/11940402/11940405.png)  
6.  With the second new task placed and clicked open, type *ask "What's your favorite color?"* then click anywhere on the BPN model to deselect the new task.  
    ![](attachments/11940402/11940404.png)  
7.  Click the new Ask task and select the Append Task icon. The task appears to the right of the Ask task. Move the new task to the right then click to place it.
8.  With the third new task placed and clicked open, type *say red* then click anywhere on the BPN model to deselect the new task.
9.  Click the Ask task and select the Append Task icon. The task appears to the right of the Ask task. Move the new task below the Ask task then click to place it.
10. With the fourth new task placed and clicked open, type *say $(response}* then click anywhere on the BPN model to deselect the new task. The *${response}* variable will display the response she receives, in this case, *blue*.  
    ![](attachments/11940402/11940442.png)  
11. Click the *say red* task and select the Append End Event icon. The End Event appears to the right of the *say red* task. Move the End Event to the right of the Say task then click to place it.  
    ![](attachments/11940402/11940441.png)  
12. Click the *say ${response}* task and select the Flow icon. The Flow line appears to the right of the *say ${response}* task. Drag the flow line to the End Event until it turns green. Click the End Event to deselect the flow line.  
    ![](attachments/11940402/11940440.png)  
13. Move the mouse over the flow line until the flow position handle appears. Click the handle and drag it to the right, under the End Event.  
    ![](attachments/11940402/11940439.png)  
14. Click the flow line between the Ask task and *say red* task. Then click the Properties panel. In the Name field, type *red*. In the Expression field, type *response:equal('red')*. Click to close the Properties Panel.  
    The Name and Expression field define edge notation, the conditions that must be met to allow the conversation process to flow between tasks. The Name field allows a concise readable name and the Expression field allows for more detailed conditional statements. In this statement, *response* is a service available within the BPN model and *equal* is a method.  
    ![](attachments/11940402/11940435.jpg)  
15. Click the flow line between the Ask task and *say ${response}* task. Then click the Properties panel. In the Name field, type *blue*. In the Expression field, type *response:equal('blue')*. Click to close the Properties Panel.
16. Click the flow line between the Ask task and the *say red* task. Click the wrench icon and select Default flow. Any response Amelia cannot process will direct her conversation to the *say red* task by default.  
    ![](attachments/11940402/11940436.png)  
17. Click the Save tab at the top left of the Process Flow workspace. Click the Deploy tab to save the BPN model to Amelia's memory. Amelia will display a warning message about the use of ${response} which can be ignored.
## Interact with Amelia
With the simpleBPN model built, click the Mind link at the top right of the administration pages to display Amelia's conversation area with the Mind view active on the right side panel.
1.  In the Mind view panel, click the Process Memory tab on the right edge. Then click the Debug link at the bottom right of the conversation area to display messages.
2.  In the text message box on the bottom left of the conversation area, tell Amelia to run the BPN model simpleBPN.  
    ``` text
    run the workflow simpleBPN
    ```
3.  Amelia will process the BPN model. The Process Memory area of the Mind view will display progress through the model. The Debug area will display messages.  
    ![](attachments/11940402/11940429.png)
# Edge Notation
Process flow lines from a task can include conditions to determine whether or not the flow is followed in a BPN process. For example, if a person buys car insurance, the value of their car might require different process flows from a task that asks for their car model. In Amelia V3, a task edge condition has both a Name and Expression, as shown in this screen shot. This helps keep the BPN model clean and easy to read.
![](attachments/11940402/11940435.jpg)
In addition, edge notation now includes a number of service prefixes to reduce ambiquity and shorten expressions used for edge conditions.
-   **response** - Operations for user-response-related navigation.
-   **slot** - Operations for slot-related navigation.
-   **ctx** - Operations associated with the current context.
-   **choice** - Allows for the specification of the choices that are available to an ask task.
-   **bpn** - For miscellaneous workflow navigation operations.
-   **upload** - Operations for resource-upload-related navigation.
In the screen shot above, in the Expression field of the Properties panel, the response service prefix is used with the default yes grammar. Any response related to yes – for example, yup or okay – allows the conversation to progress to the next task lemma.
# Precondition Tasks
Amelia V3 BPN models can be defined as dynamic stochastic models. These models have a typical set of task lemmas, flows, and gateways. However, based upon the conversation Amelia has with a person, she can jump from one task lemma to another in the model to respond in a more human and appropriate way. Some task lemmas can be set as a precondition to ensure task lemmas have the information they need when Amelia processes the lemma.
Which task Amelia jumps to is determined by a real time evaluation of her current conversation compared with the weighted value of each task lemma in the stochastic BPN. Once the appropriate task lemma is identified, Amelia jumps to any precondition task lemmas in the flow path between the current lemma and the selected lemma.
# Links
-   [BPN Getting Started Guide](BPN%20Getting%20Started%20Guide)
-   [Types of BPN Models](Types%20of%20BPN%20Models)
-   [BPN Tasks](BPN%20Tasks)
-   [Edge Notation and Flow Routing](https://docs.ipsoft.com/display/AmeliaDocsV3/Process+Flows#ProcessFlows-EdgeNotationandFlowRouting)
-   [Script Tasks](Script%20Tasks)
-   [Tabular Data Resources](https://docs.ipsoft.com/display/AmeliaDocsV3/Script+Tasks#ScriptTasks-TabularDataSources)
-   [Buckets and File Storage](https://docs.ipsoft.com/display/AmeliaDocsV3/BPN+Tasks#BPNTasks-BucketsandFileStorage)
-   [FreeMarker to Display Dynamic Data](https://docs.ipsoft.com/display/AmeliaDocsV3/Script+Tasks#ScriptTasks-FreeMarkertoDisplayDynamicData)
