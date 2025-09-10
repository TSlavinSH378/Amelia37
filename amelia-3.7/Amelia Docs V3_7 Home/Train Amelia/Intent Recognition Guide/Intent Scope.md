To recognize user intent, Amelia uses one or more intents which make up intent scope. The use case determines how high or low recognition might be for Amelia. Intent recognition plus a limited level of disambiguation, sorting out similar but different intents, are critical success factors. The selection and design of Amelia's roles and skills must address intent scope to ensure achievable levels of intent recognition.
# Identify the Intent Scope
Six tests can identify and validate intents to determine which intents belong in the collection of intents, or intent scope, Amelia uses to perform her role and use her skills.
When the intent scope is extracted and identified, the focus must be critical about what constitutes an actual intent, and for any intent accepted as a valid intent, whether it qualifies to belong in the intent scope. This can be framed as passing 6 tests or 6 criteria that must be fulfilled. Any and all intents that pass these tests, will in principle be part of the intent scope. 
Tests 1-2 represent the key principles to extract and identify a complete intent scope for role or skill set. Once a full intent scope passes the tests 1-2, the intent scope usually must be qualified and narrowed down according to any business value and forms of viability. Business value is assessed in test 3 and viability in tests 4, 5, and 6.
## 1. The Independence Test
Because Amelia is tasked to replace an existing function, it's easy to create intents based on business logic, backend system architecture, organizational rules, and similar factors. However, this is not best practice. Create intent scope independent of pre-existing frameworks. If an intent only replicates an existing framework, it should not be used.
Following are a few examples that all illustrate how this should not be done:
> [!info]  
>
> Example 1
>
> A company uses a ticketing system for handling a variety of issues. Users select the appropriate ticket type, describe the issue, and the ticket is then assigned onwards according to the ticket type. To automate this, Amelia will help users report their issues, as well as to automatically solve a number of the simpler tickets immediately. Currently, the ticketing system has 150 ticket types.
>
> Given this, the 150 ticket types are assumed to be 150 intents (as our intent scope) and implementation begins. -- TEST FAILED!
>
> **Example 2**
>
> Amelia will deal with external inquiries. These are funneled to four different departments in the organization who tag and handle them according to internal business rules for their departments.
>
> So the intent scope is split into four buckets, corresponding to the four departments, and then define specific intents according to the set of tags the various departments give the inquiries. -- TEST FAILED!
>
> Example 3
>
> Amelia is to function as a whisper agent for customer agents. The live agents currently consult a number of back-end systems for relevant information, but it’s cumbersome to look up and hard to maintain, so this knowledge should be centralized with Amelia. Agents will then ask Amelia for the relevant information.
>
> To solve this, the information architecture in these back-end systems is researched and the intent scope mapped out according to how the information is currently divided between the systems, as well as how the information is organized within the various systems. -- TEST FAILED!

All these examples start in the wrong end. Such one to one mapping very rarely (never) translates well into a good intent scope that can yield high intent recognition. If these factors are allowed to form the intent scope, intent recognition efforts will be forced into a straitjacket.
## 2. The End User Test
Instead of creating an intent scope based on pre-existing frameworks, intent scope should accommodate user needs and behaviors.
-   What intents will users express to Amelia?
-   How users will express intents?
-   How many users will work with Amelia?
Exactly how we approach this can vary according to how loosely or precisely defined Amelia's role is in the first place. Sometimes, Amelia's skill set is already quite clearly defined. The job is then to determine the intents within that skill set. Other times, we may be more free to determine the skill set overall. If so, we can do a more free exploration.
> [!info]  
>
> **Example 1**
>
> Amelia’s skills include helping hotel guests order room service and booking tables in the hotel restaurant. This will be a big help for busy reception staff. But user research finds there is limited appetite for booking restaurant tables digitally, as guests tend to do this in person in the lobby reception or at the restaurant.
>
> The intent fails the end user test.
>
> Research also finds guests wish to digitally book both the hotel’s spa treatments and the tourist trips the hotel offers via a third party. To ensure that there is value for users, consider shifting Amelia’s skill set to include those capabilities.
>
> **Example 2**
>
> Amelia will help employees with the practicalities around receiving guests in the office. In the business case, there's an assumption an intent should exist to handle this chore. User research, however, reveals users don't ask this. Rather, they express specific intents related to temporary ID cards, guest wifi access, ordering food, and so on.
>
> This means a general intent for receiving guests may not pass the end user test. But more specific intents certainly do, and should be part of the intent scope.

