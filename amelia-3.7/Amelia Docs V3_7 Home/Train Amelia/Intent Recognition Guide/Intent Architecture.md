{% version "3.x" %}
An intent architecture implements the intent scope in a way that causes high intent recognition. This includes:
-   Setting boundaries that influence what can or should shape the intent architecture
-   Defining objectives for an intent architecture
-   Identifying the means to shape intents
-   Testing qualifications of specific actions to maximize intent recognition
# Aligning with the Amelia Implementation
When building an intent architecture, be mindful of the shape of the overall Amelia implementation. This often influences how the intent architecture can and should be designed. 
## Open vs Closed Implementations
Whether or not an Amelia deployment is open or closed can have a significant impact on intent architecture choices. In some cases, however, the difference has not impact.
-   An **open** implementation, is an Amelia deployment where the natural state of a user is outside BPNs. The conversation with Amelia starts with no BPNs running. Once an intent is hit, the user moves into a BPN. Then the user moves back outside the BPNs once that process is complete.
-   A **closed** implementation is a more structured deployment where the user is at all times locked inside BPNs. The conversation starts off in a greeting BPN, enters various other BPNs, for example, via intents, then always returns back to a BPN similar to the greeting BPN, where the user can start a new and different conversation.
This difference impacts the intent architecture. Closed implementations can mean changes in the conditions of the intent architecture, as well as a broadening of the opportunities in how the intent architecture is set up.
> [!info]  
>
> Example 1
>
> Amelia works as a vehicle to submit applications. Which application depends on user nationality. Users providing their nationality could be relevant information, as an entity or maybe an intent, to start the correct application process for their nationality. However, for a closed implementation, where users must state their nationality using an auto-complete list, their nationality becomes irrelevant in intent architecture considerations.
>
> **Example 2**
>
> If Amelia works in a storage facility setting, to order new items to the warehouse, reserve items, report on missing or broken items, and so on, this is best solved in a closed implementation. The user starts inside a BPN that presents relevant options. This set-up has a fundamental impact on the intent architecture.

## Context Switching Enabled or Disabled
Amelia can be configured to enable or prevent the end user to switch to different intent during a conversation. This is called context switching. In this context, intent refers to intents in an intent model or grammar only.
In many cases, this creates a more dynamic user experience. The user starts off with intent A, then switches to intent B, then is asked by Amelia if they want to resume intent A after having completed intent B. However, it also risks accidental or unwanted context switching. Be aware of this risk as intents are designed. 
For example, an intent in an intent model can be triggered by an utterance consisting of two words. If the user might say those two words naturally, in the course of some conversation with Amelia, with no context switching intended, this will cause trouble. If context switching is enabled, take into account these risks intents are formed into an intent architecture. 
> [!info]  
>
> Example
>
> In an Amelia deployment that consistently has context switching turned on, there is an intent for FileExpense. Looking at conversation transcripts, it appears users sometimes only say 'new expense' to express this intent.
>
> However, there's also an intent for ExpenseStatus used to check the status of filed expenses. During the course of the ensuing conversation of that intent, users have to let Amelia know if they want to check the status of a new expense that's undergoing processing, or an expense that's already processed. Sometimes, users articulate the former by saying 'new expense,' causing an unwanted context switch. 
>
> To remedy this, either rework the ExpenseStatus conversation, to avoid users saying 'new expense' or turn off the possibility of context switching at that juncture in the conversation. 

## Chat vs Voice Implementation
Chat and voice Amelia implementations can impact how to think about intent recognition.
-   In part because visual aids or visual user interface elements in Amelia can't be used. While, for example, using an auto-fill list may sometimes help, or make superfluous, some part of the intent recognition, that option is not available in voice implementations. 
-   In part because there may be differences in what the end user utterances that express the intent look like. This in turn may have consequences for how an intent architecture is designed. More on these differences under [Chat vs Voice here](End%20User%20Utterance%20and%20Behavior). 
## Information via Integrations
In many Amelia deployments, we get pieces of relevant information from integrations. Most commonly, this means we won't have to extract that information in entities, because we already now this or that about the user. But sometimes, it can also affect what information we need - or rather, do *not *need - to capture as intents. 
# Objectives of the Intent Architecture
Looking briefly at what to achieve with an intent architecture will help ensure the right decisions are made and prioritized sensibly as the intent architecture is created and tested.
## Maximize Intent Recognition (Accuracy + Timeliness)
An intent architecture produces a design to maximize intent recognition along two dimensions, accuracy and timeliness.
-   Accuracy is Amelia's ability to detect the correct intent.
-   Timeliness is Amelia's ability to detect the intent with no disambiguation delay when the intent is clearly expressed and by appropriate but minimal disambiguation when the intent is expressed ambiguously or inadequately.
These dimensions apply to individual intents and the set of intents, or intent scope. When designing an intent architecture, heed the nature of each intent and consider each intent in the context of the entire intent architecture.
## Weigh Accuracy vs Timeliness
In some cases, accuracy might be prioritized over timeliness, or vice versa. The former maybe the more common, typically for use cases where accuracy in the intent recognition is important. If so, the intent architecture can be built to avoid mistriggers as far as possible, by designing for disambiguation whenever Amelia is not confident she understands the intent. That way, some timeliness in the intent recognition is traded away, but accuracy improves in return.
> [!info]  
>
> Example
>
> Say there are two close intents, A and B. Given the nature of the use case, a maximum of 5 % mix-ups in intent recognition between A and B is acceptable. However, by keeping them as separate intents, it’s clear they can only realistically achieve 90 % correct immediate intent recognition. The misfire rate will inevitably be 10 %, due to the intents' proximity.
>
> So instead, merge the two intents and handle A and B as sub-intents. The result is 50 % of users hit the correct sub-intent immediately, 47,5 % have to disambiguate, and 2,5 % misfire. Meaning the immediate intent recognition is almost halved, but the accuracy is way up, thanks to more disambiguation.

