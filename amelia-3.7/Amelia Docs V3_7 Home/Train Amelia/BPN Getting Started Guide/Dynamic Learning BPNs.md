-   [Trigger Amelia’s Learning Behavior](#DynamicLearningBPNs-TriggerAmelia’sLearningBehavior)
    -   [Requirements](#DynamicLearningBPNs-Requirements)
    -   [Create an Entity user_age](#DynamicLearningBPNs-CreateanEntityuser_age)
    -   [Create a BPN doDriverAge](#DynamicLearningBPNs-CreateaBPNdoDriverAge)
    -   [Run the Workflow doDriverAge](#DynamicLearningBPNs-RuntheWorkflowdoDriverAge)
-   [Pick Up Escalated Conversation](#DynamicLearningBPNs-PickUpEscalatedConversation)
-   [Approve a Dynamic BPN](#DynamicLearningBPNs-ApproveaDynamicBPN)
Amelia has the ability to listen to escalated conversation and learn from them, creating updated versions of BPN processes for approval by a knowledge engineer. The updated BPN versions are called dynamic or learning BPNs.
Currently only these types of escalation trigger Amelia’s learning capabilities:
-   Failure of a user utterance to satisfy an Ask task
-   Runtime failure to evaluate a task expression
-   Runtime failure to evaluate an edge expression
Escalations due to an internal error or use of the Escalate tasks do not trigger Amelia’s ability to learn.
# Trigger Amelia’s Learning Behavior
Providing an answer that does not satisfy an Ask task causes an escalation. This short tutorial creates a BPN with a single Ask task followed by a Say task. The Say task triggers only if the user responds with an expected value. Not answering with the expected response causes an escalation and triggers Amelia’s learning behavior.
## Requirements
-   Amelia 3.7.x or higher
-   An escalation team created with users assigned to the escalation team, an escalation queue created with the escalation team assigned to the queue, and the escalation queue assigned to the domain. Use the System Settings links in Amelia’s administration pages to create an escalation response capability.
## Create an Entity user_age
The first step is to create an entity slot called `user_age`. There are two ways to create an entity slot. In Amelia’s administration pages, click the Amelia Trainer link then the Entities link to display the Entities workspace.
1.  Click the Add Entities tab on the far right of the Entities workspace. The Add Entities panel appears.
2.  Type in the name `user_age` as the Entity Name and select `Integer` as the Datum Type. Then type `How old are you` as the Question/Prompt, add a description if useful, and click the Add button. The entity appears in the middle of the workspace. Or search user_age to find the new entity.
In addition, within the BPN Processes workspaces, click the![](attachments/11939509/28476317.png)wrench icon under the BPN tab then click Amelia Trainer then click Entities. The Entities popup appears. Click the + Add Entities button at the top of the popup then fill out the Entity Name (user_age), Datum Type (Integer), and Question/Prompt (How old are you?). Click the Add Entity button at the bottom of the popup to save the entity.
![](attachments/11939509/28476316.png)
Figure. Alternate Way to Create an Entity
## Create a BPN doDriverAge
The second step is to create a BPN. In Amelia’s administration pages, click the Process Memory link then the Process Knowledge link to display the Processes workspace. Right mouse-click over a folder and select Add Process from the popup menu. Add a process called `doDriverAge`. Use the table below to create the BPN.
![](attachments/11939509/28475514.png)
Figure. doDriverAge BPN Model
Table. BPN Specifications to Build doDriverAge BPN Model

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | ask for the slot user_age | With the Ask task selected, click the Properties Panel on the right edge of the workspace and select from the Question dropdown list the Amelia Asks question created with the user_age entity. |
| 2 | say you can apply for a driver’s license | Click the flow line from the Ask task to this Say task then click the Properties panel:For the Name field, type 16 or olderFor the Expression field type slot:value()>=16 |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## Run the Workflow doDriverAge
When the BPN model is built and approved, as described above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the top right edge of the Mind panel. This will display the BPN process as Amelia works through it.
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  At the top left, click your name and set your status to Ready.
3.  Ask Amelia to run the doDriverAge workflow by typing this command in the chat interface:  
    ``` groovy
    run the workflow doDriverAge
    ```
4.  When Amelia asks your age, type `14` or `14 years old`. These answers will not trigger the Say task. Amelia may tell you she’s looking for an answer 16 years or older, the value of the Name field for the flow line to the Say task.
5.  Respond repeatedly with an age value lower than 16 until Amelia escalates.
![](attachments/11939509/28475516.png)
Figure. Amelia Cannot Respond with BPN Process
# Pick Up Escalated Conversation
Handling the escalation process teaches Amelia a second possible response can be handled with a Say task. Amelia then updates the BPN process and creates a revised BPN for approval.
There are two ways to watch Amelia update a BPN. In either situation, click your name at the top left and select the Ready status.
-   To see Amelia update a BPN, open a second Mind view browser window then click the Conversations link at the top right. Click the ![](attachments/11939509/28476329.png) Pickup icon at the right of the conversation entry. This opens a new browser window in Mind view. Click the Process Memory tab at the top right of the workspace.
-   When Amelia escalates, she displays a New Escalation popup at the bottom right of the screen. Click the Accept button to accept and join the conversation. A new agent window opens in a new web browser tab.
Once the Mind view is displayed, with the Process Memory tab active and status set to Ready, the next step is to act as a support person engaging in a conversation that trains Amelia how to respond to another scenario.
1.  Ask the question from the Amelia Asks field in the user_age entity definition, `How old are you?` Doing so tells Amelia where to begin marking any changes to her process. In this case, the Amelia Asks question for the entity is mapped to the Ask task properties in the BPN. Asking the question tells her to start with the Ask task to make changes. Amelia will update the BPN in the Process Memory panel in Mind view.
2.  For the user response, type `14` or `14 years old`. Notice Amelia creates a flow line from the Ask task with a condition expression set to the utterance, 14 or 14 years old. This corresponds to the Expression and Name fields for the flow line Properties Panel.
3.  As the agent browser window, type `Great. You can apply for a driver’s permit.` Notice Amelia creates a Say task with the utterance.
4.  Complete the conversation with utterances then click the Close button in the agent browser window. This signals Amelia to stop recording the BPN.
![](attachments/11939509/11939516.png)
Figure. Amelia Dynamically Updates a BPN Process
# Approve a Dynamic BPN
Once Amelia creates an updated version of a BPN process dynamically, the new revised BPN is available in the Processes workspace for the BPN. In Amelia’s administration pages, click the Process Memory link on the left side then the Process Knowledge link. Find then open the BPN in the Processes workspace.
1.  Click the double square versions icon to the right of the BPN version numbers located at the top right of the BPN workspace. A popup appears with a list of all versions. Amelia’s dynamically created version appears with a status of pending_merge. The merge icon appears to the right of the BPN Amelia used to create her version.  
    ![](attachments/11939509/11939515.png)  
    Figure. BPN Versions Popup with Merge Icon  
2.  Click the merge icon to display the Merge popup. Dynamically created versions appear as a list on the left side. Click the checkbox the left of the BPN version Amelia created. Then click the Merge button at the bottom right of the popup. The merged BPN appears as a new version in the BPN workspace.  
    ![](attachments/11939509/11939514.png)  
    Figure. Merge Popup with Dynamic Version  
3.  Make any changes then click the Save and Deploy buttons. In this case, remove the second Say task and update the flow line from the original Ask task to the new Say task. Select the flow line and update the Properties panel to `14 or 15 years old` for the Name and `slot:equal('14')||slot:equal("15")` for the Expression field.  
    ![](attachments/11939509/11939513.png)  
    Figure. BPN Versions Popup with Merge Icon
With the updated BPN saved and deployed, talk with Amelia and use the earlier answers that triggered an escalation. Click the Mind link at the top right then click the Process Memory at the top right of the Mind panel to display the BPN as Amelia converses.
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the doDriverAge workflow by typing this command in the chat interface:  
    ``` groovy
    run the workflow doDriverAge
    ```
3.  When Amelia asks your age, type 14 or 14 years old. Notice Amelia now responds with the response you made to the earlier escalation.
![](attachments/11939509/11939512.png)
Figure. Amelia Can Respond with Updated BPN
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-12-4_12-30-17.png](attachments/11939509/11939510.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-12-4_12-27-47.png](attachments/11939509/11939511.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-40-6.png](attachments/11939509/11939512.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-38-57.png](attachments/11939509/11939513.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-38-24.png](attachments/11939509/11939514.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-37-41.png](attachments/11939509/11939515.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-34-14.png](attachments/11939509/11939516.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-32-45.png](attachments/11939509/11939517.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-27-43.png](attachments/11939509/11939518.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-8_14-26-39.png](attachments/11939509/11939519.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-26_16-23-33.png](attachments/11939509/28475453.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-27_8-48-55.png](attachments/11939509/28475514.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-27_8-51-0.png](attachments/11939509/28475516.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-13_12-5-0.png](attachments/11939509/28476316.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-13_12-5-43.png](attachments/11939509/28476317.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-13_14-22-41.png](attachments/11939509/28476328.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-12-13_14-23-10.png](attachments/11939509/28476329.png) (image/png)  