User needs and behaviors can be determined through quantitative and qualitative research.
Table. Quantitative Analysis Options

| Option | Description |
| ----|----|
| Chat analysis | If existing chat solutions cover some or all of Amelia’s skill sets, analyze the chat logs systematically and comprehensively to identify intents. Ideally, this is done both manually and automatically.Manually, to get a systematic and quantified overview of the latent intents the data. This also helps empathize with users by stepping into their shoes, and to deepen an understanding of the use cases.Automatically, to listen directly to the data, instead of filtering it through a potentially imprecise or prejudiced understanding. For how to do this, see;Cluster Analysis of Unlabelled Intent Data in V. Resources. |
| System data | If user inquiries and issues relevant to skills are stored in some system, they can analyzed to help identify intents. |
| System tagging | Sometimes relevant inquiries and issues are tagged or grouped in some way or other in a system. For example, this could be tags given to incoming issues in a CRM system, the ticket types used on incoming issues in a ticketing system, or similar grouping. This can give an indication about what intents belong in the intent scope.That said, be mindful of the data quality. Tags or groupings may be incomplete, unsound, or outdated. The actual tagging and grouping also may have been done sloppily. |
| User traffic on websites | Website traffic analytics have the advantage that they are actual user footprints, not labels set by anyone else, and so can give us indications about user pains and interests.However: web pages are a dramatically different format from a conversation. The user group may be different than from the one Amelia will be exposed to, and it can be hard to gauge exactly what users were looking for on a given web page and whether they found it. So while these analytics are interesting, they should be read with caution. |
| Other relevant data sources | ... |

> [!warning]  
>
> In all of the quantitative data above, always be mindful the apparent intent may not be what it seems on the surface.
> [!info]  
>
> Example
>
> There’s high traffic on the reset password FAQ page on a website. This can mean that a lot of users want to know the procedure for this. But it can also mean users do know the procedure for it but have not received their password reset email or have other issues with actually performing the procedure.
>
> Given this, the intent is not necessarily how do I reset my password. It could easily be troubleshooting for password reset.

Table. Qualitative Analysis Options

| Option | Description |
| ----|----|
| Interviewing / testing end users | This is the best source of truth for what users need, and so what intents they find valuable and how they think about these intents. |
| Interviewing live agents and their supervisors | This is usually representatives from a customer center, an IT help desk, etc.They typically have valuable insights into what users ask about, including;what users actually mean, no matter how users express it or how it is logged in a given system. They also know where users would like to be relieved and where they think intents may be too complex for Amelia to handle. |
| Input from subject matter experts | Among other things, subject matter experts can provide a deeper of understanding of the intents and how they interrelate. They can also provide insights into how intent scopes may change and develop, as the subject matter evolves. |
| Aligning with channel strategies etc | If there is a plan to push or incentivize users to use Amelia for certain purposes, it’s insufficient to look at historical data. If this is the case, plan the intent scope taking this into account, and make sure to coordinate with the right people to align.Typically, this can be related to new channel strategies, organizational changes, changes in the software infrastructure, and similar. |
| Other relevant sources | ... |

## 3. The Business Value Test
Once an intent scope passes the first two tests, align it against the business value. Measure whether or not the user research and analysis and intent scope match the original business case proposition. If there is a mostly or complete alignment, there is both user value and business value.
> [!info]  
>
> Example
>
> The business case for Amelia is to handle various forms of password resets and account unlocking. Today, these mundane tasks tie up significant resources in a busy IT department. Having performed user research and identified an intent scope, there is indeed a high demand among users for these services.
>
> Amelia solving these tasks has high value for the IT department staff. The intent scope passes the business value test.  

This test also is a good opportunity to reduce the intent scope to leave out any parts that do not have business value. Hopefully, these will be intents never intended for Amelia to handle directly.
> [!info]  
>
> **Example**
>
> Continuing from the previous example: In the intent scope, a couple of intents relate to setting up new accounts for certain specialty software a small subset of users use. Setting up these accounts, however, is a manual process there’s no good way to automate. They are also rare occurrences.
>
> So while there is user value to these intents, there is no business value in having Amelia handle it. Given this, these intents are marked as out-of-scope in the intent scope. They fail the business value test.