## Weigh Effort vs Reward
Sometimes, accepting slightly lower recognition works if effort is reduced substantially. Intent recognition is often hard work. It can require significant investment in time and training upfront, as well as oversight and maintenance along the way. So there can be considerable practical value in adjusting or prioritizing efforts according to the reward.
> [!info]  
>
> Example 1
>
> If it will take substantial effort to maximize the intent recognition for a certain part of the intent scope, it's quite possible to achieve decent results easily by merging a few intents. If so, an effort-reward analysis may favor the practical solution for an intent architecture, not the solution yielding the absolute best intent recognition.
>
> Example 2
>
> When considering whether to use a spanless entity model or a tabular data entity to capture a set of entity values, and certain the former will outperform the latter, the effort of sourcing training data and fine-tuning a spanless entity model might not meet the cost-benefit test. So for practical purposes, even if it probably gives slightly inferior results, use the simpler tabular data to capture the entity values in question.

# Designing the Intent Architecture
With an awareness of how the Amelia implementation works, and what goals to achieve, the next step is to transform the intent scope into an intent architecture. This can be a straightforward exercise with a simple intent scope. With more complex intent scopes, transformation can be a complicated process.
Often, the intent architecture will evolve due to experiences from testing or after go-live or as Amelia's role expands with new skills that affect the intent architecture. 
## Intent Architecture Design Process
The table below describes a process to evaluate the intent scope then design and create an intent architecture. The four steps are described in further detail further down on this page. This process tracks the intent architecture evolution to help organize information about intents and related details.
Table. Intent Architecture Evolution Process

| Depth | 2. Completeness | 3. Recognizable | 4. Distinguishable | 5. Evaluate and go back to start |
| ----|----|----|----|----|
| INTENT STRUCTURE AND SCOPE | INTENT DETECTION |  | undefined | undefined |
| Build out the;depth of the intent architecture: Organize the intent scope into intent and sub-intents, and add any relevant sub-intents that were not defined in the intent scope. | Ensure;completeness in the intent architecture:Check that the intents  and sub-intents form a coherent whole. Add any relevant intents or sub-intents to complement the existing architecture. | Asses each intent and sub-intent on whether or not it is;recognizable: Map them to the appropriate intent detection tools. Reshape, trim or remove any intents or sub-intents that are deemed to be not recognizable.  | Assess each intent and sub-intent on whether or not it is;distinguishable from competing intents or sub-intents:  Consider each intent in the context of all competing intents. Consider each sub-intent in the context of its competing sub-intents. Take any relevant actions: reshaping, merging, merging and expanding, adding checks against mistriggers, graceful intent switching.  | Once this process is completed once, evaluate the results:Check that the intent architecture makes sense overall. Then, considering that the intent and sub-intents may have changed during this process, go back to start and re-assess everything according to the same four steps.;Once going through all four steps, with no changes done, the intent architecture is complete for now. That doesn't mean it's set in stone. After testing and soft launch is another time to re-evaluate.  |

This evolutionary process can be visualized this way. Each step is described below in detail.
![](attachments/20808353/23396721.png)
Figure. Intent Architecture Process
## 1. Depth of Intent Structure and Scope
Some intents reveal a significant variety of detail in user utterances. If the user states the high level intent and a granular understanding of the intent, Amelia should pick up on these details. If she only gets a rough outline, Amelia should prompt the user to fill in any missing details. In these cases, the intent should be layered.
An intent with more than one layer has depth. The primary intent layer is on top with relevant sub-intents on a second layer.
> [!info]  
>
> Example
>
> In an insurance setting, there is an intent for FileClaim. This is the primary intent. Sometimes, users will specify the object of their claim (auto, home, boat, and so on). These are sub-intents, on a second layer.

The first step in designing an intent architecture, is to organize and build out the [intent scope](Intent%20Scope) to accommodate for this depth in any relevant intents. This will provide us with a complete picture of all intents and sub-intents Amelia will handle. For more details on how this works in Amelia, see Multi-Layered Intent Recognition under Intent Structure below.
Normally, some intents from the intent scope have various sub-intents and some don't. Sometimes, some intents in the intent scope were in fact sub-intents of other intents in the first place, typically when there was a [vertical distance](https://docs.ipsoft.com/display/AmeliaDocsV37/Intent+Scope#IntentScope-2.Distance) between the intents.
> [!info]  
>
> Example 1
>
> An intent scope has intents for UpdateProfile and UpdateEmergencyContacts:
>
> 
> | INTENT |
> | ----|
> | UpdateProfile |
> | UpdateEmergencyContacts |
> 
>
> However, users often consider emergency contact information to be part of their profile, even though technically this is not the case in the system. If users said they wanted to update their profile (with no more specifications), they expect updating emergency contacts to be one of the options Amelia provided them.
>
> As these details are consolidated into the intent architecture, UpdateProfile becomes the primary intent. Under this intent, relevant sub-intents are added, including the intent for emergency contacts, transforming this into sub-intent. Under UpdateProfile are sub-intents like Email, Address, PhoneNumber, EmergencyContacts. The intent architecture for this now single intent looks like this:
>
> |                     |                   |
> |:--------------------|:------------------|
> | INTENT              | SUB-INTENTS       |
> | UpdateProfileUpdate | Email             |
> |                     | Address           |
> |                     | PhoneNumber       |
> |                     | EmergencyContacts |
>
>   
>
> Example 2
>
> In a banking intent scope, there is an intent for users inquiring about interest. How users express this intent ranges from high level of precision (user utterance 1):
>
> User utterance 1: What interest will I get if I set up a savings account?
>
> to very low level of precision (user utterance 2):
>
> User utterance 2: I want to know what the interest is.
>
> The first utterance has all the necessary detail to understand all the relevant layers of that intent:
>
> -   set up indicates the user wants to know the interest of a new account, not any existing accounts.
> -   savings account tells us that it's an account the user wants to know the interest of, not a card, and that this account is the savings account, not for example the checking account.
>
> The second utterance will require Amelia to ask the user to disambiguate between all these various possibilities, to pick up the deeper layers of the intent.

