{% version "3.x" %}
To build and optimize an intent model for high intent recognition requires understanding the current state of the model and knowing how to build and optimize a model.
# Building and Enhancing a Model
Working with intent models has two modes, build mode and enhance mode. Build mode happens when creating a new model or expanding an existing model by adding new intents. Enhance mode improves an existing model with no change to its intents. Each mode has significant differences.
## Build Mode
Build mode adds new intents or changes intents significantly in the intent model. Intents should be worked on one intent at a time to confirm positive impacts and isolate any negative impacts caused by the addition of an intent.
Predictive machine learning models, like intent models, very quickly become highly complex creatures, with a flurry of big and small butterfly effects criss-crossing the model. When something is pulled at one end, ripple effects shift something at the other end. Throw in a bunch of intents in a model at once and introduce a labyrinth of variables and dependencies. It will be hard and sometimes impossible to isolate cause and effect.
In build mode, the process typically looks like this:

| Train | 2. Validate | 3. Analyze | 4. Select | 5. Optimize | 6. Repeat with New Intent |
| ----|----|----|----|----|----|
| Build | Enhance | Build | undefined | undefined | undefined |
| Train a model with both intent data for intent A as well as in-domain negative data for that intent.Out-of-domain negative data should also be included. | Validate the model.;Preferably against a high quality validation set, containing both intent tests and in-domain negative tests.Often, we do this validation at the same time as we train the model. | Analyze the model validation results - as outlined further down on this page. | Select one issue to address based on the analysis.While it is possible to address a few issues at once, try to limit this as much as possible. It is easier to understand the effects of addressing one issue by looking at the analysis results from the new model. | Optimize the intent data and the relevant in-domain negative training data, according to the analysis. See further down this page for details.This can include adjusting other intents as well, insofar as conflicts are visible.Then go back to start, with re-training, validating, and so on.Continue with this until the intent has high performance on the intent and on the relevant in-domain negative data. | Once happy with the performance of intent A, move on to intent B and repeat the same process.Then move to intent C, D, and so on.[!warning]As we add more and more intents, the performance will fall gradually, for both implemented intents and the new intents we add. As long as these decreases are small, this is natural. We have to expect lower performance as the model becomes more complex with more intents.  |

The build mode process works like a stacking game building and balancing a construction with a set of building blocks, one on top of the other. It's a lot easier to maintain the balance of the construction by adding a single piece a time instead of adding 2 or 5 or 50 pieces in one turn.
> [!info]  
>
> **Example 1**
>
> 20 intents need to be added into an intent model. Having planned well ahead, intents are added one by one, including in-domain negatives.
>
> The first intent easily achieves 90-95% intent recognition. As each intent is added, intent recognition gets harder with the percentages coming down gradually. In addition, the performance of already implemented intents, as well as the negative class, decreases a little bit for each new intent added. This is fine, as the new intents will interfere in small ways with the existing intents. The last intent achieves 85% intent recognition. At this point the other intents, as well as the negative class, are also at around 85%.
>
> The result is a well-balanced model with decent intent recognition. This is a solid platform to build from after go live and using this model in for Amelia soft launch.
>
> **Example 2**
>
> The same 20 intents as above are all thrown into the intent model at once along with in-domain negative data. This gives a 65% intent recognition out-of-the-box. There's lots of variation in the performance of various intents, and precision and recall scores (more on that below) that are often highly unbalanced.
>
> Trying to improve the model, it's difficult to analyze and pinpoint what's broken and what works. At times, after working to improve the training data, the results are different, not better. Sometimes even slightly worse. It's whack-a-mole. An issue is fixed here, only for the fix to cause to another issue with one or more of the other intents.
>
> After a lot of iterations, intent recognition edges towards 80% overall. But at this point it's harder and harder to find improvements while avoiding overtraining. Approaching Amelia's soft launch, it's unclear what's going on in the model and unsure how Amelia will perform in production.

