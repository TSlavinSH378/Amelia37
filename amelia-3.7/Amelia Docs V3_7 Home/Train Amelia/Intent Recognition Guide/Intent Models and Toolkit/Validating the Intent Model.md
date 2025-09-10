-   [Types of Validation](#ValidatingtheIntentModel-TypesofValidation)
    -   [Training Data Validation and Cross-Validation](#ValidatingtheIntentModel-TrainingDataValidationandCross-Validation)
        -   [Training Data Validation](#ValidatingtheIntentModel-TrainingDataValidation)
        -   [Cross-Validation](#ValidatingtheIntentModel-Cross-Validation)
    -   [Independent Data Validation](#ValidatingtheIntentModel-IndependentDataValidation)
    -   [Production Data Validation](#ValidatingtheIntentModel-ProductionDataValidation)
    -   [Other Validation Data Sets?](#ValidatingtheIntentModel-OtherValidationDataSets?)
-   [Validation Data Best Practices](#ValidatingtheIntentModel-ValidationDataBestPracticesValidationDataBestPractices)
    -   [Complete](#ValidatingtheIntentModel-Complete)
    -   [Balanced](#ValidatingtheIntentModel-Balanced)
    -   [Consistent](#ValidatingtheIntentModel-Consistent)
    -   [Different](#ValidatingtheIntentModel-Different)
    -   [Varied](#ValidatingtheIntentModel-Varied)
        -   [Test the Breadth of the Model](#ValidatingtheIntentModel-TesttheBreadthoftheModel)
        -   [Test the Reach of the Model](#ValidatingtheIntentModel-TesttheReachoftheModel)
    -   [A Little Bit Noisy](#ValidatingtheIntentModel-ALittleBitNoisy)
    -   [Fixed](#ValidatingtheIntentModel-Fixed)
-   [Avoiding Validation Data Bias](#ValidatingtheIntentModel-AvoidingValidationDataBias)
    -   [Training Data Bias](#ValidatingtheIntentModel-TrainingDataBiasTrainingDataBias)
    -   [Congruence Bias](#ValidatingtheIntentModel-CongruenceBias)
Once an intent model is trained, the next step is to evaluate the intent recognition capabilities of the model. This process is called validation. Test the model against a set of utterances, called a validation set, to see how the model predicts the intent or lack of intent in the validation set utterances. If training a model is teaching a model, then validating a model is testing and grading a model.
The purpose of validation is to:
-   Benchmark the performance of the model – How well does the model perform? How does the performance compare across iterations of the same model? Performance is the ability to generalize beyond what it's trained on to identify intent in live unscripted utterances. 
-   Expose and understand the shortcomings of the model – What are the weaknesses of the model? What causes these weaknesses? How can they be fixed?
The ability to understand a model, and what to do to improve it, depends on the quality of the validation. If the validation process gives the wrong picture, with a wrong understanding of the model's capabilities, the risk is fixing things that aren't broken and leaving untouched what's broken. This page looks at the following: 
-   Types of Validation
-   Validation Data Best Practices
-   Avoiding Validation Data Bias
For the concrete process of analyzing validation data and optimizing the model based on it, see [Building, Analyzing and Optimizing the Intent Model](Building%20the%20Intent%20Model).
# Types of Validation
There are various ways to validate an intent model.
## Training Data Validation and Cross-Validation
The simplest way to validate an intent model is to test it against the training data*. *There are two different ways to use training data to validate a model.
### Training Data Validation
The model can be validated with the utterances it was trained on. However, this approach has close to zero value in terms of assessing the actual performance of the model. Intent models exist to generalize meaning and intent from live unscripted utterances. Testing only on scripted utterances reveals very little about the quality of the model. This approach has complete bias towards what is known – the training data – rather than validate against the unknown. It is the unknown that needs to be tested. Validation with training data can be discarded as a method.
### Cross-Validation
Rather than use the training data as validation data, instead perform cross-validation of the training data. Cross-validation lets every utterance in a data set be part of a training set and validation set. In the case of 5-fold cross-validation, this works as follows:
1.  Take out a random 20% of the training data. Then train an intent model using only the 80% remaining training data. Use the 20% taken out as validation data.
2.  Repeat the operation another time, this time use a different 20% as validation data and train an intent model with the 80% remaining training data.
3.  Do this 5 times to create 5 models. Across these models all the training data also is used as validation data (20% x 5 = 100%).
4.  Then take the average performance of all the 5 trained models.
With cross-validation, training data is used to test against random utterances. This can give a decent indication of the quality of the model. In some cases, cross-validation can be good enough for a project.
However, it does have clear drawbacks. The full model is not tested, only an 80% version of the model. Results are not the actual results of the entire model. More importantly, there is a risk of [training data bias](#ValidatingtheIntentModel-TrainingDataBias), as explored further down on this page.
## Independent Data Validation
To avoid the issues with training data cross-validation, use an independent validation data set that's different from the training data. Keeping training and validation data separate provides an independent benchmark. This has a number of advantages, described under Validation Best Practices below. Using an independent validation data set is the only way to adhere to all of these best practices.
## Production Data Validation
Once in production, typically after a soft launch of Amelia, models should be validated against production data. Go into the conversation logs, extract relevant end user utterances, and validate a model against live utterances. Evaluating production data often is part of scoring Amelia's overall performance beyond the ability of the intent model to recognize intents.
Conversation logs provide extremely valuable information about what intents users ask about, how they express those intents, and how users talk about related topics without expressing intents. This information may not be available before going into production. Logs often are the first real test of the training process and becomes the new more accurate benchmark for the actual performance of the model.
However, this does not mean any independent validation data set should be discarded. Production data has great value as a set of true end user utterances. But it won't magically form a well-rounded and comprehensive validation set. Relying solely on production data to validate a model might miss checking aspects of the model provided by a well-crafted independent validation set.
Rather than leave the independent validation set behind, adjust the set according to lessons learned from production. Incorporate select parts of the production data into the independent validation set and remove unimportant parts. The independent validation set evolves into a more complete and thorough check to complement the validation done with production data.
> [!info]  
>
> **Example**
>
> Once live with an Amelia solution, one intent gets a lot more traffic than anticipated. This intent doesn't perform well. Based on the validation results from production data, this intent is retrained. Testing the re-trained model against the same production validation data gets better results.
>
> A few days later, the model is evaluated again with new production validation data. As expected, end users expressing this intent now usually get to the right place. In that sense, there's a clear improvement. However, other live conversations show a number of other intents have become unbalanced and skewed the balance between the intents and the negative class. The model might need to be backtracked.
>
> Had testing been against a well-made independent validation set and the production data, these issues might have been spotted immediately.

## Other Validation Data Sets?
Other types of validation sets can be useful, for example, a set of utterances that cause mistriggers in live conversations with Amelia. However, the priorities that lead to creating additional validation sets should not involve the independent validation set. Updating the independent data set to handle these priorities might unbalance or dilute the independent data set. Better to create other validation data sets, if needed.
> [!info]  
>
> **Example 1**
>
> As part of our Amelia project organization, there's a requirement that reported mistriggers are fixed within a certain time span and reported on. The simplest way to do this is to gather the reported utterances in a validation set so they can be tested against the model. However, if we add mistriggers directly into the independent validation set, this can lead to congruence bias (see below) in our independent validation set, as the vast majority of reported mistriggers test only the explicit requirements.
>
> To preserve the health of our independent validation set, these mistriggers are placed in a separate validation set.
>
> Example 2
>
> In an Amelia project, it's useful to ensure for certain VIP utterances to always hit correctly in the intent model. To ensure this, these utterances are placed in a validation set. However, we make sure this validation set is not mixed in with the much more well-rounded and complete independent validation set.
>
> Confusing the VIP validation set with the independent set could lead to an over-emphasis on the VIP utterances. Training data might develop in a direction that always hit the VIP utterances but with a negative impact on the overall quality of the model.

# Validation Data Best Practices
To craft a validation set that performs well at benchmarking performance and exposing shortcomings in a model, ensure the validation data set has certain best practice qualities. This also safeguards against biases. High performing validation sets are complete, balanced, consistent, and varied, among other qualities.
## Complete
The validation set must be complete and validate against all data types used to train a model.
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 28%" />
<col style="width: 35%" />
<col style="width: 36%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh" style="text-align: center;"><p>INTENT DATA</p></th>
<th colspan="2" class="confluenceTh" style="text-align: center;"><p>NEGATIVE DATA</p></th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd" style="text-align: left;"><p>It's vital to validate against <strong>all </strong>intent classes to get a complete understanding of the entire model. This helps expose poorly trained intents, check for conflicts between intents, and provide an understanding of the balance between of the intent training data compared to the negative training data.</p></td>
<td class="confluenceTd" style="text-align: left;"><p><strong>In-Domain Negative Data</strong></p>
<p>These are utterances that are topically or linguistically close to a given intent, but do not express that intent or any other intent.</p>
<p>This is a common oversight but a crucial part of validation. For each intent in a model, there should be in-domain negatives in the validation set designed to test if that intent is overtrained.</p>
<p>If these utterances fire off the intent, it's a warning about overtraining. If neglected, there's a high risk intents will be overtrained.</p></td>
<td class="confluenceTd" style="text-align: left;"><p><strong>Out-of-Domain Negative Data</strong></p>
<p>If in-domain negatives validate well, this is less important. A model that performs well on in-domain negatives will almost certainly perform even better on out-of-domain negatives. Still, it's good practice to include a set of out-of-domain negatives in the validation set.</p></td>
</tr>
</tbody>
</table>
> [!info]  
>
> **Example 1**
>
> There 24 intents in a model. Each intent has both training and validation data. A 25th intent is added late in the game. Time constraints and lack of available data delays adding proper validation data for the 25th intent.
>
> Meanwhile, testing to improve the model proceeds based on the validation set. After a few iterations of improvement, validation data for the 25th intent is found and added.
>
> As the model is trained and validated with complete validation data, the 25th intent performs much worse than other intents. The intent model thinks a lot of the validation utterances for the 25th intent belong to two other intents. The addition of training data for the 25th intent improved these two other intents and they became overtrained. The overtraining went undetected because there was no validation data for the 25th intent until late. Backtrack and readjust to train and validate with the complete data sets.
>
> It's impossible to always avoid these kinds of scenarios. However, they should be avoided as much as possible with careful planning and analysis.
>
> **Example 2**
>
> A validation set has very few in-domain negative utterances. As the model is analyzed, there are a lot of intent utterances failing in the validation set but very few negative utterances failing. The intents are strengthened with more data to improve the performance of intent utterances in the validation set. The results of intent utterance testing improves noticeably.
>
> In fact, the intents are being overtrained. Adding data to strengthen failing intents makes it easy to get great results for the intents but significantly damages the ability of the model to evaluate in-domain negative utterances correctly. The validation results do not expose this inadequate testing of in-domain negatives. In production, the model shows itself to be a highly overtrained and too trigger-happy.

## Balanced
To ensure balanced validation results, the validation set should have:
-   A decent volume balance compared to the training data set, to ensure the validation set and training set are not too similar.
-   A logical distribution of tests across the relevant intent classes.

| INTENT CLASSES |
| ----|
| Validation data vs training dataFor each intent, ideally there should be 2-3 validation utterances for each 10 training utterances.More validation utterances often makes the validation set too similar to the training data. This makes it too easy to score artificially well on the validation data and defeats the purpose of the validation set (see Different below).If there are more than 2-3 validation utterances for every 10 training utterances, and the extra validation utterances have good variation with clear differences from the training data, consider transferring parts of the validation data to the training data to strengthen the model.Distribution across intentsThere should not be big differences in the amount of validation data across intents. Otherwise, validation results may be skewed with too much weight placed on some intents instead of others.However, intents that are broad with low specificity can have more validation utterances than for narrow intents with high specificity. Broad intents will need a larger variety of utterances for testing. This works if a reasonable balance is maintained. There should be good reasons if any intent has twice as much or twice as little validation data as another intent. |
| Validation data vs training dataFor each in-domain negative, ideally there should be 2-3 validation utterances for each 10 training utterances. The validation utterances for in-domain negatives are used to test intents for overtraining. Having more validation utterances is not a problem if they are different from the in-domain training data.The negative validation data, however, should not be too big compared to the intent validation data. Otherwise, the complete validation set will not give a balanced test of the entire model. |
| Validation data vs training dataThe value of out-of-domain negatives is marginal if in-domain negatives are tested adequately. In that case, 2-3 validation utterances for each 10 training utterances for out-of-domain negatives is acceptable.As long as in-domain negatives are adequately tested agains, out-of-domain validation is more academic. But given there are;a few thousand out-of-domain negative utterances in the training data, there's nothing wrong with having a few hundred negative out-of-domain negative utterances in the validation data.[!warning]
Out-of-domain negative training data can distort the results of 5-fold cross-validation of smaller models. Because cross-validation tests against 20% of training data for validation, a large portion of testing may be against out-of-domain negatives. Cross-validation in this scenario places too strong an emphasis on out-of-domain testing, which is easy to score well on, compared to intent classes and in-domain negatives.  |

> [!info]  
>
> **Example 1**
>
> Given an unbalanced validation set where some intents have more validation data than other intents, analyzing validation results shows high-volume intents have more misclassified utterances. To improve results, training data for intents with more validation data is increased and improved, to restore balance.
>
> The result is improved overall validation scores because many misclassifications have been fixed. However, results for intents with less validation have gone down as overall results for the whole validation set have gone up.
>
> Analysis shows overtraining for intents with lots of validation data at the expense of intents with less validation data. Improved overall results hid the imbalance between high performing intents and intents with less validation data.
>
> **Example 2**
>
> Instead of an independent validation data set, 5-fold cross-validation is used. The training data has 800 intent utterances and 6500 mainly out-of-domain negative utterances. Overall cross-validation results are great.
>
> However, the positive results are mostly because the vast majority of cross-fold testing is against out-of-domain negatives. These often are easy to predict for a model because these utterances are far removed from intent utterances. The imbalance between intent utterances and out-of-domain utterances is amplified by the use of cross-validation testing.

## Consistent
When utterances are labeled with their correct intent, or as negatives, it's extremely important to be consistent in grouping utterances and classes. While obvious, mistakes are easily made:
-   In part because there are usually thousands of lines of utterances and accidental mislabeling can and will happen.
-   In part because how utterances are labeled can sometimes be subjective. Two similar utterances that express the same sentiment can be labeled differently. Sometimes labeling is a judgment call if a type of utterances should belong to intent A or to the negative class, as shown in an example below.
When mislabeling happens, validation results and improvement efforts will be flawed. Consistency is critically important:
-   Within the validation data set.
-   Between the validation data and the training data. Validation data tests the training data. Inconsistency between data sets results in testing not for the intended goal but for something different and unknown which will fail. This doesn't apply if we use cross-validation, in which case the training data is the validation data.
In practice, people working on the data need to be clear about and in agreement with any judgment calls. It is a good idea for one person to have full overview of the data and deep knowledge of Amelia's role who approves all changes to the data to ensure consistency.
> [!info]  
>
> Example
>
> For an intent labeled StopNotification, the validation data has these two utterances:
>
> "I get a lot of notifications from you."
>
> "Every day or two, I get more notifications from you."
>
> Whether or not these two utterances should trigger the intent StopNotification can be a subjective decision. But it's vital to decide and stay consistent in how these utterances are interpreted. If one utterance is labeled StopNotification, and the other as negative, the testing of the model will be inconsistent. Results and improvement efforts will be distorted.
>
> For example, if the intent model considers both utterance predict and trigger the StopNotification intent, the utterance labeled as negative will become a mistrigger. Trying to adjust utterances to fix the mistrigger is that both utterances trigger the intent and the other utterance becomes a mistrigger.
>
> > [!warning]  
> >
> > If there a lot of utterances in an intent that require a subjective decision, it might indicate the intent is not well defined sufficiently and should be [reshaped in the intent architecture](Intent%20Architecture).
>
>  

## Different
The validation data used for a model should be noticeably not marginally different from the training data. This is the best way to test the model's ability to extrapolate beyond its own training data.
> [!info]  
>
> Example
>
> Take a look at the tiny outtake of sample data in the table below for the intent DisputeCharge. The low quality validation is too closely aligned with the training data, with entire utterances that are similar to training data utterances. This makes it too easy to get a high score on our validation testing. In the high quality validation data, the utterances contain relevant patterns, but are markedly different from the training data. This will present a real test of the reach of the model.
>
> > [!warning]  
> >
> > These samples would be parts of much bigger data sets. By themselves, these few utterances won't work as training nor validation.
>
>  
>
>   
>
> 
> | Training Data | Low Quality Validation Data | High Quality Validation Data |
> | ----|----|----|
> | what's up with the charge made on my Visa yesterday? It's inaccurate, the amount isn't right. | there's a charge that's inaccurate on my card, it has an amount that clearly is not correct | Hi, i just noticed a purchase on my acct that i didn’t authorize |
> | explain how I can dispute a charge, please | I need help disputing some charges made at Zara | I think the vendor messed up the amount of my order. |
> | I need to dispute a transaction on my card | Amelia, I need to dispute this transaction on the visa card | There’s a charge that I don’t recognize! |
> | Who can I report a wrong charge to? | i need to report a wrong charge | It says I made a purchase for $54.50 at Sams Pizza, but that should’ve been $5.45 |
> | There's a transaction on my card that has what looks like a fraudulent charge | My card seems to have been misused, I have a fraudulent charge on my card | dispute charge |
> | We need to report a charge we don't recognize on our account | There's a charge on my account that I can't recognize, so I want to report it | why have I been charged twice? I think it's a fraudulent transaction |
> | how do I dispute a fraudulent purchase on my card? | tell me how I can dispute a fraudulent charge on the preferred gold premium card | I thought I worked this out with Best Buy but the $441.32 charge was supposed to be refunded |
> | I noticed a payment on my card I didn't authorize: what can be done? | I never authorized this payment that I just noticed | How do I file a dispute for a charge that wasn't of my own making? |
> 

## Varied
Strong variation in validation data tests the breadth and reach of an intent model.
### Test the Breadth of the Model
The validation set exists to challenge a model. Therefore, the goal should be a wide variety in the utterances to validate against.
-   Validation results are the foundation for improving the model. Lots of similar utterances makes the outcome too easy, limits the opportunity to improve the utterance data, and provides a false confidence in the model.
-   Validation data usually is a better reflection of what will happen when the model is exposed to real end users, not only testers. Real users with real issues are often, though not always, more varied in how they express themselves than can be anticipated. 
> [!info]  
>
> **Example 1**
>
> In the three utterances below, there is too little variation to merit having all three in a validation set. If one of these is predicted correctly by the model, it is almost certain the other two will be predicted correctly as well. Two of them are redundant. If a validation set looks like this, it is too easy to score fantastically well.
>
> 
> |  |
> | ----|
> | I need to file a claim, please |
> | Need to file a claim |
> | Need to file a claim asap, pls |
> 
>
> **  
> Example 2**
>
> There is a pool of utterance data for the intent FileClaim and people are picking selected utterances to build a validation set. Of the four example utterances below, two must be picked for the validation set. The question is, which ones to choose?
>
> 
> |  |
> | ----|
> | file claim, pls |
> | I want to file an insurance claim regarding an auto accident |
> | can you help me file a claim for the insurance |
> | ok, so yesterday my volvo got a scratch, not sure how, but I want to file a claim for that |
> 
>
> The answer is the first and fourth utterances. The differences between these two utterances better tests the breadth of the model. A model that can predict the intent of the first and fourth utterances, as tested with a validation set of utterances, also should predict the second and third utterances. The second and third utterances have lots of relevant patterns.
>
> If the second and third utterances are chose for a validation set, and the model predicts them correctly, there is no certainty the model can predict the intent for the first and fourth utterances.

### Test the Reach of the Model
Including utterances that test the outer limits of a model, and possibly a bit beyond, helps measure how extensive a model can predict live unpredictable utterances. Training a model to cover all edge cases, however, risks overreach. Testing can provide a deeper understanding of the limits of a model.
> [!info]  
>
> **Example**
>
> In these sample utterances, the low variation data will fail at testing of the ability of the model to generalize from a range of utterances. The high variation utterances will be a challenging test that definitely tests the reach of the model for this intent.
>
> 
> | Too Little Variation | High Variation |
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

## A Little Bit Noisy
To mimic live utterances, include some irrelevant word patterns or noise in some but not all validation utterances while retaining a clear intent. Noise often pulls the utterance slightly toward the negative class which is purposely trained with noisy patterns. Because the natural language people speak includes noise all the time, testing intent utterances with noise hit the correct intent is good practice.
> [!info]  
>
> **Example:**
>
> Here's a few examples of clean versus noisy utterances for the intent CancelSubscription. Notice the intent is clear in the noisy utterances.
>
> 
> | No Noise | Including Some Noise |
> | ----|----|
> | cancel my subscription | ok, so to sum up:;i want to cancel my subscription. |
> | How can I end my subscription from next month? | Hey, I have this subscription called Freemium.;How can I end it from next month? |
> | I'd like to stop my subscription asap. | Idk if you can help as you're a bot,;but I'd like to stop my subscription asap. |
> 

## Fixed
A validation set is the benchmark for the performance of a model across iterations. It reveals the impact changes have on a model and track progress over time. As much as possible, validation sets should be fixed to maintain comparability between versions of a model.
> [!info]  
>
> **Example 1**
>
> Before the first version of a model is built, a good number of validation utterances for all relevant intents were collected, as well as the negative class. In part, relevant intent and negative utterances were annotated and extracted from customer chat logs with live agents. In part, a diverse set of people in the organization were asked for help with intents where there were no relevant chat logs. They were asked to provide a small set of utterances for how they would express various intents, as well as how they might talk about relevant topics without expressing the intent.
>
> Based on this, a well-crafted validation set was put together. This validation set is kept apart as the model is built and iterated. The validation set is an unmoving yardstick to gauge the effectiveness of model changes and what progress is made.
>
> **Example 2**
>
> With no independent validation set, 5-fold cross-validation is relied upon for the first 11 versions of an intent model. A workable validation set is the result.
>
> The validation set is used for the 12th version of the model. This results in lower scores than the cross-validation results. Changes between the 11th and 12th versions of the model are not ineffective or wrong. Instead, the introduction of the validation set changed the yardstick used to measure the effectiveness of the model. Making future changes with the workable validation set as the benchmark should yield better results for the model over time.

That said, it's often impossible to maintain fixed validation sets. It's a useful goal not a holy grail. There are legitimate reasons that justify changing the validation set:
-   Mistakes in the labeling of the data make the validation results inaccurate.
-   Oversights in the validation with issues the validation set should test but which it currently isn't testing.
-   Adjustments to the intent architecture with intents changed, merged, added or removed. The validation data must reflect these changes. 
As far as possible, save up and implement these changes to be made in bulk. This helps maintain a fixed validation set over periods of time. When possible, for example in the cases of mislabeling or oversights, do retroactive validation on older iterations of the model with the new validation set to get true comparisons.
# Avoiding Validation Data Bias
Validation data can get biased easily by creating blind spots that can distort results. Therefore, establish a process where these biases are eliminated as much as possible. The less bias in the validation data, the more effective it is.
> [!warning]  
>
> Generally validation data bias is not acceptable and cannot be adapted to over time. Biases impair the ability to benchmark and optimize a model.

## Training Data Bias
If training data also is used as validation data, there is a risk of training data bias. This is an easy trap to fall into because good data is often hard to find and create. Using all available data as training data to build the best possible model, however, leaves no independent data to validate the model. While this may make sense in the short-term, it has significant risks long-term.
Below are the main drawbacks of cross-validation with training data as the main validation method: 

| Lack of independence |
| ----|
| When training data is used as validation data, the quality of validation data is the same as the quality of our training data. This can create dangerous blind spots.If training data is used as validation data, and the training data is flawed, flawed data is validated with flawed data. This approach can easily fail. Flawed validation data will often;fail to expose deficiencies in flawed training data, especially if the flaws in question are identical between training data and validation data.Think of this as self-diagnosing rather than letting the doctor do the diagnosis. |
| If training data is used as validation data, changes to the training data to improve it;also changes the validation data. The result is that we work towards a moving target.Compare this with an independent validation set which gives a fixed target as a benchmark. Progress is easily tracked and changes are understood in results from iterations of our model.As a benchmark for comparison, cross-validation results with training data is not a good choice. |
| If a model is;overtrained (overfit) and training data is used for validation, results may not show a model is overtrained.In the case of overtraining, the results may be artificially inflated because overtrained data tested on itself easily can score fantastically well - see example below. In addition, because cross-validation does not test against the full model, but against an 80% version of the model, the results won't be a true reflection of the model's actual live performance.When improvements are based off of cross-validation with training data, there also is a risk of fixing problems that don't exist in the full model but do exist in the validation results. This leads to overtraining by training the model even more on various patterns to fix what failed. |
| Because testing the reach of a model is important, validation data should be more varied than training data. When training data is used as validation data, the level of variation probably is not sufficient to test reach. |
| For cross-validation on a small model with relatively little intent data, but with a big negative class, the result usually generates an artificially high overall F-score. This is caused by the big imbalance in the validation data because the vast majority of test utterances are out-of-domain negatives utterances which are usually easy to predict correctly. |

> [!info]  
>
> **Example**
>
> For the intent BookRoom, the training set has low variation. The utterances all look like this:
>
> 
> |  |
> | ----|
> | I want to book a room, please |
> | Let me book a room |
> | Please help me with booking rooms |
> | We'd like to have a room booked at your hotel |
> 
>
> Cross-validation is used to validate the model. Because utterances are similar, the validation set becomes similar to our training set. The results are great because it's very easy to score well testing utterances similar to the utterances the model is trained in. To remedy the few mistriggers, the training data is expanded with more utterances similar to the utterances that failed. The model is retrained and gets even greater results.
>
> In this case, a fantastic model is in reality a heavily overtrained model. The cross-validation gives extremely misleading results, scoring well because of the low variation in the training and validation data. On top of that, fixing the mistriggers added more similar utterances to the training data. This boosts results even more. Not only because of the fixed mistriggers, but because validation includes these new utterances, all of which are easy to score well on because they are so similar.
>
> Not only did the cross-validation fail to diagnose the issue, it made the problem worse by making fixes to the training data even more similar.

## Congruence Bias
Validation mainly against expected use cases causes congruence bias. It's a natural impulse to test requirements for what Amelia should do. Testing then becomes congruent with the requirements. Meanwhile, unexpected but possible use cases are not considered and tested.
Congruence bias is present in any kind of testing, whether it's the daily work to implement Amelia or dedicated test sessions. Testers often are project members who have help set requirements for Amelia's skills. They're also aware of Amelia's role. Their natural instinct is to test the use cases Amelia should master. If intent recognition fails, testers often will try again in different ways to make recognition work. The result is congruence bias which also finds its way into validation of the intent model.
As the validation data set is built, it is important to look for congruence bias. Test not only the requirements but also likely use cases outside of requirements.
> [!info]  
>
> **Example 1**
>
> An Amelia implementation is under construction. There is no viable validation set for the intent model. Work begins on building a first validation set.
>
> Testers are recruited from agents Amelia will help, as well as people in the organization who have help scope the project. All testers know what Amelia is trained to do and what she cannot do. Testers use expected use cases for their tests and the intent model performs well.
>
> Intent utterances from testing are harvested and used to create a validation set then are used to provide a benchmark and improve the model based on this first validation set. However, the model and validation set are optimized only for the expected use cases. Live testing will introduce one or more unexpected cases where the model will fail.
>
> **Example 2**
>
> As an Amelia implementation is developed, project members provide feedback with tickets. The majority of tickets about intent recognition describe utterances that should have hit but didn't.
>
> These utterances are used uncritically to build a validation set which, in turn, builds congruence bias into the validation process.

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
