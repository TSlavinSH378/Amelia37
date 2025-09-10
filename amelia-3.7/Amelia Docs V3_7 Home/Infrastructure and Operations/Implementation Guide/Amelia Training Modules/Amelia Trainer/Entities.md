> [!info]  
>
> Please note this page is a work in progress. Content is likely to change as Amelia V3 evolves and more in-depth documentation becomes available.

Entities capture data from user utterances that Amelia needs to fulfill a user request. Entities are the pieces of data needed to achieve a goal or intent. For example, dates, locations, names, and other data are defined as entities then used by Amelia to capture data and complete a conversation.
Entities are defined two ways, as standalone items and as a tool to annotate chat transcripts and other data. Amelia uses both sets of entity data to create a representational model to converse with people and perform specific tasks.
# Entities Workspace
The Entities workspace includes the ability to define and add entities, as well as search and edit existing entities. A domain can be selected with a dropdown list at the top right of the interface.
![](attachments/11939584/25461268.jpg)
Figure. Entities Workspace
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
<td class="confluenceTd">Search Entities</td>
<td class="confluenceTd">Above the list of entities, type the first few characters of an entity name, BPN, or FAQ to filter the list of entity names displayed below. Then click the entity name to display its details.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd">Entity Tool Tabs</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Add Entities Tab</td>
<td class="confluenceTd"><p>Click the Add Entities tab on the right edge to display the Add Entities panel.</p>
<p>To add an entity, type the name then select the datum type of a new entity.  If a spanless entity, click the Spanless Entity toggle and type a question or prompt in the Question/Prompt field.  Click the Add button to save the new entity. The new entity appears in the list of entities. To edit the new entity, click the entity name or pencil icon to display the entity edit page.</p>
<p>The Add Entities panel also can upload multiple entities defined in a TSV file with the ability to Merge, Overwrite, or Add uploaded entities to existing entities.</p>
<p>The Import from Grammars button, when clicked, imports all entities defined in all grammars uploaded in the current domain.</p>
<div class="table-wrap">
<pre class="table"><code>| Field | Description |
| ----|----|
| Name | Name of the entity |
| Spanless Entity | Spanless entities are not directly extracted from a span of text. Instead, they have a fixed number of possible values predicted from the utterance as a whole. See Spanless and Role Entity Types section below for detailed information. |
| Datum Type | Appears if Spanless Entity is not selected. Entities also have defined data types, or datum. These are tools to extract input values from natural language inputs. Datums are pre-built entities to handle common concepts. Each datum also has a normalizer to interpret the input string identified from a conversation, create a datum type of the selected entity type, and extract meaningful data and assign the data to the datum object. For example, a user response &quot;two hundred thirty two kgs&quot; is saved as 232 kilograms in the Weight Datum type.Detailed information about datum types is in Appendix C: Datum Types. |
| Question Prompt | Appears if Spanless Entity is selected. Amelia asks this question when requesting this entity from a user. More questions can be specified after creating the entity. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Train Tab</td>
<td class="confluenceTd"><p>Click to display the widget to train models for intent classifiers, entity taggers, role entity classifiers, or spanless entity classifiers.</p>
<p>Select a type of model to train then select either an existing model or create a new model. If an existing model is selected, the Train tab panel displays datasets, intents, algorithms, and other details to configure. If creating a new model is selected, type the model name then click the button to create the model. The Train tab panel displays datasets and other details to configure.</p>
<p>See <a href="https://docs.amelia.com/display/AmeliaDocsV37/Annotate#Annotate-TrainTabPanel">Train Step Workspace section</a> for details about configuration settings for each model type.</p>
<div class="table-wrap">
<pre class="table"><code>| Model Type | Description |
| ----|----|
| Intent Classifiers | Train a machine learning model to analyze an end user utterance and detect a specific intent (intent class) or no intent (the negative class) using one of several classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Entity Taggers | Train a machine learning model to extract needed values from within an end user utterance and store it in an entity object using one of several machine learning algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Role Entity Classifiers | Train a machine learning model to extract two or more needed values of the same datum type from an end user utterance and store them accurately in one of several entity objects using a parent-children entity structure and one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Spanless Entity Classifiers | Train a machine learning model to analyze an end user utterance and detect a specific class (spanless entity class) or no class (the negative class) and store that class in an entity object using one of several sentence-level classification algorithms. Can optionally include a validation data set to test the created model. Model hyperparameters can also be modified to support refinement of the machine learning model. |
| Domain Classifier | Train a machine learning model to identify the domain of the request from a user&#39;s utterance. |
| Intent Detector | Train a machine learning model to detect whether or not the user&#39;s utterance contains an intent. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Predict Tab</td>
<td class="confluenceTd"><p>Click the Predict tab on the right edge to display the Predict Panel. Type an utterance to test whether or not the entity is triggered by the utterance.</p>
<p>Click the Advanced Options link to display additional prediction parameters.</p>
<ul>
<li>Select Filter Entity Results to filter prediction results by entity. This can be useful if there are many entities defined in a domain.</li>
<li>Select Prompt Entity to select an entity asked for within a BPN. Entities requested in a BPN may impact the result of tagging, as the question asked by Amelia is used when extracting the entity.</li>
<li>Select Scope Intent to select an intent to use to scope entity extraction.</li>
</ul>
<p>The Amelia Trainer section, of Amelia's administration pages, also includes a link to the Predict workspace which offers more granular prediction tests and results.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Edit | Delete Actions</td>
<td class="confluenceTd">Each entity can be edited or deleted. Click the pencil icon to edit, the X icon to delete, and the checkbox to include the entity in a bulk delete or edit.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Action Dropdown</td>
<td class="confluenceTd">For bulk edits, once entities are selected by clicking the checkbox to the right of each entity, click the Actions dropdown to Delete Selected or Export Selected. This dropdown also can export all entities whether selected or not.</td>
</tr>
</tbody>
</table>
Spanless and Role Entity Types
Entities correspond to either a word or phrase in an utterance, called a span, or they are inferred from a sentence as a whole. For example, for an entity about color, the word red might be a span entity, as in the phrase red Ford Focus. Entities that are inferred are called spanless entities. If someone says, for example, "queen beds two of them" you can infer they want a double hotel room from the utterance.
Entities also sometimes have a connection to other entities, for example, the start date and end date for a hotel booking or the number of bedrooms and bathrooms in a real estate listing. Amelia V3 captures these connections with an entity role classification. A hotel booking might have an entity *hotelDates* with *checkInDate* and *checkOutDate* as child entities identified as role entities and *hotelDates* identified as their parent entity. The parent-child connection only runs one level deep. While any entity can be assigned a parent entity, parent entities cannot be assigned a parent entity and child entities cannot have a child entity.
# Create an Entity
The Add Entity Form includes the ability to add entities one by one or uploading one or more entities defined in a text file.
## Add Single Entities
Creating individual entities can be done on Amelia's V3 administration site.
1.  Click the Amelia Trainer link on the left side of the main administration page. Then click the Entities link to display the Entities workspace.
2.  To add an entity, click the Add Entities tab on the far right of the workspace then type the Name and select a Datum Type.
3.  Click the spanless check box if the entity is spanless, inferred from an utterance instead of a word or phrase found in an utterance. Type a question or prompt in the Question/Prompt field.
4.  Click the Add button to save the new entity. The entity will appear at the bottom of the list of entities in the workspace.
5.  Click the new entity name in the list. The Entity Settings page appears.
6.  Type questions for Amelia to say when asking for the entity then click the Save button at the top right of the Entity Overview page.
If the entity is spanless, add examples at the bottom right of the entity edit page. For example, *Queen bed two of them* as an utterance and *double* as the value. Entries without a value are treated as negative utterances, similar to the entity but to be ignored by Amelia. For example, the utterance, "I am the King of England" is not about a request for king-sized beds.
The Entity Settings workspace displays different fields based on entity type.
### Role Entities
For Role Entities, the Entities Settings page allows a parent entity to be selected and Amelia's utterances to ask for the entity. See below for details about creating Role entities.
![](attachments/11939584/25461272.png)
Figure. Example Role Entity Settings
Table. Role Entity Settings Elements

