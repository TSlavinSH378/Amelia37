{% version "3.x" %}
How well an intent model is trained determines the ability of the model to process a live user utterance then generalize it to match similar patterns in the training data that map to an intent. Three topics determine the quality of training data and intent model training.
-   Training Data Best Practices
-   Pre-processing and Feature Extraction
-   Algorithms
> [!warning]  
>
> When training an intent model, always validate the model frequently, as described in [Validating the Intent Model](Validating%20the%20Intent%20Model). For the process of grooming and improving training data, see [Building, Analyzing and Optimizing the Intent Model](Building%20the%20Intent%20Model).

# Training Data Best Practices
Training data is a collection of example utterances used to teach a model to understand what characterizes the various intent classes and, therefore, the differences between utterances. The model uses utterance differences to predict the class of live utterances.
Creating, evaluating, and tailoring training data is where most time is spent when working on a model. Ideally, training data should be complete, balanced, and consistent, among other qualities.
## Complete
To train a complete model, use various three types of example utterances (data).

| INTENT DATA | NEGATIVE DATA |
| ----|----|
| When users express an intent, the model must be trained to recognize that intent.The model must be trained in example utterances for each intent;the intent model must be able to recognize. The combined training data for all the various intents, is called the intent data.
 | When the user says something that does;not express any intent, the model must be trained to understand the distinction. The utterance belongs to the negative (no intent) class.While this class is a single big class in the intent model, this data has two categories. For good data management, keep separate the data for these two categories. |
| In-Domain Negative DataAs users converse with Amelia, they will often say things that have a topical and/or linguistic relation to an intent, but does;not express that intent. To avoid these utterances mistakenly triggering intents, train the negative class in this type of utterance. They are crucial to balance the intents with respect to the negative class.For each intent class, train the negative class to recognize utterances that have a topical and/or linguistic relation to that intent, but do not express the intent (or any other intent).This type of negative class is called in-domain negative data. | Out-of-Domain Negative DataSimilarly, train the negative class to recognize all the things users may say to Amelia in the course of a conversation, that have no topical or linguistic relation to any intents.This type of negative class is called;out-of-domain negative data. |

> [!info]  
>
> **Example**
>
> The table below shows three tiny outtakes of sample data:
>
> 
> |  |  |  |
> | ----|----|----|
> | Intent Data (for the intent BookHotelRoom) | In-Domain Negative Data | Out-of-Domain Negative Data |
> | I want to book a room. | the room was booked for a period of two weeks | i'm well. what can you do for me? |
> | Can you help me reserve a suite for summer holidays? | i'd like to book a restaurant table | how come we didn't hear that song previously |
> | We'd like to stay at your hotel for the next weekend. Anything available? | We were quite happy with the room we booked. | We filed a police report over the stolen motorcycle. |
> | Do you have any free rooms Wednesday through Saturday? | Will the hotel book the guided tour? | I wish they didn't cancel that show |
> | I have an upcoming business trip, so wanted check what your hotel had to offer between the 22nd to the 27th. | I was reading a book while on vacation | who does the banana dance? |
> | Could I make a booking for a double room for me and my wife for first week of July, thanks | how can we change a hotel room booking we made | hello, how are you? |
> 
>
>   

## Balanced
Balancing the volume of the various intent classes* *is important in training data, to avoid biasing the model towards any classes based on sheer volume.
To ensure validation results are balanced, ensure that the validation set has both:
-   A good distribution of tests across the relevant classes.
-   A decent volume balance compared to the training data set, to ensure the validation set and training set are not too similar.

