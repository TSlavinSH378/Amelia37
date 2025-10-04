{% version "3.x" %}
This guide describes the Amelia cognitive software system and provides instructions to help Amelia identify and improve the identification of the reasons users chat with her.
# Who is Amelia?
Amelia is a cognitive software agent who listens and interacts with people to solve problems. She reads natural language, understands context, applies logic, infers implications, learns through experience, and senses emotions. She understands what is meant, not only what a person says. Amelia can take on a wide variety of rote business and engineering tasks.
# How Does Amelia Work?
How Amelia works depends on circumstances. In some cases, she might help caregivers provide patient notes into a software system where the goal is always the same. In other cases, Amelia engages in a conversation to solve one or more problems. To solve problems, she must determine user intent then follow a dynamic process to complete the conversation and perform any tasks.
This document describes the second case, where Amelia determines user intent in a conversation then helps people accomplish one or more goals.
The intent model is the most important of several methods. Models help Amelia make reasonable judgements about context in the words and phrases of a conversation, for example, to book a hotel room and choose options like bed size. But some intents are better identified by means other than the intent model, or by using various methods in combination.
During a conversation, she also captures data she needs to perform any tasks, for example, check-in and check-out dates for a hotel stay. Captured data, called entities, are processed as the conversation evolves.
# What is Intent?
In cases where Amelia solves one or more problems, she engages people in conversation and parses their words to understand their intent, their reason to chat with her. Amelia uses their intent to decide what words to say, process to follow, and actions to perform. For example, if a person asks her, "I need my password reset," Amelia is trained to ask for information needed to reset a password then perform tasks to reset their password.
Of course, not all conversations reveal intent easily. If a person tells Amelia, "I can't access my account," she asks clarifying questions to determine if the problem is a password that doesn't work or another problem. She can disambiguate details which, in turn, reveal the real intent. Her ability to ask clarifying questions is a mix of pre-defined questions and Amelia predicting the correct question to ask based on conversation utterances.
Training Amelia to solve problems involves four factors that work together as well as sequentially to identify, create, organize, and detect user intent.
-   **Intent Scope** – A collection of one or more intents Amelia should recognize in a conversation based on the project goals.
-   **Intent Architecture** – How the intent scope is to be shaped, structured, and detected with an intent model and/or other methods.
-   **Intent Detection** – Techniques and analysis to determine how well intents are recognized by Amelia.
-   **User Utterance and Behavior** – How users express intents in their utterances and online conversational behaviors.
# Creating an Intent Scope
The intent scope is the complete set of intents Amelia ideally should recognize as part of her role or skill set. The word intent is used in its colloquial sense here, not as a technical term. For example, intents in this context are not tied to an intent model. 
The intent scope is where the bar is set for how high intent recognition can be achieved realistically in an Amelia deployment. With a simple intent scope, high intent recognition and minimal need for disambiguation is to be expected, and vice versa. 
Because a certain level of intent recognition, as well as a limited level of disambiguation, is often a critical success factor in any Amelia deployment, it’s vital that the intent scope is part of the conversation when Amelia’s roles and skills are selected and designed. If not, the risk is ending up with use cases that depend on unachievable levels of intent recognition to have value.
This document describes how to identify and evaluate intent scope.
# Creating an Intent Architecture
Once a tentative intent scope is defined, the next step is to consolidate the scope into an intent architecture. The architecture shapes intents and how they are structured, as well as the intent detection tools used to detect them. The goal is to design an intent scope and architecture that results in high intent recognition. This requires balancing accuracy and speed and weighing effort versus rewards.
Designing an intent architecture requires an awareness of all Amelia features related to intent recognition and how she works. This ensures the intent structure and scope have appropriate depth and completeness while intents are recognizable and easily distinguished from other intents.
Within an intent architecture, intent recognition can happen in layers or levels. For example, the intent model can recognize the user wants to sign up for insurance while a second layer identifies they want car insurance.
Finally, intent architectures can use a variety of tools and functionality, for example, classification models, grammars, and tabular data. Which tools and functionalities depends on the intent scope and project goals.
# Detecting Intents
To implement the intent architecture requires using a range of tools and functionality to create, optimize, and deploy intent models, in addition to other methods used to identify intent. Some high level details about intent models are described in this section. Other intent detection methods are described in the rest of this document.
## What is an Intent Model?
In deployments where Amelia works with people to solve problems, and she has to determine their intents and goals, an intent model is trained and deployed. An intent model uses words, phrases, and other data to help Amelia understand one or more topics she will encounter in conversations. The model can be updated based on experience.
Intent recognition in an intent model happens with classification of natural language utterances, natural language processing, and supervised machine learning to create an intent model. Natural language is the unconstructed casual way people talk. Supervised learning includes building training data sets from utterances people will say to Amelia, as well as other techniques and tools.
For example, here's some of the steps Amelia uses to evaluate and process the utterance, "Hi, I want to check the balance of my bank accounts."
-   On a basic level, natural language processing helps Amelia understand accounts is the same word as account. If the intent model is trained only with utterances using the word account, Amelia will be able to connect the dots from account to accounts. Training the model for all possible variations of the same words isn't necessary.
-   On a more advanced level, using machine learning algorithms, the intent model will read and assess words in context. For example, the word bank in the utterance above will be read differently than if it appeared in the utterance "We walked along the river bank." The algorithm has a pre-trained understanding that bank in the first context has a substantially different meaning from bank in the second context.
### How Intent Models Work
Intent models are built to break utterances and parts of utterances into pieces then classify them based on intents. They're not built for search. Do not use Amelia's classification tools as a keyword search engine. If the intent model is built as a search tool working with a search algorithm, the results will inevitably be bad. The intent models' algorithms will be forced to do something they're not designed to accomplish.
Although simplified, this table shows a few key differences between classification and search.
Table. Key Differences Between Classification and Search