## Enhance Mode
Enhance mode works to enhance the performance of an existing model with no changes to the intents. Just as with building models, this is ideally an incremental process. Tackle one or a only a few issues at a time, to the extent this is practically possible.
In enhance mode, the process typically looks like this:

| Train | 2. Validate | 3. Analyze | 4. Select | 5. Optimize |
| ----|----|----|----|----|
| Enhance | undefined | undefined | undefined | undefined |
| Train a model. | Validate the model. Preferably against a high quality;validation set, containing both intent tests and in-domain negative tests.Often, validation is done at the same time as the model is trained. | Analyze the model validation results, as outlined further down on this page. | Select issues to address, based on the analysis.Preferably, limit the number of issues as far as possible.;It is easier to understand the effects of addressing one issue by looking at the analysis results from the new model. | Optimize the training data according to the analysis. See further down this page for details.Then go back to start with re-training, validating, and so on, to evaluate the impact of the fixes.If not happy with results, do another round of fixes for the same issues. When happy with the results, move on to new issues. |

# High-Level Analysis
Start with high level view of the validation results of the model provided by metrics. These are the metrics used to evaluate the model and compare it across iterations, for both the model and the individual intent classes.
> [!warning]  
>
> All the statistics and output outlined below is only as good as the [validation set](Validating%20the%20Intent%20Model) we use to get it. So we should look at this measure with an awareness of this.

## Performance (Accuracy)
When a model is tested, one metric to look at is the performance of the model. This metric is calculated for the model as a whole and individually for each intent class, including the negative class.
The phrases, "85% intent recognition" or "80% accuracy" describe performance. In a development setting and testing against a validation set, performance metrics are the best estimate of the strength of the model. In a production setting and testing against production data, performance metrics provide the answer about how well the model worked.
The performance metric is relevant in three different contexts:
-   To assess the current quality of the model, for example, measuring performance against a goal.
-   To compare the performance of this iteration of the model with the previous iteration, to understand the impact of the enhancements.
-   To help select what should be enhanced next.
### Reading the F-score
Performance is best measured in what we technically call the F-score (also called F1 score, F-measure, etc).
> [!info]  
>
> **Example 1**
>
> Below is a table of the stats output a model is validated in Amelia. For now, look at the last column, F-score.
>
> As seen in this table, the overall intent recognition rate is 85%. This means that out of all the utterances tested, 85% hit the correct intent. For the intent XX, we have an F-score of 87%. That means the intent recognition for this intent is 87%.
>
> 
> | 
>  | Correct | Actual | Predicted | Precision | Recall | F-score |
> | ----|----|----|----|----|----|----|
> | Overall |  |  |  |  |  |  |
> | None |  |  |  |  |  |  |
> | xx |  |  |  |  |  |  |
> | xx |  |  |  |  |  |  |
> | xx |  |  |  |  |  |  |
> | xx |  |  |  |  |  |  |
> | xx |  |  |  |  |  |  |
> | xx |  |  |  |  |  |  |
> 
>
> **Example 2**
>
> Below are results for the same model as the example above but this time tested on cross-validation.
>
> This gives a much higher overall F-score which is artificially boosted. When cross-validation is performed on a small model with relatively little intent data, but with a big negative class, an artificially high overall F-score usually results. This is due to the big imbalance in the validation data because the vast majority of test utterances are out-of-domain negatives utterances which are usually quite easy to predict correctly.
>
> 
> | 
>  | Correct | Actual | Predicted | Precision | Recall | F-score |
> | ----|----|----|----|----|----|----|
> | Overall | 6900 | 7047 | 7047 | 97.91 | 97.91 | 97.91 |
> | None | 6636 | 6639 | 6730 | 98.60 | 99.95 | 99.27 |
> | CloseAccount | 19 | 63 | 39 | 48.72 | 30.16 | 37.25 |
> | dmb | 64 | 83 | 71 | 90.14 | 77.11 | 83.12 |
> | dtt | 46 | 62 | 50 | 92.00 | 74.19 | 82.14 |
> | escalate | 65 | 76 | 66 | 98.48 | 85.53 | 91.55 |
> | tapp | 31 | 70 | 49 | 63.27 | 44.29 | 52.10 |
> | tv | 39 | 54 | 42 | 92.86 | 72.22 | 81.25 |
> 