## 4. The Amelia Test
Next, keep in mind Amelia is the tool to handle the intent scope. Qualify the intents with a review of Amelia's capabilities. Avoid developing an intent recognition strategy that is not viable given her intent recognition technology.
For example, some intents may be solved better by optimizing the logic of a search engine instead of relying on Amelia to do something she's not optimized to do.
> [!info]  
>
> Example
>
> In the intent scope, 1/3 of the intents clearly lend themselves to being solved with search engine logic rather than a virtual agent. Amelia, however, is not designed for search. If we force her to solve this part as if she were a search engine, this would yield sub-par results.
>
> In this case, consider what to do with this part of the intent scope with a realistic view of what Amelia can and cannot do.

## 5. The Organizational Test
The intent scope also should be developed in a way that optimizes the organizational framework around it, as one way to solve problems in its daily business. Hopefully, Amelia fits the organization clearly. 
If the intent scope has altered or added nuance to the use cases, it's also possible the organizational impact has changed. New parts of the organization might need to be included or responsibilities shift. In some cases, the intent scope at this point might challenge the organizational framework and require a business decision about if and how to adapt the organization.
> [!info]  
>
> Example
>
> In the intent scope, in addition to expected intents, research finds a high demand among users for various tasks that are today handled by the reception staff. For example guest ID cards and guest wifi. These uses cases clearly have promise. In the business proposition, however, the reception was not included as part of the organization that is to use Amelia.
>
> So unless there’s an opportunity and desire to bring the reception onboard, these intents do not pass the organizational test.

The organizational framework also might change. As the intent scope is evaluated, track how the organization will look like at the end of the implementation process.
> [!info]  
>
> Example
>
> Amelia is to replace a legacy system for sorting and processing customer complaints. This system is tied to an old framework of routines and responsibilities in the organization. Since then the organization has undergone various organizational changes. It also replaced the CRM system where the complaints are logged. The organizational framework, however, is still largely the same, though it's now partially redundant and patched up numerous times.
>
> As the intent scope is identified, it becomes clear that parts of this organizational setup is a bad fit for what will be the most natural intent scope. But if forced to adjust the intent scope too heavily according to organizational factors, the result will be a sub-standard intent scope which will inherit and cement the shortcomings in the organizational framework.

Finally, be aware the organizational framework may may change. Often, implementing Amelia is part of a wider reorganization where Amelia is a single component inside a maze of circumstances and priorities. In larger entities especially, this kind of reorganization can easily become a shifting ground of diverging interests with unclear outcomes.
With this mind, as the intent scope is evaluated, try to stay on top of what the organization will in fact look like at the end of the process. Losing sight of that risks defining an intent scope that’s misaligned with the organization that will manage it. The result fails the organizational test.
## 6. The System Test
The intent scope also must respect the system infrastructure. The system limits what intents are relevant and viable for the intent scope. In most cases, the system impacts are worked out as the business case is defined. However, it's important to confirm the intent scope is appropriate for the system infrastructure.
Typically, the issue of system fit is resolved as the business case was defined. If so, this test is passed long before the intent scope is defined. However, it’s still important to tick the system viability boxes.
> [!info]  
>
> Example 1
>
> Amelia dealing with expense reporting will have great value provided Amelia can take the user through the end-to-end process of filing an expense claim. However, the relevant integrations to make this happen don't exist. So this intent, while promising, fails the system test.
>
> Example 2
>
> Amelia is to operate as a factory facility agent, used by coordinators and on-the-ground workers for various tasks. The current process for reserving assorted factory machinery, such as trucks and lifts, is manual and inefficient.
>
> This looks like a prime candidate for attractive intents for our intent scope. However, the system that accepts these reservations is a legacy system that cannot integrate with Amelia. Given this limitation, these intents are left out of the intent scope.
>
> Example 3
>
> Amelia will guide users through various ticket submission processes, as well as automatically solve a selection of those tickets. For some use cases, Amelia will rely on a new ticket system that’s under development and will be rolled out in tandem with Amelia.
>
> However, the specifications for this new system has changed during the development process. Amelia won't be able to use this system to handle parts of the original scope after all. Instead, users will continue to do this in a legacy system, at least for the foreseeable future.
>
> The specific intents related to these tasks have now become moot in our intent scope. They do not pass the system test.