## 2. Completeness of Intent Structure and Scope
Having built out an architecture with relevant sub-intents, it is clear what Amelia should be able to recognize. At this point, take a step back and consider the completeness of it all. That is, whether the intent structure and scope forms a coherent whole. 
Users will expect that, if Amelia can do X and Y, she will naturally also be able to do the closely related Z. That does *not *mean intents for all facets of Amelia's role should be included. However, it can mean existing intents or sub-intents should complement any intents or sub-intents that are very close neighbors.
This can also help simplify intent recognition. If very closely related use cases are part in-scope and part out-of-scope, that can present a challenge for intent recognition.
> [!info]  
>
> Example 1
>
> As an online shopping assistant, an intent adds a new credit card for your purchases. As the intent architecture is designed, it becomes clear that removing a card is *not *included. This may come off as incomplete to users. An agent that can add cards should surely be able to delete cards as well. In fact, users often will want to remove an existing card before adding a new one.
>
> With this in mind, add an intent for RemoveCard to complement the existing intent AddCard. Until the skill is built out in Amelia, for now her answer will be to provide a link to where the user can do it. But at least Amelia understands the full picture of adding and removing cards.
>
> **Example 2**
>
> There are intents to start and end a membership. There is also an option to pause memberships temporarily. This is more rarely invoked by users, and Amelia will have to escalate to a live agent as she currently is not set up to handle that process end-to-end. But to complete the skill set for managing a membership, add this pause membership intent into the architecture.
>
> **Example 3**
>
> In a banking setting, an intent for NewCard lets people apply for credit cards. Amelia is still not trained to provide debit cards and set up a corresponding checking account. But for the sake of completeness, and to avoid misunderstandings, add in two sub-intents under this intent: CreditCard and DebitCard. When the former is triggered, Amelia does as planned. When the latter is triggered, Amelia will escalate to a live agent.

## 3. Recognizable Intents
Ensuring all intents and sub-intents are recognizable is the first requirement of a good intent architecture. In simple terms, common and discernible language patterns in how users express their intents must be present. These patterns are used to detect intents with an intent detection tool. Overlooking recognizable patterns leads to low intent recognition.
It can be useful to understand what characterizes an unrecognizable intent or sub-intent.
-   Too varied (insufficient consistency) - This occurs when there are lots of relevant language patterns to pick up, but too little consistency in those patterns. Numerous relevant hints for Amelia to trace never coalesce into a single recognizable intent. In theory, for example, training such an intent or sub-intent in with a classification model sounds appropriate. However, it requires a big effort with large amounts of data, and still probably results in both very low performance and an unbalanced model.
    > [!info]  
    >
    > Example
    >
    > Amelia is an internal help desk agent, specializing in installation, permissions, debugging, and other software related tasks. Users also request help with specific functionality questions for different applications. Ideally, Amelia should point users to a documentation repository. However, there is no common thread to how users express their functionality-related questions.
    >
    > The range of issues, across dozens of applications, is practically infinite. For example, users ask, “Why am I unable to add a new user row in Virga?” or “Don’t know what to put under ID in the account page” or “In T-Dex, what does ‘Lower Threshold’ mean?” This complexity is not a feasible intent because it is impossible to cover such vast variation.
    >
    > Because it's not feasible to cover such vast variation, this intent is not feasible.
-   Too vague (insufficient particularity) - This occurs when an intent or sub-intent is too diffuse, too unspecific, to form a recognizable intent. This variation of low recognizability correlates with low specificity, as covered under Intent Scope. There is simply too little meat on the bone for Amelia to be able to sniff her way to the intent.
    > [!info]  
    >
    > Example
    >
    > Amelia works as an e-shop assistant. As the user chats with her, whenever the user feels frustrated or is lost in the process with Amelia, she should escalate the user to a live agent. Her ability to use frustration as an intent is difficult, however. Users express such an intent in very vague and varied utterances, “I think the blue is a different one” or “Huh?” or “I said I wasn’t sure” and so on. Consistent and predictable intent recognition is unrealistic.
There are several actions that can be taken to fix intents and sub-intents that are too varied or too vague.
-   *Trim intent / sub-intent *- Extract the relevant parts of an intent or sub-intent that are in fact recognizable - and reshape the intent to cover that.
    > [!info]  
    >
    > **Example**
    >
    > As noted in an example above for too varied intents with insufficient consistency, it's difficult or impossible to catch the breadth of questions users will have about a software application. However, common solutions are possible. FAQs can be placed in multiple intents or in a combined intent.
    >
    > The intent is narrowed down to the recognizable part of the user intent. The intent is no longer SoftwareQuestions. It's SoftwareFaqs.
-   *Remove intent / sub-intent and open outside pathway to it *- While Amelia cannot detect the intent using traditional intent recognition, consider advising the user on how to  reach this intent by different means.
-   *Remove intent / sub-intent *- Sometimes, drop the intent from the intent architecture.
## 4. Distinguishable Intents
Within an intent architecture, every intent has to be reasonably distinguishable from a crowd of competing intents. Language patterns used to detect an intent must be unique to that intent, to some extent.
Classification is the core of intent recognition. Classification assigns a class (intent) to an input (the utterance). A classifier is a big sorting machine. Any intent in an architecture, as users express that intent, has to be realistic for Amelia to learn to distinguish a specific intent from any competing intent classifying it.
→ This is the action of discriminating the intent. For Amelia to be able to discriminate the intent, it must be distinguishable.  
In practice, an intent must pass two hurdles:
-   The intent has to be distinguishable given the competition. Depending on how intents are organized, this may be all intents or a subset of intents. This often correlates with distance as covered under Intent Scope.
-   It has to be distinguishable given the particular intent detection method used for it.
    > [!info]  
    >
    > **Example 1**
    >
    > One intent to submit expenses and another to update emergency contacts. These are clearly distinguishable from one another.
    >
    > **Example 2**
    >
    > One intent to report fraudulent transactions and another to report suspicious transactions. These might be indistinguishable if users use similar or identical language patterns to express these intents. These two intents might be merged into a single intent in an intent architecture.
    >
    > **Example 3**
    >
    > One of Amelia's skills helps employees with receiving guests at their office. How Amelia handles this depends on whether guests are internal, from another company office, or external. Therefore, GuestInternal and GuestExternal could be separate intents in the intent scope.
    >
    > As the intent architecture is built, the first instinct might be to design two sub-intents under the intent Guests. Looking into the utterance data, however, users express these sub-intents with language patterns that are often both vague and varied. No matter the sub-intent detection tools used, It will be difficult to determine with confidence whether a guest is internal or external.
    >
    > In practice, therefore, these two sub-intents are *in*distinguishable, at least in the majority of instances. Given this, Amelia will always ask the user whether the guests are internal or external.
