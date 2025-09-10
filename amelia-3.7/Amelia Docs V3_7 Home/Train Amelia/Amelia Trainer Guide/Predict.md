The Predict page tests different Natural Language Processing (NLP) models. Previously, the only way to test these models was in conversation with Amelia. The Predict page displays useful data about how Amelia processes and understand what users say to her. Currently, only one utterance can be tested at a time.
Click the Amelia Trainer link on the left side of the administration pages then click the Predict link to display the workspace. Clicking results in the search results area in some cases opens the intent, entity, or other element.
![](attachments/11939612/25461593.jpg)
Figure. Predict Workspace with Entities Search Results
Table. Predict Workspace Elements
<table class="wrapped relative-table confluenceTable" style="width: 99.8493%;">
<colgroup>
<col style="width: 22%" />
<col style="width: 77%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh" style="width: 22.0799%">Element</th>
<th class="confluenceTh" style="width: 77.7694%">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd" style="width: 99.8493%"><strong>Search Terms and Parameters</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 22.0799%">User says...</td>
<td class="confluenceTd" style="width: 77.7694%">Type a test utterance.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd" style="width: 99.8493%"><strong>Advanced Options</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 22.0799%">Filter Entity Results</td>
<td class="confluenceTd" style="width: 77.7694%">Optional. Filter prediction results by entity. This can be useful if there are many entities defined in a domain.</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 22.0799%">Prompt Entity</td>
<td class="confluenceTd" style="width: 77.7694%">Optional. Select an entity asked for in a BPN. Entities requested in a BPN may impact the result of tagging, as the question asked by Amelia is used when extracting the entity.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 22.0799%">Scope Intent</td>
<td class="confluenceTd" style="width: 77.7694%">Optional. Select an intent to use to scope entity extraction.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd" style="width: 99.8493%"><strong>Search Results</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 22.0799%">Intents and Entities</td>
<td class="confluenceTd" style="width: 77.7694%"><div class="content-wrapper">
<p>Displays the intent and entities identified based on the User says... utterance at the top center of the page. Output displays Intent Name, BPN Name, and BPN Type (Execute Process or Answer FAQ).</p>
<p>Click intent and entity names to view and make changes.</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 22.0799%">Domains</td>
<td class="confluenceTd" style="width: 77.7694%"><p>Identifies the domains where any predicted intents and entities are located.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="width: 22.0799%">System NLP</td>
<td class="confluenceTd" style="width: 77.7694%"><p>Displays results from three system classifiers: Sentence Type, Sentiment, and Insult/Compliment.</p>
<ul>
<li>Answer Type returns I Don't Know (IDK), Yes, No, or Other</li>
<li>Overall Sentiment returns Positive, Neutral, or Negative</li>
<li>Agent Sentiment returns Insult, Compliment, or Neutral</li>
<li>Problem Type provides a guess at whether or not the user is expressing a request and needs help. When a user expresses a problem request, Amelia may ask an elaborating question. When the user makes a request or information request Amelia doesn't understand, she may escalate.</li>
</ul></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="width: 22.0799%">CQA</td>
<td class="confluenceTd" style="width: 77.7694%">Clarifying Question Asker module attempts to clarify user intent in cases where meaning is ambiguous. For example, if a user asks to open a bank account, a clarifying question might be to ask if the account is for savings or checking. Displays probabilities and a statement whether or not Amelia detects ambiguity.</td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Train Tab</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Train</td>
<td class="confluenceTd">Click the tab on the right side of the workspace to display the Train Models panel. See <a href="Annotate_11939620.html#Annotate-TrainTabPanel">Train Tab Panel</a> for details about how to use this functionality.</td>
</tr>
</tbody>
</table>