# Evaluate the Intent Scope
With intent scope tested, the next step is to evaluate the difficulty of achieving intent recognition and what amount of disambiguation is needed. There are four factors to consider.
## 1. Number
More intents in a scope usually means more difficulty Amelia will have achieving high intent recognition. She will have too many intents to select from when predicting user intent. However, in cases where the other evaluation factors determine the intent scope is reasonable for Amelia, high intent recognition might be possible.
Intent recognition will not always be proportionally harder with more intents. If the intent scope is reasonable according to the points below, high intent recognition might be achieved with a high number of intents. However, it does require a bigger effort to build big than to build small.
> [!info]  
>
> **Example 1**
>
> In her role as an administrative agent at a large dental office, scheduling and managing appointments and collecting relevant information from patients, we have identified 12 intents for Amelia to recognize.
>
> This is a modest scope. Based purely on this variable, high intent recognition can be achieved with no herculean effort needed.
>
> **Example 2**
>
> Amelia will work as a system support agent internally in a company. This means Amelia will have to be taught a number of skills. For various software applications used across this company, Amelia will handle accesses, permissions, installation, renewals, and so on. For many of these systems, Amelia also will do troubleshooting and answer a large number of questions concerning the use of the system. In total, to fulfill this role 100%, 150 intents have been identified that we want Amelia to handle.
>
> This is a much taller order, requiring a substantially bigger effort. The end result may have noticeably lower intent recognition than the example above.

## 2. Distance
The difference between subject matter of two intents determines their distance. Asking Amelia to view subscription plans and order a subscription are closely related intents. Changing a password and checking an expiration date have greater distance. The greater the distance between intents, the easier intent recognition becomes. Closely related intents are harder for Amelia to determine intent.
> [!warning]  
>
> Distance between intents should be viewed from the user point of view. While apples and oranges are different fruit, with obvious distance, users might ask for them the same way, by saying, "I want fruit." If so, there's little actual distance.

### Types of Distance
The distance between intents can be measured as horizontal or vertical. While the distance between intents can be one, some, or both, the solution for horizontal and vertical distance can be different.
#### Horizontal Distance
How close or far intents are related determines horizontal distance and how much overlap to expect in how users express one or the other intent.
Table. Horizontal Distance Examples

| High Distance (easier) | Low Distance (harder) |
| ----|----|
| a. change password | a. see current subscriptions |
| b. create new account | b. get new subscription |
| c. see current products | c. change current subscription |
| d. check expiry date | d. delete subscription |
| e. subscribe/unsubscribe to newsletter | e. check end date for subscription |

#### Vertical Distance
Intents with hierarchical relationships have vertical distance. As a result, it's possible users can overlap in the way they express one or the other intent.
For example, a ChangeAccountUsername intent is a subcategory of a ManageAccount intent. In expressing these two intents, there's likely low vertical distance between how users ask for one or the other.
Often, vertical distance will be reflected in how generic or specific users are when expressing their intent. An intent higher up in a hierarchy tends to get more diffuse user inquiries, for example, “Please open my account, I have some things I need to change there.” An intent lower down in the hierarchy gets more precise inquiries, for example, “Please open my account, I need to change my username.” There can be significant overlap in the how they’re asked - low vertical distance - due to the close hierarchical relationship.
### Forms of Overlap and Ambiguity
Low distance intents often provide a challenge for intent recognition because of language pattern overlap and semantic ambiguity. 
#### Language Pattern Overlap
Language patterns in related intents resemble each other more than language patterns in unrelated intents, even if the intent expressed in the utterance is clear. This can increase the chance of mishits, or need for disambiguation, because Amelia has difficulty distinguishing between related intents.
> [!info]  
>
> Example: Take the low distance intent scope from the table above. In the following utterance, there are language patterns that indicate three different intents at once:
>
> User: “I’ve deleted my subscription, as I want to change it and want to get a new.”

The correct intent is new subscription, but the utterance contains strong language patterns that mean it easily can be misunderstood as change subscription or delete subscription.
Relevant intents with unique patterns to distinguish them from each other can work if there’s a lot of overlap. If so, use the common patterns to identify the general intent, then use the unique patterns to determine what specific “sub-intent” the user asked for. If so, it's possible to achieve high intent recognition even if the intents are low distance (see Depth under Intent Architecture).
> [!info]  
>
> **Example: **In the intent scope, there are a number of intents to get access to different systems. Utterances for these intents could be very similar (“I need access to system X.”, “I need permissions to use system Y.”)  However, the exact system they need access to is unique for each intent; as long as users mention the system, the intent is easy to determine. While these various intents are very low distance, they can still be easily recognized, due to the unique system name. If the user doesn’t specify the system, or mentions a system Amelia isn’t trained to recognize, Amelia can disambiguate.

