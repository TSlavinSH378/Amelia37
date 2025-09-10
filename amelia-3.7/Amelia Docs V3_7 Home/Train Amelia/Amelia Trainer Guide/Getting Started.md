-   [Key Terms](#GettingStarted-KeyTerms)
-   [The Training Process](#GettingStarted-TheTrainingProcess)
-   [Define Training Goals](#GettingStarted-DefineTrainingGoals)
-   [Collect Materials](#GettingStarted-CollectMaterials)
-   [Create Intents and Entities](#GettingStarted-CreateIntentsandEntities)
    -   [Intents](#GettingStarted-Intents)
    -   [Entities](#GettingStarted-Entities)
    -   [Negatives](#GettingStarted-Negatives)
    -   [Automatic Intent and Entity Creation](#GettingStarted-AutomaticIntentandEntityCreation)
    -   [How to Use Intents and Entities](#GettingStarted-HowtoUseIntentsandEntities)
-   [Create a Conceptual Model](#GettingStarted-CreateaConceptualModel)
    -   [Create a Test Data Set](#GettingStarted-CreateaTestDataSet)
    -   [Create a Training Data Set](#GettingStarted-CreateaTrainingDataSet)
-   [Test and Refine a Conceptual Model](#GettingStarted-TestandRefineaConceptualModel)
    -   [Train and Iterate Data Sets](#GettingStarted-TrainandIterateDataSets)
    -   [Training Algorithms](#GettingStarted-TrainingAlgorithms)
        -   [Intent Training](#GettingStarted-IntentTraining)
        -   [Entity Training](#GettingStarted-EntityTraining)
    -   [Use Model Statistics](#GettingStarted-UseModelStatistics)
        -   [Statistics](#GettingStarted-Statistics)
        -   [Misclassifications](#GettingStarted-Misclassifications)
-   [Store and Maintain Models](#GettingStarted-StoreandMaintainModels)
Training an artificial intelligence (AI) like Amelia is similar to training a person. People and AIs are not born knowing how to speak a language or perform tasks. Learning requires study of relevant information with lots of practice and testing.
Before starting to train Amelia, it's important to understand key concepts, terms, and the training process. This document describes how to train Amelia, at a high level, with an emphasis on best practices.
> [!warning]  
>
> Conversations with Amelia can involve personal user data. Any information related to a natural person/data subject that can directly or indirectly identify that person is personal data. This data must be anonymized, or excluded if possible, when training Amelia.
>
> Government regulations control the use and storage of personal data. For consumer data, follow the “[Principles relating to processing of personal data](http://www.privacy-regulation.eu/en/5.htm)” EU GDPR article and other sources.

# Key Terms
It helps to understand terms used to describe Amelia and how she is trained. These terms are explained in more detail below in the course of training. Refer to this table, as needed, while reading the rest of this page.
Table. Key Terms and Definitions

| Term | Definition |
| ----|----|
| Classifier Model | A data set Amelia creates with intents, entities, utterances, and other data to understand conversation used to describe a topic. Algorithms process the input data to evaluate the importance and weight of words and phrases in the data set. |
| Datum | Datums are pre-built entities used to handle common concepts found in natural language utterances, for example, a date or a person's age or name. Each defined entity has an assigned datum type. The exception is an entity defined as a custom type for which a Custom Datum type is used. |
| Domain | A distinct set of knowledge created within an instance of Amelia's software, for example, IT help desk or HR policies. |
| Entity | Data collected to complete an intent goal, for example, a date of birth for a loan application. |
| Gazetteer | A data set that maps unnormalized or related terms to normalized values. They help optimize the extraction of conversation data into entities. For example, one person might say Word meaning Microsoft Word while another person says MS Word to Amelia. Creating an entity using a gazetteer that maps the unnormalized and related terms Word, MS Word, msword, and ms word to one normalized value, Microsoft Word, ensures Amelia uses one entity to extract all four possible ways to describe the same software. |
| Grammar | Grammars are written in natural language with the help of notation, keywords, regular expressions, and pre-defined elements. They're used to capture intent goals and data needed to meet goals by matching words, numbers, phrases, and other data found in a user conversation with Amelia. |
| In-Domain | An utterance directly related to an intent. For example, "I need a hotel room" is in-domain if the intent is to reserve a hotel room.Negative utterances are in-domain if they're used to help Amelia, for example, to recognize the difference between the in-domain negative utterance "I need a rental car" and "I need a hotel room" for an intent to reserve a hotel room. |
| Instance | A single installation of Amelia software within an organization. |
| Intent | The user's goal, for example, to qualify for an auto loan. The goal requires a process to complete. |
| Label | A;persistent tag used to identify a set of training utterances, for example, resetPassword. Labels reflect user goal intents. Labels should be descriptive and consistent in any usage of CamelCase or snake_case. |
| Negative Utterances | An unlabelled training utterance, negatives help Amelia;learn the difference between tasks and knowledge she is trained on and things she is not. They help Amelia understand words that are similar but have different unrelated meanings than utterances used to trigger the intent goal and Amelia's processes. |
| Out-of-Domain | An utterance not directly related to an intent. "I like pizza" is out-of-domain if the intent is to reserve a hotel room. |
| Process | The steps Amelia is trained to take to help a user accomplish their goal. Business Process Network (BPN) flow diagrams define the processes Amelia follows. |
| Spanless Entity | Entities that are inferred are called spanless entities. If someone says, for example, "queen beds two of them" you can infer they want a double hotel room from the utterance. |
| Utterance | Words that represent a natural language sentence, for example, "I want to reset my password." A variety of possible utterances a person might say in a conversation are used to train Amelia. |

# The Training Process
To train Amelia, a conceptual model is built from a variety of materials. Amelia uses the model to parse the unconstructed casual way people talk. A model helps Amelia understand natural language to recognize the user’s goal intent (Intents) and data (entities) needed to address their intent.
For example, a conversation to manage paid time off requests would require a conceptual model built from common words and phrases for time off requests, as well as company policies. "I need a vacation" might cause Amelia to ask for more information about calendar dates.
Training Amelia is an iterative process similar to training humans.
1.  Define the goal and expected results of training Amelia.
2.  Collect possible utterances and other material relevant to the conversation topic, for example, to reset a password.
3.  Create goal intents to capture user goals found in utterances and create entities to capture entity data needed to meet goals, for example, start and end dates for a hotel stay.
4.  Create and import materials then train a conceptual model Amelia can use to parse and understand the casual way people talk about the conversation topic.
5.  Test the conceptual model and make changes to utterances, intents, entities, and other materials to refine the conceptual model.
Business Process Networks (BPNs) are used to direct the process flow of Amelia's responses, as described in the [BPN Getting Started Guide](#).
# Define Training Goals
What can Amelia do for an organization? The answer depends on what is needed, as well as the skills and resources available. Because no one is born knowing how to do things, training is needed to match needs with skills to solve problems. Needs help determine goals.
A scenario distilled from goals organizes how Amelia will be trained to perform a task. A goal might be to complete a password reset, for example. The scenario is a user locked out of their account who talks with Amelia, answers a few security questions from her, and has their password unlocked. Scenarios are processes with an action that complete one or more tasks.
These questions can help convert a user intent goal to a viable scenario where Amelia can help solve problems.
-   What is the name of the intent goal that triggers the process that, in turn, requires training? For example, ResetPassword. These names are called labels.
-   What are example utterances a person might use in conversation with Amelia to trigger the intent goal? For example, "I'm locked out of my computer again" and "Could you reset my laptop password?" or "Somehow my password no longer works."
-   What are questions Amelia will need to ask to get the data entities needed to complete the scenario process? Amelia's questions should not generate yes or no answers. Her questions should generate answers filled with data needed to perform tasks.
Answers to these questions, and any materials needed to support Amelia as she completes a process, are described in the training steps below.
# Collect Materials
A variety of data is used to train Amelia. The intent goals and scenario determine what materials to collect.
-   **Utterances** with enough variety and subtlety to help Amelia understand a person asking about a specific topic. For training, a modest training set of 50-100 utterances is ideal.
-   **Negative utterances** to help Amelia understand words that are similar but have different unrelated meanings than utterances used to trigger the intent goal and Amelia's processes.
-   In some cases, simple structured **tabular data** Amelia can use as a cross reference to support an intent model, entity model, and/or custom datum type for entities.
# Create Intents and Entities
Intents and entities needed to accomplish the intent goal are the heart of training Amelia. Once a classifier model is trained, deployed, and used in an Amelia domain, every user utterance in a conversation is compared to the model. If the utterance can be classified as one of the intent labels provided in the training data, the model will produce that label as a result. Amelia then determines what to do with the result, for example, launch a BPN process.
## Intents
Intents are a critical part of Amelia's training because they capture and represent the user goal for a conversation. They trigger Amelia to perform a process to address the person's goal. Intents are specific to a domain, for example, reserve a hotel room is an intent for a domain with data to train Amelia to book hotel rooms. However, intents can be imported and exported into other domains and instances.
Intents are created manually or imported with an annotated data set that includes labels and utterances.
## Entities
Identifying an intent goal in a conversation with Amelia triggers a process to collect data needed to achieve the goal. Entities are created and optimized to help Amelia extract data. Entities use datum types, for example, names, numbers, dates, weights, and other common values to validate data. Data captured by an entity is available to the Business Process Network (BPN) process Amelia uses to respond to intent goals, for example, to integrate with backend systems or decide future actions to take.
Entities are used to annotate utterances as part of training entity models. Annotation shows Amelia how words and phrases connect to entities. This helps her learn how to evaluate conversations and map words and phrases in a conversation to entities.
Entities are created manually or imported with an annotated data set that includes labels and utterances.
## Negatives
All of the labeled training data is used by Amelia to recognize what the user is saying and classify it with a label, but what if the user says something Amelia should not recognize?
Negative data is any unlabeled training utterance. They create a difference between tasks and knowledge Amelia is trained on and things she is not. Negative data would handle the simple case of Amelia being trained on password resets, but not on ordering lunch.
If a user says, "I want to reset my password," this should be correctly classified by the model and Amelia will take the appropriate action. If a user says, "I want to order tacos," this should not be classified as any label by the model and Amelia will yield to her other subsystems to determine the best response to the user, maybe an FAQ about how to order lunch.
The problem becomes more complex when we need to handle utterances with negation. A user may say "I don't want to reset my password" and this should not be labeled the same way as the previous utterance even though they are very similar. Or if the user is ordering tacos, and they say "no guac on my taco" the entity handling toppings should not pick up "guac."
Negatives are imported and not annotated. They include utterances that should not launch any intent. Negatives should be both in-domain and out-of-domain, for example, "I want to reserve a car for a weekend" is an in-domain negative for an intent to reserve a room and "I like pizza with mushrooms" for out-of-domain. These utterances should be saved as a data set with a memorable file name. Include the data and version for the data set.
## Automatic Intent and Entity Creation
Amelia has the ability to learn intents and entities from escalated conversations. These intents and entities are linked automatically to generated BPNs. Entity types are guessed from agent questions. Intents are based on the escalating utterance from the user.
In escalated conversations, when an agent asks the user a question, Amelia first tries to match existing entities in the current domain. If no match is found, she checks existing built in types for a match. In the worst case, she creates an entity that accepts the user response directly.
The agent’s question is used to supply the entity name. The trigger for the intent is extracted from the escalation utterance and agent utterance. The placeholder implementation is a new intent model.
New entities are linked to the generated BPN. Any new intent points to the generated BPN as well. Any necessary model training/generation kicks off, and the resulting models are deployed automatically. This is managed through Amelia’s batch service.
## How to Use Intents and Entities
Amelia includes a diverse set of tools and methods to optimize use of intents and entities based on typical use.
Table. Intents and Entities Usage Matrix

| 
 | Typical Use | Example Utterance | Example Result |
| ----|----|----|----|
| Intent | Launch a process (BPN) or if Negative class is triggered, "social talk" subsystem responds | "I want to reserve a hotel room."; | Triggers the intent reserveARoom and launches a BPN to help the end user make a hotel reservation |
| Intent (referencing a Grammar V2 Goal) | Launches a process (BPN) based on an exact/nearly exact match to the Grammar. Can be combined with an intent model. Grammar is checked first and if no match, then the utterance runs through the model. | "Billing discrepancy needs to be resolved." | Triggers a BPN to help look up and resolve a billing issue given a match to the Grammar goal:(billing DISCREPANCY *that needs to be resolved) |
| Entity (Standard Entity/Tagger Entity) | Extract a feature(s) from an end user utterance based on the datum type and entity model and store in an entity's slot | "Can we book a suite and check in tomorrow?" | DATE datum type entity model extracts the value "tomorrow". It is normalized and stored in the entity as YYYY-MM-DD format. |
| Entity Using TEXT Datum | Extract a feature(s) from an end user utterance based on a model and store in an entity's slot | "My favorite movie is Ferris Bueller's Day Off so can you recommend a movie to watch on pay per view?" | TEXT datum type entity model extracts the value "Ferris Bueller's Day Off" and stores in the entity. |
| Entity Using Custom Datum - Gazetteer (Tabular Data) | Extract a feature(s) from an end user utterance by referencing a gazetteer (tabular data set) and store in an entity's slot | "Coming to atl and need a place to stay" | Gazetteer includes various abbreviations of different cities in the US in which the hotel chain has locations. "atl" is extracted from the utterance. Because there is a normalized value in the gazetteer, the value that is stored in the entity is normalized to Atlanta. |
| Entity Using Custom Datum - Gazetteer (Tabular Data) with Regex | Extract a feature(s) from an end user utterance by referencing a gazetteer (tabular data set) with a regular expression pattern and store in an entity's slot as a normalized value | "I can't seem to access www.ipsoft.com and need to have it whitelisted." | Gazetteer includes a regular expression pattern that matches standard website URL formats. The The custom datum entity references the Gazetteer to determine if there is a pattern within the utterance that matches the Regex. If one is found, it is extracted and stored in the entity. |
| Entity Using Custom Datum - Grammar (V2 Slot) | Extract a feature(s) from an end user utterance by referencing a grammar (V2 slot) and store in an entity's slot | "Need to order the mushroom pizza from your room service menu" | Grammar includes list of available items from room service menu. The value mushroom pizza matches the Grammar slot:(*mushroom pizza *pie) |
| Role Entities | Extract features(s) of the same datum type from an end user utterance based on a model and store each value in the appropriate entities' slot | "Get a hotel room checking in on Monday and checking out on Friday." | DATE datum type role entity model extracts the values "Monday" and "Friday" and determines, based on the sentence context, that "Monday" should be normalized and stored in the checkInDate entity and "Friday" should be normalized and stored in the checkOutDate entity. |
| Role Entity Using TEXT Datum | Extract features(s) of the TEXT datum type from an end user utterance based on a model and store each value in the appropriate entities' slot | "Please transfer $50,000 from my XYZ Bank Super Checking to my ABC Bank Deluxe Savings." | TEXT datum type role entity model extracts the values "XYZ Bank Super Checking" and "ABC Bank Deluxe Savings" and stores "XYZ Bank Super Checking" in the transferFromAccount entity and "ABC Bank Deluxe Savings" in the transferToAccount entity. |
| Role Entity Using Custom Datum | Extract features(s) from an end user utterance by referencing a gazetteer or grammar and based on a model store each value in the appropriate entities' slots | "Provide me with a plane ticket from newark to dallas." | Gazetteer includes various city names in which there are airports to which the airline flies. The role entity model in conjunction with the Gazetteer determines which city fits into the appropriate role entity and normalizes the value to the appropriate airport code - newark would be extracted, normalized to EWR, and stored in the airportFrom role entity and dallas would be extracted, normalized to DFW, and stored in the airportTo role entity. |
| Spanless Entity | Analyze the entire end user response and given a model determine which class (label) is the best match then fill the entity's slot with that class/label | "There are two of us and we each need our own bed." | Spanless entity model analyzes the full sentence and the context of the sentence to determine which provided class the utterance meaning best fits. The model determines that the sentence best fits in the doubleRoom class, which represents a room with two beds. The spanless entity stores the value doubleRoom. |

# Create a Conceptual Model
Amelia uses at least two models to understand natural language about a topic. An intent model trains her to understand goals for the topic, for example, to reset a password. Entity models help Amelia extract data needed to perform a task that a person might describe different ways, for example, to understand Office and Microsoft Office are the same software package.
There can be only one intent model for each domain but multiple entity models. Mixing user intent goals for an IT help desk with HR vacation policies would confuse and make training more difficult.
For each model, best practice is to create one data set for baseline testing over time and a second training data set to optimize Amelia's performance.
## Create a Test Data Set
The first step to creating a high performing classifier model is to create a test set. The test set should be an extensive list of correctly labeled utterances end users will say. It should be about 20% the size of the training data set. This Validation data set should be a static baseline to test the training. As the model is revised over time, the Validation data set should remain the same so that it is clear how any changes to the model affect the scoring of the validation.
## Create a Training Data Set
Unlike the test data set, the training data set should be an evolving set of utterances organized by labels. Start with 50-100 utterances per intent class plus a negative data set that includes both in-domain and out-of-domain example utterances. Hundreds of utterances per label are not needed. In practice, the distribution of utterances among the labels is the most influential property on classifier model performance.
Always remember, quality not quantity. Training utterances should be different from test utterances.
Training data also should be well thought out to capture a large variety of utterances, not repeat similar ones. The data set should have variety in sentence structure and word choice. Repeating the same sentence structures – for example, "I want" – causes Amelia to tag every instance of that structure with the same intent label, right or wrong.
One person might create the training data set, train the model, and revise the model while another person creates the validation test data set given only the use case and customer journey and the audience. This can help minimize the likelihood that creation of the training data set will not influence the validation data set and vice versa.
# Test and Refine a Conceptual Model
Once data sets for testing and training have been created, the next steps are to train, test, and refine classifier models.
## Train and Iterate Data Sets
When training a model, it may be easier to take an iterative approach. For example, if there are five intents and a set of negative utterances – both in-domain and out-of-domain, start off creating a model with only one intent and negatives. Then look at the model statistics to determine what to do next. If the statistics show confusion between the two classes, revise the model. If not, add another intent data set, retrain the model, check the statistics, and repeat. The data set used to create the validation training model should be about 20% the size of the complete training data set.
After making updates, always run regression tests. Because training is additive, re-uploading an entire training data set is not needed.
## Training Algorithms
The best algorithm to use depends on the use case, utterances, negatives, test results, and other factors. The recommended algorithm is the Meta Classifier because it creates the most accurate model using the five linear algorithms. The Meta Classifier starts with the default settings for the linear algorithms – Passive Aggressive, Linear SVM, Logistic Regression, Confidence Weighted, and Soft Confidence Weighted – and runs a random search through the hyperparameters of all five models.
The Deep Neural Network algorithm requires more data and time for training to evaluate the data.
### Intent Training
Table. Intent Training Algorithms

| Algorithm | Description |
| ----|----|
| Passive Aggressive | Allows for multiclass, single label classification |
| Linear SVM | Similar to Passive Aggressive, maximizes the distances between classes. Useful when two intents have data sets with similar example utterances (e.g., make a hotel reservation vs. cancel a hotel reservation) |
| Logistic Regression | Produces scores that can be interpreted as probabilities which can be used to create thresholds to control the precision of the classifier. (I don’t believe there is currently a way to use those thresholds directly though. |
| Confidence Weighted | Takes parameter confidence information into account. The Adaptive margin property assigns different margins for different instances via a probability formulation. |
| Soft Confidence Weighted | Includes a parameter similar to Passive Aggressive to temper updating strategy. |
| Deep Neural Network | Bidirectional Long Short-Term Memory (LSTM) model – can work well with larger data sets. |

### Entity Training
Table. Entity Training Algorithms

| Algorithm | Description |
| ----|----|
| Passive Aggressive Tagger | Similar to Passive Aggressive for intents but this is a Passive Aggressive tagger. |
| Linear SVM Tagger | Works well when entities are a length of 1-2 tokens. Can work well when there is less data available. |
| Conditional Random Field (CRF) | Hands long distance dependencies well as it considers “neighboring” samples, meaning it can work with entities that are more than two tokens long. Tokens (values to be extracted) should be contiguous and order should be important. A larger data set may be needed. |
| Deep Neural Network | Bidirectional Long Short-Term Memory (LSTM) model – can work well with larger data sets. Given sufficient training data, the Deep Neural Network (DNN) tagger is expected to perform better than both linear models, without the need for gazetteer features. |

The Passive Aggressive and Linear SVM Taggers work differently than the Conditional Random Field (CRF) Tagger.
The Passive Aggressive and Linear SVM Taggers both tag sentences sequentially. They base predictions of the next token in the sequence only on the immediate previous predictions, not later predictions, as well as locally extracted features. This works well for single-word entities, or short phrasal entities like named entities, where there are no real dependencies between entities, and the prediction of the entity can be mostly based on its first few tokens.
The CRF tagger, however, learns the probability of transitions between labels in a sequence then maximizes the probability across the whole sequence of tokens. In practice, this means CRF does better for longer sequences of labels, entities with more words, when the label of the whole entity depends more on later tokens in the entity instead of the first few tokens. CRF also uses a transition matrix to estimate transition weights which requires more training data than Passive Aggressive or Linear SVM taggers.
Both of these taggers typically need gazetteers to perform well in tagging tasks.
## Use Model Statistics
Two screens are useful to help refine the performance of classifier models. The Statistics screen displays accuracy performance while the Misclassifications screen identifies test utterances that could not be classified.
Both screens are visible from the Dashboard workspace which, in turn, is located in Amelia's administration pages by clicking the Amelia Trainer link on the left side then clicking the Dashboard link. The Stats icons, when clicked, display a Models Evaluation popup with icons to display Statistics, Confusion Matrix, and Misclassifications for the selected model.
![](attachments/11939562/11944105.png)
Figure. Amelia Trainer Dashboard Example
### Statistics
The Statistics screen displays scores for a variety of standard machine learning metrics.
![](attachments/11939562/11944106.png)
Figure. Statistics Results Screen
Table. Statics Results Headings

| Heading | Description |
| ----|----|
| Correct | True positives where the model predicts the correct class. |
| Actual | True Positives + False Negatives. The number of actual occurrences of this intent/entity in the data set. |
| Predicted | True Positives + False Positives. The number of times the classifier predicted this intent/entity in the data set. |
| Precision | What proportion of positive identifications were actually correct? Correct divided by System. |
| Recall | What proportion of actual positives was identified correctly? Correct divided by Gold. |
| F1 | The average of Precision and Recall (harmonic mean). (2*(Precision*Recall)/(Precision+Recall)) |

### Misclassifications
The Misclassifications screen shows which specific utterances were either labeled as something incorrect (not what was in the test set), or not labeled at all.
> [!info]  
>
> When model training begins, Amelia knows nothing. Her first several predictions of which label an utterance belongs to are essentially guesses, so there will likely be some misses in any model that is trained.

![](attachments/11939562/11944107.png)
Figure. Misclassifications Results Screen
After reviewing these metrics, there probably will be imbalances in the training data that needs to be corrected. There are several options to consider.
-   Strengthen a label by adding more utterances containing key phrases
-   Weaken a label by removing utterances containing key phrases
-   Reclassify some utterances to different labels
Please do NOT just add more data. The data set should have variety in sentence structure and word choice. Repeating the same sentence structures – for example, the same beginning phrase such as “I want to book a room”, “I want to get a room”, “I want to reserve a room” – will likely overfit the sentence structure. Every time a person says to Amelia, “I want to” whatever, she will match the overfitted label.
After making any changes to your training data you should retrain your model and run it against the same validation set to see how your results changed, repeating this process until the overall statistics for your model have improved in a balanced way (i.e., the validation statistics for one intent have not significantly dropped in lieu of the validation statistics for another improving a little)
# Store and Maintain Models
Ideally, all classifier data should be stored in a version control repository and updated with any changes. The repository is a resource for new projects and projects looking to expand their data sets.
Utterances that did not cause Amelia to return the correct label should not be put into a training set and used to retrain. Instead, these utterances should be put in the test data set.
Then experiment by adding and removing different variations of the missed utterances into the training set until the utterances added to the test set no longer miss with no regressions. Analyze sentence structure and word choice in the missed utterances, as well as those of the current training data set, to determine how to revise the training data to retrain the model. The new different utterances should not be identical to the utterances that didn't return a correct label.
Repeat this process until the model performance is optimized. Once changes are made, check into version control the new training set, test set, and classifier model.
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-9-4_15-36-11.png](attachments/11939562/11939563.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-4_15-33-10.png](attachments/11939562/11939564.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-4_15-32-16.png](attachments/11939562/11939565.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-4-9_10-41-5.png](attachments/11939562/11944105.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-4-9_10-43-31.png](attachments/11939562/11944106.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-4-9_10-44-13.png](attachments/11939562/11944107.png) (image/png)  
