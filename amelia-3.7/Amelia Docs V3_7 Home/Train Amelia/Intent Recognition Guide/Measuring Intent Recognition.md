-   [Intent Recognition and Metrics Data Selection](#MeasuringIntentRecognition-IntentRecognitionandMetricsDataSelection)
    -   [Utterance Selection](#MeasuringIntentRecognition-UtteranceSelection)
        -   [Prompted Intent Utterances](#MeasuringIntentRecognition-PromptedIntentUtterances)
        -   [Unprompted Intent or Intent-Like Utterances](#MeasuringIntentRecognition-UnpromptedIntentorIntent-LikeUtterances)
    -   [Scope Selection](#MeasuringIntentRecognition-ScopeSelection)
        -   [Utterances that Express a Trained Intent](#MeasuringIntentRecognition-UtterancesthatExpressaTrainedIntent)
        -   [Utterances that Express an Untrained Intent](#MeasuringIntentRecognition-UtterancesthatExpressanUntrainedIntent)
    -   [Speech-to-Text for Voice Implementations](#MeasuringIntentRecognition-Speech-to-TextforVoiceImplementations)
-   [Intent Recognition Metrics by Sample](#MeasuringIntentRecognition-IntentRecognitionMetricsbySample)
    -   [Selecting Sample Data](#MeasuringIntentRecognition-SelectingSampleData)
        -   [Representative Samples](#MeasuringIntentRecognition-RepresentativeSamples)
        -   [Sufficiently Precise Samples](#MeasuringIntentRecognition-SufficientlyPreciseSamples)
        -   [Independent Samples](#MeasuringIntentRecognition-IndependentSamples)
    -   [Calculating Sample Size + Margin of Error + Confidence Level](#MeasuringIntentRecognition-CalculatingSampleSize+MarginofError+ConfidenceLevel)
        -   [Variables and Terminology](#MeasuringIntentRecognition-VariablesandTerminology)
        -   [Calculation Spreadsheet](#MeasuringIntentRecognition-CalculationSpreadsheet)
    -   [Using Samples for Intent Recognition Metrics in Amelia Projects](#MeasuringIntentRecognition-UsingSamplesforIntentRecognitionMetricsinAmeliaProjects)
Intent recognition should be measured in production environments to understand current status at any time and to improve intent recognition. There are three aspects to measuring intent recognition.
-   **Selecting the Data Basis for Intent Recognition Metrics** — what to measure when measuring intent recognition
-   **Measuring Intent Recognition by Sample** — how to measure intent recognition
-   Annotating to Measure Intent Recognition  — how to efficiently and accurately get the data to measure intent recognition
# Intent Recognition and Metrics Data Selection
In every Amelia deployment, a decision must be made about what conversation utterances should be used to measure intent recognition.
Intuitively, it may feel natural to base the intent metrics purely on utterances where users express an intent. However, that approach can easily give incomplete or skewed metrics. To get truer metrics, depending on the nature of the Amelia implementation, set up boundaries for what data to include with two sometimes three criteria.
-   Utterance Selection
-   Scope Selection
-   Speech-to-Text (only relevant for voice implementations)
## Utterance Selection
First, define exactly what utterances from the conversation between the user and Amelia to extract as a basis for the intent recognition metrics. Below are relevant criteria to use to determine what utterances out of the entire conversations should count in this context.
### Prompted Intent Utterances
Clearly, include all utterances where Amelia prompts the user for an intent, specifically, all utterances where the user is expected to express an intent. These are location-dependent utterances because they always happen in the same place in every conversation. 
Typically, this includes:
-   The user's first utterance in the conversation - if they are prompted by Amelia to express an intent there. This also includes any rephrasings of the intent, for example, if Amelia did not understand the intent and prompted the user to ask in a different way.
-   Once a process is completed, and the user is back to square one, they may express another intent if they have another issue to solve. If so, these utterances should form part of the basis for the intent recognition metrics as well.
In many Amelia deployments, this will cover all relevant utterances. The other possible criteria can be disregarded.
> [!warning]  
>
> This criterion does *not *equal "utterances where the user expresses an intent". Even if Amelia prompts the user to express their intent, not all users will. Some may instead for example greet Amelia or say they have a request without specifying the request. These non-intent utterances should be included in the metrics. True intent recognition also includes understanding when the user does not express an intent (the negative class), and so these utterances form a natural and logical part of our metrics. If we exclude these non-intent utterances, we will get incomplete metrics.

### Unprompted Intent or Intent-Like Utterances
When context switching is active, the criterion above will not suffice because it will not include unprompted intent or intent-like utterances. Relevant utterances that are independent of any particular location in the conversation, that arrive out of the blue, will not be included in measuring intent recognition. 
Whenever context switching is active, intent recognition takes place continuously. However, including all utterances said at any time that the user could context switch seems overblown. That would include lots and lots of conversation utterances instead of expected intent utterances. As a result, this criterion can be refined instead to include the following: 
-   All utterances that triggered an intent - excluding the negative class.
-   Ideally, all utterances that *should *have triggered an intent. 
-   Ideally, all intent-like utterances that *could *have triggered an intent, but shouldn't / didn't (this will be subjective). 
> [!info]  
>
> **Example**
>
> To illustrate, the example conversation below includes utterances meeting the various criteria above. 
>
> Amelia: Hi Astrid, what can I help you with? 
>
> User: Hey Amelia, I got a request for you. — Included, as the user is expected to express an intent at this point, so Amelia must correctly evaluate this as the negative class.
>
> Amelia: Hi Astrid. 
>
> User: I need to process a client application for a grant. — Included, as the user is still expected to express an intent at this point.
>
> Amelia: What is the client's name? 
>
> User: Oh, actually, I need to register the client first, it's a new one. — Included, as this triggers a new intent (context switch). 
>
> Amelia: What is the new client's name?
>
> User: Pippi Mackrelmint Longstocking.
>
> Amelia: Thank you. I'm adding the client information to the right as we proceed. If I get anything wrong, you can just click Edit and I will help you change it.
>
> Amelia: What is the user's date of birth? 
>
> (...)
>
> Amelia: Thank you. Pippi is now registered as a new client.
>
> Amelia: Do you want to continue processing a grant? 
>
> User: Hold on, I'm just gonna check the system that Pippi was registered in the backend too. — Included, as this utterance can resemble an intent (RegisterNewClient) even though it isn't. That is, it's intent-like, and so presents a real challenge for intent recognition and forms a natural part of the basis for intent recognition metrics.
>
> Amelia: I'm afraid I'm not sure what you mean. 
>
> Amelia: Do you want to continue processing a grant? 
>
> User: It's all good, yes, please continue.
>
> (...)

## Scope Selection
Once utterances relevant in the conversations are identified, in some cases consider whittling down what forms the basis for intent recognition metrics based on trained versus untrained intents. This won't always be relevant, but may be relevant in certain Amelia implementations.
### Utterances that Express a Trained Intent
All utterances that express a trained intent – whether intent recognition was correct or not –  should of course form part of the metrics basis.
### Utterances that Express an Untrained Intent
In some Amelia deployments, Amelia will be trained for a number of skills but not yet trained for a number of other skills. In other words, Amelia isn't yet trained for these other skills *neither as intents nor in the negative class*.
Even so, she may be asked about those skills. If that happens, consider whether or not to include user utterances for untrained skills in the metrics. 
By analogy, imagine a factory that's 80% finished and 20% half-finished. The production output is high for the finished part, but low for the unfinished part. To get the truest measure of the production output, should the production stats from the unfinished part of the factory be included or excluded? The answer depends on what we want to measure.
In an Amelia setting, to measure Amelia on what she's in fact trained on, only include the metrics for the 80% that's finished. To get a complete picture of the output, including the untrained part, include everything.
> [!info]  
>
> **Example**
>
> Amelia will be trained in a total scope of about 80-90 intents. At go live, Amelia is trained to recognize and process 40 of those intents. 20 intents have, for now, been trained to the negative class. The final 20-30 intents Amelia hasn't yet trained for in any way because of uncertainty about their nature and merit as intents. Going live will help to get user data to better understand if and how users ask for these 20-30 intents, so Amelia can more easily and accurately be trained for them.
>
> In terms of measurements, in this situation, keep double metrics. One set of metrics is for intents that Amelia is trained in where she is expected to perform well. The second set of metrics also includes how she handles utterances for the 20-30 intents she's not trained in, where performance is expected to be lower.

## Speech-to-Text for Voice Implementations
In voice implementations, the speech-to-text conversion constitutes an extra layer that can cause failed intent recognition. If the speech-to-text incorrectly converts one or more words into text, that can of course impact Amelia's evaluation of what intent if any the utterance should trigger.
When this occurs, there's nothing wrong with Amelia's intent recognition, as the fault lies in the speech-to-text conversion. That said, the end result is nonetheless failed intent recognition. The question, then, is if and then how incorrect translations to text should be counted in the intent recognition measurements.
# Intent Recognition Metrics by Sample
Using sample data is usually the best way to determine intent recognition levels, especially in high-volume Amelia deployments. Annotating *all* conversations will often be impossible. In fact, it may be a waste of time to annotate too much data, much less all data, because sufficiently accurate measurements can be gotten using *sample* data.
To do this right, answer two important questions with minimum effort:
-   What is Amelia’s actual intent recognition rate?
-   What was the actual impact of the intent recognition improvements?
This section explains the theoretical basis for using sample data to measure intent recognition with desired accuracy, and provides practical guidance, including calculation formulas and tables, for how to use sample data for this purpose.
-   Sample Selection (what constitutes a good sample)
-   Calculating Sample Size + Margin of Error + Confidence Level (including ready-made calculators)
-   Using Samples for Intent Recognition Metrics in Amelia Projects
This applies equally to any other metric used to measure based on conversations logs, not only intent recognition.
## Selecting Sample Data
*Sampling* means taking a small subset of data to represent a full set of data. The metrics of the sample then give us an estimate of the total metrics of all the data. For example, if you poll 2000 people about their political affiliation, that's a sample that gives you an estimate of the political affiliation of the entire population. In other words, you can *infer *an approximation of the political affiliation of the entire population, using the result of your sample.
In Amelia, we take a sample of conversations, then extract the relevant utterances from that sample of conversations. Exactly utterances from the conversation logs should form part of the sample is discussed above in the Intent Recognition Metrics Data Selection section. 
When sampling is used in an Amelia project, make sure that samples fulfill the criteria explained below. 
### Representative Samples
As far as possible, a sample must be an unbiased representation of the full or unlimited set of data. In practice, the sample data should be a completely random outtake of the total data. 
Exactly what utterances from the conversations logs should be included is discussed below.
> [!info]  
>
> **Example**
>
> Every week, Amelia handles 20 000 conversations. In these conversations, Amelia always prompts the user to express their intent at the start of the conversation and once a process is finished. Context switching is disabled. In the logs, we find 19 750 conversations where the user responded to at least one of Amelia's prompts. In the remaining conversations, the user quit Amelia before saying anything.
>
> From these conversations, 21 000 user utterances were responses to Amelia prompting the user for an intent. From these, take out a sample of 3000 *random* utterances. This maximizes the chance we get a balanced sample, with a representative distribution across intents, users, day-of-week, time-of-day, and so on.

### Sufficiently Precise Samples
Samples must be large enough to give results with meaningful precision. In practice, the margin of error must be limited to whatever is acceptable. In most cases, a sample with an intent recognition rate somewhere between 70% and 85% is worthless. A sample with an intent recognition is 80-81% will usually be sufficiently accurate.
> [!info]  
>
> **Example**
>
> Over the course of 10 weeks, the goal is to improve intent recognition with 4 percentage points in an Amelia deployment. To measure status and progress, a new sample validation set is extracted and analyzed bi-weekly over these 10 weeks. The size of these sample sets gives a margin of error of 3% with a confidence level of 95%. 
>
> The bi-weekly results are shown below:
>
> 
> | Week | Intent Recognition |
> | ----|----|
> | 1-2 | 78-84% |
> | 3-4 | 77-83% |
> | 5-6 | 81-87% |
> | 7-8 | 79-85% |
> | 9-10 | 81-87% |
> 
>
> What can be learned from these results? The intent recognition generally is probably in the low-to-medium 80s. But in terms of the progress over the 10 weeks, this shows nothing was learned. In fact, it's perfectly possible Amelia's intent recognition abilities moved backwards instead of forward. The real results week 1-2 might have been 84% while the real result at week 9-10 might have been 81%. Based on our sample results, it's impossible to draw conclusions.
>
> On top of that, during these 10 weeks, there is no way to know if changes made from one week to the next actually improved performance. It’s possible to waste time with misdirected efforts.
>
> It's also possible to calculate a probability measure for whether the results every two weeks show a clear (upwards) trend, or whether there's no real trend at all. That is, whether the trend is in fact a trend, if it has statistical significance.
>
> --- FAIL!
>
> To get meaningful results, the sample set must have a margin of error that's significantly lower.

### Independent Samples
Ideally, a sample should *not* be from a data set used to improve intent recognition. The sample probably would achieve higher intent recognition than the full or unlimited data set. Even with a big sample, the improvements will probably have a greater impact on the validation data used as a sample that they're based on than on the mostly unseen data.
> [!info]  
>
> **Example**
>
> Starting with the example to illustrate issues around sufficiently precise samples, this time a single big sample is extracted after two weeks and used for all bi-weekly measurements. This sample has a margin of error of only 0.5%.
>
> Using this method, the intent recognition level is 81.0-82.0% for week 1-2. For week 9-10, the recognition level is 86.0-87.0%. Based on this sample, significant gains are clearly demonstrated.
>
> However, if the data in the sample is used for metrics AND as a basis to improve intent recognition, the results are suspect. Even if the improvements made will generalize well to unseen data not in the sample, gains on the sample data almost certainly were bigger than on all the data. Therefore, the real intent recognition in the full data set for week 9-10 is probably a bit lower than 86-87%.

## Calculating Sample Size + Margin of Error + Confidence Level
When sampling is done, results are approximate. For *exact* results, results must be based on all the data.
However, exactly how precise our sample results are can be calculated with high precision. If done right, samples will provide a degree of accuracy in the results that are meaningful to whatever the purpose of the results.   
The variables and context for these calculations is explained in this section, and the associated spreadsheet provides ready-made formulas and tables that can be used to easily perform or look up the actual calculations for any data sets. 
### Variables and Terminology
Let's first look at the variable values and terminology used when performing this kind of calculations. 

| Symbol | Value | Explanation |
| ----|----|----|
| n | Sample size | The;sample size is the number utterances included in a sample. If measuring against a sample of 2000 utterances, the sample size is 2000. |
| N | Population size | The;population size is the total number of existing utterances. By analogy, if the presence of a tree disease is tested on a sample of 1000 fir trees, but the entire forest has 1 000 000 fir trees, the population size is 1 000 000.When sampling intent recognition metrics, a population size is often unavailable. There's no static number of utterances said to Amelia – it grows as more users speak with her. The population is unlimited or infinite.To measure intent recognition on a limited finite set of utterances, there is a population size. For example, to measure intent recognition for a given month, with a total 50 000 relevant utterances from user conversations with Amelia in that month, then the population size will be 50 000.  |
| MoE | Margin of error | The;margin of error describes the accuracy of results for the sample. That is, how much of an approximation or estimation the result is - how close to the actual result (of the entire population) the sample result is. For example, for a sample result accurate to within 1% of the actual result, the margin of error should be 1% or less. If the actual result is 85%, the sample result should be 84-86%.In other words, the sample result will give a range not an exact value. Based on the sample the actual result is somewhere in that range defined by the margin of error. The bigger a sample size, the smaller the margin of error will be – and vice versa.  |
| conf lvl | Confidence level | However, it's impossible to be certain the sample result reflects the actual result within the margin of error. A small level of uncertainty exists that the sample falls outside the actual population result. The certainty level is called a confidence level.In statistics, the confidence level is often set to 95%, meaning a 95% certainty the sample result is accurate. However, the confidence level can be set to any number. A lower number requires a smaller sample size with less confidence the sample represents the full data set. |
| z | Confidence interval | Based on the confidence level, a range of values can be calculated which includes the real population result. This range, or area, is called a confidence interval.To calculate the confidence level, a;probability distribution for the data must be known or assumed. The distribution reflects how spread out or closely aligned the data is, as measured using standard deviations. This is a measure of how far from the mean the values in the distribution are on average. The average distance is equal to 1 standard deviation. If there's a lot of values quite far from the mean or high variance, the standard deviation will be high. If the values cluster quite closely around the mean or low variance, deviation will be low.For our measurements, use the normal probability distribution of values, the bell curve or Gaussian curve. Using this, 95% of the area of the distribution is within 1.96 standard deviations from the mean.  There's a 95 % chance that our sample result will fall within 1.96 standard deviations from the true result of the full data set. There's a 2.5% chance the sample result will fall below -1.96 standard deviations from the mean, the actual result of the population – and a 2.5% chance the sample result will fall above 1.96 standard deviations from the mean, a 5 % chance that the sample result will be outside the margin of error.Therefore, the confidence Interval is a range of values that includes the real population result. This is calculated based on the confidence level, given a certain distribution of the values and the corresponding standard deviation. It also is assumed the value distribution follows the normal distribution. |
| p | Proportion of successes | The proportion of;expected successes, or correct intent recognition, is a variable in the calculation. If the accuracy of intent recognition is known with some accuracy, provide a conservative estimate of that value as p. For example, if the intent recognition rate from experience is 75 and 85%, set p to 0.75. Be conservative and pick the lowest number.If the intent accuracy rate is unknown or below 50%, set p to 0.50 initially to indicate maximum uncertainty. If a calculation using p set to 0.50 returns an estimated intent recognition rate of 70-75%, for example, redo the calculation with the lower p number of 0.70 or 70%. The new calculation returns a slightly smaller sample size needed. |
| N/A | Number of intents | The number of intents is currently;not part of the calculation. However, this can be a relevant factor. If we have only 5 intents, there's a good likelihood that the variation among the utterances will be a lot less than if we have 100 intents. In turn, that may mean a smaller sampler size will still be sufficiently representative.  |

### Calculation Spreadsheet
Intent recognition is a question of whether intent recognition was successful or not. It is a binary or boolean problem. Given this, approach sampling of intent recognition as a question of binomial probability distribution. This provides relatively simple mathematics/statistics to calculate, for example, the margin of error for given variables X and Y, what sample size is needed given variable X and Y, and so on.
The spreadsheet includes ready-made formulas and tables to do this, along with instructions: Intent Recognition Sample Calculations.
> [!warning]  
>
> As calculations are performed, an assumption is made about the distribution of data set values, both the sample set and full data set. Calculations in the spreadsheet linked above operate under the assumption data sets have a normal distribution with a bell curve or Gaussian distribution.

## Using Samples for Intent Recognition Metrics in Amelia Projects
Start measuring intent recognition when an Amelia project goes into production. In low-volume deployments, measurement can be done on all data. High-volume deployments, however, require measuring with samples. Using samples, there are fundamentally two approaches which can be blended in various ways:
-   Measuring against a *fixed* sample data set, that's only updated when the Amelia implementation changes
-   Measuring at given intervals against *new / expanded* data sets
Both of these approaches have pros and cons.