| Intent Data |
| ----|
| VolumeFor each intent, there should usually be at least 50 example training utterances. More often, around a 100 utterances per intent is ideal. But this is highly dependent upon the nature of the intent as well as what algorithm we use (more on this below).If starting to build a model, without access to a large pool of good utterances, then 50 utterances per intent may be a decent foundation to start. The number can be expanded as the model is tested and augmented.[!warning]
Do not add more utterances to add more volume, if that means the quality of the utterances has been compromised. Typically, it may mean start adding utterances that are very similar to utterances already in the training set. 75 example utterances with good variation is better than 100 utterances with little variation.  Distribution across intentsIf one intent is trained with ten times more example utterances than other intents, there's a high risk that the intent will be overtrained compared to the others. As a rule of thumb, the amount of training data should be reasonably balanced between intents.However, this is certainly not an absolute rule. Often, for narrow highly specific intents, there will be fewer ways to express the intent. For broader low specificity intents, there are many more ways to describe the intent in utterances. The broader intents require a greater volume of training data while narrow intents will require a lesser volume. |
| VolumeIn many cases, there should be about as many in-domain negative utterances as intent utterances.However, the ratio between intent utterances and in-domain negatives utterances can depend on a number of factors:In some Amelia deployments, it may not be a big deal if intents sometimes fire when they shouldn't. If so, consider having fewer in-domain negatives. In other Amelia deployments, the opposite may be true, limiting misfires as much as possible is important. More in-domain negative utterances in the training data than intent utterances might be a good approach.Some Amelia deployments have very comprehensive intent models because users very rarely ask for anything that's not an intent. If so, training relatively fewer in-domain negatives is appropriate. Other Amelia deployments have less comprehensive intent models, in which case relatively more in-domain negatives might work best.In some Amelia deployments, users will have a very good understanding of what Amelia can and cannot do, and will tend to be very precise in what they ask for. This might reduce the need for in-domain negatives. In other Amelia deployments, it may be upside down, and more in-domain negatives might be needed.Finally, the need for in-domain negatives may change depending on the algorithm used to train a model. Deep neural networks models tend to require less in-domain negatives than models using linear algorithms.This balance is important, and often difficult. But if balancing the model with sufficient in-domain negative utterances is neglected, there's a high risk that intents will mistakenly fire off too often. |
| VolumeTo train the model for out-of-domain negatives, use a big data set that contains thousands of generic utterances.For intents and in-domain negatives, maintaining good balances can be a fine line to walk. For the out-of-domain negatives, however, it's less of an issue. Training data for intents is usually very different from the training data for the out-of-domain negatives. For the out-of-domain negatives, a big data set of several thousands utterances will usually work well out-of-the-box, with less fine-tuning needed. |

> [!info]  
>
> Example 1
>
> There are two intents ResetEmailPassword and ProblemWithAccount.
>
> ResetEmailPassword is a very narrow intent, as it specifically only covers a single issue, for example, resetting an email password. This intent trains with 75 example utterances in the training data. ProblemWithAccount is much broader. The intent covers any problem the user may have with their account, for example, being locked out, unable to change account details, forgotten account password, unable to activate a new account, and so on. This intent trains with 150 example utterances.
>
> While this appears unbalanced, 75 utterances for one intent and 150 utterances for the second intent, it could be a decent balance given one intent is narrow and the other is broad.
>
> Example 2
>
> The intent SetUpDoctorsAppointment is trained with 100 utterances. But in the hurry to go live, there is no training with in-domain negatives for this intent.
>
> The result is a lack of balance in the model. Chat log analysis shows this intent has triggered frequently on utterances related to doctor's appointments but do not express an intent to set up an appointment. For example:
>
> User: "I visited doctor Jones last Monday, but haven't received the prescription drugs yet."
>
> User: "The insurance should cover my doctor's appointment fee."

## Consistent
When utterances are labelled with their correct intent, or as negatives, it's extremely important to be consistent in what utterances are considered to belong to what intent class. This may sound obvious, but it's very easy to go wrong:
-   In part because training data can have thousands of lines of utterances, and labels accidentally labeled incorrectly does happen.
-   In part because labelling utterances can sometimes be subjective. Two similar utterances that express the same sentiment can be labeled differently. Sometimes it is a judgment call if a certain type of utterances should belong to intent A or if they should belong to the negative class.
When this happens, the training data becomes schizophrenic. A single mislabeled utterance will undo the good work of many correctly labeled utterances. The result is a confused model. It's vital all utterances and labels have full consistency:
-   Within the training data set.
-   Between the training data and the validation data. If consistency is lacking between them, the validation data won't test what has been trained, but something different, which then will fail. This doesn't apply if cross-validation is used, in which case the training data is the validation data.
People working on the data need to agree on these judgment calls. To ensure consistency, confirm all data changes with one person who has a full overview of the data and deep knowledge of Amelia's role.
> [!info]  
>
> Example:
>
> There is an intent to CheckInvoiceDetails. In the training data, there are the following two utterances:
>
> "I'm wondering about this invoice."
>
> "I have a question about my last invoice."
>
> It can be subjective whether or not these two utterances should trigger the intent CheckInvoiceDetails. But it's vital to decide then stay consistent in how these subjective questions are interpreted. If one utterance is labelled as CheckInvoiceDetails, and the other as negative, the training of the model will be inconsistent. This result is a confused model.
>
> If there are a lot of these subjective utterances in an intent, that may signal that the intent is not sufficiently well defined and, as a result, maybe the intent should be [re-shaped in the intent architecture](Intent%20Architecture).