# Shape, Structure, and Detect Intents
The method used to shape, structure, and detect intents is part of testing one or more tools used to detect intents. Intents can be reshaped by merging or splitting. The structure of an intent can be as an intent or an entity. Both intents and sub-intents can be detected. Several questions arise as means and tools are evaluated.
-   Is the intent recognizable given the detection tool?
-   Is the intent distinguishable given the competing intents or sub-intents?
These questions and their answers are both independent and interdependent.
> [!info]  
>
> **Example**
>
> A small intent scope with three intents, Reset intranet password, Reset Outlook password, Connect to printer. As they are transformed into an intent architecture, these assessments are made: 
>
> First, look at the intent to connect to the printer. Clearly, there are no conflicting or close intents, so this intent is not changed. The intent can be expressed with a wide variety of utterances. In terms of detecting the intent, the intent model is done. 
>
> Second, the two intents to reset intranet and Outlook passwords are close. Users also sometimes will not specify what password they want to reset. It will be hard and sometimes impossible to distinguish these utterances in the intent classifier. Therefore, these two intents should be reshaped into a single merged intent. In addition, an entity will be created to capture whether the user wants to reset their intranet password or their Outlook password.

## Intent Structure
Typically, some intents will operate only on intent level while other intents operate both on the primary intent level and on a secondary entity level. The configurations for how intents and entities are used can vary a lot according to the nature of the problem to solve.
There are mainly three scenarios where intents can operate on one or more levels:
-   In the case of intents with depth, that are solved using a general intent and various specific sub-intents. 
-   In the case of intents that are sometimes or always indistinguishable, in which case intents can be reshaped into a single merged intent. 
-   In cases where adding a second level check on an intent is useful, to pick up potential mistriggers. 
Consider what intents will and won’t require multilevel intent recognition as the intent architecture is worked out. This is more than looking through the intents of the intent scope. Multilevel intent recognition also can often involve redefining or reshaping intents to have them fit into a sensible structure.
### Intent Level / Entity Level / Domain Level
The table below describes the intent and entity level, as well as the domain level:

| INTENT LEVEL (INTENTS) |
| ----|
| Normally, this is where intents are handled. Typically, full-fledged intents have both some implied action and some implied object. For example, the utterance, "I want to buy (action) a phone (object)." |
| Normally, an entity is only an object, or less often, only an action. For example, a type of product - phone, tablet, computer, etc.; |
| In multi-domain Amelia deployments, a;domain level might be used.If Amelia has various roles, or is trained in sets of skills that belong in very different areas, these areas can sometimes be implemented as separate domains in Amelia. If Amelia processes both HR requests and IT requests, these could be placed in different domains. There would be two intent scopes and architectures, one for HR and for IT, with each living in their respective domains.If so, use a domain model to allow users to jump between domains. This model is trained to recognize not intents but domains or topics, in this case either HR or IT. So if the user is in the HR domain, but says something that clearly relates to IT, then the domain model will determine the user should switch to that domain. |

### Multi-layered Intent Recognition
This applies to intents with depth (see above), when users routinely will vary the level of relevant detail when expressing the intent. In those cases, consider working in levels in the intent architecture. That way, Amelia can respond appropriately, according to what layers of information the user provides. On the intent level, a general intent is detected while on entity level any sub-intents are detected. If no sub-intent is detected, Amelia typically disambiguates (example 1 below).
Note that sometimes, intents with depth can be handled as multiple intents instead of using sub-intents. If users consistently express the general intent in distinctly different ways from the specific sub-intent(s), and vice versa, then they could function fine as separate intents on intent level. If there is vertical distance between them, it doesn't mean they have to be placed in a hierarchy in an intent architecture (example 2 below).
In some cases, it's useful to have intents on intent level that are broad categories or themes more than straightforward intents. Then on entity level, distinguish between the intents of that broader category (example 3 below).
> [!info]  
>
> Example 1
>
> Amelia issues new credit and debit cards. From an internal point-of-view, these are separate processes. The debit card is linked to an account which the credit card is not, the credit card pre-supposes a certain credit score that the debit card doesn’t, and so on. In the intent scope these are marked as two separate intents.
>
> However, user research reveals that many users express these intents as just wanting a card, with no further specification. So in the architecture, the intent level intent will be NewCard, with two possible sub-intents on entity level: Credit and Debit. When users do convey the sub-intent, Amelia will detect that and skip straight to the correct process for either Credit or Debit. When users do not specify, Amelia will ask the users if they mean Credit or Debit.
>
> **Example 2**
>
> One of Amelia's skills is to help users update their profile. Technically, this includes managing push and email notifications. But user research reveals that users don't associate notifications with their profile. Instead they just ask for it in ways that have no relation to inquiries about the profile, for example:
>
> User: "How do I stop getting email notifications?"
>
> User: "No more push messages, pls!"
>
> Rather than make this a sub-intent on entity level under the intent UpdateProfile, keep it as its own intent ManageNotifications on the intent level. Also consider adding two sub-intents beneath this intent, for Email and Push.
>
> Example 3
>
> Amelia works as an IT help desk agent. Part of her job is to answer and process questions and requests regarding the company’s email system. For all email inquiries Amelia isn’t trained to deal with, she will escalate to a particular live agent queue for email system requests.
>
> In this scenario, consider having a single broad super-intent for all intents regarding the email system. Then on entity level, capture the exact intent of the user. If no entity value is captured, Amelia will transfer directly to a live agent. 

### Multi-step Intent Recognition
This applies to competing intents with low distinguishability or that are virtually indistinguishable. In those cases, merge those intents and perform intent recognition over two steps. 
In the case of intents with low distinguishability, maybe merge the intents on intent level then on entity level see whether it is sub-intent A or B. If this is impossible to determine with reasonable confidence, Amelia will ask the user to disambiguate. If the sub-intent can be determined, Amelia will skip ahead to the relevant branch. 
In the case of intents that are virtually indistinguishable, for example, if users often mix them up and ask for one when they mean the other, merge the intents. This forces to disambiguation with no sub-intents on entity level.
> [!info]  
>
> **Example**
>
> Using the example from above, two separate intents are used to report fraudulent transactions and suspicious transactions. However, the lines are so blurred between these two intents that, in practice, there's no way to distinguish them. Therefore, the intents are merged and a step added to disambiguate with the user whether it's fraud or just suspicious.

