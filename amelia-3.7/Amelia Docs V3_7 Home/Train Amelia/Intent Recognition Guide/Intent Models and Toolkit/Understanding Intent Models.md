{% version "3.x" %}
In most Amelia deployments, the intent model does the lion's share of intent recognition. This page describes intent models and what models can achieve, as well as how to approach training and validating a model and then how to build, analyze and optimize it.
# What the Intent Model Is and Isn't
As with any tool, the intent model should be used for what it's designed to do, not something it's not designed to do. 
## What the Intent Model Is
In the intent model, intent recognition takes place by classification of natural language utterances, using supervised machine learning and natural language processing.
### Supervised Machine Learning
When an intent model is trained, supervised machine learning (as opposed to unsupervised machine learning) is used. Simplified, this works as follows:
1.  Build a training data set. With Amelia, this is a set of example end user utterances mapped to their respective intents or, in the case of the utterances that have no intent, utterances are mapped to the negative class.
2.  Select an algorithm. With Amelia, there is a selection of algorithms to choose from, all tailor-made to process exactly the kind of language data in the training data set.
3.  Train the algorithm on the training data. This is the supervised learning. Supervised learning does not mean memorizing utterance X maps to class Z. Instead, the training data is analyzed to identify the relevant combinations of patterns that best map an input (the training data) to an output (the class). It is learning to generalize beyond exactly what the training data tells it.
4.  This training/learning process results in a model. This model is used to determine the intent (or lack of intent) of whatever end users say to Amelia. In mathematical terms, the model is a function: it's what determines the output (the assigned class), given the input (the user utterance).
### Classification
As touched on above, the intent model operates with classification, not regression. As Amelia converses with people, the model classifies user utterances as best it can into the best-fitting class out of all of the classes defined. These classes are the intents and the negative class.
### Natural Language Processing
There is a significant natural language processing component in the intent model. Language data is critical for how the intent model is trained and the user utterances it processes. The model must read language data as smartly as possible. How this works depends on the learning algorithm used, as well as any pre-processing. Here are a few examples of how natural language processing works:
Take the utterance: "Hi, I wanted to check the balance of my bank accounts."
-   On a basic level, natural language processing helps Amelia understand the word accounts is the same word as account. If the intent model is trained only with utterances using the word account, Amelia will connect account singular to accounts plural. This simplifies training. It's not necessary to train the model for all possible variations of the same words.
<!-- -->
-   On a more advanced level, using advanced learning algorithms, the intent model will read and assess words in context. For example, in the utterance above, the word bank will be read differently than if it appeared in the utterance, "We were walking along the river bank." The algorithm has a pre-trained understanding that bank in the first utterance context, a financial institution, has a substantially different meaning from bank in the second utterance context, a landform.
## What the Intent Model Isn't
### Search
The intent model is built for classification, not for search. Therefore, avoid using the classifier as a keyword search engine. Training an intent model as a search tool, as if it is a search algorithm, will yield bad results. It forces the intent model algorithm to do something it's not designed to do.
Although simplified, this table shows a few key differences between classification and search:

| Classification | Search |
| ----|----|
| Has pre-defined intent classes to organize parts of an utterance. With Amelia, those classes are the various intents plus the negative class (the unlabeled training utterances that help her understand words similar but unrelated to the intent). As best it can, the classifier predicts what;class the user utterance belongs to. | Does not have pre-defined classes. Instead, the search algorithm aims to spot relevant documents, for example web pages, within an unstructured mass of information. |
| Looks at context. For example, asking to check a bank balance is different than saying we walked along a river bank. | Typically looks mainly at keywords, not context. |
| Has structured (classified) training data. As such the performance of algorithm is highly dependent on the quality of the training data. | Does not have structured data to train on. |
| Best for high value information, that is, information with concentrated meaning (like a user utterance). | Best for large volumes of disorganized information (like a collection of web pages). |