## Varied
For the utterances used to train a given intent class, ensure is a good variation. There are two primary reasons for this:
-   Avoid overtraining – Any class with low variation in the training data has a high risk of overtraining. If the intent ResetPassword is trained with lots of very similar utterances containing words like "reset" and "password", the risk is teaching the model that this intent should fire no matter what, as long as the user utterance contains a couple of the right words. 
-   **Reach **– With good variation comes good reach. The aim of the model is to be able to extrapolate to live utterances. For this to happen, expose the model to a wide variety of ways to express an intent, to use as a basis for the generalization it will do live. More often than not, end users are more creative in how they express their intents than is anticipated and planned. Try to prepare each model for that creativity by having good variation in the training data.
> [!info]  
>
> **Example**
>
> Below is a small sample data set for the intent BookHotelRoom. Imagine a full data set is scaled up with more utterances. The training data with too little variation will give an overtrained intent model with low reach, while the good variation set will give a much more healthy model.
>
> 
> | Too Little Variation | Good Variation |
> | ----|----|
> | I want to book a room | I want to book a room. |
> | Want to book a room. | Can you help me reserve a suite for summer holidays? |
> | Wanting to book a room, thanks | We'd like to stay at your hotel for the next weekend. Anything available? |
> | Want you to book a room for me | Do you have any free rooms Wednesday through Saturday? |
> | What do I do if I want to book a room? | I have an upcoming business trip, so wanted check what your hotel had to offer between the 22nd to the 27th. |
> | How can I book a room? | Could I make a booking for a double room for me and my wife for first week of July, thanks |
> | Please book a room for me and my wife | Please make a reservation for a single room for this Monday, including breakfast. |
> 

## Unambiguous
Training data utterances should be unambiguous. If it's unclear whether an utterance actually expresses a given intent or not, it does **not** belong in the training data. If ambiguous utterances are included in the training data, the borders between the classes will blur, resulting in a less effective model.
> [!info]  
>
> **Example**
>
> As part of her role, Amelia helps users with frequently asked questions concerning Outlook. The intent OutlookAttachment is for helping users with attachments. Utterances like the following, however, are ambiguous with respect to this intent:
>
> User: "I'm unable to send this picture in my email."
>
> This can either relate to pictures as attachments or pictures copied directly into the email itself.
>
> Utterances like this included in training data can lead to mistriggers because this intent is trained to fire on utterances that have nothing to do with attachments.

If there are many instances of utterances that could or could not express a given intent, maybe reevaluate the intent, re-assessing the [intent architecture](Intent%20Architecture). Possibly, the intent can be defined more clearly, maybe reshaped in small ways to make life easier both for ourselves and Amelia.
> [!info]  
>
> **Example**
>
> Picking up the example from above, to avoid confusion with pictures as attachments versus pasted into an email, do as follows:
>
> Reshape the intent to include **both** pictures as attachments **and** pictures in the email, and use an entity pick it out when users ask about pictures, images,  and so on. Amelia's answers in the BPN are changed accordingly.
>
> This approach removes the ambiguity and these utterances can be included in the training data.