### Adding Levels to Check against Mistriggers
In some cases, add a level as a check to prevent mistriggers from executing the intent’s process. Intent A sometimes mistriggers on intent B. However, certain clear cues tell Amelia with high confidence an utterance may not be intent B. If so, consider checking for those cues on the entity level and adding disambiguation if found. This may reduce timeliness a bit but can increase accuracy.
> [!warning]  
>
> Ideally, the correct intent is selected directly. Avoid adding levels into the intent architecture. But adding levels can be an option when unique language patterns are present and the issue cannot be fixed through more conventional means.
> [!info]  
>
> **Example 1**
>
> One intent for users wanting check if they paid an invoice, InvoicePaid, and a second intent for users wanting to pay invoices, Pay. However, utterances for InvoicePaid sometimes mistrigger on the Pay intent.
>
> Analyzing the misclassified utterances, reveals a significant share of the mistriggers include patterns with words like “pay” in past tense, for example, "paid” or ”have paid”. Training data cannot resolve this problem, in part because the classifier normalizes word forms, for example, “pay” and “paid” are read identically.
>
> The solution might be to add a check in the InvoicePaid intent BPN. At the start of the BPN, an entity is checked with tabular data that matches against “paid” and other clear cues. If this entity is captured, Amelia disambiguates between InvoicePaid and Pay. While some disambiguation is added now and then, the number of mistriggers is reduced.
>
> **Example 2**
>
> An intent helps internal employees connect to and troubleshoot wifi. Sometimes, this intent triggers when the user inquires about wifi access for guests which is handled in a separate intent concerning guests.
>
> Analyzing the misclassified utterances, checking if the user utterance includes words like "guest(s)", "visit(ing)", "visitor(s)", and other words that relate to guests coming to the office identifies most misclassified utterances. The solution adds a check and creates a process for Amelia to disambiguate between the two intents whenever this check is triggered.

## Intent Detection Methods
As the intent architecture is defined, determine what methods will be used to detect the intents and capture in the architecture. Amelia, includes tools for detection and capture. What tools are used depends on the set of intents, as well as the characteristics of each intent within that set. Use the tool that’s the best fit to yield high intent recognition.
> [!warning]  
>
> This section covers how to select the best intent detection methods for any intent or sub-intent based on its nature. For best practices around using these tools, see [Intent Models and Toolkit](Intent%20Models%20and%20Toolkit).

The table below shows intent detection tools (see next section) available for the various levels.
Table. Amelia's Intent Detection Tools
| TOOLS                     | (DOMAIN LEVEL)     | INTENT LEVEL                                                                          | ENTITY LEVEL                   |
|----------|---------------|------------------------------|------------------|
| Classifier (Intent) Model | YES - Domain model | YES - Intent model                                                                    | YES - Spanless entity model    |
| Grammars                  | NO                 | YES                                                                                   | YES                            |
| Tabular Data              | NO                 | Only in closed implementations or open implementations as fallback with a sweeper BPN | YES                            |
| SWEEPER                   | NO                 | NO                                                                                    | YES - Under the negative class |
| Edge Expressions          | NO                 | Only in closed implementations                                                        | NO                             |
### Classifier (Intent) Model
The classifier intent model is usually the default tool to detect intents. In most Amelia deployments, the intent model is the primary candidate when picking recognition tools. Another tool would have to yield significantly better performance to replace intent models.  
For any intent to be a good fit with an intent model, several criteria should be considered.
Table. Criteria to Use Intent Models

| CRITERIA | DESCRIPTION |
| ----|----|
| Full utterances in natural language | The intent model looks for patterns in natural language and works best when the user utterances are full-fledged utterances. |
| Significant variety of ways to express the intent | The classification method in the intent model is designed to be able to detect the same intent even in utterances that are significantly different from each other. It’s a good fit for intents expressed with great variety. If the intent is more or less always expressed in a few very specific ways, that intent may be better served using other means. |
| Clear language patterns | If users express their intent using generic language, with no strong patterns to indicate their intent, it can be challenging to use the intent model. The intent is not recognizable. |

### Spanless Entity Model
Entities that are inferred are called spanless entities. If someone says, for example, "queen beds two of them" it can be inferred they want a double hotel room from the utterance. There are a fixed number of possible values predicted from the utterance as a whole.
A spanless entity model works the same way as intent models but with entities not intents. Criteria for when to use a spanless entity model are more or less the same as intent models. Typically, this ties the main intent detection to a specific Ask task edge in a Business Process Network (BPN) process. Then sometimes a spanless entity model is used on that edge for intent recognition.
> [!info]  
>
> Example
>
> A broad intent detects any inquiries relating to the company’s email system. On entity level, use a spanless entity model to detect the more concrete request from the user. In this example, the spanless entity model detects intents (colloquially speaking).

However, the circumstances for spanless entity models are often a bit different from intent models, in ways that can change the conditions for work with the model. Break these into three points, outlined below.
> [!warning]  
>
> It's a common misconception that a spanless entity model can do more nuanced classification than an intent model because they are sometimes used to detect sub-intents. This is wrong. A spanless entity model does classification the same way as an intent model. That said, in some cases, a spanless entity model can be more nuanced if the circumstances allow, as seen below.

A spanless entity model most often is used to detect specific information. When a spanless entity model is used to detect intents, there will be some variations in the entity model compared to a traditional intent model.
-   The entity model will often often will have less classes, as it detects a subset of classes within a more or less discrete field.
-   The entity model may sometimes not have any no value class (none/negative), as one of the subset of classes has to be true.
#### Often Fewer Classes
As spanless entity models are often used to disambiguate between a limited set of sub-intents in a more or less discrete field, they often have significantly fewer classes than an intent model. This simplifies classification.
> [!info]  
>
> An intent exists to report lost or stolen goods. However, as the business rules for how to handle lost versus stolen goods are different, there is a need to distinguish between whether the user thinks the goods were lost or stolen. Under this single intent, a spanless entity model is used to check if the user clearly expressed that the goods were lost ("I dropped my phone down a drain") or stolen ("The phone was in bag, which was nicked from me") or if it's unclear ("My phone is gone").
>
> The spanless entity model has only three classes: one for lost, one for stolen, and a negative class for when it's unclear, in which case Amelia will ask the user to disambiguate.