### Calculating the F-score
The F-score is calculated as shown below. The terms precision and recall are described in the next section.
![](attachments/20808367/20808758.png)
In practical terms, this calculation means the following:
-   For the overall score*, *this calculation is equivalent to the share of correct predictions out of the total number of tests. If there are 2000 utterances in a validation set and the model predicts the correct intent class for 1500 of those, then the F-score will be 75%.
-   For the score of each individual intent class, however, it's more complicated. Simply calculating the share of correct predictions for a class over the total number of tests for that class fails to take into account utterances that were incorrectly predicted to the class in question. See the example below for more details. For these reasons, using the F-score calculation provides the complete picture.
> [!info]  
>
> **Example**
>
> Among the 2000 utterances in a validation set, exactly 100 utterances test the intent class FreezeMembership. If only the share of correct predictions of this class is measured, out of the 100 test utterances, this will give inadequate metrics:
>
> -   Out of the 100 test utterances, 90 were predicted correctly as true positives and 10 were incorrectly predicted to other classes as false negatives. On this metric, accuracy is 90 / 100 = 90%.
> -   However, this metric does not account for the fact that 22 utterances belonging to different classes were incorrectly predicted to the FreezeMembership class as false positives. In total, the model predicted that 110 utterances belonged to this class. Out of these, 90 were correct as true positives, but 22 were incorrect as false positives. This metric has an accuracy of 90 / 112 = 80 %.
>
> Therefore, rely on the F-score to measure performance because the score represents a balanced average of these two scenarios.

## Balance, Overtraining, and Undertraining
Once the overall accuracy of the model is understood, check how well it's [balanced](Understanding%20Intent%20Models), to spot any [overtraining or undertraining](Understanding%20Intent%20Models) that needs to be addressed. This applies to:
-   **Each individual intent**– check if they are well balanced among themselves.
-   **The negative class** – check if the negative class is well balanced compared to the combination of all the intent classes, and vice versa.
### Signs of Overtraining and Undertraining
Statistics generated from training intent models can show signs of whether a model and intent classes within the model are overtrained or undertrained.

| Overtrained Model / Class | Undertrained Model / Class |
| ----|----|
| High recall scores, but low precision scores | High precision scores, but low recall scores |
| Lots of false positives | Lots of false negatives |
| Often scores artificially well in cross-validation testing | Has representative (ie bad) scores in cross-validation testing |
| Scores badly on a good validation data set | Scores badly on a good validation data set |

