Amelia can direct a conversation to different domains in real time based on utterances. Each utterance is evaluated by a processor that detects the correct domain to handle the utterance. When a new domain is detected, Amelia completes or suspends the existing context and sends an outbound domain change message to the session. This outbound message leads to a change in the domain handling the conversation.
For example, a parent domain handles HR requests. It has two child domains, one to handle user accounts and a second domain to handle PTO balance requests. A conversation with the utterance, "I'm locked out of my computer," would be processed by the parent HR domain classifier model and routed to the child domain that handles user accounts. Later in the same conversation, if the person says, "show me my pto balance," the parent HR domain classifier model would evaluate this utterance and route the conversation to the child domain that handles PTO balance requests.
Configuring Amelia to handle domain switches requires creating parent/child domains, training models, and configuring settings in the application.
-   Create at least three domains, one parent and two child domains
-   Configure each domain to allow switching in and out of each domain
-   Train intent models for each child domain
-   Train a domain model for the parent domain
-   Configure the NLU setting to trigger domain CQA
-   Configure Ask BPN tasks to allow domain switches
These steps are described in detail below.
# Create Domains
Before domains are created, go through a design process to confirm the scope of the parent and their child domains. Refer to the [Intent Recognition Guide](Intent%20Recognition%20Guide) for help defining scope for domains and intents. At least three domains should be created, a parent domain and two child domains.
Domains are created in Amelia's administration pages by clicking the System Settings link on the left side then clicking the Domains link to display the Domains workspace.
1.  To create a domain, click the New Domain button at the top right of the Domains workspace. The New Domain form will appear.
2.  If creating a child domain, scroll down the New Domain form to find the Basics panel and the Parent Domain dropdown list. Select the parent domain.  
    ![](attachments/28476266/28476290.png)  
    Figure. Parent Domain Dropdown  
3.  Scroll down the form to find the Domain Switching panel. Select Allow Switch In and Allow Switch Out settings.  
    ![](attachments/28476266/28476289.png)  
    Figure. Domain Switching Panel  
4.  Refer to the [Domains](Domains) page in the Administration Guide for details about the rest of the New Domain form.
5.  Click the Save button at the top right of the form to save the domain definition.
# Train Intent Models in Child Domains
An intent model must be created for each child domain. Each model must be able to process utterances and capture intent with minimum ambiguity.
Intent models are created in Amelia's administration pages by clicking the Amelia Trainer link on the left side then clicking the Dashboard link to display the Dashboard workspace. Then click the Train tab on the right edge of the Dashboard workspace. The Train tab panel appears on the right.
![](https://docs.ipsoft.com/download/attachments/11939658/amelia-v3-dashboard-workspace-3.7.40.jpg)
Figure. Dashboard Workspace
Next, click the Select model type to train dropdown and select Intent Classifier. Then type the model name in the Or create a new model text field.
![](attachments/28476266/28476291.png)
Figure. Train Tab Panel
Click the Save button that appears to create the new model. The Train tab panel will display configuration settings to train a model.
Refer to the [Intents List](Intents%20List), [Annotate](Annotate), [Dashboard](Dashboard), and [Clarifying Question Asker (CQA)](Appendix%20F_%20Clarifying%20Question%20Asker) pages for details about creating intents and training intent models.
# Train a Domain Model
A domain model is trained on the intent models for each of its child domains. The domain model routes utterances to the appropriate domain.
A domain model is created in Amelia's administration pages by clicking the Amelia Trainer link on the left side then clicking the Dashboard link to display the Dashboard workspace. Then click the Train tab on the right edge of the Dashboard workspace. The Train tab panel appears on the right. 
Select Domain Classifier as model type then type a name for the new model in the Or Create a New Model input field.
Figure. Select Domain Classifier as Model Type
The model definition form appears. In the Datasets section, click the Use All Child Domains switch to activate it.
Figure. Select Use All Child Domains Switch
Training a domain model uses settings the same as the intent models trained for their child domains. Refer to the [Intents List](Intents%20List), [Annotate](Annotate), [Dashboard](Dashboard), and [Clarifying Question Asker (CQA)](Appendix%20F_%20Clarifying%20Question%20Asker) pages for details about creating intents and training intent models.
> [!info]  
>
> By default all intent data from the child domains are used to train the domain classifier model. However, custom data documents can be added with the Training datasets dropdown list.
>
> Entity utterances also can be used to train a domain model by toggling the Use entity utterances setting on.

Once the training model is created, it will be listed in the Dashboard workspace.
# Configure Domain CQA
The Domain CQA (Clarifying Question Asker) settings for a domain help Amelia handle utterances that are similar but different. Amelia evaluates a user utterance, compares the utterance to two intents, and finds ambiguity with the user utterance and the two intents. The clarifying questions helps Amelia decide which intent is satisfied by the utterance. The two domain CQA settings define thresholds Amelia uses as she parses a conversation.
The domain CQA is set in the NLU Settings tab in the Dashboard workspace in Amelia's administration pages. Click the Amelia Trainer link on the left side then click the Dashboard link to display the Dashboard workspace. Then click the NLU Settings tab on the right edge of the Dashboard workspace. The NLU Settings tab panel appears on the right.
Scroll down and click to toggle the Enable domain CQA on. If needed, adjust the values for the Domain ambiguity threshold and CQA domain threshold. Refer to the [Dashboard](Dashboard) and [Clarifying Question Asker (CQA)](Appendix%20F_%20Clarifying%20Question%20Asker) pages for details about CQA.
![](attachments/28476266/28476292.png)
Figure. Enable domain CQA Settings
Table. Enable domain CQA Settings

| Enable Domain CQA | When selected, enable clarifying question asking (CQA) for Domain ambiguity |
| ----|----|
| Domain Ambiguity Threshold | If the difference in scores of the top two domains is less than this value, the input utterance is considered domain ambiguous. 0.6 is the default. |
| CQA Domain Threshold | If the top domain score is less than this value, CQA will be ignored. 0.3 is the default. |

# Configure BPN Ask Tasks
Individual Ask tasks in BPNs used by the child domains can be configured to allow switching domains based on the user response to the task.
Ask tasks are configured in Amelia's administration pages by clicking the Process Memory link on the left side then clicking the Process Knowledge link to display the Processes workspace. BPNs are sorted into folders on the left side of the Processes workspace. Clicking a BPN model displays the model in the right side of the workspace.
Select Ask tasks, as appropriate, then click the Properties Panel tab on the right edge of the Processes workspace. The Properties panel appears. Scroll down to the Allow domain switch setting. Click Yes in the dropdown to allow domain switching.
![](attachments/28476266/28476293.png)
Figure. Allow Domain Switch Setting in BPN Ask Task
# Test Domain Switching
Once Amelia is configured to handle domain switches, test the functionality with distinct utterances for each child domain.
![](attachments/28476266/28476295.png)
Figure. Example Domain Switching Test Utterances
# Domain Switching Impact on Metrics
Domains get scores at the context level because a user can access multiple domains in the same conversation. In addition, a domain name prefix is added to BPNs and intents triggered during a conversation then logged. These can be viewed with Journey Analytics and Metrics summaries in Amelia's administration pages.
If the Transcripts panel on a Domain form has Anonymize User selected, the conversation summary will anonymize user data.
