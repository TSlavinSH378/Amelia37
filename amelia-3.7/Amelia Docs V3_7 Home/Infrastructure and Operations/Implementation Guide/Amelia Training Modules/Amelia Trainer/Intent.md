{% version "3.x" %}
Intents define user goals and intents, often with a reference to expected data and utterances required to meet the goal. For example, to retrieve a copy of a hotel bill, an intent might include the utterance, "I lost my hotel bill. Can you send me a copy?"
Intents connect specific user phrases with responses from Amelia to confirm entities or call a BPN.
Intents can be collected in a tab-separated value (TSV) classifier file with the intent name(s) in one column and utterances to their right in a second column. However, these files cannot include negative utterances or FAQs. Importing these TSV files adds each intent with all their utterances.
Intents are defined two ways, as standalone items with utterances and as a tool to annotate chat transcripts and other data. Amelia uses both sets of intent data to create a representational model to converse with people and perform specific tasks.
> [!warning]  
>
> For optimal results, there should only be one intent model active and deployed for one domain.
>
> Intent models also should not be created in the global domain. The global domain has access to intent models, intents, and other elements in child domains.

# Intents Workspaces
Intents are added and modified with Amelia's administration pages, in the Amelia Trainer section and Intents inks. The default Intents workspace lists current intents with the ability to search, add, upload, edit, or delete them. The intent tool tabs are described in the table below.
![](attachments/11939566/25461436.jpg)
Figure. Intents Workspace
Table. Intents Workspace Elements
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 13%" />
<col style="width: 86%" />
</colgroup>
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
<td colspan="2" class="confluenceTd"><strong>Intent Tool Tabs</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Add Intents Tab</td>
<td class="confluenceTd"><p>Click the New Intent tab on the right edge to display the New Intent panel. To add an intent, type the name and short description of a new intent and click the Add button. The new intent appears in the list of intents. To activate the new intent, click the intent name to display the intent edit page. Click the Activate this Intent toggle directly under the intent name to make the intent available for use in annotation and BPNs.</p>
<p>The New Intent panel also can be used to upload multiple intents defined in a TSV file.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Train Tab</td>
<td class="confluenceTd"><p>To train a model, select the model type then select either an existing model or create a new model. Training configuration options appear based on model type selected. Define the training options as needed then click the Train button to train with the options. Click the Deploy button to deploy the model.</p>
<p>See <a href="https://docs.amelia.com/display/AmeliaDocsV37/Annotate#Annotate-TrainTabPanel">Train Step Workspace section</a> for details about configuration settings for each model type.</p>
<div class="table-wrap">
<pre class="table"><code>| Model Type | Description |
| ----|----|
| Intent Classifier | Train a machine learning model to analyze an end user utterance and detect a specific intent (intent class) or no intent (the negative class) using one of several classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Entity Taggers | Train a machine learning model to extract needed values from within an end user utterance and store it in an entity object using one of several machine learning algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Role Entity Classifiers | Train a machine learning model to extract two or more needed values of the same datum type from an end user utterance and store them accurately in one of several entity objects using a parent-children entity structure and one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Spanless Entity Classifiers | Train a machine learning model to analyze an end user utterance and detect a specific class (spanless entity class) or no class (the negative class) and store that class in an entity object using one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Domain Classifier | Train a machine learning model to identify the domain of the request from a user&#39;s utterance. |
| Intent Detector | Train a machine learning model to detect whether or not the user&#39;s utterance contains an intent. |</code></pre>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Predict Tab</td>
<td class="confluenceTd"><p>Click the Predict tab on the right edge to display the Predict Panel. Select an intent model then type an utterance to test whether or not the intent is triggered by the utterance. Intent models are created and deployed with the Annotate workspace.</p>
<p>The Amelia Trainer section, of Amelia's administration pages, also includes a link to the Predict workspace which offers more granular prediction tests.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Actions</td>
<td class="confluenceTd">Each intent can be edited, deleted, or bulk edited. Click the pencil icon to edit, the X icon to delete, and the checkbox to include the intent in a bulk edit.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Bulk Action Dropdown</td>
<td class="confluenceTd">For bulk edits, once intents are selected, click the Bulk Actions dropdown at the bottom right of the workspace to Delete Selected, Export Selected, or export all intents whether selected or not.</td>
</tr>
</tbody>
</table>
# Create an Intent
In the Intents workspace, click the Add Intents tab on the right edge to display the Add Intents panel. Type the name and short description of a new intent and click the Add Intent button. The new intent appears in the list of intents. Click the pencil icon to the right of the new intent name to edit the intent in the Intent Settings form, as shown below. In the Add Intents panel, also click the X in top right of the panel to close.
![](attachments/11939566/25461437.png)
Figure. Intent Edit Form
Table. Intent Edit Form Elements
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 30%" />
<col style="width: 69%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Element</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd"><strong>Actions</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">Save Changes</td>
<td class="confluenceTd">When a change is made, this button becomes active. Click to save changes to the intent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Revert Changes</td>
<td class="confluenceTd">When a change is saved, this button becomes active. Click to revert previous saved changes.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Active/Inactive</td>
<td class="confluenceTd">Intents are enabled by default. When button is Disable intent, click to disable and remove the intent for use by Amelia. When button is Enable intent, click to enable and make the intent available for use by Amelia</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Delete</td>
<td class="confluenceTd">Click to delete the intent.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Intent Workspace</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Add a description...</td>
<td class="confluenceTd">Click the text then type a description for the intent. Click the Save changes button to save.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Scoped entities</td>
<td class="confluenceTd">Select one or more entities that should be scoped to this intent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">When intent is identified...</td>
<td class="confluenceTd"><p>Intents by default are linked to a Business Process Network (BPN). Execute Process is selected by default. Answer FAQ is the second option.</p>
<ul>
<li>Execute Process intents are connected to a BPN process and captured through a conversation with Amelia.</li>
<li>Answer FAQ intents are questions and answers Amelia stores to respond to common questions.</li>
</ul></td>
</tr>
<tr class="even">
<td class="confluenceTd">Execute the process...</td>
<td class="confluenceTd">If Execute Process is selected for When intent is identified dropdown setting, select a previously created BPN process to connect to the intent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">When returning to the root context after this intent, execute the process...</td>
<td class="confluenceTd">Displays for Execute Process and Answer FAQ are selected for the When intent is identified... setting. Select a BPN process to execute when returning </td>
</tr>
<tr class="even">
<td class="confluenceTd">On switching to a new intent, this becomes...</td>
<td class="confluenceTd">If Execute Process is selected for When intent is identified dropdown setting, select what happens when Amelia switches to a new intent based on the conversation. The intent is either suspended or completed. Suspended is default. Complete is the other option.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">When resuming this intent, Amelia...</td>
<td class="confluenceTd">If Execute Process is selected for When intent is identified dropdown setting, select whether or not Amelia should respond automatically when resuming this intent. Automatically is default. Other options are Never and Always.</td>
</tr>
<tr class="even">
<td class="confluenceTd">asks...</td>
<td class="confluenceTd">If Execute Process is selected for When intent is identified dropdown setting, click to type Amelia's question when the intent is resumed.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">When cancelling this intent, Amelia...</td>
<td class="confluenceTd">Displays when Execute Process is selected for the When intent is identified... setting. Select how to cancel this intent. Options are Automatically, Never, and Always. Automatically is the default. </td>
</tr>
<tr class="even">
<td class="confluenceTd">asks...</td>
<td class="confluenceTd">Displays when Execute Process is selected for the When intent is identified... setting. Click to type Amelia's response if the intent is cancelled.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">When the utterance triggering this intent is negated (e.g. Do not set an alarm)...</td>
<td class="confluenceTd">Displays for Execute Process and Answer FAQ are selected for the When intent is identified... setting. Select how to proceed. Options are Ignore Intent, Proceed as usual, and Execute alternative intent. Default is Proceed as usual</td>
</tr>
<tr class="even">
<td class="confluenceTd">The user wants to...</td>
<td class="confluenceTd">Displays for Execute Process and Answer FAQ are selected for the When intent is identified... setting. Click to type a short phrase to describe user intent.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Intent keywords and phrases...</td>
<td class="confluenceTd"><p>Displays for Execute Process and Answer FAQ are selected for the When intent is identified... setting. Click to add keywords, phrases, or tags to describe the intent. Keywords and phrases are displayed in decreasing order of importance.</p>
<p>Keywords and phrases can be created manually or automatically. Automatic creation happens during model training as part of the Clarifying Question Asker (CQA) module. This module allows Amelia to ask questions to clarify ambiguous utterances. For example, if a person asks, "I want to open an account," Amelia could clarify by asking if they want to open a savings account or a checking account. See the <a href="https://docs.amelia.com/display/AmeliaDocsV37/Appendix+F%3A+Clarifying+Question+Asker">Clarifying Question Asker</a> appendix for details.</p></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>User Says Workspace</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Add an example utterance for this intent...</td>
<td class="confluenceTd">Displays for Execute Process and Answer FAQ are selected for the When intent is identified... setting. Click to type an example utterance that triggers this intent.</td>
</tr>
<tr class="even">
<td class="confluenceTd">See all / Collapse</td>
<td class="confluenceTd">Displays for Execute Process and Answer FAQ are selected for the When intent is identified... setting. Click to toggle between a default view of first five utterances and a paginated view of all utterances.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Use intent grammar...</td>
<td class="confluenceTd">Displays for Execute Process and Answer FAQ are selected for the When intent is identified... setting. Click to select a previously saved intent grammar to connect with the intent.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Amelia Says</td>
<td class="confluenceTd">Displays when Answer FAQ is selected for the When intent is identified... setting. Click the text field to add an example utterance for this intent.</td>
</tr>
</tbody>
</table>
# Edit an Intent
The Intents workspace lists all active and inactive intents. Click the pencil icon to the right of an intent name in the Intent workspace. The edit form will appear. For details about the edit form, see Intent Edit Form Elements table, in the Create an Intent section above.
The intent edit form can add utterances, delete utterances, enable or disable the intent, and other tasks.
-   To add an utterance, type in the User Says input field above the list of classifier utterances. Press the Enter key to save the utterance to the bottom of the list.
-   To delete an utterance, click the checkbox to the left of an utterance in the User Says panel. The Delete button below becomes active. Click the Delete button.
-   To edit an utterance, click the utterance then type changes inline. Click the Save changes button at top right of workspace to save changes.
-   To bulk delete utterances, click the check box to the left of each utterance then click the Delete button that appears at the bottom of the page.
-   To make the intent active and available to Amelia, click the Active/Inactive Intent toggle at the top right of the form. If the Active intent button is visible, the intent is active and available for use.
-   To select how the intent is to be used, click the Execute Process or Answer FAQ from the dropdown list at the top left of classifier utterances, in the When intent is identified dropdown list. Selecting a BPN from the Execute the process... dropdown list connects the utterances to a BPN when training Amelia. If the intent is triggered, the BPN will be triggered. The Answer FAQ option displays an Amelia Says field at the bottom of the page for Amelia's answer to question utterances added to the intent.
-   To specify how the intent behaves if a conversation causes Amelia to switch to another intent, click the On switching to a new intent, this intent becomes... dropdown list and select the behavior, Suspended or Complete. Then click the When resuming this intent, Amelia... dropdown and select Always, Automatically, or Never. Finally, if appropriate, click the text field under the asks.. heading and type a question for Amelia to ask to continue working with this intent.
-   To add keywords and phrases in addition to utterances, click the text field under the Intent keywords and phrases... heading then enter data.
-   To connect this intent to an intent grammar, at the bottom of the Intent Settings workspace click the dropdown list under the Use intent grammar... heading and select a previously created intent grammar.
-   To connect one or more entities to an intent, select them from the Scoped entities... dropdown list at the top of the workspace.
Click the Save changes at the top right of the Intents workspace to save any changes.
# Delete an Intent
The Intents workspace lists all active and inactive intents. Click the X to the right of an intent name in the Intent workspace. In addition, in the Intent Settings workspace, to delete an intent, click the Delete button at the top right of the intent edit form.
# Upload Intents
In addition to manually creating intents one by one, multiple intents can be created in a file then uploaded into the Intents workspace. File upload of intents can include numerous utterances with each intent instead of manually entering utterances in the intent edit form.
Two types of intents can be uploaded:
-   Execute Process intents are connected to a BPN process and captured through a conversation with Amelia.
-   Answer FAQ intents are questions and answers Amelia stores to respond to common questions.
The intent edit form defines the type of intent.
Intent files must be in tab separated value (TSV) format and less than two megabytes in size. The file formats are shown below.
> [!warning]  
>
> While the Execute Process intent type can include HTML in Amelia's answers, the Answer FAQ intent type cannot include HTML.