| Setting | Description |
| ----|----|
| Code | A unique identifier for the entity which can be used elsewhere in the application. Use alphanumeric without spaces. Underscores are allowed. |
| Parent Entity | Name of the entity that relates to this child entity. |
| Edit Parent | Click to edit the parent entity. The workspace switches to display the parent entity in the edit workspace. |
| Amelia Asks | See All link | Click the See All link to display a text field and add questions for Amelia to ask to capture this entity value. |

### Custom Datum Entities
For Custom Datum Entities, the Entity Settings page displays a Custom Entity Settings section. Each dropdown and ? icon provide details about options.
![](attachments/11939584/25461281.png)
Figure. Example Custom Datum Entity Settings
Table. Custom Entity Settings Elements
<table class="wrapped relative-table confluenceTable" style="width: 99.9985%;">
<colgroup>
<col style="width: 12%" />
<col style="width: 87%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh" style="width: 147.0px">Settings</th>
<th class="confluenceTh" style="width: 1217.0px">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Datum Type</td>
<td class="confluenceTd" style="width: 1217.0px">Specifies which built-in entity extractor and normalizer to use for the entity. Custom Datums allow for normalization and extraction with tabular data. Text datums are left unnormalized and extracted by training an entity tagger.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Custom entity type</td>
<td class="confluenceTd" style="width: 1217.0px"><p>Specifies the general entity normalization/extraction approach.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| Tabular Data Lookup | Matching uses a lookup from a table using Tabular Data |
| Grammars | Matching uses context free grammars |
| Lookup Table | Matching uses a lookup from synonym mappings and/or regex specified directly in the entity |</code></pre>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Lookup Strategy</td>
<td class="confluenceTd" style="width: 1217.0px"><p>A lookup strategy is applied to match entries in a given table to spans of text in the user utterance.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| Exact Match | Exact match from a lookup table |
| Regex Matcher | A match based on regular expressions |
| Approximate Matcher | A match using Levenshtein distance approximate matching |</code></pre>
</div></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd" style="width: 1364.0px"><strong>Advanced Options</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Extract/Normalize</td>
<td class="confluenceTd" style="width: 1217.0px"><p>Specifies whether to normalize, extract, or perform both using a normalizer. For example, if using a trained entity tagger, the resulting spans can be normalized when using the Normalize Only option.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| Normalize | Only normalize the entity. Requires training an entity extractor. |
| Normalize and Extract | Extract and normalize results using a normalizer. |
| Extract Only | Use a lookup to extract values but do not perform normalization. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Fallback Strategy</td>
<td class="confluenceTd" style="width: 1217.0px"><p>Provides a default normalized value when an entity is extracted but cannot be normalized.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| None | Don&#39;t extract entities that cannot be normalized. |
| Provided | Use specified input as the fallback normalized value. |
| Original | Use the original un-normalized matched text. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Grammar</td>
<td class="confluenceTd" style="width: 1217.0px">For the Custom entity type of Grammar, select a slot grammar to use to extract/normalize this entity.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Preprocessors</td>
<td class="confluenceTd" style="width: 1217.0px"><div class="content-wrapper">
<p>For the Custom entity type of Tabular Data Lookup, the preprocessors applied both to the user utterance and table entries prior to matching. Lowercase and Normalize Unicode are the default preprocessors.</p>
<blockquote>
<p>[!warning]<br />
</p>
<p>When using the Regex Matcher option for the Lookup Strategy setting, only the user utterance is pre-processed, not table entries.</p>
</blockquote>
<p> </p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Lemmatize Nouns</td>
<td class="confluenceTd" style="width: 1217.0px">Toggle on or off to normalize (lemmatize) nouns to their base forms, for example, in an utterance the word apples becomes apple or strawberries becomes strawberry.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Lookup Table Entries</td>
<td class="confluenceTd" style="width: 1217.0px"><p>Create a set of mappings from user inputs to normalized outputs</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Normalized Output</td>
<td class="confluenceTd" style="width: 1217.0px">The value produced when the input given to the right of this column is extracted</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Inputs</td>
<td class="confluenceTd" style="width: 1217.0px">Input text or regular expressions of user's text mapping to normalized output</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">+ Add an Entry</td>
<td class="confluenceTd" style="width: 1217.0px">Click to add a row with Normalized Output and Inputs</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 147.0px">Delete Entries</td>
<td class="confluenceTd" style="width: 1217.0px">To delete lookup table entries, click the check box to the left of an entry then click this button. To delete all lookup table entries, click the check box to the left of this button to select all entries then click this button to delete them.</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 147.0px">Amelia Asks | See All link</td>
<td class="confluenceTd" style="width: 1217.0px">Click the See All link to display a text field and add questions for Amelia to ask to capture this entity value</td>
</tr>
</tbody>
</table>
### Spanless Entities
For Spanless Entities, the Entities Settings page displays a User Says section where examples of user utterances can be mapped to a value that can be used in a BPN process flow. For example, for a hotel reservation, there are many ways to ask for a single or double room. Mapping utterances to the values *single* or *double* helps Amelia translate utterances to an entity value.
Utterances used for spanless entities can be exported in tab-separated value (TSV) format, as well as deleted in bulk. The list of utterances at the bottom right of an entity workspace, in the User Says area, also includes the ability to filter dynamically all utterances with a word or phrase and/or a value, for example, single or double.
![](attachments/11939584/25461297.png)
Figure. Example Spanless Entity Settings
Table. Spanless Entity Settings Elements