#### Often Closer Classes
As spanless entity models are often used to disambiguate between sub-intents, the various classes can often be quite close. So when considering using spanless entity models and working with them, pay extra attention to the distance between the classes.
Train the classes quite narrowly so they are only triggered when it's very clear from the patterns that this is the correct class, and have Amelia ask a disambiguation question whenever it's less clear. That way, what is often a high risk of collisions between classes is minimized. See the first example below.
> [!warning]  
>
> Sometimes, the sub-intents placed in spanless entity models are so close in distance it may be too challenging to train a model for it. Consider skipping the model and instead have Amelia ask the user to disambiguate in all cases. See the second example below.
> [!info]  
>
> **Example 1**
>
> Continuing with the example from above, it's clear the classes for lost and stolen can often be quite close. If any of the sub-intents are overtrained, an utterance like "My phone disappeared on the subway" can easily be read by the model as either lost or stolen, when in fact the utterance is ambiguous in this respect.
>
> To avoid confusion, train the sub-intents lost and stolen strictly. Try to direct any utterances showing any sign of ambiguity to the negative class, with Amelia then asking the user to disambiguate.
>
> **Example 2**
>
> In an insurance setting, one of Amelia's skills is processing home insurance claims. For outdoor equipment, like lawn mowers, there's a business distinction between whether or not these were stored "inside" or "outside." In this case, inside means a construction with walls, roof, and a door, typically a closed shed, garage, or similar structure. Outside means anywhere else, including for example in open garages with no carport, and so on.
>
> These are very subtle distinctions, even when they are expressed by users. They are very hard to pick up and easy to misunderstand. Given this, discard attempting to use a spanless entity classifier for this. Instead, Amelia will always ask. 

#### Sometimes No Negative Class
While intent models almost always will have a negative class, spanless entity models sometimes don't. This is when one of the relevant classes must be present in the user utterance.
> [!info]  
>
> **Example**
>
> There is an intent to activate or deactivate a subscription. On the entity level, a spanless entity model is used to capture whether the user needs to activate or deactivate. It has to be either or, there's no in-between or third option, so there's no need for a negative class. The utterance expresses a wish either to activate or to deactivate. Train a spanless entity model with two classes and nothing else.

### Grammars
Grammars are a rule-based intent detection method, where an utterance is matched against defined static patterns.
Table. Criteria to Use Grammars

| CRITERIA | DESCRIPTION |
| ----|----|
| Small variety of in how users express the intent | For grammars to be effective, the variety in how users express the utterance must be low. If there’s a lot of variety in the users’ intent utterances, there’s no way to cover a sufficient share of these using static grammars. Using an intent model is a better option in that case. |
| Small risk of overlap with other utterances | Grammars are naive. If the patterns in the utterance match the grammar rules, then the intent will trigger no matter what. If there’s a risk users can express other intents using some of these same patterns, then grammars are not a good choice.If so, using an intent model trained on training data is a better option. In some cases, grammars can be refined to avoid the overlaps, but then there’s a risk they become too narrow and/or too complex. |

> [!info]  
>
> Example 1
>
> In a large enterprise, Amelia is used for a number internal tasks and frequently asked questions. This includes providing information on the company founder and CEO Lorenzo Suleyman. Very low traffic on this intent is expected, so it's not worth including in an intent model.
>
> Instead, a simple grammar is built to handle this question. There's also virtually no risk users will mention CEOs or Lorenzo Suleyman for other intents, so a basic grammar works well.
>
> Example 2
>
> Amelia has a highly specialized role, where she sets up user access to various systems, pulls reports from various systems, and checks status for various monitoring systems. Users know what Amelia can and cannot do, so the ways they express their intents are quite limited. Typically, intent utterances look like this:
>
> User: "Need access to SalesForce for jdoe."
>
> User: "Get FinRec July report."
>
> User: "Health check VMonitor."
>
> Given the low variation in how users express these intents, they can easily be detected using grammars.
>
> As grammars also easily can pick up and distinguish between the various system names, consider building this into the grammars as well instead of using sub-intents for this.
>
> **Example 3**
>
> For a small Easter Egg intent in an Amelia implementation, if users ask about Lemmi, the company mascot, Amelia will acknowledge this and link to Lemmi's page on the intranet. Therefore, a tiny grammar is built that matches on the word Lemmi.
>
> Example 4
>
> Amelia is designed to politely ask the user to rephrase if a user swears. This is not really an intent, but grammars can be used to pick this up easily.

### Tabular Data
Tabular data is a rule-based detection method more geared towards using various forms of lists than grammars.
Table. Criteria to Use Tabular Data

| CRITERIA | DESCRIPTION |
| ----|----|
| Lists | Sometimes the user’s intent is to a large extent informed by mentioning an item from a given list, sometimes in combination with what should happen to that item. In such cases, consider using tables in tabular data. |
| Unique patterns | When the user provides specific and unique information in the utterance, that’s a give-away of the intent and use pattern matching in tabular data. If an intent is associated with tickets, and the ticket names have specific patterns, they can be detected using regex in tabular data. |
| Small risk of overlap with other utterances | As with grammars, tabular data are blind. They will always hit or not hit. So if there’s a risk that users can express other intents using some of these same patterns, then they are not a good choice.If so, use an intent model trained on training data. In some cases, tabular data can be refined to avoid the overlaps. However, there’s a risk they become too narrow and/or too complex. |

