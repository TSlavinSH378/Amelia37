{% version "3.x" %}
Intent recognition isn't only determined by how Amelia understands the user. It also matters how the user expresses their intent to Amelia. While working on intent recognition, it's important to be aware of this part of the equation as well.
# User Understanding of Amelia
In terms of intent recognition, it's an advantage that users have a reasonable understanding of Amelia and her role. Typically, that can include points covered below. 
## Who and What Amelia Is
Users express themselves and behave differently based on their ideas about who Amelia is and their reactions to interacting with her. Their ideas and reactions can impact intent recognition.
### Virtual Agent vs Human Agent
The distinction between virtual and human agent is most important. The presentation should ensure all users understand that Amelia is a virtual agent.
-   If half the users knows Amelia is a virtual agent, while the other half thinks she is a human agent, this can give a wider variety user utterances and behavior. This in turn makes it harder to train for intent recognition, as more bases have to be covered.
-   When speaking to a virtual agent, users may express their intent with less complexity, nuance and context than to a human agent. This can often be beneficial for intent recognition. The user understands that a virtual agent can take in less than a human agent, and so may leave out irrelevant information and express the intent more clearly.
-   In addition, users can react negatively if they think they speak to a human agent, then realize they speak to a virtual agent.
> [!info]  
>
> Example
>
> The first user utterance below has a higher risk of hitting the negative, due to irrelevant context information, ie noise (purple). The second simplified utterance, directed at a virtual agent, is much more precise in terms of intent and should normally be an easy hit.
>
> User: “Hi there! I’m waiting for a delivery from you, that I think should have arrived today. FYI, I’m going on vacation to Spain on Friday, so it’s becoming urgent. Is there anything you guys can do? Where can I track it?”
>
> User: “I’m waiting for a delivery from you. Where can I track it?”

### Virtual Agent vs Keyword Search Engine and Simplistic Chatbot
In some cases, users may mistake Amelia for a keyword search engine or a simplistic chatbot. Instead of speaking to Amelia in natural language, they provide a couple keywords or speak in incomplete sentences. This typically is not beneficial for intent recognition, depending on the intent architecture. In the presentation we can influence users to not go in this direction.
> [!info]  
>
> **Example**
>
> To continue with the example from above, if the simplification is taken too far, user utterances become as shown below. If this intent is to be detected by an intent model, the utterance below will give the classifier less input to work with than a full sentence utterance. This increases the possibility of hitting the negative or a wrong intent.
>
> User: “tracking info”

## What Amelia Can and Cannot Do
In some use cases, we can guide the user on what Amelia can / cannot do. The aim is to limit the variety in the utterances that users provide, thus allowing for easier intent recognition training.
-   If the users are given carte blanche, that will give a wider variety in what users ask about. This poses a challenge in terms of intent recognition, as it’s harder to train Amelia for wide variation, just as it’d be for a human agent.
-   If users have an understanding of Amelia's role, or even an understanding of the topics Amelia can handle, that may affect our intent recognition positively.
> [!warning]  
>
> Users often adopt the vocabulary they are exposed to. If users are clued in to what Amelia can and cannot do, some users will mimic the language. Therefore, it's important to word any descriptions carefully, so any descriptions and recommendations will work when users adopt it for their utterance.

## How to Interact with Amelia
There are several key points to keep in mind about intent recognition and interactions with Amelia.
### Expressing the Intent
Intent recognition usually works best when a user utterance is not too long, not too short, and to the point. As such, try to influence users to express themselves accordingly.
### Response to Unsuccessful Intent Recognition
When intent recognition is unsuccessful, try to influence the user to respond to this failure in a way that increases the chance of successful intent recognition on the next attempt. Or at least help them avoid repeated failed intent recognition.
Typically, try to achieve these options:
-   The user rephrasing in a way that gives a higher chance for successful intent recognition.
-   Having the user escalate directly, if this is an option in the use case design.
On the opposite end, avoid user behavior detrimental to intent recognition:
-   The user just repeating the utterance, or making only minor changes to it.
-   The user responding with an utterance that only contains a couple of keywords, as they wrongly concludes Amelia is a search engine or simple chatbot.
-   The user giving a multiple sentence utterance that gives too much context (noise), as the user believes the lack of detailed information was the reason intent recognition failed.
Normally, these are the most relevant ways to influence users in a positive way:
-   If the user utterance fails to trigger the correct intent, and instead hits the negatives, Amelia’s reply can instruct the user what to do next. These replies are part of Amelia’s response pool, and are customizable, for example, she says, “I’m not sure I understood. Can you please rephrase your question?”
-   Also consider including this kind of guidance in other parts of the presentation. In the case of false positives, when a wrong intent is hit, Amelia’s reply utterance won’t be helpful guiding the user what to do next. The user will rely instead on information in other parts of the presentation for any guidance.
-   Ensure users can escalate to a live agent easily in case of repeated failed intent recognition. This includes efficient logic in the BPN process to ensure the user doesn't get stuck. In some cases, include an intent for escalation to capture user utterances asking for escalation, for example, “I need to speak to a human," then ensure they get escalated. Maybe consider adding an option for direct escalation in Amelia's interface, for example, a button users can click to transfer their conversation to a human agent.
# Presenting Amelia
To get information about Amelia and her role across to users, there are various places in an Amelia deployment that can be leveraged. The web page and app environments normally clue users in on various things and can inform user behavior.
## Referral Information
Before users arrive on the web page or in the app, they may have been directed to it from a different place. Any information given around inbound links and link labels can influence user behavior.
> [!info]  
>
> **Example**
>
> Click here to speak to us! - This may result in the user clicking the link expecting to chat with live agents, then not bother to look at any information provided at the landing page and app, and start chatting with Amelia believing she is human.
>
> Click here to speak to our virtual agent Amelia! - This sets user expectations much more clearly, which in turn can influence user behavior positively.

