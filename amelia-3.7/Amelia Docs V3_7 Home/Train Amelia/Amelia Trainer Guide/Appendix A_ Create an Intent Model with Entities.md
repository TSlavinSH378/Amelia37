Intent models help steer conversations with Amelia towards the best BPN process to address the needs of the conversation. An intent model helps Amelia understand and make reasonable judgements about context in the words and phrases of a conversation, for example, to book a hotel room. Models are created with the Intents, Entities, and Annotate functionality in the Amelia Trainer section of Amelia's administration pages.
Once an intent helps Amelia choose the best BPN process to complete a conversation, entities help Amelia capture data she needs to perform any tasks.
This demonstration shows how to create an intent and entities needed to create, train, and deploy reasoning models Amelia can use to answer questions about transferring money between countries.
1.  Create an intent
2.  Create entities
3.  Annotate utterances with the intent and entities
4.  Train and test an intent model
5.  Deploy the intent model
6.  Create a BPN and update the intent
7.  Test the intent, entities, intent model, and BPN
# Create an Intent
Intents connect specific user phrases with responses from Amelia to confirm entities or call a BPN. In Amelia V2, intents were called goal grammars.
Intents define user goals and intents, often with a reference to expected data and utterances required to meet the goal. For example, to retrieve a copy of a hotel bill, an intent might include the utterance, "I lost my hotel bill. Can you send me a copy?"
In Amelia V3, as in V2, intents can be collected in a tab-separated value (TSV) classifier file with the intent name(s) in one column and utterances to their right in a second column. However, in V3 these files cannot include negative utterances or FAQs. Importing these TSV files adds each intent with all their utterances.
Intents are defined two ways, as standalone items with utterances and as a tool to annotate chat transcripts and other data. Amelia uses both sets of intent data to create a representational model to converse with people and perform specific tasks.
## Intents Workspace
Intents are added and modified with Amelia's administration pages, in the Amelia Trainer section and Intents links. The Intents workspace lists current intents with the ability to search, add, upload, edit, or delete them.
![](attachments/11939699/11939747.jpg)
Figure. Intents Workspace
Table. Intents Workspace Elements
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Search Intents</td>
<td class="confluenceTd">Above the list of intents, type the first few characters of an intent name, BPN, or FAQ to filter the list of intent names displayed below. Then click the intent name to display its details.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd">Intent Tool Tabs</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Add Intents Tab</td>
<td class="confluenceTd"><p>Click the New Intent tab on the right edge to display the New Intent panel. To add an intent, type the name and short description of a new intent and click the Add button. The new intent appears in the list of intents. To activate the new intent, click the intent name to display the intent edit page. Click the Activate this Intent toggle directly under the intent name to make the intent available for use in annotation and BPNs.</p>
<p>The New Intent panel also can be used to upload multiple intents defined in a TSV file.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Train Tab</td>
<td class="confluenceTd">Click to display the widget to train models for intent classifiers, entity taggers, role entity classifiers, or spanless entity classifiers.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Predict Tab</td>
<td class="confluenceTd"><p>Click the Predict tab on the right edge to display the Predict Panel. Select an intent model then type an utterance to test whether or not the intent is triggered by the utterance. Intent models are created and deployed with the Annotate workspace.</p>
<p>The Amelia Trainer section, of Amelia's administration pages, also includes a link to the Predict workspace which offers more granular prediction tests.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Predict All Tab</td>
<td class="confluenceTd"><p>Type a user utterance then click the Predict button to display any intent, entity, or model triggered by the utterance.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Actions</td>
<td class="confluenceTd">Each intent can be edited, deleted, or bulk edited. Click the pencil icon to edit, the X icon to delete, and the checkbox to include the intent in a bulk edit.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Bulk Action Dropdown</td>
<td class="confluenceTd">For bulk edits, once intents are selected, click the Bulk Actions dropdown at the bottom right of the workspace to Delete Selected, Export Selected, or export all intents whether selected or not.</td>
</tr>
</tbody>
</table>
## Create an Intent
For this demonstration, uploading a tab-separated value (TSV) file creates an intent with multiple utterances. The Description and question Amelia asks if the person wants to continue to transfer money are added after import.
The transfer_money_abroad intent is created by importing the [intents-payment_money_abroad-trimmed.txt](attachments/11939699/11939717.txt) file. The ideal number of utterances depends on the conversation and tasks Amelia must complete. The variables ${country} and ${continent} in the TSV file are matched by Amelia with any country or continent name.
To import this file to create an intent, from the Intents workspace, click the Add Intents tab on the right edge of the workspace then click the Browse link in the Upload Intents section. When importing is done, use the workspace search to find then select the new intent.
On the Intent Settings form, click the Add a description... text under the intent name and enter a description. Press the Save changes button at the top right to save.
Click the text underneath the asks... heading and type a question Amelia will ask if the person wants to continue with their intent to transfer money.
![](attachments/11939699/11939745.png)
Figure. Edit Intent Form after Uploading
Table. Intent Edit Form Elements
|                                               |                                                                                                                                                                                                                                                                     |
|----------------------|--------------------------------------------------|
| Element                                       | Description                                                                                                                                                                                                                                                         |
| **Actions**                                   |                                                                                                                                                                                                                                                                     |
| Save Changes                                  | When a change is made, this button becomes active. Click to save changes to the intent.                                                                                                                                                                             |
| Revert Changes                                | When a change is saved, this button becomes active. Click to revert previous saved changes.                                                                                                                                                                         |
| Enable/Disable Intent                         | Intents are enabled by default. When button is Disable intent, click to disable and remove the intent for use by Amelia. When button is Enable intent, click to enable and make the intent available for use by Amelia                                              |
| Delete                                        | Click to delete the intent.                                                                                                                                                                                                                                         |
| **Intent Workspace**                          |                                                                                                                                                                                                                                                                     |
| Add a description...                          | Click the text then type a description for the intent. Click the Save changes button to save.                                                                                                                                                                       |
| When intent is identified...                  | Intents by default are linked to a Business Process Network (BPN). Execute Process is selected by default. Answer FAQ is the second option.                                                                                                                         |
| Execute the process.                          | If Execute Process is selected for When intent is identified dropdown setting, select a previously created BPN process to connect to the intent.                                                                                                                    |
| On switching to a new intent, this becomes... | If Execute Process is selected for When intent is identified dropdown setting, select what happens when Amelia switches to a new intent based on the conversation. The intent is either suspended or completed. Suspended is default. Complete is the other option. |
| When resuming this intent, Amelia...          | If Execute Process is selected for When intent is identified dropdown setting, select whether or not Amelia should respond automatically when resuming this intent. Automatically is default. Other options are Never and Always.                                   |
| asks...                                       | If Execute Process is selected for When intent is identified dropdown setting, click to type Amelia's question when the intent is resumed.                                                                                                                          |
| The user wants to...                          | Click to type a short phrase to describe user intent.                                                                                                                                                                                                               |
| Intent keywords and phrases...                | Click to add keywords, phrases, or tags to describe the intent.                                                                                                                                                                                                     |
| **User Says Workspace**                       |                                                                                                                                                                                                                                                                     |
| Add an example utterance for this intent...   | Click to type an example utterance that triggers this intent.                                                                                                                                                                                                       |
| See all / Collapse                            | Click to toggle between a default view of first five utterances and a paginated view of all utterances.                                                                                                                                                             |
| Use intent grammar...                         | Click to select a previously saved intent grammar to connect with the intent.                                                                                                                                                                                       |
# Create Entities
Entities are defined two ways, as standalone items and as a tool to annotate chat transcripts and other data. Amelia uses both sets of entity data to create a representational model to converse with people and perform specific tasks.
## Entity Workspace
The entity workspace includes the ability to define and add entities, as well as search and edit existing entities.
![](attachments/11939699/11939744.jpg)
Figure. Entity Workspace
Table. Entities Workspace Elements
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 83%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Entity Tool Tabs</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">Add Entities Tab</td>
<td class="confluenceTd"><p>Click the Add Entities tab on the right edge to display the Add Entities panel. To add an entity, type the name, code, datum type, and description of a new entity and click the Add button. The new entity appears in the list of entities. To edit the new entity, click the entity name to display the entity edit page.</p>
<p>The Add Entities panel also can upload multiple entities defined in a TSV file with the ability to Merge, Overwrite, or Add uploaded entities to existing entities.</p>
<p>The Import from Grammars button, when clicked, imports all entities defined in all grammars uploaded in the current domain.</p>
<div class="table-wrap">
<pre class="table"><code>| Field | Description |
| ----|----|
| Name | Name of the entity |
| Code | A unique identifier used to refer to the entity. Alphanumeric with no spaces and underlines allowed. A code test 1 generates an error while test_1 will not generate an error. |
| Datum Type | Entities also have defined data types, or datum. These are tools to extract input values from natural language inputs. Datums are pre-built entities to handle common concepts. Each datum also has a normalizer to interpret the input string identified from a conversation, create a datum type of the selected entity type, and extract meaningful data and assign the data to the datum object. For example, a user response &quot;two hundred thirty two kgs&quot; is saved as 232 kilograms in the Weight Datum type.Detailed information about datum types is in Appendix C: Datum Types. |
| Description | A short description of the entity |
| Spanless Entity | Spanless entities are not directly extracted from a span of text. Instead, they have a fixed number of possible values predicted from the utterance as a whole. See Spanless and Role Entity Types section below for detailed information. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Train Tab</td>
<td class="confluenceTd"><p>Click to display the widget to train models for intent classifiers, entity taggers, role entity classifiers, or spanless entity classifiers.</p>
<div class="table-wrap">
<pre class="table"><code>| Model Type | Description |
| ----|----|
| Intent Classifiers | Train a machine learning model to analyze an end user utterance and detect a specific intent (intent class) or no intent (the negative class) using one of several classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Entity Taggers | Train a machine learning model to extract needed values from within an end user utterance and store it in an entity object using one of several machine learning algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Role Entity Classifiers | Train a machine learning model to extract two or more needed values of the same datum type from an end user utterance and store them accurately in one of several entity objects using a parent-children entity structure and one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Spanless Entity Classifiers | Train a machine learning model to analyze an end user utterance and detect a specific class (spanless entity class) or no class (the negative class) and store that class in an entity object using one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Predict Tab</td>
<td class="confluenceTd"><p>Click the Predict tab on the right edge to display the Predict Panel. Select an entity model then type an utterance to test whether or not the entity is triggered by the utterance. Entity models are created and deployed with the Annotate workspace.</p>
<p>The Amelia Trainer section, of Amelia's administration pages, also includes a link to the Predict workspace which offers more granular prediction tests.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Predict All Tab</td>
<td class="confluenceTd"><p>Type a user utterance then click the Predict button to display any intent, entity, or model triggered by the utterance.</p></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Entity Workspace</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Search Entities</td>
<td class="confluenceTd">Above the list of entities, type the first few characters of an entity name, BPN, or FAQ to filter the list of entity names displayed below. Then click the entity name to display its details.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Actions</td>
<td class="confluenceTd">Each entity can be edited or deleted. Click the pencil icon to edit, the X icon to delete, and the checkbox to include the entity in a bulk delete or edit.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Action Dropdown</td>
<td class="confluenceTd">For bulk edits, once entities are selected, click the Actions dropdown to Delete Selected or Export Selected. This dropdown also can export all entities whether selected or not.</td>
</tr>
</tbody>
</table>
## Create an Entity
The Add Entity Form includes the ability to add entities one by one or uploading one or more entities defined in a text file. Creating individual entities can be done on Amelia's V3 administration site. In this demonstration, the entities country_transfer_from and country_transfer_to will be children to a parent entity country_transfer. This helps Amelia understand the two entities are related.
For this demonstration, repeat these steps to create two entities, *country_transfer_from* and *country_transfer_to* with a parent entity *country_transfer*.
1.  Click the Amelia Trainer link on the left side of the main administration page. Then click the Entities link to display the Entities workspace.
2.  To add a parent entity *country_transfer*, click the Add Entities tab on the right edge of the workspace. In the Add Entities page, type the Name, Code, and Datum Type. Confirm the Domain is correct at the top left of the page, next to the logo.
3.  Click the Add button to save the new entity. The Entity Settings page appears, as shown below.
4.  For each child entity, *country_transfer_from* and *country_transfer_to*, click the Add Entities tab and type the Name, Code, and Datum Type for each new entity. Click the Add button to save.
5.  On the Entities page, for each child entity, click the name or Pencil icon to display its Entity Settings page. Click to select the Role Entity slider. To assign a parent entity, select *Country Transfer* as the Parent Entity.
6.  In the bottom left side of the form, type one or more questions for Amelia to say when asking for the entity then click the Add button.
7.  Click the Save button on the Entity Settings page to save each child entity.
8.  Click the Entities link on the left side to display the Entities workspace. Use the search box to find *country \_transfer*, the parent entity, and click its name or Pencil icon to view its Entity Settings page. Confirm the two child entities appear as Role Names in the center of the page.
![](attachments/11939699/11939741.png)
Figure. Add Parent Entity
![](attachments/11939699/11939742.png)
Figure. Create a Child Entity and Specify Parent Role
![](attachments/11939699/11939743.png)
Figure. Entity Overview for Parent Entity (Role Name Values Appear After Assignment)
# Annotate Documents
With intents and entities defined, the next step is to use the Annotate workspace to create representational models for Amelia to use in conversations. This process uses entities and intents as well as chats and other data imported into the Annotate workspace. Data to import includes free flowing chat conversations, chat transcripts, and negative utterances.
The Amelia Trainer link on the left side of the Amelia V3 administration pages when clicked displays links to create intents, entities, and annotate data.
## Annotate Workspace
The Annotation Framework workspace contains all the tools needed to load, annotate, train, and export models that help Amelia to understand conversation.
The workspace includes a progress bar to track past, current, and future steps in the annotation process with tool tabs on the far right edge and a central area that changes based on the activity.
![](attachments/11939699/11939739.jpg)
Figure. Annotate Workspace
Table. Annotation Workspace Elements
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 88%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Progress Bar</td>
<td class="confluenceTd">Displays current active step in the annotation process with the ability to click and jump to past and future steps.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Annotate Tool Tabs</td>
<td class="confluenceTd"><p>Each tab displays a sliding panel information and tools for different steps in the annotation process. To close a panel, click the x in the top right of the panel.</p>
<div class="table-wrap">
<pre class="table"><code>| Tab Name | Description |
| ----|----|
| Load | Buttons to load existing data from Amelia, a new file, or conversations not processed. |
| Annotate | Select options to automatically annotate utterances, for example, datum type, model type, and whether or not to include named entities. An intent or entity model also can be selected to optimize the auto-annotation process. |
| Train | Choose the type of model to train, define the model, then train the model. |
| Queue | Display any models currently in the process of training. |
| Export | Buttons to export intent models or entity models. |
| Chart | Display charts to show the number of intent and entity annotations. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Workspace</td>
<td class="confluenceTd">When a conversation or other file is imported, the content displays on the left side of the Annotate workspace. As content is annotated, words and phrases in the source content are highlighted.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Load New</td>
<td class="confluenceTd"><p>Select file type then drop a file on the center of the workspace or click the center area to browse and upload a file.</p>
<div class="table-wrap">
<pre class="table"><code>| File Type | Description |
| ----|----|
| Plain Text | Unformatted text with a single sentence or utterance per line. |
| User-Agent Dialog | A user-agent dialog with a single utterance per line. The start of each line should indicate the speaker.Agent: How can I help you today?John: I need a car insurance quote. |
| Annotated Document | Annotated JSON document exported from Amelia. |
| TSV | A tab-separated intents or entities file used for import and export. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Load Existing</td>
<td class="confluenceTd">Select from a list of all files currently loaded in Amelia. Click to select a file then click the Load Selected File button to load the data for the annotation step.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Learn</td>
<td class="confluenceTd"><p>Click the Learn tab to display a workspace with a configurable number of recent conversations. Conversations from the prior 1-9 days and a maximum of 1-9 conversations can be set. Click the Load Utterances button to load matching conversations. Click an entry to display the utterances.</p>
<p>To select individual conversations, toggle the All checkbox above the list of conversations to deselect and select. Conversations available are ones Amelia is unable to answer. Click the Learn tab to select conversations from Amelia's modules, for example, Process Memory, Episodic Memory, and Semantic Memory, as well as conversations where she did not an answer or engaged in chit chat. Click the Learn Utterances button to transfer the conversation to the Annotate workspace.</p>
<p>With one or more conversations selected, click the Learn Utterances button to load the conversations into the Annotate step workspace.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Skip, go to annotate</td>
<td class="confluenceTd">Click this button if returning to the Annotate page from the Load/Learn page.</td>
</tr>
</tbody>
</table>
## Annotate a Conversation
The annotation process includes steps to Import then annotate documents manually or automatically.
### Import
This demonstration uses a modified set of questions removed from the utterances used to train the intent, [intents-annotate-chat.txt](attachments/11939699/11939711.txt). The intent name and tab from the intent utterance TSV file have been replaced with *User:* and a space.
1.  Click the Amelia Trainer link then click the Annotate link to display the Annotate workspace.
2.  On the left side of the Annotate workspace, select Plain Text then click the Browse button in the center of the workspace. The File Explorer popup appears.
3.  Navigate to the [intents-annotate-chat.txt](attachments/11939699/11939711.txt) file to upload, select the file, then click the Open button at the bottom right of the File Explorer popup. The text will appear in the Annotate workspace.
### Manual Annotation
Importing a document will display the Annotate workspace with the document to be annotated. The Save As at the top right of the workspace saves an annotated document with the file name typed to the left of the button. Documents also can be downloaded and deleted with icons near the Save As icon.
To annotate intents, move the mouse under the Intent column of the workspace and a plus sign appears. Click then select the intent to connect with an utterance.
To annotate entities, highlight words and phrases then select the entity name from a dropdown list that appears. Entity names and values appear on the right side of the workspace, under the Entities column.
![](attachments/11939699/11939736.png)
Figure. Manually Annotate a Document
# Train and Test an Intent Model
With a document annotated with an intent and entities, the next steps are to train an intent model then do a quick test using the intent prediction tool.
> [!info]  
>
> For this demonstration, an entity model is not needed. Entity models are created to help Amelia understand the context around phrases that yield the data she needs to complete a BPN process. To give a simplistic example, the phrase "my favorite color is" could yield multiple answers. If Amelia understands how this phrase leads to the user specifying a color, she can grab the word that follows and use it within the BPN.