### Similarity Matching
The intent model is built for pattern matching, not similarity or matching. When the intent model training process analyzes a user utterance, it does not look for similar utterances in the data set. Instead, training looks for similar patterns in the training data. The model is attuned to patterns that are frequently used for a given intent, and rarely used for other intents. In this example, the most relevant patterns are in bold:
“Hey Amelia, **I can’t login**. Been on vacation, and have **forgotten my password**.”
The patterns in bold indicate the intent. With an adequate training data set, the model will be trained on utterances with similar patterns – though not necessarily similar utterances – for the relevant intent. To predict the correct intent, the classifier will find a high match in these patterns that also are rarely present in the data for other intents.
This doesn’t mean the classifier won’t hit correctly when the user utterance is nearly identical to a training data utterance. It will hit correctly. However, the match happens because those utterances have relevant similar patterns, not because the utterances are almost identical.
To train an intent model as a similarity matching algorithm requires training data to be populated with all ways to express an utterance, with these consequences:
-   Training data will become unsustainable to maintain. The intent model is designed to build a comparatively small and manageable tool that can generalize beyond its training data. Because there are semi-infinite ways to express an intent in natural language, a concise model that can generalize is a better solution. As an aside, if there's a very limited set of ways to express an intent, building and using a classifier for the intent might be a waste of time.
-   Use of the training data will inevitably lead to overtraining, as defined below. Intelligence in the model will be lost.
> [!info]  
>
> **Example**
>
> Every utterance that fails in the intent model is added into our training data. After a while, not only has the training data become bloated and unmanageable, but the intent model has become extremely overtrained and lost a lot of nuance in its understanding of user utterances.
>
> One intent is for resetting a password. However, because so many training data utterances for this have been added, the model now often trigger the reset password intent as long as the user mentions the words password or reset. The intent model has become a low-level keyword matching engine not a concise intent model that can generalize based on sophisticated pattern matching.
>
> In Amelia, grammars or tabular data are the best tools for similarity matching against a smaller set of expected utterances. In some cases, Ask task edge expressions in a BPN process also work if the expected utterances are few or have unique patterns.

# The Goal of the Intent Model
Understanding the goal of intent recognition provides a deeper understanding of how intent recognition works.
## Maximizing Predictive Performance on Unseen Utterances
The goal of the intent model is to have the best possible predictive performance on utterances that have not been used with the model.
Intent models must account for the semi-infinite ways to express a given intent. Pre-training an intent model to identify all possible expressions is impossible. A rule based approach is too narrow. Similarity matching won't scale.
The solution is to train a tool to use patterns to predict the intent of an utterance with high accuracy, whether the utterance has been used with the model before or not. The goal of an intent model is to generalize beyond its training data into all the utterances it will encounter in Amelia's conversations. The predictive performance and power determines the success or failure or an intent model.
There are training practices that create intent models that perform well with utterances beyond their training data.
## Building a Balanced Model
A balanced model generalizes well with unknown utterances and results in high intent recognition.
### Finding the Perfect Balance
Start by thinking of signal and noise. When the user says something to Amelia, the intent model should:
1.  Capture the patterns in the user utterance that indicate its intent class. These patterns are the signal. The model should be attuned to the signal for the correct intent class for the utterance.
2.  Ignore the patterns in the user utterance that do not indicate the intent class. These patterns are noise. The model should avoid noise because it provides no meaningful indication of the correct intent class for the utterance.
This is a simplification, however. Signal and noise are not binary. Instead, patterns in utterances are a spectrum with shades and nuance. Some patterns send out stronger signals than other patterns. Some patterns are more noisy than other patterns.
The goal of a balanced and attuned intent model, for every intent class, is to capture as much signal as possible and as little noise as possible.
This can be illustrated with an example:
> [!info]  
>
> Example
>
> User: “Hey Amelia, my password has expired. I’d like for you to reset it. Can you help me with that?”
>
> In simplified terms, the parts in **bold **can be considered signal for the intent ResetPassword, while the remaining parts are noise for that intent.

This binary signal and noise understanding is not quite accurate, as shown in this more nuanced example:
> [!info]  
>
> Example
>
> User: “Hey Amelia, my password has expired. I’d like for you to reset it. Can you help me with that?”
>
> Assume language patterns about resetting pop up in utterances for multiple distinct intents, for example, to reset settings and reset passwords. In that case, the bold and underlined words are a stronger signal for the intent ResetPassword class than the parts in bold.

To be more precise, consider the relevance of the signal relative to other classes in the model. A pattern can resonate strongly with classes A and B, but not at all with class C. If so, it's a strong signal for class A relative to class C, but not a strong signal for class A relative to class B:
> [!info]  
>
> Example
>
> “Hey Amelia, <u>**my password has expired**</u>. I’d like for you **to reset it**. *Can you help me with that?*”
>
> The pattern in italics can be considered a mild signal because it indicates a request. This suggests the italicized pattern is more likely to be an intent than belong to the negative class. Relative to the negative class, it’s a mild signal.
>
> At the same time, it probably doesn’t provide any indication as to exactly what intent is correct. Relative to the other intents, the pattern in italics is still noise.