## Clean
Training data should be clean by avoiding the inclusion of obvious noise in example utterances. Noise is irrelevant sections of the utterance that have absolutely no bearing on the intent. Because noise does not indicate the class, they should be cleaned from the training data to avoid imbalances.
> [!info]  
>
> **Example**
>
> In the table below, sections of the utterance that are pure noise are marked in red.
>
> 
> | Noisy | Clean |
> | ----|----|
> | Hi, how are you?;I have a complaint regarding the vacuum cleaner I bought last week. | I have a complaint regarding the vacuum cleaner I bought last week. |
> | I bought a mix master from you last year that now broke. Is still on warranty.;Yours truly, Tony Soprano | I bought a mix master from you last year that now broke. Is still on warranty. |
> | Amelia, are you a bot? Anyway,;the washing machine I purchased from seems to have shut down - no response when we try to turn it on. | the washing machine I purchased from seems to have shut down - no response when we try to turn it on. |
> 
>
>   

# Pre-processing and Feature Extraction
When Amelia analyzes an utterance to detect the intent, she doesn't read the utterance verbatim in its raw form. Amelia polishes the utterance to simplify intent recognition. This pre-processing is important to understand while working with training data.
Working with linear algorithms, pre-processing is customizable to address different needs. With deep neural network algorithms, pre-processing is not customizable.  Deep neural network algorithms can configure Negation which technically is not part of the pre-processing.
> [!warning]  
>
> Customizing normally won’t have a major impact on intent recognition. The benefits are potential minor specific improvements and simplification of some of training data work. When working to improve a model, fix any challenges by improving the training data. It's often quite simple to test customization, provided there is a [good validation set](Validating%20the%20Intent%20Model) to test. While the positive effect of algorithm customization may be small, it can be easy to test.

## Tokenization
All utterances are tokenized with a language specific tokenizer. With natural language in English, for example, spaces convert sentences into words which can be considered tokens. Amelia's algorithms segment pre-processed utterances in different ways to extract tokens and meaning from the utterance. For more on tokenization, see for example [the Wikipedia article](https://en.wikipedia.org/wiki/Lexical_analysis#Tokenization). Amelia’s tokenization is not customizable.
## Lemmatization
All words in an utterance are lemmatized, provided Amelia finds the word in her language specific lemmatizer dictionary. No matter how a word is inflected, Amelia will identify the word’s base form (the “lemma”) and use that as her input. This simplifies building training data because there's no need to include all forms in intent training data. Especially, for example, Italian, Spanish, and other Romance languages which can have 15 forms of a single verb.
> [!info]  
>
> **Example**
>
> forget, forgets, forgot, forgotten, forgetting → forget
>
> can't → can not

However, lemmatization introduces a few quirks. Amelia won’t distinguish between present and past from a verb form. For example, buy and bought will be pre-processed into the same base form, buy. However, if the inflection happens with a compound form like have bought, this can give Amelia an indication of tense. In this case, have bought would be pre-processed input as have and buy.  
Amelia’s lemmatization can be turned off. However, there are few or no cases where shutting off lemmatization improves training data.
## Normalization
When pre-processing utterances, Amelia performs a series of tasks to standardize words and numbers in the utterance. This makes evaluation of each utterance more predictable than using the raw utterance.
-   **Lowercase** – All letters are made lowercase, so *Yes* is normalized to *yes*. Case doesn't have to be taken into account in data sets.
-   **Normalize Digits** – Replaces every digit in a word with a hashtag or pound symbol, for example, 34.00 becomes ##.##.
-   **Normalize Unicode** – Replaces Unicode characters with their normalized ASCII form, for example, *ésta* becomes *esta*. Note that this does not mean words with and without Unicode characters will always be evaluated identically. The natural language parsing will take into account the Unicode characters, which in turn means the classifier can evaluate *ésta* and *esta* differently.
Normalization features can be added or removed in an intent model but the default will work best in most cases.
## Speech-to-Text Transcription
In voice implementations, speech-to-text (STT) technology transcribes speech to text before pre-processing happens. Amelia reads the transcribed text as she tries to predict the correct intent, or lack of intent, in an utterance. It's important for test utterances to mimic what transcribed text looks like when building and validating training data for voice implementations.
> [!info]  
>
> Many STT technologies do not add any punctuation into the transcribed text. If this is the case, the data we use to train and test Amelia should be similar, with no punctuation.