## Train an Intent Model
1.  Click the Train tab on the right edge of the Annotate workspace. Select Intent Classifier from the Select Type dropdown list. Type a name for an intent classifier model in the Create new model field, for example, *transfer_money*. Click the Create a new model button to save.
2.  Define the Datasets to include to train the model. If needed, click the Datasets heading.
    1.  Click to disable the Include all intents slider.
    2.  Select the transfer_money_abroad intent from the Intents dropdown list.
    3.  Select the file name for the annotated chat from the Training datasets dropdown list. It should be the first item in the list.
3.  Define the Algorithm to include to train the model. If needed, click the Algorithm heading. Select Passive Aggressive Classifier as the Model Type.
4.  Click the Train button at the top of the Train tab panel. Click the Queue tab on the right edge of the Annotate workspace to see if the model is training.
## Test an Intent Model
Intent and entity classifier models can be tested to learn how Amelia connects utterances to models, entities, and intents. The Intents and Entities workspaces include a Predict tab on the right edge of their workspaces. There also is a Predict workspace for more detailed tests with deployed models, available in the Amelia Trainer links in the administration pages.
### Predict Tabs
Both the Intents and Entities workspaces include a Predict tab on the right edge to test how different utterances trigger the correct intent or entity.
To perform a quick test of the intent model, from the Annotate workspace click the Intents link at the top right to display the Intents workspace. Then click the Predict tab on the right edge of the Intents workspace. Select the intent model created above, type a question related to the topic of transferring money abroad, then click the Predict button to see what Intent Amelia connects to your question.
Type questions different from the utterances used to train the model. For example, utterances might use different countries and synonyms for send. If Peru and Hong Kong are not used in the training document, typing "can I post money from Hong Kong to Peru" should show the *transfer_money_abroa*d intent model is activated by this utterance.
![](attachments/11939699/11939734.png)
Figure. Predict Tab Panel in Intents Workspace
### Predict Workspace
Once a classifier model is deployed, as described below, the Predict workspace is available to test utterances. Click the Predict link on the left side of Amelia's administration pages, under the Amelia Trainer links, to display the Predict workspace. Type the same question, Can I post money from Hong Kong to Peru?, and click the Predict button. In the screen shot below, Amelia connected the question to the correct intent, *transfer_money_abroad*, the correct intent model, *transfer_money*, and the link to the BPN process connected to the intent, *doMoneyTransfer*, also is correct.
![](attachments/11939699/11939735.png)
Figure. Predict Workspace to Test Intent Models
A look at the intent utterance file [intents-payment_money_abroad-trimmed.txt](attachments/11939699/11939717.txt) shows the verb *post* is not present. Instead, Amelia extends the concepts of send, transfer, and other synonyms to post, as well as picks up the concepts of from and to.
# Deploy an Intent Model
The Amelia Trainer Dashboard workspace displays all active and inactive trained intent and entity classifier models. This includes system models, for example, datum types for US English numbers and quantity.
Once a few simple tests with the Intents workspace indicate the intent model works reasonably well, the next step is to deploy the intent model so a BPN process can be created to be triggered by the intent model and capture the *country_from* and *country_to* entities.
Trained classifier models appear in the Dashboard workspace available by clicking the Amelia Trainer link in the Amelia administration pages then clicking the Dashboard link. The Dashboard workspace appears with a list of available trained models. A yellow ready text and circle indicate models ready to be deployed. A green deployed text and circle indicate models currently deployed by Amelia to respond to people.
In the Dashboard workspace, an up arrow icon in the Actions column indicates a model is ready to deploy and, when clicked, deploys the model. In the Actions column, the circled down arrow icon undeploys a model when clicked while clicking the x icon deletes a model.
To deploy the transfer_money model, click the circled up arrow in the actions column. The yellow ready text changes to green deployed text.
Figure. Amelia Trainer Dashboard Workspace
> [!info]  
>
> While not relevant to this demonstration, clicking the Logs, Stats, and Training Data icons to the right of a model displays useful information about the performance of a specific model. The data can be used to optimize a model through a series of changes to intents, entities, utterances, annotated documents, and other elements used to train intent and entity models.