## Create Intent Files
Uploading a file with intents include intent name, example utterances, and other data in a tab-separated (TSV) file format.
> [!warning]  
>
> The first two commented lines in the code below define two BPNs, *thisIsAnIntentFAQ* and *thisIsAnIntent*, to associate and execute with each intent, *thisisanintentfaq* and *thisisanintent*, as well as the structure to define elements of the Intents Settings form. Each element is separated by a tab in the order specified. And each commented header entry starts and ends with a \# (pound) sign.
>
> In this example, each intent also includes example utterances which should trigger the intent.

**Sample Intents File in TSV Format**
``` bash
# thisIsAnIntentFAQ   thisisanintentfaq   ANSWER_FAQ  null    null    null    This is an alternative answer the FAQ|||This is the answer to the FAQ   ACTIVE  null    {"keyPhrases":[],"keyPhraseCreatorType":"MANUAL","actionPhrase":"This is a description"}  AUTOMATIC   SUSPEND null    AUTOMATIC   null    null    IGNORE  null    #
#   thisIsAnIntent  thisisanintent  EXECUTE_BPN bpn process name    description of this intent  Amelia asks when resuming   null    ACTIVE  activeb {"keyPhrases":[],"keyPhraseCreatorType":"MANUAL","actionPhrase":"The user wants to action"}   AUTOMATIC   SUSPEND Amelia asks when cancelling AUTOMATIC   return process to execute   null    IGNORE  null    #
thisisanintentfaq   This is another question for an FAQ?
thisisanintentfaq   This is a question for an FAQ?
thisisanintent  This is an intent utterance
thisisanintent  This is another intent utterance
```
The commented lines of the header in the file define the intents in some detail, as described in the table below. The position of elements in the header determine which part of the intent edit workspace are populated. The tabs also act as delimiters, eliminating the need for single or double quotes for values in most cases.
Table. Sample Intents File Header Structure