## Coreference Resolution
In natural language conversations, people use pronouns – this, that, they, these, she – to refer to details mentioned earlier. Amelia's pre-processing routines try to map pronouns back to their corresponding mentions.
> [!info]  
>
> **Example**
>
> In a conversation with Amelia, the end user needs to provide their username. In the implementation, there's also an intent for ForgottenUsername. Notice how Amelia uses coreference resolution to replace the pronoun in the user's second utterance, which gives her the chance to understand the utterance as an intent.
>
> Amelia: What is your username?
>
> User: I can't remember it. → *I can't remember \[your username\].*
>
> *ForgottenUsername intent fired*
>
> Amelia: "I'm happy to remind you of your username. Please provide your email address, and I will send it to you."

## Negation
Intents can be set to ignore a hit if the utterance is phrased with a direct negation of the intent. For example, for an intent DeactivateAccount, utterances similar to "Don't deactivate my account" could be set to be ignored while utterances similar to "Deactivate my account" would trigger this intent. Achieving the same result with training data is challenging because the patterns of negated utterances can be so similar to non-negated utterances.
Technically, this is not part of any pre-processing of training data because this operation is done outside of the model training process. Intents are defined in the Amelia Trainer section of Amelia's administration pages, as part of defining an intent, setting what happens when an utterance triggering an intent is negated. However, it's relevant for how training data can be shaped.
> [!info]  
>
> **Example**
>
> Amelia helps users manage their newspaper subscriptions. When users talk about changing or freezing their subscription, users specify they do **not **want to end their subscription. This might trigger the intent EndSubscription. However, when defining the intent, having selected to ignore the EndSubscription intent for when utterances triggering the EndSubscription are negated, negated utterances won't trigger the intent. And this risk won't have to be included in the training data for the negative class.
>
> User: "No, don't deactivate my subscription" - EndSubscription is hit, but negated, so the process associated with the intent is not executed.
>
> User: "Deactivate my subscription" - EndSubscription is hit and the process associated with the intent is executed.
> [!warning]  
>
> This functionality applies from 3.7.14 in normal models, from 3.7.17 in CQA models.