## Avoiding Overtraining and Undertraining (Overfitting and Underfitting)
To understand balanced models, it's useful to understand unbalanced models. A balanced model is a model that is neither overtrained nor undertrained. Unbalanced models are overtrained or undertrained.
-   Overtraining (overfitting) –  This occurs when an intent model is too closely aligned with the training data. The model often will be unable to distinguish accurately between signal and noise. When a model evaluates if an utterance pattern matches to an intent, it can easily read both signal and noise as signal.
-   **Undertraining (un**derfitting) –  This occurs when an intent model is unable to capture the underlying structure of the training data. The model often won't be able to pick up any signal at all. When a model evaluates if an utterance pattern matches to an intent, it won't be able to recognize the signal as signal, but will instead mistake it for noise.
A balanced model lies in between these two. It balances curiosity with skepticism. It is curious enough to seek out and identify the signal, but skeptical enough to avoid picking up noise at the same time. In the table below are different ways to conceptualize these differences.

| Overtrained Model (Overfitting) | Undertrained Model (Underfitting) |
| ----|----|
| Captures both signal and noise as signal, as it's unable to distinguish between the two | Hardly picks up any noise, but hardly picks up any signal either |
| Has memorized the training data, but not understood it | Was unable to make sense of and understand the training data |
| In tune / Attuned | Out of tune |
| Is fit too tightly to the training data | Is fit too loosely to the training data |
| Is on steroids | Is anemic |
| Is too greedy | Is too modest |
| Is too strong | Is too weak |
| Is too trigger-happy | Is too slow to pull the trigger |
| Mistakes noise for signal | Mistakes signal for radio silence |

> [!info]  
>
> Example
>
> There are two tiny sample sets of utterances for the intent BookHotelRoom. They are too small to use in a model, but they can illustrate what overtraining and undertraining looks like in utterance data.
>
> -   The overtrained intent might easily fire off on any utterance including words like book, room or “I want to,” no matter the actual intent. It will read noise as signal ("I want to") and overestimate the strength of a signal (book - which also can be used to book a hotel restaurant table).
> -   The **undertrained** intent may never fire off at all, as the training data is so varied it has no relevant common patterns. It won't know what signal to look for.
>
> 
> | Overtrained Intent | Undertrained Intent |
> | ----|----|
> | I want to book a room | I want to book a room |
> | Want to book a room | Do you have anything free Saturday-Sunday? |
> | Wanting to book a room, thanks | Need the wedding suite 15-17 June |
> | I wanted to book a room, if possible | Can you house two people tomorrow? |
> | Want you to book a room for me | What’s the availability this weekend? |
> | What do I do if I want to book a room? | I’d like a place to stay for four next week |
> | How can I book a room? | Have something for two persons on your top floor for Easter? |
> | Please book a room for me and my wife | Who do I speak to to make a reservation? |
> | Hi, I want to book a room | Any help with getting me overnight accommodation |
> | Book a room | In need of a single bed for three nights |
> 

**More from the Intent Recognition Guide**
-   [Introduction to Intent Recognition](Introduction%20to%20Intent%20Recognition)
-   [Intent Scope](Intent%20Scope)
-   [Intent Architecture](Intent%20Architecture)
-   [Intent Models and Toolkit](Intent%20Models%20and%20Toolkit)
    -   [The Intent Model (Not Used)](The%20Intent%20Model%20_Not%20Used_)
    -   [Understanding Intent Models](Understanding%20Intent%20Models)
    -   [Training the Intent Model](Training%20the%20Intent%20Model)
    -   [Validating the Intent Model](Validating%20the%20Intent%20Model)
    -   [Collecting and Sourcing Data](Collecting%20and%20Sourcing%20Data)
    -   [Building the Intent Model](Building%20the%20Intent%20Model)
    -   [Data Curation](Data%20Curation)
-   [End User Utterance and Behavior](End%20User%20Utterance%20and%20Behavior)
-   [Measuring Intent Recognition](Measuring%20Intent%20Recognition)
-   [Intent Recognition Resources](Intent%20Recognition%20Resources)
-   [Intent Recognition FAQ](Intent%20Recognition%20FAQ)
{% /version %}
