-   [Annotation Framework Workspace](#Annotate-AnnotationFrameworkWorkspace)
-   [Annotate a Conversation](#Annotate-AnnotateaConversation)
    -   [Load/Learn Step Workspace](#Annotate-Load/LearnStepWorkspace)
    -   [Annotate Step Workspace](#Annotate-AnnotateStepWorkspace)
    -   [Train Step Workspace](#Annotate-TrainStepWorkspace)
    -   [Simplified Entity Annotation for Text File Import](#Annotate-SimplifiedEntityAnnotationforTextFileImport)
-   [Negative Utterances](#Annotate-NegativeUtterances)
-   [Export to TSV Format](#Annotate-ExporttoTSVFormatExportUtterancesTSV)
-   [Misclassifications](#Annotate-Misclassifications)
    -   [Requirements](#Annotate-Requirements)
    -   [Tag Misclassified Utterances](#Annotate-TagMisclassifiedUtterances)
    -   [Edit Misclassified Utterances](#Annotate-EditMisclassifiedUtterances)
With intents and entities defined, the next step is to use the Annotate workspace to create representational models for Amelia to use in conversations. This process uses entities and intents as well as chats and other data imported into the Annotate workspace. Data to import includes free flowing chat conversations, chat transcripts, and negative utterances.
The Amelia Trainer link on the left side of the Amelia V3 administration pages when clicked displays links to create intents, entities, and annotate data.
# Annotation Framework Workspace
The Annotation Framework workspace contains all the tools needed to load, annotate, train, and export models that help Amelia to understand conversation.
The workspace includes a progress bar to track past, current, and future steps in the annotation process with tool tabs on the far right edge and a central area that changes based on the activity.
![](attachments/11939620/25461532.jpg)
Figure. Annotation Framework Workspace
Table. Annotation Framework Workspace Elements
<table class="wrapped relative-table confluenceTable" style="width: 100.0%;">
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
| Export | Buttons to export intent models or entity models. |</code></pre>
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
<td class="confluenceTd">Misclassifications</td>
<td class="confluenceTd">This tab provides tools to correct Amelia's intent predictions within conversations. See the Misclassifications section below for details.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Skip, go to annotate</td>
<td class="confluenceTd">Click this button if returning to the Annotate page from the Load/Learn page.</td>
</tr>
</tbody>
</table>
# Annotate a Conversation
Matching intents and entities to words and phrases in a transcript then building a model from the annotated transcript provides Amelia with a mental model she uses to make sense of utterances as she talks with people. The model helps her pick the correct process to follow and collect data from people.
## Load/Learn Step Workspace
Click the Amelia Trainer link then click the Annotate link to display the Annotation Framework workspace on the right side of the screen. The default workspace is the Load/Learn step which includes three options to load conversation and other data for annotation.
> [!warning]  
>
> All text files must be in UTF-8 format to handle special characters correctly.

Table. Load/Learn Workspace Elements
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Load New</td>
<td class="confluenceTd"><p>Select file type then drop a file on the center of the workspace or click the center area to browse and upload a file.</p>
<div class="table-wrap">
<pre class="table"><code>| File Type | Description |
| ----|----|
| Plain Text | Unformatted text with a single sentence or utterance per line. |
| Annotated Document | Annotated JSON document exported from Amelia. |
| TSV | A tab-separated intents or entities file used for import and export. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Load Existing</td>
<td class="confluenceTd">Select from a list of all files currently loaded in Amelia. Click to select a file then click the Load Selected File button to load the data for the annotation step.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Learn</td>
<td class="confluenceTd"><p>Click the Learn tab to display a workspace with a configurable number of recent conversations. Conversations from the prior 1-9 days and a maximum of 1-9 conversations can be set. Click the Load Utterances button to load matching conversations. Click an entry to display the utterances.</p>
<p>To select individual conversations, toggle the All checkbox above the list of conversations to deselect and select. Conversations available are ones Amelia is unable to answer. Click the Learn tab to select conversations from Amelia's modules, for example, Process Memory, Episodic Memory, and Semantic Memory, as well as conversations where she did not an answer or engaged in chit chat. Click the Learn Utterances button to transfer the conversation to the Annotate workspace.</p>
<p>With one or more conversations selected, click the Learn Utterances button to load the conversations into the Annotate step workspace.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Misclassifications</td>
<td class="confluenceTd"><p>Click the Misclassifications tab to view intent predictions that have not been marked thumbs up or thumbs down in the NLU Settings tab of the Dashboard workspace.</p>
<p>User must have the AUTHORITY_MISCLASSIFICATION_ANNOTATION assigned to their user account.</p></td>
</tr>
</tbody>
</table>
## Annotate Step Workspace
Once data is imported into the Annotation Framework page with the Load/Learn step, the data appears in the Annotate step workspace. When a conversation or other file is imported, the content displays on the left side of the Annotate workspace. As content is annotated, words and phrases in the source content are highlighted.
-   To tag data with an entity, highlight the word or phrase and select the entity name from a dropdown that appears.
-   To assign an intent to a line of data, click the Intents column to the right of the data then click the +Add Intent text that appears. Select the intent name from the dropdown list of intents that appears. For Episodic Memory models, intent names must be preceded by epm and a space, click on the intent tag area and add epm and a single space in front of a new intent name.
Intents and entities can be created during the tagging process by typing in a new name into the dropdown list that appears and pressing the Enter key.
![](attachments/11939620/25461546.jpg)
Figure. Annotate Step Workspace
Table. Annotate Step Workspace Elements

| Element | Description |
| ----|----|
| Search | Typing a word or phrase filters the data loaded into the workspace, for example, to refine annotations for specific entries. |
| Auto Annotate | This button at the center top of the workspace triggers a basic automatic annotation processing of workspace data with no options.To auto annotate with options, click the Annotate tab on the right edge of the workspace to select datum types and models to use for automatic annotation. There are several options:Include all intents and entities – select intents and entities in the current domain to be included during auto-annotation. Uses all available deployed models and applies extraction results from custom entities.
Datum types – select any built-in entities to be included in auto-annotation.
Include Named Entities – convert (or not) named entities to their generic form, for example, "Can I wire money to France?" converted to "Can I wire money to COUNTRY?" which matches COUNTRY to any country name.
Intent model – select a specific intent model to use for auto-annotation.
Entity model – select a specific entity model to use for auto-annotation. |
| Train | This button at the center top of the workspace opens the Train tab panel on the right edge of the workspace. |
| Delete | Clear all data from the Annotate workspace. |
| Download | Download the data from the Annotate workspace in JSON or TSV file format. |
| Save | Save the data in the Amelia instance. File names for annotated files must be less than 45 characters in length. |
| Tag Outputs | The Intents and Entities columns display the results of manual and auto annotation. Tags are for manual and automatic annotation based on existing entities and intents, as well as datum types, for example, People and Location. Colors are assigned arbitrarily. Click the x in a tag to delete it. |

## Train Step Workspace
Clicking the Train step in the progress bar in the Annotation Framework workspace opens the Train tab on the right edge of the workspace. Intent, Entity, and Episodic Memory models can be configured and training started with the Train tab.
![](attachments/11939620/11939626.png)
Figure. Train Models Tab
Table. Train Models Tab Elements
|                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------|----------------------------------------------------------|
| Element                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Select Type**             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Intent Classifiers          | Train a machine learning model to analyze an end user utterance and detect a specific intent (intent class) or no intent (the negative class) using one of several classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model.                                                                                          |
| Entity Taggers              | Train a machine learning model to extract needed values from within an end user utterance and store it in an entity object using one of several machine learning algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model.                                                                                                           |
| Role Entity Classifiers     | Train a machine learning model to extract two or more needed values of the same datum type from an end user utterance and store them accurately in one of several entity objects using a parent-children entity structure and one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Spanless Entity Classifiers | Train a machine learning model to analyze an end user utterance and detect a specific class (spanless entity class) or no class (the negative class) and store that class in an entity object using one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model.                           |
| Domain Classifier           | Identify the domain of a request from a user's utterance                                                                                                                                                                                                                                                                                                                                                                                                       |
| Intent Detector             | Classifier used to detect whether or not the user's utterance contains an intent                                                                                                                                                                                                                                                                                                                                                                               |
| **Other Options**           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Select from existing        | Click dropdown list to select and existing model to train.                                                                                                                                                                                                                                                                                                                                                                                                     |
| Create new model            | Type the name of a new model to display a Create a New Model button. Click the button to create a model to train.                                                                                                                                                                                                                                                                                                                                              |
Once an existing model is selected, or a new model created, the Train Models panel displays a workspace to define datasets, evaluation parameters, and algorithm to use.
Click the Datasets, Evaluation, or Algorithm heading to display settings and options. Click the plus ( + ) or minus ( - ) to the right of the model name to toggle display of the model details with the default form to create a model.
![](attachments/11939620/25461547.png)
Figure. Train Models Tab with Intent Classifier Dataset Options
Table. Train Models Tab with Datasets, Evaluation, Algorithm, Metadata Settings
<table class="relative-table wrapped confluenceTable" style="width: 99.9231%;">
<colgroup>
<col style="width: 19%" />
<col style="width: 80%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh" style="width: 19.6923%">Element</th>
<th class="confluenceTh" style="width: 80.2308%">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd" style="width: 19.6923%">Undeploy</td>
<td class="confluenceTd" style="width: 80.2308%">Click to undeploy the model.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 19.6923%">Train</td>
<td class="confluenceTd" style="width: 80.2308%">Click to train the model with its current settings.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd" style="width: 99.9231%"><strong>Datasets</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 19.6923%">Include all intents (or entities)</td>
<td class="confluenceTd" style="width: 80.2308%">Include training examples from all active intents and entities. Disable this option to select specific intents or entities for training.</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 19.6923%">Intents (or entities)</td>
<td class="confluenceTd" style="width: 80.2308%">Click the dropdown list to select one or more intents (or entities, depending on the model type). Selected items display in the dropdown area. Click the x next to an item to delete.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 19.6923%">Training datasets</td>
<td class="confluenceTd" style="width: 80.2308%">Click the dropdown list to select one or more datasets. Selected items display in the dropdown area. Click the x next to an item to delete.</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 19.6923%">Add fallback examples</td>
<td class="confluenceTd" style="width: 80.2308%">For intent models only. Automatically add examples to the training data to help recognize non-intent utterances and avoid false positives. This can be accomplished manually by adding training documents without labels.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd" style="width: 99.9231%"><strong>Evaluation</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 19.6923%">Validation datasets</td>
<td class="confluenceTd" style="width: 80.2308%"><p>Click the dropdown list to select one or more validation datasets. Selected items display in the dropdown area. Click the x next to an item to delete.</p>
<p>Add documents used to evaluate the generalization performance of a model. If none are include, evaluation will be automatically performed on the training data.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 19.6923%">Cross-validation</td>
<td class="confluenceTd" style="width: 80.2308%">Perform cross-validation to estimate the accuracy of a model on new data. Options are None, 3-fold, 5-fold, and 10-fold.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd" style="width: 99.9231%"><strong>Algorithm</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 19.6923%">Classification Algorithm</td>
<td class="confluenceTd" style="width: 80.2308%"><p>Select the type of algorithm to use for training.</p>
<div class="table-wrap">
<pre class="table"><code>| Algorithm | Description |
| ----|----|
| Linear SVM Tagger | Similar to Passive Aggressive but without multi-label classification, maximizes the distances between classes |
| CRF Tagger | For entity tagger models only.; |
| Passive Aggressive Tagger | Allows for multi-label classification, the ability to identify multiple intents in one training example |
| DNN Tagger | For entity and intent detector models only. The Deep Neural Network (DNN) Classifier is used primarily to train models with ELMo (Embeddings from Language Models). With DNN Classifier selected as Model Type, Click the Edit model settings toggle then set the Contextualize inputs dropdown to true.ELMo is a recent approach to representing words for use in NLP machine learning applications. One key difference from previous approaches (like word2vec or GloVe) is that representations for each word are computed dynamically for each sentence. The representations ELMo computes for the word bank will be drastically different in the sentence, “We had a picnic on the river bank” than in the sentence, “I deposited my paycheck at the bank.”Dynamically computing a representation for each word in a sentence can take additional time to train models with the DNN algorithm, depending on the number of words and sentences. |
| Meta Tagger | For intent and entity models only. |
| Logistic Regression | For Role Entity and Spanless entity models only. Produces scores that can be interpreted as probabilities which can be used to create thresholds to control the precision of the classifier |
| Confidence Weighted Classifier | For intent, Role Entity, Spanless Entity, Domain Classifier, and Intent Detector models only.  |
| Soft Confidence Weighted Classifier | For intent, Role Entity, Spanless Entity, Domain Classifier, and Intent Detector models only.  |</code></pre>
</div>
<p>Currently, Passive Aggressive and Linear SVM are recommended with Passive Aggressive generating better results in many cases.</p>
<p>Click to turn on the Use custom features to edit or upload features used to train a model. See <a href="https://docs.ipsoft.com/display/AmeliaDocsV3/Appendix+B%3A+Feature+Extraction">Feature Extraction</a> for more details.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 19.6923%">Classifier Settings</td>
<td class="confluenceTd" style="width: 80.2308%"><p>Default settings are recommended. Therefore, model hyperparameters should be modified only by advanced users.</p>
<div class="table-wrap">
<pre class="table"><code>| Parameter | Description |
| ----|----|
| Patience | Maximum number of epochs to continue training with no improvement on validation data. Default is 30. Options are 5, 10, 15, 20, 25, 30. |
| C | Controls aggressiveness of updates. Lower values limit size of connections. Default is 0.0025. Options are 25, 2.5, 0.25, 0.025, 0.0025, 0.00025. |
| Averaging | Use weighted average of parameters across epochs. This may improve generalization, but can sometimes lead to mistakes on training data. Default is true. Options are true, false. |
| Calibrate confidence scores | Calibrate scores of this model to produce valid probabilities as outputs. No calibration is the default. Options are Softmax, Platt, No calibration. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 19.6923%">Train out-of-domain classifier</td>
<td class="confluenceTd" style="width: 80.2308%">For intent models only. Train a separate classifier to detect out-of-domain utterances. All negative examples in original training data will be removed from the intent classifier and used to train the out-of-domain classifier. This classifier will need to be deployed separately and will have the same name as the intent classifier, for example, intents and intents.000.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Extract key phrases</td>
<td class="confluenceTd">For intent models only. Automatically extract keywords and phrases for each intent during training to help distinguish between them and for use as descriptions.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Use Entity Features</td>
<td class="confluenceTd">For intent models only. Select a list of entities, automatically extract them as features for training an intent classifier. These features are helpful to capture out-of-vocabulary words.</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 19.6923%">Use Dictionary Features</td>
<td class="confluenceTd" style="width: 80.2308%"><div class="content-wrapper">
<p>For intent and entity models only. Select a list of lookup tables with input/output mappings to automatically add to feature extraction.</p>
<p><strong>Resources</strong> – Select a lookup table from the dropdown list<br />
<strong>Input Column</strong> – For the selected lookup table, choose a data input source<br />
<strong>Output Column</strong> – For the selected lookup table, choose a data output source</p>
<p>When a resource and input/output columns are selected, click the Add button to add the dictionary features.</p>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 19.6923%">Enable feature editor</td>
<td class="confluenceTd" style="width: 80.2308%"><p>For intent, entity, and domain models only. Toggle displays only for intent, Entity Tagger, Spanless Entity Classifier models. When enabled, displays the Open feature editor button. Click the Open feature editor button to display the Feature Editor. The feature editor allows editing and testing of features.</p>
<p>When disabled, default features are used or a custom feature XML file can be uploaded with the Upload feature template are that appears below.</p>
<p>See <a href="https://docs.ipsoft.com/display/AmeliaDocsV3/Appendix+B%3A+Feature+Extraction">Feature Extraction</a> for more details.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Upload Feature Template</td>
<td class="confluenceTd">Click Browse to use File Explorer to find and upload a feature template file or drag and drop a feature template file on to the square.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd" style="width: 99.9231%"><strong>Metadata</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 19.6923%">Revision Name</td>
<td class="confluenceTd" style="width: 80.2308%"><p>Name for the revision of the classifier. Can be used for tagging changes between versions.</p></td>
</tr>
</tbody>
</table>
## Simplified Entity Annotation for Text File Import
Files uploaded to annotate entities with the Load workspace can include annotation, thus removing the need to manually tag utterances with the Annotate Step workspace. Files must be in tab-separated (TSV) format. Each row in the file is an utterance then a tab then one or more entity_names; in the utterance, entity examples are wrapped in curly braces with one entity example for each entity_name value. The entity_name values must be in the same order as the entity examples.
``` groovy
I want to check in {tomorrow} and check out on {Tuesday}.<TAB>checkInDate, checkOutDate
I need a {Wednesday} checkout<TAB>checkOutDate
```
# Negative Utterances
Adding negative utterances to Amelia repeats some of the annotation steps – Load and Train – without annotating the file. The utterances are stored in a file with one line per utterance. Once imported, negative utterance files can be included to train one or more files.
Negative utterances are statements similar to what people say when they want to perform a task but clearly not part of a class or group. For example, the utterance, “I used to have an AOL account with a tricky password,” is about passwords but not about forgetting a password. When Amelia builds her conceptual model, negative utterances help her identify irrelevant words and phrases, as well as help rate some words and phrases more or less than others.
**Sample V3 Negative Utterances File**
``` bash
A brand new taxi is pulling up now , sir
A broken chain lies at her feet
A button came off my shirt
A couple , but I ’m not sure if I want to go as something scary or something funny
A couple of months ago
A dozen will be fine
A flea market is a big outdoor place where you can buy all sorts of second-hand things
```
# Export to TSV Format
Utterances used for annotation can be exported in tab-separated value (TSV) format from the Annotate workspace. Click the Amelia Trainer link on the left side of Amelia’s administration pages then click Annotate. The Annotate workspace appears. Select a file with the 1. Load/Learn workspace. The 2. Annotate workspace will appear. Next to the file name under the step navigation links click the download icon to display the TSV export format option.
![](attachments/11939620/11941808.png)
Figure. Export Utterances in TSV Format
The ability to export in TSV format allows non-technical people to work with utterances then import them back into Amelia with the 1. Load/Learn workspace.
# Misclassifications
The Misclassifications tab provides tools to correct Amelia's intent predictions within conversations. Tagging utterances with the correct domain and intent helps train Amelia to identify and understand a broader range of utterances she might encounter.
## Requirements
-   To view and use this functionality, the user must have the AUTHORITY_MISCLASSIFICATION_ANNOTATION authority assigned to their account.
-   The Enable Intent Correction setting must be activated. The setting is part of the NLU Settings tab on the right edge of the Dashboard workspace in the Amelia Trainer section. If needed, configure the Intent Correction Threshold setting used to trigger this functionality. The default is 0.7.
-   Tagging of utterances happens in the default User workspace available by clicking the navigation links at the top right of Amelia's administration pages.
## Tag Misclassified Utterances
When Amelia predicts an intent match score for an utterance lower than the Intent Correction Threshold setting will display ![](attachments/11939620/25462331.png) icons under each user utterance. Click the ![](attachments/11939620/25462332.png) icon to confirm the intent match is correct. The icon turns green when selected and the utterance is added to the intent training data set. Click the ![](attachments/11939620/25462333.png) icon to flag the intent match is incorrect. The icon turns red when selected.
Clicking the ![](attachments/11939620/25462334.png) icon displays a popup above the icon to select a domain. When a domain is selected, a second dropdown appears to select the correct intent. If an utterance is assigned to a domain and intent, the utterance will be added to the intent training data set.
![](attachments/11939620/25462336.png)
Figure. Select Correct Domain and Intent for an Incorrect Intent Match
When one or more utterances are tagged with the ![](attachments/11939620/25462351.png) icon but not assigned to a domain or intent, they are added to a list of misclassified utterances.
Click the ![](attachments/11939620/25462337.png) icon at the bottom right of the conversation message box to close the conversation. A Close Conversation popup will appear. Click the Auto-deploy learnt knowledge check box in the popup then click the green Yes button to save changes.
## Edit Misclassified Utterances
With utterances tagged, navigate to Amelia's administration pages and click the Amelia Trainer link on the left side then click the Annotate link that appears. The Annotate workspace will appear with the Load/Learn tab selected. Click the Misclassifications tab in the Load/Learn tab workspace to view tagged entries.
![](attachments/11939620/25462338.png)
Figure. Misclassifications Workspace with Tagged Entries
For each entry, select the correct domain and intent from the two dropdown lists. When an intent is selected, a popup will appear to confirm the domain and intent selections. Click the OK button to close the confirmation popup.
To delete a tagged entry, click the checkbox to the left of an entry then click the Delete button at the top right of the Misclassifications tab workspace.  
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-11-20_10-33-21.png](attachments/11939620/11939621.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-20_10-22-28.png](attachments/11939620/11939622.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-20_10-0-34.png](attachments/11939620/11939623.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-20_9-58-2.png](attachments/11939620/11939624.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-20_14-40-52.png](attachments/11939620/11939625.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-20_13-6-43.png](attachments/11939620/11939626.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-workspace-3.5.9.jpg](attachments/11939620/11939627.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-9-14_17-6-33.png](attachments/11939620/11939628.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_12-12-8.png](attachments/11939620/11939629.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_12-8-50.png](attachments/11939620/11939630.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-46-17.png](attachments/11939620/11939631.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-43-4.png](attachments/11939620/11939632.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-31-42.png](attachments/11939620/11939633.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-30-4.png](attachments/11939620/11939634.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-27-19.png](attachments/11939620/11939635.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-23-59.png](attachments/11939620/11939636.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-13-59.png](attachments/11939620/11939637.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-9-34.png](attachments/11939620/11939638.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-3-38.png](attachments/11939620/11939639.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_11-1-59.png](attachments/11939620/11939640.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-step-3.4.2.jpg](attachments/11939620/11939641.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-workspace-3.4.2.jpg](attachments/11939620/11939642.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-1-24_11-46-14.png](attachments/11939620/11939643.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-24_11-45-47.png](attachments/11939620/11939644.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-11_14-12-7.png](attachments/11939620/11939645.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-11_13-4-28.png](attachments/11939620/11939646.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-11_13-2-59.png](attachments/11939620/11939647.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-workspace-2.jpg](attachments/11939620/11939648.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-27-38.png](attachments/11939620/11939649.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-28-45.png](attachments/11939620/11939650.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-33-32.png](attachments/11939620/11939651.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-34-24.png](attachments/11939620/11939652.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-38-7.png](attachments/11939620/11939653.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-39-19.png](attachments/11939620/11939654.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-8_10-40-9.png](attachments/11939620/11939655.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-11-29_13-37-6.png](attachments/11939620/11939656.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-6_13-14-11.png](attachments/11939620/11939657.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-2-7_16-55-48.png](attachments/11939620/11941808.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-workspace-3.7.38.jpg](attachments/11939620/25461532.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia-v3-annotate-step-3.7.38.jpg](attachments/11939620/25461546.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2019-10-3_13-12-7.png](attachments/11939620/25461547.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-3_13-56-23.png](attachments/11939620/25461548.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-1-0.png](attachments/11939620/25462331.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-3-48.png](attachments/11939620/25462332.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-4-17.png](attachments/11939620/25462333.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-4-31.png](attachments/11939620/25462334.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-7-10.png](attachments/11939620/25462335.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-12-3.png](attachments/11939620/25462336.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-14-5.png](attachments/11939620/25462337.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-19-8.png](attachments/11939620/25462338.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-30_17-30-56.png](attachments/11939620/25462351.png) (image/png)  