| Position | Element or Example Value | Location in Intent Settings Page | Description |
| ----|----|----|----|
| 1 | intent name | Top left of the Intent Settings page | Name of the intent |
| 2 | intent code |  | Code used in the first column of the TSV file |
| 3 | intent type | When intent is identified... | EXECUTE_BPN or ANSWER_FAQ |
| 4 | execute process | Execute the process... | Name of the BPN process to execute when intent is identified |
| 5 | intent description | Under the intent name | A short description of the intent |
| 6 | Would you like to resume this intent? | asks... | What Amelia asks when resuming this intent |
| 7 | faq answers | Amelia Says | If intent type is ANSWER_FAQ, one or more answers to the FAQ with each answer separated by three pipe (|||) characters.If intent type is EXECUTE_BPN, the value must be null. |
| 8 | intent status | Top right of the Intent Settings page | ACTIVE or INACTIVE. The Active or Inactive button at the top right of the Intent Settings page |
| 9 | grammar name | Use intent grammar... | Optional grammar name if the grammar exists. Otherwise, the value must be null. |
| 10 | "keyPhrases":["test","another test"] | Intent keywords and phrases | Values are empty angle brackets [] by default. Any values use double quotes and comma separated. |
| 11 | "keyPhraseCreatorType":"MANUAL" |  | MANUAL or AUTOMATIC |
| 12 | "actionPhrase":"perform a test" | The user wants to... | What the user wants to do with the intent. |
| 13 | ALWAYS | When resuming this intent, Amelia... | If intent type is EXECUTE_BPN, ALWAYS, NEVER, or AUTOMATICALLY. Otherwise, the value must be null. |
| 14 | COMPLETE | On switching to a new intent, this intent becomes... | If intent type is EXECUTE_BPN, COMPLETE or SUSPENDED. Otherwise, the value must be null. |
| 15 | Would you like to cancel? | asks... | If intent type is EXECUTE_BPN, what Amelia asks when cancelling this intent. Otherwise this value must be null. |
| 16 | NEVER | When cancelling this intent, Amelia... | If intent type is EXECUTE_BPN, ALWAYS, NEVER, or AUTOMATICALLY. Otherwise, the value must be null. |
| 17 | null | When returning to the root context after this intent, execute the process... | Name of the BPN process to execute when returning to the root context after this intent is completed. |
| 18 | scoped entities | Scoped entities... | One or more entities by title |
| 19 | CONTINUE | When the utterance triggering this intent is negated (e.g. 'Do not set an alarm')... | CONTINUE maps to Proceed as usualIGNORE maps to Ignore intent
ALTERNATIVE_INTENT maps to Execute alternative intent |
| 20 | alternative process | Use intent | Appears only if ALTERNATIVE_INTENT is selected in position 19. Otherwise the value must be null. |