The best pointer for overtraining and undertraining are the **precision **and **recall **scores. A clear discrepancy between these two for a given class is a sign of imbalance. A divergence of a few percentage points isn't significant. However, moving towards a gap of 10 percentage points or more should trigger a deeper investigation.
The divergence in precision and/or recall scores of a class is not necessarily due to shortcomings in the training data of that particular class. It can just as easily be caused by imbalances in the training data for another intent which, in turn, destabilizes this intent.
## Conflicts, Collisions, and Overlap
A confusion matrix shows how the model sorted all the validation utterances into intent classes, correctly and incorrectly. It's also called an error matrix. The confusion matrix shows exactly what classes any given intent collides or overlaps with. The statistics already showed intent X had low performance but not what classes intent X conflicted with to cause the low performance. The confusion matrix shows conflicting classes.
This is vital information to understand what to address in training data or sometimes what to address in an intent architecture, for example, if two classes overlap so much it becomes clear distinguishing between them as two separate intents is difficult or impossible.
The misclassifications* *are a list of all the utterances in a validation set where the validation failed in the model. The statistics and confusion matrix are only numbers, so they can tell what classes need to improve. For example, that 25% of the validation utterances for EditProfile failed. As the hard manifestation of those numbers, the misclassifications is the best guide to why they failed and how to address the failure. If validation set is good, misclassifications are the best foundation to improve a model.
# Selecting What to Fix
Once test results are generated and understood, decide what to focus on improving in a model. The answer should not be everything that failed. Instead, selectively hand-pick preferably one or two areas to address. The criteria outlined below offer useful guidelines. 
## High Impact
Naturally, tackle the high impact issues before the small impact issues.
-   In part because we want our changes to big impact, and so we should select the big fish before the small fry.
-   In part because this will help minimize the butterfly effect. The bigger the change, the more the model will shift due to the ripple effects of that change. These ripple effects can easily alter what small fixes are needed for the model. If both the engine and the exhaust pipe need repair, do the engine first then re-check status of the exhaust pipe afterwards. If it's still broken, fix it, but sometimes it may already have fixed itself.
There are typically two metrics that indicate high impact potential:
-   **Low performance** – To improve a model efficiently, prioritize the classes with the lowest performances in the validation tests.
-   **High traffic** – The expected traffic of the intents is also important to take into account, as high traffic intents will impact overall intent recognition more in a live deployment than low traffic intents.
> [!info]  
>
> **Example 1**
>
> On average, a model performs at 83% on the validation set. However, there is one major outlier in the intent ReportIssue with only 68% intent recognition. This intent is optimized over a few iterations and performs at 81% intent recognition.
>
> The major improvement of ReportIssue has shifted other parts of the models significantly. Because the biggest intent was optimized first, however, lower priority issues can be fine-tuned. If instead other intents were fine-tuned first, parts of that tuning might have been misdirected, given the updated state of the model after the bigger structural changes that came from fixing ReportIssue.
>
> **Example 2**
>
> The two lowest performing intents in a model are ChangeMaritalStatus and ChangePassword, with ChangeMaritalStatus scoring the lowest. Because most people change their passwords more often than their spouse, ChangePassword has a lot higher traffic. While ChangePassword scored a bit better, it is prioritized first because it has greater impact in terms of usage volume.

## Systemic Fixes
As far as possible, try to implement systemic fixes. Rather than address misclassified utterances one by one, try to identify larger issues and address them at core.
-   **Unbalanced Precision / Recall*** – *Classes with a big discrepancy between their precision and recall scores are unbalanced. There is a pattern here that can be addressed, either undertraining or overtraining. Systemic fixes to balance the intent might be done, with a higher impact than if the intent was already balanced.
-   **Clear Confusion Patterns*** – *Also check if there are classes with clear patterns in how the model has misclassified the failed utterances of that class. If there are patterns, prioritize addressing those rather than the cases where there are no clear patterns.
> [!info]  
>
> **Example**
>
> If the intent CheckOrderStatus has 5 misclassified utterances in a validation set, but all five are misclassified into different classes, then there are no clear patterns. But if all 5 utterances are misclassified into the intent CheckInvoice, there's a pattern here worth investigating.

# Deep Dive Analysis and Training Data Optimization
Once an area or two is identified to fix, it's time to analyze why they performed poorly in validation tests. Armed with the relevant misclassifications, dig into the training data to figure out what went wrong and what can be improved. Avoid falling for the temptation to take the shortcut and just add a few a similar utterances into the training data to the ones that failed. Instead, try to improve a model by investigating and understanding why the validation utterances failed and then address that core issue. 
> [!info]  
>
> As results for the intent ApplyForCourse are inspected, it's noticed that training data is not trained in any of the course names related to a popular set of courses people often apply to attend. This is a good candidate for a systemic fix to fill a major hole in the

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