> [!info]  
>
> Example 1
>
> Amelia is used to take food orders. She picks up the menu items the user wants (the “intent”) by checking against lists of all possible items, as given in tabular data. This is combined with checking against customized word lists, also in tabular data, to understand whether the user wants the item added, removed, etc, from the order.
>
> Example 2
>
> In the following example, tabular data is used in combination with an intent model to detect the intent with both on intent level.
>
> As part of her role, Amelia handles requests to check or modify ticket status. All tickets have a ticket code that adheres to a certain format, for example, 2 letters followed by 5 digits.
>
> In a closed implementation, it's a certainty users convey the ticket status intent if they mention a ticket code. Tabular data can match against that pattern to detect the intent. When users express the intent without a ticket code, it can be picked up with an intent in an intent model.
>
> Tabular data is used when it’s the easiest way to spot the intent, and an intent model when tabular data doesn't work.

### Filter
Sometimes, utterances may have certain tells that, while hard to capture predictably with an intent in an intent model, are highly significant for what the user wants. In this situation, consider implementing a filter to filter out these utterances and redirect them before a conventional intent is executed.
This intent detection method should only be used in very specific cases. 
> [!info]  
>
> **Example:**
>
> For a company providing television and internet services, Amelia handles incoming requests regarding internet, but not television. However, sometimes users mistakenly end up in the wrong channel and ask her about television issues.
>
> Therefore, these requests need to be filtered out as much as possible so Amelia can redirect those users to the correct channel. However, placing 'television' in an intent seems difficult, in part because the range of television issues is so great. In part because they are often very close to internet issues except for certain keywords being different.
>
> After testing, it's possible to confidently identify 90% of television requests by matching against words and patterns. For example, when users mention decoder, TV, and similar TV-related words and phrases - they're almost consistently talking about television issues. This intent is implemented as a filter that is checked before any conventional intent is executed. If the user utterance passes through the filter, Amelia proceeds as normal. But if the utterance is caught in the filter, Amelia will redirect the user to the television channel or could ask a disambiguation question.

### Sweeper
Sometimes, short utterances with only a keyword or two can express a particular intent or indicate a theme that can be picked up. Often, this will be hard to do in an intent model. Intent models are designed to read natural language, not keywords. Using grammars or tabular data to match blindly against the keywords fails because these keywords may pop in utterances expressing various intents. Amelia should handle these keywords in a particular way only when the keywords are more or less stand-alone.
For these short utterance intents, consider using a *sweeper*. This is a method where, after* *no intent class is hit by an intent model or grammars, the short utterance is swept to check for any of the relevant keywords. This is done within a BPN, using entities, typically with tabular data. In practice, this means a check on entity level is added under the negative (no intent) class.
> [!warning]  
>
> Whether or not an intent is picked up in a sweeper, the intent also can be a regular intent in, for example, an intent model. When the intent is expressed with a full sentence in natural language, the intent also will be picked up in an intent model. When it's expressed using a single keyword, the sweeper captures the intent. Two different intent detection methods are deployed to detect the same intent, based on how the intent is expressed.
> [!info]  
>
> **Example 1**
>
> In the role of an internal HR agent, Amelia is trained to help users with their expenses. She has a number of intents for this in an intent model, for example, FileExpenses, MealExpensesRates, ExplainMileage, and so on.
>
> But sometimes users only say, for example, "expenses" or "expenses help." If so, Amelia should present the issues she can help with regarding expenses. Building this as a distinguishable and balanced intent in an intent model will be tricky and a grammar can't handle this scenario satisfactorily.
>
> Instead, this intent is covered with a sweeper in the intent architecture. A tabular data entity checks for matches on "expenses," "expenses help," and so on, whenever no intent is found on intent level. If there is a match, Amelia will give the user options for what she can help with regarding expenses. If no match, Amelia handles it as a regular utterance with no intent detected.
>
> **Example 2**
>
> As a whisper agent for customer advisers in a bank, there two intents users frequently express with a keyword or two.
>
> -   CheckCreditRate - An intent to check the credit rating of a customer, often expressed as just "credit rating jane doe" or "john doe credit score."
> -   LookUpCip - An intent to look up what's internally called "CIP" ("Consumer Investment Plan"), often expressed by the user telling Amelia just "cip."
>
> Both the words "credit rating/score" and "cip" can easily turn up in utterances expressing entirely different intents: "What's the minimum credit score for granting auto loans?" or "Help me set up this client with the 3,5 % investment plan, I believe it's the one called Pro-Active in CIP".
>
> It's only when the utterance expresses no other intent that these keywords should trigger the intents for CheckCreditRate and LookUpCip. Therefore, a sweeper BPN picks up the intents, as in the example above.

To use a sweeper, enter or stay inside a BPN. This means that:
-   A sweeper in closed implementations is easiest, as the user is already inside a BPN, where branches can be added as needed.
-   To use it in open implementations, designate the negative class of the intent model as an intent to execute the BPN that contains the sweeper. This will have some consequences to consider. For example, the escalation logic for failed intent recognition won't come into effect by itself, but will have to implemented in the BPN.
    > [!warning]  
    >
    > When using a sweeper in this way, pay attention to how this will affect any context switching inside a conversation.
-   In closed implementations, the sweeper BPN will only work in the edges where it's implemented.
-   In open implementations, it will work on any edge where context switching is enabled. Be careful about any unwanted context switching this may cause. If any of the keywords is something a user might say as part of a conversation without expressing any intent then that can be an issue.
### Edge Expressions
In special cases, BPN Ask task edges can be used to recognize intents. Three conditions must be met for edge expressions to be a relevant alternative.
Table. Criteria to Use Edge Expressions

| CRITERIA | DESCRIPTION |
| ----|----|
| Closed implementation | For edges to be an alternative, the utterance expressing the intent will have to come on an Ask task edge in a BPN. So this is only available in closed implementations. |
| Context switching typically won’t be an option | As the intent detection is tied to Ask tasks, context switching within the conversation will not happen unless these edges are added on all relevant Ask tasks. |
| Short and highly predictable utterances | The intent will in part or full be expressed with short utterances. There’s a limited predictable set of expected utterances, which are short and to the point. |