#### Semantic Ambiguity
Low distance intents typically increase the risk of ambiguous utterances because they express either one of two related intents or multiple intents at once.
Incomplete user utterances are possible because they clearly match some intent, but there’s not enough info in the utterance to know which one, as the intents are topically close to each other.
> [!info]  
>
> Example 1: “I want the subscription called Family.” Can be both NewSubscription and ChangeSubscription.
>
> Example 2: “Please get me a new credit card.” Can be both NewCard and ReplaceCard.
>
> Example 3: “I’m unable to login.” Can be both ForgotUsername and ResetPassword.

User utterances might contain multiple intents. This typically happens more often when intents are closely related. The user may want two related intents addressed, so asks for both at the same time (Example 1), or the “context” part of an utterance happens to match an intent, while the “intent” part of the utterance matches another (Example 2).
> [!info]  
>
> Example 1: “Can I see my current subscriptions? I want to get a new one.” Both SeeSubscriptions and NewSubscription.
>
> Example 2: “I want to delete my subscription. When is my subscription end date?” Both DeleteSubscription and SubscriptionEndDate.

## 3. Specificity
High intent recognition can be easier to achieve if intents are more narrow than broad. Therefore, intent specificity is useful as a factor in an intent scope, as high specificity intents can be easier to work with than low specificity intents.
> [!info]  
>
> Example 1: ResetEmailPassword - This is a very narrow intent with high specificity. It only covers a single issue.
>
> Example 2: ProblemWithAccount - This is a very broad intent with low specificity. It covers any problem the user may have with her account, for example, locked out, unable to change account details, forgotten account password, or unable to activate a new account.
> [!warning]  
>
> Even if two intents are very specific, they still usually need to have distance between them. Breaking intents into highly specific intents can be problematic if only very subtle nuances separate them.

Table. Specificity Characteristic Examples

| High Specificity Intents (narrow) | Low Specificity Intents (broad) |
| ----|----|
| Typically covers only;one specific issue, with Amelia handling this issue specifically. | Typically covers;multiple different issues, giving a more general answer / proffering a drill-down process in Amelia. |
| Usually easier to train, as most of what/how users will ask can be more easily anticipated. | Usually harder to train, and requiring more data, as all the various issues contained in the intent need to be covered. |
| Small, well-defined target. Usually has clear borders compared to other intents, and compared to the negative class. | Big target. May have fuzzier boundaries compared to other intents, and compared to the negative class. |
| Low risk of many false positives, as the user must have a certain precision in her utterance for the intent to fire. | Higher risk of false positives as the intent is trained for a broad variety of patterns, some of which will probably have some overlap with patterns in other intents, and compared to the negative class. |
| Higher risk of false negatives, as the intent easily can be trained too narrowly. | Lower risk of false negatives, as the intent may easily be trained too broadly. |

> [!warning]  
>
> Always adopt the user’s outlook. If users tend to specifically ask for having their locked accounts be opened, that’s a legitimate intent with high specificity. However, if users only tend to say that they have issues with their account, then there may not be any high specificity intent available on this topic. Sometimes, half the users are specific, while the other half isn’t. In that situation, consider adding entities and/or disambiguation (more on this under [Intent Architecture](Intent%20Architecture)).

## 4. Volume
The volume of intents factors heavily into the total intent recognition in an intent scope. It's always easier to achieve high intent recognition for some intents more than others. If those intents also have high volumes, that will drive the total score up.
Assessing the volume across potential intents is an important part of identifying an intent scope. Sometimes, low volume intents that don’t give satisfactory intent recognition, despite some effort. As a result, that might interfere with the intent recognition of other intents, and could be better left out-of-scope if the intent scope complexity is too high.
> [!info]  
>
> **Example 1: **As a customer agent in a telco company, Amelia will handle various customer inquiries. There is a total intent scope of 23 intents, and a goal of 85% intent recognition overall. Based on user research, two intents - adding data and resetting PIN - are estimated to have particularly high volume, possibly as much as 25% of all traffic. To evaluate the feasibility of an intent scope in comparison to the 85% target, take this and other expected volume differences into account. In this case, it's possible to achieve intent recognition upwards of 90% for both high-volume intents. In the overall picture, this factors positively into the overall estimation of whether 85% intent recognition is achievable.

Once intents have been identified and evaluated, placing them into an intent architecture is the next step.
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
