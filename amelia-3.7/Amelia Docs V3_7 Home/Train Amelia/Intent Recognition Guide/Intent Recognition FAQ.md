-   [How many intents can Amelia handle?](#IntentRecognitionFAQ-HowmanyintentscanAmeliahandle?)
-   [In my model, how much training data do I need per intent class?](#IntentRecognitionFAQ-Inmymodel,howmuchtrainingdatadoIneedperintentclass?)
-   [When do I use intents and when do I use entities](#IntentRecognitionFAQ-WhendoIuseintentsandwhendoIuseentities)
-   [How do I know what intent recognition I can expect once I go live with my Amelia solution?](#IntentRecognitionFAQ-HowdoIknowwhatintentrecognitionIcanexpectonceIgolivewithmyAmeliasolution?)
-   [What counts as a good intent recognition rate?](#IntentRecognitionFAQ-Whatcountsasagoodintentrecognitionrate?)
## How many intents can Amelia handle?
There is no fixed answer to this. It depends on a number of factors, notably these two:
-   What are the intents and how do they fit together?
-   How high intent recognition do you expect?
The best way to understand if a satisfactory intent recognition can be achieved for an Amelia role, is to start by identifying the full set of intents she should recognize in that role. This is the [intent scope](Intent%20Scope). That will provide a decent understanding of how how many intents are needed, what these intents look like, and how they relate. At this point, do an estimation of the realistic intent recognition for this intent scope. Ideally, to get a deeper understanding, also assess how intent recognition will happen based on the full scope of identified intents. That is, design an [intent architecture](Intent%20Architecture).
Instead of asking how intents Amelia can handle, a better question is often: In the role Amelia is being considered for, what intents should she recognize? That provides a concrete case to evaluate. This is usually more fruitful than picking a number out of the air, which inevitably ends up being semi-arbitrary.
Nonetheless, to put a couple of very generic numbers out there: 10 intents is modest and a 100 intents is a lot*.* That doesn't mean 10 intents will be a walk in the park. That depends on the intents. It also doesn't mean that 100 intents are out of reach. It certainly can be doable, if the intents are clearly distinguished from each other and have clear unique language patterns for each intent.
## In my model, how much training data do I need per intent class?
This depends on what intents (classes) are in the model, how much training data the other intents have, and it varies with the individual nature of each individual intent. It also depends on how your user base express the intent, and what levels of intent recognition you expect. That said, if you have less than 50 utterances for any intent, chances are this class won't perform well. Machine learning models rely on training data to identify in patterns that will help it correctly predict the intent of utterances it has never seen before. So if we starve them on data, they won't be able to find these patterns.
Following are a couple of pointers:
-   As a rule of thumb, aim towards 100 utterances per intent, sometimes higher. That doesn't mean start with 100, especially if the result is very low variation between a lot of those utterances. Start with 50, for example, and then build from there in response to testing.
-   The amount utterances needed for an intent also depends on how broad or narrow a class is. A general class for troubleshooting Outlook covers a lot of ground and will need more training data, as there are a multitude of ways to express that intent. A class for resetting your Outlook password is a lot more limited, with fewer ways to express the intent and so will need less training data.
A couple of other things to keep in mind:
-   Don't forget that any intent should be balanced by in-domain negative training data. If an intent for resetting Outlook passwords is trained but have nothing about resetting passwords in the negative training data, chances are that this intent can easily trigger on any utterance containing relevant patterns, even if the utterance has nothing to do with the intent. Always develop intent data and negative data in parallel.
-   Always reserve quality data for [validation](Validating%20the%20Intent%20Model), to test the model.
-   Models that use linear algorithms usually require less training data than deep neural network models.
## When do I use intents and when do I use entities
For intent recognition purposes, usually use intents and entities in combination. Typically, the intent captures the coarse-grained intention of the user, while an entity can pick out more fine-grained information that can help us pinpoint the intent further. If Amelia is used in an insurance setting, and one of her skills is to process claims, first determine the user's intent (filing a claim) on intent level, but determine what kind of claim (auto, home, travel, etc) on entity level. For some intents, there won't be any relevant information on the entity level, in which case only operate with an intent. For more details on how intents and entities work, see [Intent Detection Methods](Intent%20Architecture).
In some rare cases, do intent recognition directly with entities, as described for the various entity types under in the link above.
## How do I know what intent recognition I can expect once I go live with my Amelia solution?
Cross-validation rarely gives a true picture of model's actual performance. In fact, it can very easily exaggerate the performance of the model, sometimes dramatically. More on this here: [Training Data Cross-validation Bias](Validating%20the%20Intent%20Model). Avoid relying on it in the first place, and instead put our money on a high quality [independent validation set](Validating%20the%20Intent%20Model).
## What counts as a good intent recognition rate?
There is no set answer to this. In a live Amelia deployment, if there is a big set of intents, many of which are quite close to each other, 70% can be a decent intent recognition rate. If the case is much simpler, with both fewer and more distinct intents, then sometimes 90% intent recognition is realistic. Moving up towards 100% is almost never realistic. Live agents too sometimes misunderstand what end users mean and so will Amelia.
Note that in testing, scores are usually better, so set the bar higher in testing. There's a couple of reasons for this. Firstly, real users often make things more complex and unpredictable than can be anticipated in the validation set. Secondly, the validation set typically is what to improve the intent recognition against, so the improvements made to the intent recognition, while hopefully they generalize beyond the validation set, will probably work better on the validation set than on real life users.
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