| Setting | Description |
| ----|----|
| Scope to intents | Click to toggle on or off. If on, only extract this entity when selected intents are in progress. A Scoping Intents dropdown will appear below this switch with a list of possible intents to use to restrict this entity. |
| Scope to context | Click to toggle on or off. If on, entities will only be visible in the context in which they were originally extracted. For example, repeat executions of the same process do not re-use the same context and, therefore, entities extracted during the first execution will not be visible by the second or additional executions. |
| Spanless | Click to toggle on or off. An entity with a fixed number of possible values predicted from the user utterance as a whole instead of being extracted like a phone number or name. |
| Amelia Asks | See All link | Click the See All link to display a text field and add questions for Amelia to ask to capture this entity value |
| User Says | Click text input field to add an example user utterance and the value the utterance represents, for example, "need multiple beds in the room" would map to the value, double, for a room with double beds. Click the Save Changes button at the top of the workspace to save entries. |
| Export All Utterances | Click to export example utterances and values. |
| Upload Spanless Entity Utterances | Drag and drop a file of example utterances and corresponding values. Or click the Browse link to open the File Explorer popup and navigate a local computer to find then upload a file. |

## Upload Exported Entities
The Add Entities tab panel, on the right edge of the Entities and Entity Settings workspaces, provides the ability upload entities exported with the Actions dropdown at the bottom of the Entities workspace. Entity data is exported in JSON format.
# Edit an Entity
Once an entity is created, the bottom of the Entity Overview page includes the ability add, edit, and delete questions and answers. Questions added to the bottom of an Edit entity form appear in the Question field in the BPN Properties Panel for Ask tasks that collect entity information.
1.  Click the Amelia Trainer link on the left side of the main administration page. Then click the Entities link to display the Entities workspace.
2.  To edit an entity, click the Pencil edit icon to the right of an entity name in the list on the dashboard. The Entity Settings workspace appears.
3.  As needed, add questions Amelia will ask in the BPN Ask task collecting information for the entity.
4.  If a spanless entity, inferred from an utterance instead of a word or phrase found in an utterance, add utterances and values to the Examples at the bottom right of the form.
5.  To save changes, click the Save button at the top right of the Entity Settings workspace.
# Delete an Entity
The Entities workspace lists all active and inactive entities. Click the X to the right of an entity name in the Intent workspace. In addition, in the Entity Settings workspace, click the Delete button at the top right of the intent edit form to delete an intent.
# Create Role Entities
Entities can have a connection to other entities, for example, the start date and end date for a hotel booking with the person saying, "I need to book a hotel room from June 5th to 6/8." Amelia V3 captures these connections with an entity role classification. A hotel booking might have an entity *hotelDates* with *checkInDate* and *checkOutDate* as child entities identified as role entities and *hotelDates* identified as their parent entity. Training entity models with these entity definitions helps Amelia understand how they are used in conversations.
1.  Click the Amelia Trainer link on the left side of the main administration page. Then click the Entities link to display the Entities workspace.
2.  To add a parent entity, click the Add Entities tab at the top right of the workspace. Then type the Name, Code, Datum Type, and Description. The selected Datum Type will apply to child role entities to extract their data. Click the Add button on the Add Entities tab to save.
3.  To add a role entity for the parent entity, click the Add Entities tab at the top right of the workspace. Then type the Name, Code, Datum Type, and Description. The parent entity Datum Type overrides the role entity Datum Type. Click the Add button on the Add Entities tab to save.
4.  To edit the role entity, in the Entities workspace, click the Pencil edit icon to the right of the role entity name. The Entity Settings workspace appears.
5.  Click the Role slider. The Parent Entity dropdown list appears. Select the name of the parent entity.
6.  At the bottom of the role entity form, add at least one question for Amelia to ask. The question is used to define the Question property of a BPN Ask task.  
    ![](attachments/11939584/11939592.png)  
    Figure. Role Entity Edit Form  