## Amelia's Greeting Statement
In addition to information displayed around the actual chat, Amelia speaks directly to the user in her opening statement. This is a spot to place relevant information that helps the user ask in a way that affects intent recognition positively.
> [!info]  
>
> **Example**
>
> If we use Amelia to help users file insurance claims, and that's the extent of Amelia's skill, this detail can be specified in the greeting statement. That can avoid lots of user utterances that may cause trouble. This can be helpful even if the user is on a web page specifically designed for filing insurance claims.
>
> Amelia: "Hi, I'm Amelia. I'm here to help you file your insurance claim. What can I do for you?" - This frames the conversation towards Amelia's skills, increasing the chance of relevant intent utterances.
>
> Amelia: "Hi, I'm Amelia. What can I do for you?" - Open-ended, which can mean there will be a higher risk users will sometimes ask for various things Amelia can't handle. This may in turn be more challenging in terms of intent recognition.
> [!warning]  
>
> Depending on the web design, many users may not even read Amelia’s greeting statement, as they assume it’s just a generic greeting. Be careful with placing important information only here. If this for example is the only place the user is informed that Amelia is a virtual not human agent, a significant share of users may believe they're speaking to a human.

## Amelia's Response to Perceived Negatives
If no intent is triggered by the user’s utterance, Amelia's response can guide the user’s next step. Unlike the greeting statement, this is a response the user will read. Including relevant content in her response can avoid the user repeating their previous utterance or rephrasing in unhelpful ways. The risk for repeated failed intent detection is minimized.
Here are some candidates for relevant information Amelia can include in her response to utterances that don't match any intents:
-   Ask the user to rephrase and give advice on how to rephrase.
-   Point out what topics she can and cannot help with.
-   Indicate how the user can escalate, if relevant.
> [!info]  
>
> **Example**
>
> Continuing with the example above, a user starts disputing a previous claim that was not accepted. This is beyond Amelia's skills, and hits the negative intent. To remain helpful, and avoid repeated tries for a non-existent intent, we can for example do as follows in Amelia's response:
>
> Amelia: "I'm sorry, I did not understand that. I'm happy to help you file insurance claims, but if you have other questions, please call us on 999-999-9999."

# Platform and Audience
The platform and audience also can affect intent recognition and interactions with Amelia.
## Device
Users may phrase themselves differently on desktop and mobile. If Amelia is to be used largely by only one of these, keep this in mind. If Amelia is to be used on both, that can give a broader variety of user utterances. In turn, ensure that both variations are covered, to achieve satisfactory intent recognition.
The table below shows a few typical differences in user utterances mobile vs desktop:

| Mobile | Desktop |
| ----|----|
| Shorter utterances. Fewer multi-sentence utterances. | Longer utterances. More multi-sentence utterances. |
| Potentially more “texting language”, ie abbreviations and simplifications like “4” instead of “for”. | Potentially more correct language. |
| Potentially worse spelling, though, with the coming of auto-correct and auto-suggest, mobile can also give better spelling than desktop. | Potentially better spelling. |

The device can also determine what user groups will tend to use Amelia, see below.
## Channel and Conversational Interfaces
The channel, and the conversational interface of that channel, can influence how users phrase their utterances, and thus intent recognition. The medium messages are expressed in often impacts how a message is shaped.
### Chat
The channel Amelia is used in influences what the user utterances will look like. A full-site chat experience can easily give different longer utterances than a small popup screen at the bottom right of a user screen. As such, the channel is worth keeping in mind when working on intent recognition.
> [!info]  
>
> **Example**
>
> Users are writing very long initial utterances to Amelia to express their intent. To encourage shorter utterances, that are easier for Amelia to understand, the conversational interface is tweaked.
>
> Start by changing the size of the message field where users enter their utterance. This was on the larger side, and all text remained visible even with very long utterances. Reduce the size of this field, as well as only give a smaller text length remain visible. If the user writes longer than this, the first part will disappear and they’ll have to move back to see it.
>
> Next, to further reduce the length of the user's utterances, one option is implementing functionality for maximum message length.

### Voice
If the user can communicate with Amelia by voice, using speech-to-text, this can have significant influence on user interactions.
-   **How the user phrases the utterance**. Users may be used to low quality robot voice communication from speech recognition in phones. If so, the share of intentionally simplistic and short utterances may go up.
-   **How the speech is transcribed to text**. Punctuation may be handled differently, or not at all, according to what speech-to-text technology is used.  
## Audience
On digital platforms especially, lingo in user utterances can vary according to user group characteristics. Millennials may generally use a casual and conversational language, while baby-boomers phrase themselves more formally and email-like. IT professionals will generally use a different language than non-technical consumers seeking IT help.
When working intent recognition, be mindful of the audience expected to use an Amelia deployment. Tailor Amelia’s intent recognition abilities for that group.
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
