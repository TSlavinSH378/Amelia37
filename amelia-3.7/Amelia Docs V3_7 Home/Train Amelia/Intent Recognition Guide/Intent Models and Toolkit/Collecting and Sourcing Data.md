-   [Collecting Existing Data](#CollectingandSourcingData-CollectingExistingData)
    -   [Sources](#CollectingandSourcingData-Sources)
    -   [Privacy](#CollectingandSourcingData-Privacy)
-   [Sourcing New Data](#CollectingandSourcingData-SourcingNewData)
    -   [Sources](#CollectingandSourcingData-Sources.1)
    -   [Quality](#CollectingandSourcingData-Quality)
    -   [Methodology](#CollectingandSourcingData-Methodology)
High quality data is needed to train and validate an intent model. However, data can be hard to find or develop. The best place to start is by collecting existing data from chat, voice, messaging, ticketing, and other systems. New data sources might include end users, support agents, Amelia team members, and crowd sourcing. Once data is collected, quality and privacy issues need to be addressed.
# Collecting Existing Data
Live end user data is the best existing data to collect, if it exists. Collecting existing data can happen as part of the use case discovery process. To determine the relevant use cases for Amelia to deal with, it can be useful to dig into existing data to extract intent utterances and an overview of what users ask about.
## Sources
For existing data sources, people might express themselves differently in one context than how they interact with a virtual agent. However, these sources can be a valuable source of useful data and provide ideas for use cases and how people express their needs.

| Existing Chat Solutions |
| ----|
| Amelia often is used as part of an existing chat solution, to relieve live agents from their straightforward tasks. Or she may replace an earlier more simple chatbot. If so, chat logs for the existing solution will usually have a wealth of utterances to use.This could be a source for both utterances that express an intent and in-domain negative utterances. |
| The same dynamic applies when requests come through a phone call.In this case, the utterances have to be transcribed by a speech-to-text technology and reviewed. If Amelia will be used as a voice virtual assistant, ideally transcribe these utterances with the same speech-to-text technology to be used by Amelia. This ensures some consistency between transcribed utterances used for training and validation and the transcribed user utterances Amelia will process in production. |
| If the use cases Amelia will handle are currently solved with messaging system, collect log files to extract relevant utterances.Because messaging systems are different from a conversational platform like Amelia, messaging utterances may be too long or short. Picking out a relevant sentence or two from a larger message might be required.Messaging systems can be a source for intent utterances and will include lots of relevant in-domain negative utterances. |
| If the use cases Amelia will handle are currently handled with a ticketing system, this system may have relevant data in the comments users made in the tickets. These comments may sometimes be utterances that express an intent.Adding a comment in a ticket is very different from conversing with a virtual agent. Be selective in what is extracted. However, extracting utterances from comments can work better than nothing. |

## Privacy
With existing data sources, sensitive information must be deleted from utterances, to be compliant with GDPR and other privacy regulations. This is especially true for customer data, as opposed to data from internal employees.
If deletions are needed, a screening process should be set up to replace sensitive information with made-up information. This can apply to:
-   Names
-   Addresses
-   Phone numbers
-   Emails
-   Anything else that can indicate the identify of the person (subscriptions, medical conditions, etc).
# Sourcing New Data
In practice, sourcing new data is needed to build out training and validation data. 
## Sources
For new data sources, people might express themselves differently in one context than how they interact with a virtual agent. However, these sources can be a valuable source of useful data and provide ideas for how people express their needs.

| Future End Users |
| ----|
| Crowd sourcing within a company can be a good way to collect new utterances, especially if Amelia will be an internal agent used by these contributors. |
| Often, Amelia will be used as part of an existing chat solution, to relieve live agents from their more straightforward tasks. These live agents will have a deep understanding of the mindset and issues of end users.Based on their experience with callers, ask agents to image themselves as being their callers then write down relevant utterances for the different reasons they call.If possible, ask the live agents to note down user utterances as they receive them. If calls are not logged, there is no transcript to evaluate. When call traffic is low, ask agents to note down the question or inquiry of every fifth call they receive as best they can. |
| The implementation team also can create utterances. However, these utterances should form only part of the utterance data set. Team members will have a natural bias because of their knowledge of Amelia's capabilities which ends users will not possess, as well as their role building a tool they likely will not use. |
| In cases where the intents are easily understandable for strangers, paying for external crowd sourcing of utterances might be another source. |

## Quality
When new utterance data is sourced, ensure the data is as high quality as possible.
-   **Avoid priming** – Guiding and instructing contributors too closely when they create utterances will bias them.
-   **Ensure independence** – Have contributors provide their utterances without access to how other people phrased their utterances. If they see what other people did, they will be influenced by those utterances.
-   Quality over quantity – Do not ask individual users to provide a big number of varied utterances for one intent. Maximum three utterances per intent is a useful guideline. If asked for more, their creativity will run out and they will either repeat themselves or come up with utterances they never would use in real life.
-   Diversity – The more diversity among the contributors, the more variation will result. This provides a better representation of what Amelia will be exposed to in production and results in better training and validation data.
-   **Vet all utterances** – All contributor utterances must be vetted by members of the team that will implement Amelia. Half the contributors might provide good data while the other half may not. In addition, users may provide utterances that in fact do not express the intent.
## Methodology
There are several ways to collect and format utterances.  

| MEANS OF COLLECTING UTTERANCES |
| ----|
| Small workshops where contributors are placed in a room for 30 minutes might be an effective means to source utterances. Give instructions to the group and keep the contributors focused. Typically, this will generate more utterances than if contributors are asked to provide utterances when they have time sitting at their desk. |
| Collect utterances by requesting help from contributors wherever they are located. This can yield fewer utterances than workshops. People are busy so the task typically needs to be low effort to encourage contributions. For example, don't use a big instruction manual and do provide a simple means to submit utterances. |


| FORMAT TO COLLECT UTTERANCES |
| ----|
| Forms are one way to collect sourced utterances. For each of the intents, provide instructions then three form fields, one for each utterance. |
| If shared documents for sourcing utterances are used, be careful how they are shaped. If exposed to the utterances from other contributors, they will be influenced by what they see. This will lead to less variation in the utterances. |
| Various communication systems like email and Slack can be used. However, this may require data management to organize afterwards. |
| Once in test mode with an Amelia solution, source utterances by having users test the solution then retrieve the chat logs to extract relevant utterances.It's also possible to use Amelia to harvest utterances from contributors before Amelia is trained for relevant use cases. Set up Amelia with a basic conversational flow where she asks contributors to provide utterances for specific intents. While easy to build, it requires a relevant environment for Amelia and access for contributors, perhaps with a shared ID.Amelia asking for utterances has a couple of advantages:The user is in an actual chat or voice experience where they provide their utterances in a context close to the real context in production.Contributors may be curious about Amelia in the first place and this works as a small testing grounds for Amelia and tempt contributors to provide utterances.Having Amelia ask for utterances may take work to set up and to retrieve chat logs and extract utterances. But a well designed small Amelia solution provides a number of benefits. |

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