# Create a BPN
The BPN process directs Amelia's actions and responses as she completes a task. For this demonstration, a BPN titled *doMoneyTransfer* will help Amelia collect basic information about what country the person wants to send money from and where they want to send money.
![](attachments/11939699/11939751.png)
Figure. doMoneyTransfer BPN Model
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doMoneyTransfer. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create doMoneyTransfer Process

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say I can help you transfer money | Let the user know the correct BPN workflow has started and initialize Amelia |
| 2 | ask for the slot country_transfer_from | Click the task and select the Properties Panel tab on the right edge of the workspaceSelect a question previously defined for this entity in the Question setting dropdownFor this demonstration, also set the Ask behavior (1st pass) and Ask behavior (subsequent) settings to Ignore if responded |
| 3 | set the variable cty_from to ${ctx:latestSlot('country_transfer_from').value()} |  |
| 4 | ask for the slot country_transfer_to | Click the task and select the Properties Panel tab on the right edge of the workspaceSelect a question previously defined for this entity in the Question setting dropdownFor this demonstration, also set the Ask behavior (1st pass) and Ask behavior (subsequent) settings to Ignore if responded |
| 5 | set the variable cty_to to ${ctx:latestSlot('country_transfer_to').value()} |  |
| 6 | say you want to send money from ${cty_from} to ${cty_to} | Display user inputs |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
# Test Intent, Entities, Intent Model, and BPN
The final step in this demonstration is to engage Amelia in different conversations to see how well she uses the intent, entites, intent model, and BPN model to answer queries.
When the BPN model is built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the right edge of the Mind panel.
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Type an opening statement or question that may or may not result in Amelia answering with the doMoneyTransfer BPN model. Instead of asking if you can transfer money from one country to another, ask questions designed to test her reasoning abilities, for example, "I'm in Canada. I'd like to post money to Peru" or "Can I post money" or similar. Then provide answers to test her ability to identify countries.  
    ![](attachments/11939699/11939732.png)  
    Figure. Amelia User Interface with Mind View and Process Memory