## Upload Intent Files
To upload an intent file, click the Add Intents tab on the right edge to display the New Intent panel. Click the Add dropdown and select what to do with any duplicate files, Merge with existing file(s), Overwrite existing file(s), or Add to existing intents. Then drag an intent file to the upload area on the panel or click the Browse button to navigate to the intents file. Click the X at top right of the panel to close the tab.
> [!info]  
>
> Intent files upload automatically once selected. DO NOT click the Import from Grammars button. That button imports intents from all grammars uploaded to the current domain.

![](attachments/11939566/11939567.png)
Figure. Add Intents Tab Panel with Upload Options
Table. Add Intents Tab Panel Elements
|                         |                                                                                                                                                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Element                 | Description                                                                                                                                                                             |
| **Add Intents**         |                                                                                                                                                                                         |
| Enter an intent name    | Type the name for a new intent                                                                                                                                                          |
| Add a description       | Type a short description for a new intent                                                                                                                                               |
| Add Intent              | Click to add a new intent to the current domain. The new intent appears in the default Intents workspace. Find and configure the new intent.                                            |
| **Upload Intents**      |                                                                                                                                                                                         |
| Merge                   | Select how to handle uploaded intents that are duplicates of existing intents in the current domain                                                                                     |
| Drag and Drop or Browse | Either drag an intent file to upload or click the Browse link and use the File Manager popup to find a file. Once selected or dropped on the panel, the file will upload automatically. |
| Import from Grammars    | Click to import intents from all grammars uploaded to the current domain.                                                                                                               |
To upload intents, click the Upload Intent tab on the right edge of the Intent page. If intents are connected to a BPN, the import file format is defined above. For Answer FAQs, intents are questions instead of statements with a third column to define the intent name to create. In both cases, intent files to upload must be in tab separated value (TSV) format and less than two megabytes in size.
# Test Intents and Intent Models
Amelia provides two ways to test intents and intent models, both available through the Amelia Trainer workspaces.
Use the Predict tab on the right side of the Intents workspace to test an intent model, intents, and utterances. In the Predict panel, select the intent model, type an utterance, and then click the Predict button to see which intent is triggered. The triggered intent name displays below.
The Dashboard workspace also includes a Stats button to the right of each model name with detailed information about misclassifications, confusion matrix, and other details useful to tune models.
# Manage Intents in the Process Knowledge Workspace
While intents are primarily managed in the Intents workspace, available as part of the Amelia Trainer link on the left side of Amelia's administration pages, intents also can be managed while working with BPN process models.
BPN models are available by clicking the Process Memory link, located on the left side of Amelia's administration pages. Then click Process Knowledge and select a BPN model to edit. The Intents popup link is to the right of the Import and Export links at the top of the BPN workspace.
![](attachments/11939566/25461435.jpg)
Figure. Intents Popup Link in a BPN Workspace
Click the Intents link to display the Intents popup. The Add Intents, Train, and Predict buttons at the top of the Intents popup behave the same way as the Add Intents, Train, and Predict tabs in the Intents workspace, as described above.
![](attachments/11939566/11939575.png)
Figure. Intents Popup in a BPN Workspace
# Intent Best Practices
Creation of effective intents depends on several factors.
-   Do not create an intent model in the Global domain, the parent domain for all other domains. The Global domain has access to intent models in child domains.
-   Minimize confusion creating an intent model by working with small amounts of data and building the model in multiple steps. Start with one intent and the negative data set to create a model. Add a second intent with negatives to the model, for a total of two intents and the negative data for these intents. Train the model, check accuracy statistics in the Amelia Trainer Dashboard, revise the training data, and repeat. This process cleans the first intent data set and negative data set before adding new intents and negatives.
-   Varied sentence structures and word choices are more important than the number of sentences. Begin with fewer utterances then build iteratively. 50 to 100 examples per intent works best. More than 100 examples are not needed unless there is a high variation of expression in user intent.
-   Combine intents that are ambiguous and disambiguate in the BPN.
-   Thoughtful negative examples are very important.
-   Use descriptive class names. Be consistent in the use of camelCase or snake_case notation.
-   For best results, use live chat examples to test the intent model. Use test utterances as close as possible to what people would say to trigger the model and process. Consider extreme programming techniques, for example, one person creates utterances to train the model while a second person creates utterances to test the model.
-   If overmatching happens with an intent, add similar sentence structures and word choices in the negative class that would not trigger the intent model.
{% /version %}