| Classification | Search |
| ----|----|
| Has pre-defined intent classes to organize parts of an utterance. With Amelia, those classes are the various intents plus the negative class (the unlabeled training utterances that help her understand words similar but unrelated to the intent). As best it can, the classifier predicts what;class the user utterance belongs to. | Does not have pre-defined classes. Instead, the search algorithm aims to spot relevant documents, for example web pages, within an unstructured mass of information. |
| Looks at context. For example, asking to check a bank balance is different than saying we walked along a river bank. | Typically looks mainly at keywords, not context. |
| Has structured classified training data. As such, the performance of algorithms are highly dependent on the quality of the training data. | Does not have structured data to train on. |
| Best for high value information, that is, information with concentrated meaning like a user utterance. | Best for large volumes of disorganized information like a collection of web pages. |

### Goals for Intent Models
The ideal intent model achieves several goals:
-   **Maximizes predictive performance using live utterances** – What a person wants can be expressed in a semi-infinite number of ways. Therefore, training on every possible utterance is impossible. Rule-based approaches can be too narrow and similarity matching doesn't scale. Instead, the model must predict the intent of a live utterance with high accuracy whether or not the utterance has been used before. The model must generalize beyond what it knows, the training data, into the unknown, what it will be exposed to in future conversations.
-   **Builds a balanced model** – To build a model that generalizes well for unknown utterances, the model must capture patterns that indicate the class the utterance falls into while ignoring patterns that do not indicate class. The model must be able to generalize a spectrum of nuanced patterns, from patterns that give off strong indications of user intent to patterns that give off weak indications.
-   **Avoids overtraining and undertraining** – An unbalanced model cannot extract accurate intent from background data. With overtraining, the intent model is too closely aligned with the training data. Undertrained models cannot capture the underlying structure of a data set. Every evaluation of an utterance can't distinguish between strong or weak intent indications in the training data.
### Training an Intent Model
The flesh and blood of the intent model is training data. These are all the example utterances used to teach the model to understand what characterizes the various classes of intents, and what distinguishes one from another. In turn, training data is what enables the model to predict the class of unseen utterances.
For example, utterances used in training must be varied. Utterances that say the same thing with only minor variations in word choice perform poorly. For example, there's little difference between, "I want insurance," "I want insurance, please," and "I want insurances." Using, "I bought a new car and need insurance" and "Can I get insurance? My old insurance expired" work better for training. Utterances with a wider variety of word choices and phrasing provide Amelia with a more diverse set of words and phrases to compare when she evaluates live utterances with the intent model.
When Amelia analyzes an utterance to detect the intent (if any), she doesn't read the utterance verbatim. Rather than process the utterance in its raw form, Amelia polishes the utterance in various ways, to simplify intent recognition. This pre-processing is important to understand while working with training data.
### Validating the Intent Model
Once training data has been turned into a model with a mix of Amelia's tools and functionality, the model should be validated with a data set of utterances.
In pre-production, intent models are validated with best guess utterances, historical utterances from other platforms if they are available, as well as with training utterances. Once Amelia is live, the validation data set can include utterances from people interacting with Amelia to complete their tasks.
## Other Intent Detection Methods
While intent models are a powerful way for Amelia to detect user intent in a conversation, other methods are useful to support models and/or capture intent in ways models cannot.
-   Grammars – Sets of rewriting rules that represent Natural Language patterns concisely, for example, the unconstructed casual way people talk.
-   Tabular Data – Provides BPNs with data in CSV table format for quick searches to retrieve data, for example, postal code data or details about insurance plans. Within a BPN, Script tasks can be used to evaluate user utterances with results used to route the user with BPN Ask task edges.
These methods and more are described in detail in the rest of this document.
# The Development Process
Beyond training Amelia, whether to provide a service with a single repeatable goal or to solve problems conversing with people, understanding the conversation experience also is important. The possible paths each conversation might take helps determine what training data is useful and how to shape the conversation process.
Once a conversation process is defined, the process is recreated with BPN (Business Process Network) syntax in a drag and drop interface. Connections to any third-party software, code to capture entity data needed to complete tasks, and other details are all defined within the BPN process then deployed. For details about the complete end to end development process, read the [Getting Started](https://docs.ipsoft.com/display/AmeliaDocsV37/Getting+Started) page about training Amelia.
However, the first step is to optimize how Amelia determines intent for a specific topic and task. The rest of this document describes in detail how to help Amelia identify intent in what people will say to her in conversation.
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