## Punctuation Filter
The punctuation filter filters out punctuation at the end of an utterance but not all punctuation. This happens for a few reasons:
-   Whether or not the user includes, for example, a full stop period at the end of an utterance or not, usually does not give an intent model any valuable indication of the intent. Identical utterances with and without ending punctuation may give different results, depending on the training data for a model.
-   It simplifies building training data. Variations of ending punctuation don't have to be included in the training data utterances to cover both scenarios.
This is the default regex to filter out symbols at the end of the utterance:
``` groovy
[!"#$%&'()*+,-./:;<=>@^_`{|}~\[\]\\]+
```
> [!warning]  
>
> The ending question mark (?) in the default regex is not filtered out by default, as this can often be considered a significant indication of intent in an utterance. In some cases the question mark might be useful to add.

The punctuation filter is customizable, so we can add or remove any symbol we’d like.
> [!warning]  
>
> To filter out in-sentence punctuation, use stop words (see below).

## Customized Dictionary Normalization (Macros / Synonyms / Misspellings)
To simplify training, as part of building an intent model, specified words can be pre-processed and normalized before evaluation by the model. For example, there might be long word lists for one concept. Normalizing every word in the list to one concept or word can strengthen intent recognition. Other uses include synonyms, misspellings, and so on.
> [!info]  
>
> Example 1
>
> Amelia works as a logistics and warehouse assistant in a company with a product line of 500 products. Some intents relate to products and the user utterance can mention any one of the 500 products. There is no way to include all 500 product names in the training data. And it's problematic to leave them out, as the intent model is then trained in utterances that are only partially representative.
>
> The solution is to normalize the 500 product names into a canonical variation and use that variation in the training data, for example, “where is PRODUCTX”, “check order status of PRODUCTX”, and so on.
>
> Example 2
>
> Amelia is deployed with a voice interface. An app called Coar is used by two intents. But the speech-to-text technology often misinterprets the app name and transcribes it as core or cure.
>
> Training data could include core and cure rather than Coar. Because core and cure are rarely used in any other context, normalize these two words to Coar to avoid this misunderstanding.
>
> Example 3
>
> In some languages, there are multiple words and spellings for the word email. For an intent that relates to email, it can be hard to train that intent well with all the variations without at the same time overtraining the training data.
>
> Take all those variations for the word email and normalize them to EMAIL.

# Algorithms and Feature Extraction
Different learning algorithms can be used to train an intent model. The algorithms process training data and extracts meaning. The most significant differences between algorithms is between linear and deep neural network algorithms. 
## Linear Algorithms
Linear algorithms take the words (unigrams) and word pairs (bigrams) of the training data as inputs. After pre-processing, unigrams and bigrams are the features the algorithm extracts from the training data.  This is called feature extraction.

| Utterance | Features |
| ----|----|
| "Renew my diamond card" | Unigrams: renew, my, diamond, cardBigrams: renew my, my diamond, diamond card |

This also can be customized. For example, bigrams can be replaced with syntactic bigrams which use the dependency parser in Amelia to extract bigrams according to the syntactic structure of the sentence:

| Utterance | Features |
| ----|----|
| "Renew my diamond card" | Unigrams: renew, my, diamond, cardSyntactic Bigrams: renew card, my card, diamond card |

## Deep Neural Networks (ELMo)
Deep neural network algorithms (DNN) are different from linear algorithms because they are pre-trained. Using huge text corpora, DNN algorithms have already learnt about common relations and correlations in language.
ELMo (Embeddings from Language Models) is a recent DNN approach to representing words for use in NLP machine learning applications. Representations for each word are computed dynamically for each sentence. The representations ELMo computes for the word bank will be drastically different in the sentence "We had a picnic on the river bank" than in the sentence "I deposited my paycheck at the bank."
When an intent model is trained with a DNN algorithm, the algorithm is doubly trained. It is already generically trained in normal patterns and structures of language - and then trained specifically to detect intents using Amelia's training data.
### Deep Neural Network Algorithms vs Linear Algorithms
DNN algorithms become substantially different from linear algorithms.
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 40%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr class="header">
<th class="confluenceTh" style="text-align: left;"><br />
</th>
<th class="confluenceTh" style="text-align: left;"><p>Linear Algorithm</p></th>
<th class="confluenceTh" style="text-align: left;"><p>Deep Neural Network (ELMo)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th class="confluenceTh" style="text-align: left;">Contextual Understanding</th>
<td class="confluenceTd" style="text-align: left;"><p>In linear algorithms, features are processed by the algorithm with no consideration to the context they appear in. Consider the following two utterances:</p>
<p>"We walked along the river bank."</p>
<p>"I want to open a new bank account."</p>
<p>In these, the word bank has two completely different meanings. Even so, a linear algorithm will evaluate bank identically in both utterances.</p>
<p>For linear algorithms, all words and features are equal.</p></td>
<td class="confluenceTd" style="text-align: left;"><p>In DNN algorithms, features are considered and weighed according to the context they appear in. Let's look at the same two utterances:</p>
<p>"We walked along the river bank."</p>
<p>"I want to open a new bank account."</p>
<p>In contrast to the linear algorithm, the DNN algorithm will look at the context to determine how it should read the word "bank".</p>
<p>For DNN algorithms, words and features are weighted.</p></td>
</tr>
<tr class="even">
<th class="confluenceTh" style="text-align: left;">Distance Understanding</th>
<td class="confluenceTd" style="text-align: left;"><p>Linear algorithms are unable to make the cognitive leap to understand a certain feature sometimes could have been a different feature, the way a synonym or a word that for practical purposes represent the same thing.</p>
<p>Here are two utterances for the intent AddMegabytes:</p>
<p>"I want to add two hundred megabytes to my phone."</p>
<p>"I want to add three hundred megabytes to my phone."</p>
<p>In this case, whether the user says two and three (or any other number) makes no difference in terms of the intent. So ideally, the intent model should evaluate these utterances identically, no matter what number of megabytes the user wants to add.</p>
<p>But a linear algorithm will not understand that the numbers are interchangeable. So if the training data for an intent has many instances of two but not three, then the chance of this intent firing off will be noticeably higher if an utterance contains the feature two than if it contains the feature three.</p></td>
<td class="confluenceTd" style="text-align: left;"><p>DNN algorithms can understand when there is some chance that a certain feature might be replaced by a different feature. Given the pre-training, it knows that feature 1 often appears in exactly the same contexts as feature 2. If the user says mentions feature 2, it assumes the user might instead have said feature 1. They have low distance.</p>
<p>Let's look at the same two utterances as to the left:</p>
<p>"I want to add two hundred megabytes to my phone."</p>
<p>"I want to add three hundred megabytes to my phone."</p>
<p>Given the pre-training of the algorithm, it knows that various numbers, no matter which number, often are used in same contexts.</p>
<p>DNN algorithms can extrapolate that, if the user said <em>three</em>, there's a good chance the number might have been <em>two</em> or any other number. With this understanding, it will then evaluate <em>two</em> and <em>three</em> in the utterances above more or less identically if the training data has lots of <em>two</em> and no <em>three</em>.</p></td>
</tr>
<tr class="odd">
<th class="confluenceTh" style="text-align: left;">Feature Extraction</th>
<td class="confluenceTd" style="text-align: left;">With linear algorithms, the feature extraction is defined beforehand and is static. Typically, it picks unigrams and bigrams.</td>
<td class="confluenceTd" style="text-align: left;">With DNN algorithms, the feature extraction is determined by the algorithm itself.</td>
</tr>
</tbody>
</table>
### DNN Algorithm Drawbacks
Overall, DNN algorithms tend to perform better than linear algorithms. However, they are not always the right choice. The table below describes the most important potential drawbacks using a DNN algorithm.

| 
 |
| ----|
| DNN algorithms require more training data than linear algorithms.So if training data is limited, linear algorithms may be the better choice. |
| Models using DNN algorithms take significantly longer to train than models using linear algorithms. For big models, with high volumes of training and validation data, it can take over an hour or two to train a model. This is especially true if cross-validation is used, which typically trains five extra models for validation purposes instead of training a single model.When models are trained frequently, it may be more practical to use a linear algorithm. Once the model is more mature, and updates are more rare, consider migrating to a DNN algorithm. |
| DNN models are pre-trained to understand words;in context. That's usually a benefit. However, if some key words are used in non-traditional ways, for example, part of product name, this can cause issues. The pre-training of those words may then be at odds with the actual use of those words in an Amelia deployment.If a lot of technical words are to be used, a lot of internal names, a linear algorithm might work best. |
| For DNN models, pre-processing and feature extraction cannot be customized.Given this, linear algorithms may be the better choice if it's important to customize pre-processing and feature extraction. |

# Thresholds / Confidence Scores
When a model processes a user utterance, it scores the utterance against every intent class the model is trained in. Scoring is expressed as a numerical score for each class. The higher the score, the better the match. Given the utterance, "I'd like to cancel my subscription, please", example scores might be CancelSubscription: 0.91, GetSubscription: 0.32, Negative: 0.23, and so on. 
Scores have a double purpose that create the two hurdles an intent class has to pass to become the predicted class:
-   **Competition (ranking)** *– *The score functions as a competition score with all available classes ranked according to their score. The top scoring class wins and is set to become the predicted class. In the example above, that's the class CancelSubscription. 
-   **Confidence (threshold)** *– *However, the score also represents a confidence score*, *a representation of how confident the model is that the utterance belongs to the class. If this confidence is not sufficiently high, even if it's the top score among the classes, then the model will still default to the negative class, whether or not the negative class was not the top scoring class. In addition to ranking first, the score has to pass a given threshold.
This threshold is customizable. As a model is trained, experiment with increasing or decreasing this threshold to find the threshold best aligned with the best overall results for the model. If there are a lot of false positives for utterances when an utterance should have hit the negative class, consider increasing the threshold score. If the opposite, consider reducing the threshold. 
All that said, this functionality is not an excuse to **not** work on the training data to fix issues. The main method to improve a model remains the training data. 
**More from the Intent Integration Guide**
Unable to render {children}. Page not found: How Amelia Recognizes Intent.
{% /version %}
