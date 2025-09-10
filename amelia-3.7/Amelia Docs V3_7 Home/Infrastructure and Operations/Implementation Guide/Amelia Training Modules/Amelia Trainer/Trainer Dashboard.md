The Amelia Trainer Dashboard workspace displays all active and inactive trained intent models and entity models. This includes system models, for example, datum types for US English numbers and quantity.
# Dashboard Workspace
Once a model has been trained with the Annotate workspace, models appear on the dashboard. A green deployed status indicates models currently deployed which Amelia can use to respond to conversations.
The Actions icons when clicked export, delete, or deploy the selected model. Clicking the Logs icon displays the training log output while clicking the Stats icon displays a popup with links to validation, confusion matrix, and misclassification results to help train models to be more precise.
To see prior revisions of a model, click the model name or revision number.
> [!warning]  
>
> For optimal results, there should only be one intent model active and deployed for one domain regardless of algorithm used.

![](attachments/11939658/25462219.jpg)
Figure. Amelia Trainer Dashboard Workspace
Table. Dashboard Workspace Tabs
<table class="relative-table confluenceTable" style="width: 99.9252%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 88%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Tab</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">NLU Settings</td>
<td class="confluenceTd">Define the baseline Natural Language Unit (NLU) settings for models.
<div class="table-wrap">
<pre class="table"><code>| Setting | Description |
| ----|----|
| Auto Training | When selected, automatically train and deploy auto-training models |
| Intent Prediction Threshold | If the highest score for an intent is less than this value, no intent will be predicted. |
| Domain Switching Threshold | If the highest score for a domain is less than this value, there will not be a domain switch. |
| Enable Intent CQA | When selected, enable clarifying question asking (CQA) for intents in this domain |
| In-Domain Threshold | If the in-domain score is less than this value, no intent will be predicted. |
| Intent Ambiguity Threshold | If the difference in scores of the top two intents is less than this value, the input utterance is considered intent ambiguous. |
| CQA Intent Threshold | If the top intent score is less than this value, CQA will be ignored. |
| Enable Domain CQA | When selected,;enable clarifying question asking (CQA) for Domain ambiguity |
| Domain Ambiguity Threshold | If the difference in scores of the top two domains is less than this value, the input utterance is considered domain ambiguous. |
| CQA Domain Threshold | If the top domain score is less than this value, CQA will be ignored. |
| Enable Intent Correction | When selected, allow sending prediction result to users for manual annotation.;Users must have the AUTHORITY_MISCLASSIFICATION_ANNOTATION authority assigned to their user account. |
| Intent Correction Threshold | Utterance with highest prediction intent score is less than equal to\n the provided threshold are considered for manual annotation by user. All misclassified utterances can be viewed under Annotate. |
| Enable Intent Learning | Enable auto-learning new intents from escalated conversations. |
| Edit Learned Intents | Enable modification of auto-learning new intents by agent while escalated conversations |
| Enable Entity Learning | Enable auto-learning new entities from escalated conversations. |
| Edit Learned Entities | Enable modification of auto-learning new entities by agent while escalated conversations |</code></pre>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">Upload Models</td>
<td class="confluenceTd">To upload a model file, drag and drop a file or click the Browse link to display the file explorer and navigate to a file to upload</td>
</tr>
<tr class="odd">
<td class="confluenceTd">Train</td>
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
<tr class="even">
<td class="confluenceTd">Import/Export</td>
<td class="confluenceTd"><p>To import files, drag and drop a file or click the Browse link to display the file explorer and navigate to a file to upload</p>
<p>To export files, click the switches next to data types to select or deselect exporting intents, entities, classifiers, grammars, and NLU settings</p></td>
</tr>
</tbody>
</table>
# Performance Statistics
In the Dashboard workspace, the Stats graph icon, when clicked, displays graphs to help measure the performance of a model with a variety of criteria, for example, folds, misclassifications, correct use of an intent or entity, and a confusion matrix. These charts replace the manual performance evaluation process used in Amelia V2. Click the Statistics icons on the right of the initial Stats popup to display additional graphs.
![](attachments/11939658/11939665.png)
Figure. Model Evaluations Stats
Table. Model Evaluation Icons

| Icon | Description |
| ----|----|
|  | Click to display a popup to export Statistics data. Select statistics type and export format then click the Export button. |
|  | Click to display a popup with numbers correct, actual, predicted, precision, recall, and F1 score. Hover over question mark ( ? ) help icon for details. |
|  | Click to display Confusion Matrix results |
|  | Click to display Misclassifications |

The **Statistics** popup displays how Amelia measures a model based on precision and recall.
![](attachments/11939658/11939669.png)
Figure. Model Validation Statistics
Table. Statistics Popup Columns

| Column | Description |
| ----|----|
| Correct | For each label row, the number of examples predicted correctly, true positives. |
| Actual | The total number of examples for each label row, true positives plus false negatives. Also called Gold. |
| Predicted | The total number of examples for each label row predicted correctly or incorrectly, true positives plus false positives. Also called System. |
| Precision | For each label row, the number of examples predicted correctly (the Correct value) divided by the total number of times this label was predicted correctly or incorrectly (the System value), true positives / (true positives + false positives). |
| Recall | For each label row, the number of examples predicted correctly (the Correct value) divided by the total number of examples with true positives and false positives (the Gold value), true positives / (true positives + false positives). |
| F1 | A combined measure of precision and recall, the harmonic mean of the two values, 2 * (precision * recall) / (precision + recall). |

The **Confusion Matrix** popup shows the number of times each label row was mislabeled as a different label. Rows correspond to predicted labels, columns correspond to actual labels, and cells correspond to the number of examples where a label was predicted for an example row that should have been the actual corresponding label column.
![](attachments/11939658/11939668.png)
Figure. Confustion Matrix
The **Misclassification** popup provides details about utterances that were not classified accurately.
![](attachments/11939658/11939667.png)
Figure. Misclassifications
Table. Misclassifications Popup Columns

| Column | Description |
| ----|----|
| Prediction | The actual predicted label for the example. |
| Span | In the case of entity tagging, the span of text given the label. |
| Context | The sentence that was mislabeled. |

# Export and Import Models
A model can be exported to a ZIP archive using the export button on the model revision. Exported models can be uploaded to Amelia with the Upload Models tab on the right edge of the Dashboard workspace.