In the example below, edge expressions are used in combination with other intent detection mechanisms.
> [!info]  
>
> Example
>
> Amelia takes food orders. The menu items are picked up by entities, and so the same BPN is looped back for as long as the user adds new menu items, until the order ends. In this looping BPN, Amelia asks questions like, “Would you like anything else?” and “What else can I get you?”
>
> When the user is done, they can signal this intent in variety of ways, “Thanks, I’m ready to pay now”, “Nothing more”, “Done”, and so on. If the user wants the order cancelled or restarted, they say, “Wait, you got it all wrong”, “No, no, please go back to the beginning”, “Cancel”, “Start over”, and similar utterances.
>
> The longer more complex utterances used to finish the order may be best handled by an intent model. Meanwhile, the short one-two word utterances are much more easily covered on an edge from a BPN Ask task, so edge expressions on flow lines are used to detect those. That way, two intent detection methods are combined for one and the same intent, using each method for what it’s best at.

## Define and Shape Intents
Creating an intent architecture includes reshaping some or all intents after they've been defined as an intent scope. This happens because of the nature of the intents, the way they're structured, and how they'll be detected by Amelia.
### Merge Intents to Disambiguation Intent
Intents that are virtually indistinguishable have to be merged. The merged intents become a single disambiguated intent, where Amelia asks if the user wants A or B, then sends the users down the correct branch. Instead of trying to recognize the correct intent, the solution is a multi-step intent recognition of intent. While this creates an extra step for the user, there's no other option because the intents are close and often indistinguishable. If the intents are not merged, intent recognition for these two intents will suffer, as will the user experience.
> [!info]  
>
> **Example**
>
> The intent scope identified one intent to report fraudulent transactions and another to report suspicious transactions. Amelia should handle these two situations differently, as there are a few extra steps for suspicious transactions, to check if they are indeed fraudulent.
>
> There is very short distance between these two intents. Users express the two in quite similar and interchangeable ways. For example, an utterance like, "I didn't make that transaction of 49.90 yesterday" can mean the user is convinced it's fraud, at other times that the user considers it to be suspicious.
>
> In the architecture, reshape these two intents into a single merged intent. In the BPN process this new intent triggers, build in a disambiguation question to determine whether the user knows the transaction is fraudulent or is only suspicious. That way, Amelia will know exactly what the user means and avoid misunderstandings.

### Merge and Expand
Sometimes merging the intents into a disambiguation intent can be avoided. The intents are merged and the scope of the merged intent expanded. That way, the intents covers both original intents but with no sub-intents.
> [!info]  
>
> Example
>
> As an internal IT service assistant, one of Amelia's skills to handle inquiries about printers. The intent scope has identified two intents, one to connect a computer to a printer, and one to report a printer needs service. However, the utterances for both are sometimes indistinguishable, for example, “I’m trying to print, but nothing seems to happen.”
>
> To handle this, the intent is expanded to cover for both, by adding extra information (purple) to Amelia’s answer: “To connect your computer to your nearest printer, please follow this guide. If the printer needs ink or toner refill, or is out-of-service, please call 999-999-999.”

If Amelia is in a live environment, this can sometimes also apply to intents dogged by false positives. In those cases, sometimes simply expand the intent so that Amelia’s answer also covers the extra question/request that this intent (unintentionally) tends to trigger.
### Merge Intents to Disambiguation Intent + Add Sub-Intents
At times, it makes sense to keep the original intents from an intent scope as sub-intents to the new merged intent. This typically applies to layered intents which users sometimes express generically and sometimes in great detail. In these cases, the primary intent is placed on the intent level with the sub-intents on the entity level. This is described in more detail in the Intent Structure section.
In this situation, if the intent is hit, and it’s clear from the utterance the user wants sub-intent X, skip disambiguation and go straight to the sub-intent X branch. If the utterance hits the intent, but it’s not clear whether the user wants sub-intent X or Y, Amelia will disambiguate.
To use this approach successfully, the various sub-intents must be sufficiently distinct from each other for Amelia to pick it up when the user is sufficiently specific. She can make this distinction in two ways:
-   By recognizing static patterns that are taken as fail-safe indication of what entity the user is looking for. This is done with regex or tabular data.
-   By adding a second classifier at entity level. If the merged intent is hit, a new classifier trained in the various sub-intents is run. If there is no match in this second-level classifier, Amelia will disambiguate. If there is a match, Amelia will jump straight to the branch of that sub-intent.
> [!info]  
>
> **Example:**
>
> In a banking setting, an intent to add authorized users to a card, and a different intent to add users to a shared account. However, users often express this in similar ways. Sometimes it's not clear if the user wants to share a card or an account.
>
> To deal with this, these two intents should be merged and two sub-intents added. The sub-intent for card will trigger when the user mentions words like "card", "visa", and so on. The sub-intent for account will trigger when the user mentions words like "account", "savings", and similar utterances. If no sub-intent is triggered, Amelia will ask the user if they meant card or account. 

### Change Intents to Sub-Intents
If intents have a vertical distance, instead of merging intents, one or more of the intents can be converted into sub-intents.
> [!info]  
>
> Example
>
> Amelia is a shopping assistant for kitchenware. There is one intent for ovenproof dishes, and one for clay pot ovenproof dishes. To optimize intent recognition, the clay pot variation converts into a sub-intent to the general ovenproof dish intent.
>
> So if the user says, “I want to know more about ovenproof dishes,” the intent is triggered but not the sub-intent. Amelia then provides general information to the user about ovenproof dishes, including clay pot dishes.
>
> If the user says, “Want to know more about ovenproof dishes. The clay ones, like a römertopf," then both the intent and the sub-intent is triggered. In this case, Amelia gives the user specific information about the clay-pot.

### Graceful Intent Switching
Instead of merging intents, sometimes graceful intent switching between the intents works best. The language and logic of Amelia says and does is tweaked to allow the user to easily switch to the correct intent, in case the wrong intent was triggered.
> [!info]  
>
> Example
>
> Users who need the intent ManualLoginReset often hit the intent ForgotPassword. To solve this, build in graceful intent switching:
>
> User: "I can’t log in."
>
> Amelia: "Please give me your email address, and I’ll send you a link for resetting your password."
>
> Amelia: "If you don’t have access to your email, just let me know, and I’ll help you."
>
> User: "I don’t have access to the email, I think I used the work email in my former job."
>
> Amelia: *kicks off process for ManualLoginReset*

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