> [!warning]  
>
> How Amelia responds depends on a variety of factors. For example, if this demonstration is the only data set in a domain, chances are high Amelia will pick the correct BPN process. However, a domain with many potentially conflicting BPN processes, entities, intents, and other data may yield different results. A successful implementation of Amelia depends on careful planning as much as the data used to train her.

## Attachments:
![](images/icons/bullet_blue.gif) [image2017-11-20_12-26-12.png](attachments/11939699/11939700.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-20_12-19-54.png](attachments/11939699/11939701.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-20_12-17-13.png](attachments/11939699/11939702.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-20_9-58-59.png](attachments/11939699/11939703.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-58-52.png](attachments/11939699/11939704.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-52-17.png](attachments/11939699/11939705.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-51-5.png](attachments/11939699/11939706.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-train-intent-transfer-money.jpg](attachments/11939699/11939707.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-45-41.png](attachments/11939699/11939708.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-42-20.png](attachments/11939699/11939709.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-41-26.png](attachments/11939699/11939710.png) (image/png)  
![](images/icons/bullet_blue.gif) [intents-annotate-chat.txt](attachments/11939699/11939711.txt) (text/plain)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-27-17.png](attachments/11939699/11939712.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-26-14.png](attachments/11939699/11939713.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-23-32.png](attachments/11939699/11939714.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-17-55.png](attachments/11939699/11939715.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-17_15-16-1.png](attachments/11939699/11939716.png) (image/png)  
![](images/icons/bullet_blue.gif) [intents-payment_money_abroad-trimmed.txt](attachments/11939699/11939717.txt) (text/plain)  
![](images/icons/bullet_blue.gif) [image2017-11-17_13-57-28.png](attachments/11939699/11939718.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-6_13-6-9.png](attachments/11939699/11939719.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-workspace-transfer-money.jpg](attachments/11939699/11939720.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-27-38.png](attachments/11939699/11939721.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-28-45.png](attachments/11939699/11939722.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-33-32.png](attachments/11939699/11939723.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-6_13-14-11.png](attachments/11939699/11939724.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-6_13-0-37.png](attachments/11939699/11939725.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-12_12-33-7.png](attachments/11939699/11939726.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-12_12-29-7.png](attachments/11939699/11939727.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-workspace-2.jpg](attachments/11939699/11939728.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-1-12_11-22-17.png](attachments/11939699/11939729.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-12_11-21-11.png](attachments/11939699/11939730.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-11_10-32-44.png](attachments/11939699/11939731.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-26_10-28-48.png](attachments/11939699/11939732.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-dashboard-workspace-app-a-3.4.10.jpg](attachments/11939699/11939733.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-9-25_16-56-36.png](attachments/11939699/11939734.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-25_16-51-3.png](attachments/11939699/11939735.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-25_16-24-55.png](attachments/11939699/11939736.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-25_16-21-43.png](attachments/11939699/11939737.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-25_16-20-56.png](attachments/11939699/11939738.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-workspace-3.5.9.jpg](attachments/11939699/11939739.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia-v3-aiml-workspace-3.4.9.jpg](attachments/11939699/11939740.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-9-25_15-34-20.png](attachments/11939699/11939741.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-25_15-29-57.png](attachments/11939699/11939742.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-25_15-28-41.png](attachments/11939699/11939743.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-entities-workspace-3.6.jpg](attachments/11939699/11939744.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-9-25_14-45-29.png](attachments/11939699/11939745.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-25_14-42-11.png](attachments/11939699/11939746.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-intents-workspace-3.5.7.jpg](attachments/11939699/11939747.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-1-12_11-11-53.png](attachments/11939699/11939748.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-entity-workspace-2.jpg](attachments/11939699/11939749.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia-v3-intent-workspace-2.jpg](attachments/11939699/11939750.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2017-11-20_13-7-55.png](attachments/11939699/11939751.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-20_12-29-49.png](attachments/11939699/11939752.png) (image/png)  
