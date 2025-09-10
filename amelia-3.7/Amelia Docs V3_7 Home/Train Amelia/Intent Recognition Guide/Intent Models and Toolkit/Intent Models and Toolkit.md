-   [Intent Model](#IntentModelsandToolkit-IntentModel)
-   [Intent FAQs](#IntentModelsandToolkit-IntentFAQs)
-   [Spanless Entity Model](#IntentModelsandToolkit-SpanlessEntityModel)
-   [Domain Model](#IntentModelsandToolkit-DomainModel)
-   [Edge Expressions](#IntentModelsandToolkit-EdgeExpressions)
Once a proposed [intent architecture](Intent%20Architecture) is created, the next step is to implement the architecture with Amelia. In practice, this involves implementing and optimizing the tools will use to *detect* any intents and sub-intents users express as they interact with Amelia. 
This section covers best practices for working with the various tools in the intent detection toolbox, as used in an intent recognition context. The vast majority of the content will be on machine learning models, as these by far are both the most common and most complex tools used.
Following are the various tools available to find an intent (if any) of a user utterance. As noted under [Intent Architecture](Intent%20Architecture), these tools are used in various configurations or combinations to support each other.
# Intent Model
As this is the most important intent detection tool, and by far most complex, the topic is covered in these pages:
The Intent Model (Not Used)Understanding Intent ModelsTraining the Intent ModelValidating the Intent ModelCollecting and Sourcing DataBuilding the Intent ModelData Curation
# Intent FAQs
Although intent FAQs are uploaded in Amelia in a different way than intent models, they are identical to intents in the intent model in terms of how intent detection takes place. So all best practices for the intent model apply equally to a Intent FAQs.
# Spanless Entity Model
Spanless entity models are identical to the intent model in terms of how intent detection takes place. All best practices for the intent model apply equally to a spanless entity model.
Often, spanless entity models will be used in a different way, which can have some impact on how they should be optimized, as described in more detail in the intent architecture page. Typically, when a spanless entity model is used to detect sub-intents.
# Domain Model
Multi-domain Amelia deployments can operate with a domain classification model. This enables dynamic domain switches inside the user's conversations with Amelia.
-   At beginning of the conversation with Amelia, the user will typically be in a parent domain. A domain model is used to determine when the user should enter a relevant child domain. When a user says something that indicates domain A, they will be moved that domain, and remain in that domain until a potential domain switch happens.
-   Once inside a given domain, users sometimes express an intent that belongs to a different domain. The domain model picks this change up and the domain switch takes place.
Apart from the data of the negative class, the training data for domain models are automatically generated from the training data of the intent models on the relevant child domains. Therefore, in training a domain model, only negative training data needs to be added. Typically, in-domain negative data may be largely or wholly irrelevant for these models, determining the proper domain is the only purpose, not resolving any particular intent. So if a domain is for an IT service desk, and the user says something related to that, it's fine if the user is moved to that child domain, even if no intent is hit on the domain.
> [!warning]  
>
> For each domain on an Amelia instance, domain switching can be selected into the domain, out of the domain, both, or neither.
> [!info]  
>
> **Example**
>
> Amelia has two roles: IT service desk agent and HR agent. As we want users to be able to inquire about both of these to one and the same Amelia, we we organize these two roles on two different Amelia child domains, organized under a parent domain.
>
> When the user starts chatting with Amelia, they are on a parent domain. On this parent domain, we run a domain level classifier on the user's utterance to determine if the user is inquiring about IT or HR. According to the result of the classification, the user is then sent to the corresponding child domain. In that child domain, the user's utterance is *then *processed by an intent model that's local to that domain (given that the domain uses an intent model).
>
> So all user utterances will typically be classified twice. Take this utterance: "My anti-virus subscription seems to have run out - what do I do?" First, the domain model places this utterance in the IT domain class. Then, the intent model in the IT domain reads it as the intent RenewAntivirus.

# Edge Expressions
The use and syntax of edge expressions is covered under Process Flows and Edge Notation and Service Prefixes.
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