7.  To edit the parent entity, in the Entities workspace, click the Pencil edit icon to the right of the parent entity name. The Entity Settings workspace appears.
8.  Confirm the role entities are listed correctly.  
    ![](attachments/11939584/11939591.png)  
    Figure. Parent Entity Edit Form
The final step in defining role entities is to use the Annotate workspace to annotate utterances then train entity models based on these entity definitions. The models help Amelia understand how the entities are used in conversations.
# Create Composite Entities
Entities can be created with a COMPOSITE datum type. The entity can include one or more single sub-entities which can be set as optional or required. For example, a composite entity named order_item could have sub-entities food and count. Food might be an entity with a CUSTOM_DATUM type using tabular data that includes burger, fries, and pizza. The count sub-entity might be an integer. The utterance, “I’d like 5 burgers” might fill the order_item composite entity with count a value of 5 and food a value of burger.
Create sub-entities first before creating a composite entity. To create a composite entity, select COMPOSITE as the datum type then add sub-entities as new fields for the composite entity.
![](attachments/11939584/25461376.png)
Figure. Composite Entity Form Example
Table. Composite Entity Settings Elements
|                             |                                                                                                                                                                                                                                                                                                                                     |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Setting                     | Description                                                                                                                                                                                                                                                                                                                         |
| Scope to intents            | Click to toggle on or off. If on, only extract this entity when selected intents are in progress. A Scoping Intents dropdown will appear below this switch with a list of possible intents to use to restrict this entity.                                                                                                          |
| Scope to context            | Click to toggle on or off. If on, entities will only be visible in the context in which they were originally extracted. For example, repeat executions of the same process do not re-use the same context and, therefore, entities extracted during the first execution will not be visible by the second or additional executions. |
| Role                        | Click to toggle on or off. If on, this entity provides a specialization of a given parent entity, for example, start date vs end date or source location vs destination.                                                                                                                                                            |
| Allow Overlap               | Click to toggle true ( on ) or false ( off ). If true, this entity is allowed to overlap with other entities of the same type within an utterance.                                                                                                                                                                                  |
| **Composite Entity Fields** |                                                                                                                                                                                                                                                                                                                                     |
| Composite Entity Fields     | Define sub-entities (fields) extracted as part of this composite entity.                                                                                                                                                                                                                                                            |
| \+ Add New Field            | Click to add a row for a new composite entity field                                                                                                                                                                                                                                                                                 |
| Entity                      | Click this field to select the sub entity extracted within this overall composite entity.                                                                                                                                                                                                                                           |
| Optional                    | Click to toggle true ( on ) or false ( off ). If false, this field is required. If true, this field is optional and will be extracted, if available and included in the user utterance, but will be considered valid whether or not it is present.                                                                                  |
| Multiple                    | Click to toggle true ( on ) or false ( off ). If true, all available entities of this type will be extracted and included in the composite entity. If false, only one entity of this type will be extracted, the first entity.                                                                                                      |
| Positions                   | The positions in which this field can appear in text. If 0, the field can appear anywhere in the span. Multiple fields can have the same positions and will be considered interchangeable.                                                                                                                                          |
| Default Value               | The default value for optional fields when a value is not provided. This should correspond to text provided by a user for the field, before any normalization.                                                                                                                                                                      |
| Delete Entries              | To delete composite entity entries, click the check box to the left of an entry then click this button. To delete all entries, click the check box to the left of this Delete Entries button to select all entries then click this button to delete them.                                                                           |
| **Field Groups**            |                                                                                                                                                                                                                                                                                                                                     |
| Group Type                  | Type of field group                                                                                                                                                                                                                                                                                                                 |
| Entities                    | Collection of entities to include in a group.                                                                                                                                                                                                                                                                                       |
| Add New Field Group         | Click to add a row for a new field group                                                                                                                                                                                                                                                                                            |
| Amelia Asks \| See All link | Click the See All link to display a text field and add questions for Amelia to ask to capture this entity value                                                                                                                                                                                                                     |
# Handling Negation with Entities and Entity Models
Amelia recognizes if an entity has been negated. The utterance, “I want a sandwich with no tuna” has two entities, sandwich and tuna. However, Amelia needs to understand “no tuna” means the person does not want a tuna sandwich, only a sandwich that does not have tuna.
Amelia uses a collection of language-specific negation terms to evaluate utterances and extract entities. She understands “anything but”, “no”, and similar terms are negations. For example, the utterance, “Sandwich with no tuna, anything but Swiss cheese” builds a set of entities with “sandwich” and two negated entities, “tuna” and “Swiss cheese,” so a BPN Script task can access which entities have exclusions based on negation.
In a BPN Script task, ${ctx:latestSlot('entityName').datum().negated()} can be used to test an entity for negation, where entityName is the name of an entity. For example, iterating through entities in a Script task and testing each entity for negation can be used to have Amelia respond with their order and state what she is not including. The .datum.negated() returns a Boolean value, true or false.
# Test an Entity and Entity Models
Amelia provides two ways to test entities and entity models, both available through the Amelia Trainer workspaces.
Use the Predict tab on the right side of the Entities workspace to test an entity model, entities, and utterances. In the Predict panel, select the entity model, type an utterance, and then click the Predict button to see which entity is triggered. The triggered entity name displays below.
The Dashboard workspace also includes a Stats button to the right of each model name with detailed information about misclassifications, confusion matrix, and other details useful to tune models.
# Manage Entities in the Process Knowledge Workspace
While entities are primarily managed in the Entities workspace, available as part of the Amelia Trainer link on the left side of Amelia's administration pages, entities also can be managed while working with BPN process models.
BPN models are available by clicking the Process Memory link, located on the left side of Amelia's administration pages. Then click Process Knowledge and select a BPN model to edit. The entities popup link is to the right of the Import and Export links at the top of the BPN workspace.
![](attachments/11939584/25461429.jpg)
Figure. Entities Popup Link in a BPN Workspace
Click the Entities link to display the Intents popup. The Add Entities, Train, and Predict buttons at the top of the Entities popup behave the same way as the Add Entities, Train, and Predict tabs in the Entities workspace, as described above.
![](attachments/11939584/11939588.png)
Figure. Entities Popup in a BPN Workspace
# Add Multiple Entities in Annotate Workspace
The Annotate workspace also can upload TSV files with multiple entities defined.
A file with entities includes multiple sentences with a single word or token on each line and a blank line between sentences. Each word is followed by a tab and one of three characters:
-   0 indicates the word is out of bounds of the entity.
-   An entity name connects the word to an entity.
-   B indicates the beginning of a chunk with an entity name.
-   I indicates the inside of a chunk with an entity name.
**Sample Entity Upload TSV File**
``` bash
I O
want    O
a   O
red carColor
ford    B-carMake
focus   I-carMake
Get O
me  O
the O
blue    carColor
ford    B-carMake
mustang I-carMake
```
To reach the workspace, click the Amelia Trainer link on the left side of Amelia's administration pages. Then click the Annotate link. The Annotation Framework 1. Load/Learn workspace appears with the Load New tab selected by default.
In the 1. Load/Learn workspace, click the TSV radio button on the left side then upload a TSV file with the contents above or similar. The Annotation Framework workspace displays the 2. Annotate workspace. The workspace will display the two sentences above or similar marked up. The entities are listed in the Entities workspace. However, the new entities need further definition and editing in the Entities workspace for use in training entity models.
![](attachments/11939584/11939586.png)
Figure. Annotate Workspace after Multiple Entities Uploaded
## Attachments:
![](images/icons/bullet_blue.gif) [image2017-9-15_15-25-45.png](attachments/11940396/11940397.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-15_15-25-24.png](attachments/11940396/11940398.png) (image/png)  
