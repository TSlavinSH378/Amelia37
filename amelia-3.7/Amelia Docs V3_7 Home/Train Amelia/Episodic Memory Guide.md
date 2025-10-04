{% version "3.x" %}
Amelia can use past conversations to navigate through a real time conversation. As a conversation progresses, she identifies relevant past conversations to find the best process to follow. This dynamic capability is called episodic memory.
Creating Amelia's episodic memory requires the creation, training, and deployment of three models. An intent model uses words, phrases, and other elements to help Amelia understand one or more topics she will encounter in conversation. Two episodic memory models also are created, a Thought Vectors model to generate the five best responses and a Contextual LSTM model to rank and pick from the five best responses.
All three episodic memory models are created with the Annotate workspace in Amelia's administration pages. The workspace annotates chat transcripts and other materials to identify intents and entities.
Before creating Amelia's episodic memory models, create at least one intent and collect chat transcripts and other materials to annotate. The Amelia Trainer link on the left side of the Amelia V3 administration pages when clicked displays links to create intents, annotate data, and train models. As of version 3.1, a domain can be selected with a dropdown list at the top left of the interface, next to the logo.
# Create and Train an Intent Model
Intent models help Amelia identify the ideal BPN model process to use as she converses. Training an intent model uses chat transcripts from prior conversations to mark them up to connect words and phrases to intents.
Chat transcripts must follow these guidelines:
-   Each interaction utterance must begin with either Amelia: or User:
-   Multiple conversations can be included by adding a \## as the conversation delimiter between two conversations.
On the left side of the Amelia V3 administration pages, click the Amelia Trainer link and the Annotate link when it appears. The Annotate workspace appears.
1.  If not displayed, click the Load/Learn tab. The Load/Learn workspace appears on the right side.
2.  Click the Browse link in the center of the workspace to upload a chat transcript to annotate. Or click the Load Existing tab and select an existing document. The chat transcript appears in the Annotate workspace.
3.  Annotate the transcript with intents. As needed, highlight a word or phrase. Then click to the right of the utterance under the Intents column. A plus sign and Add Intent appear where the computer mouse appears.
4.  Click the plus sign and Add Intent to display a list of intents. Click the appropriate intent to select. Repeat until the transcript is annotated.
5.  When the transcript is annotated, click the Save As icon at the top right of the workspace.
6.  Click the Train tab above the workspace and select Train Intents. The Train Intent Models panel appears on the right side of the workspace.
7.  As needed, select an existing intent model or click the minus sign ( - ) to the right of the intent name, enter a new model name, then click the Create a New Model button that appears. Complete the Train Models form as needed then click the Train button at the top of the Train panel.
For more details, refer to the [Train Step Workspace](https://docs.ipsoft.com/display/AmeliaDocsV36/Annotate#Annotate-TrainStepWorkspace) in the [Annotate](Annotate) guide.
# Create and Train Episodic Memory Models
With an intent model trained, the next step is to create the two episodic memory models. Both models are created and trained with the Train Episodic Memory panel available in the Annotate workspace.
Each model repeats the process used to create and train an intent model with one key difference. When an utterance is tagged with an intent, click on the intent tag area and add *epm* and a single space in front of the intent name. Or when the intent is created with the Intent List workspace, add `epm` and a space before the intent name then select it from the list that appears when the Annotate workspace is clicked under the Intents column. This tells Amelia the intent is part of creating her episodic memory models.
![](attachments/11939903/11939905.png)
Figure. Add epm Prefix to Intent Tag Label
Once the annotated chat is saved with the Save As icon in the Annotate workspace, the next step is to train the two episodic memory models.
1.  Click the Episodic Memory link on the left side of Amelia's administration pages then click Episodic. The Episodic Memory workspace appears.
2.  Click the gear icon at the top right of the Train tab and select Train Episodic Memory. The Train Episodic Memory panel appears on the right side of the workspace.
3.  Complete the Episodic Memory workspace as needed.  
    ![](attachments/11939903/11939904.png)
    Figure. Episodic Memory Workspace
    Table. Episodic Memory Workspace Settings
    <table class="wrapped confluenceTable">
    <tbody>
    <tr class="header">
    <th class="confluenceTh">Element</th>
    <th class="confluenceTh">Description</th>
    </tr>
    &#10;<tr class="odd">
    <td colspan="2" class="confluenceTd"><strong>Tabs</strong></td>
    </tr>
    <tr class="even">
    <td class="confluenceTd">Add Single</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="odd">
    <td class="confluenceTd">Upload File</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="even">
    <td colspan="2" class="confluenceTd"><strong>Test Model</strong></td>
    </tr>
    <tr class="odd">
    <td class="confluenceTd">Select a model</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="even">
    <td class="confluenceTd">Accuracy</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="odd">
    <td class="confluenceTd">Test</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="even">
    <td colspan="2" class="confluenceTd"><strong>Train Model</strong></td>
    </tr>
    <tr class="odd">
    <td class="confluenceTd">Encoder Models</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="even">
    <td class="confluenceTd">Scoring Models</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="odd">
    <td class="confluenceTd">Use Named Entities</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="even">
    <td class="confluenceTd">Use Custom Entities</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="odd">
    <td class="confluenceTd">Model Name</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="even">
    <td class="confluenceTd">Training Corpus</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="odd">
    <td class="confluenceTd">Use Validation Dataset</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    <tr class="even">
    <td class="confluenceTd">Validation Corpus</td>
    <td class="confluenceTd"><br />
    </td>
    </tr>
    </tbody>
    </table>
    OLD TABLE DATA:
    
    | Settings | Description |
    | ----|----|
    | Thought Vectors | This generates possible responses based on Amelia's past conversation history. Currently there is one thought vector option. Select the default model. |
    | Contextual LSTM | This ranks possible response generated by the Thought Vector algorithm. Currently there is one contextual LSTM option. Select the default model. |
    | Parameterize Named Entities | Use output of built-in named entity recognition system (entities belong to same set as above), replacing words with their corresponding entities, for example, the phrase “George Bush left office in 2008" becomes "PERSON PERSON left office in DATE". This makes the training data a bit more generalized. |
    | Parameterize Custom Entities | Custom entities are user-defined entities defined through the Entity List page. As with the Parameterize Named Entities setting, this setting replaces words with their corresponding entity label if annotated. |
    | Model Name | Type a unique name for the new model |
    | Training Corpus | Selection of documents saved from the Annotate workspace that have been annotated with intents and entities |
    | Use validation dataset | Select slider to choose a validation dataset to use for training. Validation datasets are documents created with the Annotation workspace. They allow performance comparisons, using statistical charts available through the Dashboard page, as algorithms and/or data are changed. |
    | Validation Corpus | Select a validation corpus |
    
4.  Click the small gears icon next to the Thought Vector heading to display the Encoder Settings popup. The Default Probability and Optimizer settings work in most cases. Batch Size should be half the number of utterances included in the Training Corpus. 50 epochs should work fine for training 100 utterances. For training size of more than 200 and very large data sets, setting epochs to 150 should work fine. Click anywhere in the Annotate workspace to close the popup.  
    ![](attachments/11939903/11939911.png)  
    Figure. Encoder Settings Popup  
5.  Click the small gears icon next to the Contextual LSTM heading to display the Scorer Settings popup. The Default Probability and Optimizer settings work in most cases. Batch Size should be half the number of utterances included in the Training Corpus. 50 epochs should work fine for training 100 utterances. For training size of more than 200 and very large data sets, setting epochs to 150 should work fine. Click anywhere in the Annotate workspace to close the popup.  
    ![](attachments/11939903/11939910.png)  
    Figure. Scorer Settings  
6.  Click the Train Dialog Models button at the bottom of the panel to save settings and start training.
To confirm the models are training, click the Training Queue link on far right edge of the Annotate workspace.
# Deploy Models
To deploy the intent model and two episodic memory models, click the Dashboard link visible when the Amelia Trainer link is clicked in Amelia's V3 administration pages. Deploy the intent model first then the Thought Vector and Contextual LSTM models. Find the model names in the dashboard list and click the thumbs up Ready icon to deploy each model. Deployed model listings have a light blue background stripe in the dashboard.
# Test Episodic Memory Models
Once the three episodic memory models have been created, trained, and deployed, Amelia's V3 chat interface displays how she navigates from past conversations based on the current conversation. To see her episodic memory, click the Mind link at the top right of the chat interface then click the Episodic Memory tab icon on the right edge of the Mind panel. Then engage Amelia in conversation. She navigate past conversations that address the context and needs in the current conversation.  
{% /version %}
