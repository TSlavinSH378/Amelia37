-   [Pre-Requisites](#EsETLandAnalyticsTools-Pre-Requisites)
-   [Import the Interaction Script to the BPN Script Library](#EsETLandAnalyticsTools-ImporttheInteractionScripttotheBPNScriptLibrary)
-   [Create an Optimized BPN Process Flow](#EsETLandAnalyticsTools-CreateanOptimizedBPNProcessFlow)
    -   [Set up Common BPNs](#EsETLandAnalyticsTools-SetupCommonBPNs)
    -   [Create BPN Process Flow(s)](#EsETLandAnalyticsTools-CreateBPNProcessFlow(s))
    -   [Create Intents, Entities, and Models](#EsETLandAnalyticsTools-CreateIntents,Entities,andModels)
-   [Engage Amelia in a Conversation](#EsETLandAnalyticsTools-EngageAmeliainaConversation)
-   [Extract the Conversation Log with EsETL](#EsETLandAnalyticsTools-ExtracttheConversationLogwithEsETL)
    -   [How EsETL Flattens Conversation Logs](#EsETLandAnalyticsTools-HowEsETLFlattensConversationLogs)
    -   [Extract and Process Conversation Logs](#EsETLandAnalyticsTools-ExtractandProcessConversationLogs)
    -   [Data Dictionary](#EsETLandAnalyticsTools-DataDictionary)
-   [Import the EsETL Output to a Visualization Tool](#EsETLandAnalyticsTools-ImporttheEsETLOutputtoaVisualizationTool)
> [!warning]  
>
> As of April 2019, this page describes an internal IPsoft process. It is not part of an official IPsoft deliverable. However, clients are welcome to use this process to augment conversation logs and prepare those logs for analysis with visualization tools.

Analysis of Amelia's conversations can be done manually or automated. The Elasticsearch ETL (EsETL) tool is part of a process to tag conversations then export data for automated analysis. Tagging uses the concept of an interaction with a range of tags to describe each interaction. Tags use the [ACE Scoring Methodology](attachments/11944907/11944964.pdf) but naming conventions can be customized to fit any client needs by updating the script naming conventions.
An interaction is a series of utterances that belong to a single task Amelia tries to accomplish in a conversation. A conversation can have one or more interactions, for example, if a person requests different things which trigger different intents within the conversation. There are five main components to an interaction:
-   **Sequence ID Start **- Unique sequence ID that represents the utterance that triggered the Interaction
-   **Interaction ID **- UUID that represents a group of utterances that are all related to each other as an interaction
-   **Intent** - The triggered intent `code` retrieved from Amelia's Context Service
-   **Score** - The corresponding ACE scoring tag for the interaction. By default, all Interactions are tagged `trained_performance` or `tp`.
-   **Abandoned** - Boolean value that denotes whether the current interaction was abandoned or not. By default, all Interactions are tagged `abandoned = true`. This tracks and tags interactions where the user purposefully or inadvertently disconnects before the termination of the interaction.
This tutorial describes steps to extract, process, then display conversation data for automated analysis.
1.  Import the Interaction script into the BPN Script Library. This contains methods used to tag and capture conversation data.
2.  Create a BPN process flow then add tasks and tags used for data analysis.
3.  Engage Amelia in a conversation to generate data for analysis.
4.  Use the EsETL tool to extract conversation data, transform and prepare the log file for visualization tools, and load data for analysis.
5.  Build visualizations and dashboards to analyze data.
# Pre-Requisites
-   Amelia 3.6+
-   Elasticsearch ETL (EsETL) Tool
-   Visualization Tool
-   [Interaction script](attachments/11944907/11944937.groovy)
-   [Six common BPNs](attachments/11944907/11944938.zip)
# Import the Interaction Script to the BPN Script Library
To track each interaction and tags, a Groovy script with pre-defined methods is imported into a BPN Script Library and available to all BPN process flows in a domain.
To import the Interaction script into the BPN Script Library for a domain, click the Process Memory link on the left edge of the administration page then click the Script Library link to display the Script Library workspace. Right mouse-click over a folder on the left side of the workspace and select Add Script. The Create New Script popup appears. Name the new script `Interaction` with no s for plural. Then copy/paste this script into the editor and save.
**Interaction Script**
``` groovy
import groovy.json.*
class ScoredInteraction {
    int seqStart
    String intent
    String score
    String abandoned
    String uuid
    Map details
    ScoredInteraction (String intent, int seqStart) {
        // Default to trained performance
        this.score = "tp"
        this.intent = intent
        this.seqStart = seqStart
        this.abandoned = "true"
        this.uuid = UUID.randomUUID().toString()
    }
    def getDetails() {
        this.details = [
            "seqStart":     this.seqStart,
            "intent":       this.intent,
            "score":        this.score,
            "abandoned":    this.abandoned,
            "uuid":         this.uuid,
        ]
        return this.details
    }
    def setScore(String score) {
        def validScores = ["tp", "to", "te", "up", "uo", "ue"]
        if (validScores.contains(score)) {
            this.score = score
        }
    }
}
def initScoredInteraction() {
    def intent = contextService.triggeredIntent().intent().code()
    def seqStart = getLastSequenceId()
    def currentInteraction = new ScoredInteraction(intent, seqStart)
    storeToTransient(currentInteraction)
}
def initScoredInteraction(String intent) {
    def seqStart = getLastSequenceId()
    def currentInteraction = new ScoredInteraction(intent, seqStart)
    storeToTransient(currentInteraction)
}
def terminateScoredInteraction() {
    def interaction = getCurrentInteraction()
    interaction.abandoned = "false"
}
def getCurrentInteraction() {
    def interactions = transientVariableService.getVariable('interactions')
    def currentInteraction
    // Loop backwards through list of interactions
    for (i = interactions.size() - 1; i >= 0; i--) {
        // Find the most recent interaction that is abandoned
        currentInteraction = interactions[i]
        if (currentInteraction.abandoned) {
            break
        }
    }
    return currentInteraction
}
def getLastSequenceId() {
    def transcriptUtterances = conversationService.getTranscriptUtterances()
    def lastUtterance = transcriptUtterances.last()
    return lastUtterance.sequenceId()
}
def storeToTransient(ScoredInteraction interaction) {
    def interactions = transientVariableService.getVariable('interactions') ?: []
    interactions.add(interaction.details)
    transientVariableService.addVariable("interactions", interactions)
}
def setInteractionScore(String scoreCode) {
    def interaction = getCurrentInteraction()
    def lcScoreCode = scoreCode.toLowerCase()
    interaction.score = scoreCode
    interaction.abandoned = false
}
def writeInteractionsToMetrics() {
    def interactions = transientVariableService.getVariable('interactions')
    // Add empty object to array if only one interaction
    if (interactions.size() == 1) {
        interactions.add([:])
    }
    def interactionsJson = JsonOutput.toJson(interactions)
    customMetricService.upsertMetric("interactions", interactionsJson)
}
```
The Interaction script has four common methods called in BPNs to set tagging metrics.
**initScoredInteraction **- Flags the start of an interaction** **and sets default values for the interaction.
**terminateScoredInteraction***** **- *Flags the end of an interaction and updates the **Abandoned** value to `False`*`.`*
**setInteractionScore***** **- *Sets the* *tag of the current **Interaction. **By default, all interactions are set to `tp`.
**writeInteractionsToMetrics** - Writes all tags to the Custom Metrics Service
Table. One Conversation with Two Interactions and Interaction Method Calls
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Sequence ID</th>
<th class="confluenceTh">Interaction ID</th>
<th class="confluenceTh">User Type</th>
<th class="confluenceTh">Message Text</th>
<th class="confluenceTh">Intent</th>
<th class="confluenceTh">Score</th>
<th class="confluenceTh">Abandoned</th>
<th class="confluenceTh">Interaction Script Method</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd" style="text-align: center;">0</td>
<td class="confluenceTd" style="text-align: center;">-</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd">Hi, I'm Amelia and I will be your Service Desk agent today.</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;">1</td>
<td class="confluenceTd" style="text-align: center;">-</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd">How can I help you?</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">2</td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">1</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">USER</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">I need to open a new ticket.</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">add_new_ticket</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">tp</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">true</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><strong>initScoredInteraction</strong></td>
</tr>
<tr class="even">
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">3</td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">1</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd">I'd be happy to help you submit a new ticket. Can you give me a short description of your issue?</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">4</td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">1</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">USER</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">This is a test ticket.</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
</tr>
<tr class="even">
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">5</td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">1</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd"><p>For your reference, the ticket number is INC0033011.</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">6</td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">1</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd"><p>I've marked this ticket as <strong>Medium</strong> urgency, would you like me escalate it to <strong>High</strong>?</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">7</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">2</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">USER</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">How much PTO do I have?</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">pto_balance</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">tp</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">true</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><strong>initScoredInteraction</strong></td>
</tr>
<tr class="odd">
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">8</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">2</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd"><p>You currently have 17 Vacation days and 6 sick days left.</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">9</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">2</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd"><p>Do you want to take some time off?</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">10</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">2</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">USER</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">No.</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
</tr>
<tr class="even">
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">11</td>
<td class="highlight-blue confluenceTd" style="text-align: center;" data-highlight-colour="blue">2</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd"><p>Glad I could help.</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">false</td>
<td class="confluenceTd"><strong>terminateScoredInteraction</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;">12</td>
<td class="confluenceTd" style="text-align: center;">-</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd"><p>Do you want to continue submitting a ticket?</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">13</td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">1</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green">USER</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><p>No</p></td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
<td class="highlight-green confluenceTd" data-highlight-colour="green"><br />
</td>
</tr>
<tr class="odd">
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">14</td>
<td class="highlight-red confluenceTd" style="text-align: center;" data-highlight-colour="red">1</td>
<td class="confluenceTd">AMELIA</td>
<td class="confluenceTd"><p>I understand</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td colspan="4" class="confluenceTd" style="text-align: center;"><em>pre_close BPN</em></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><strong>writeInteractionsToMetrics</strong></td>
</tr>
</tbody>
</table>
In this example, Amelia successfully launched two interactions in one conversation (add_new_ticket and pto_balance). She completed one interaction (add_new_ticket) and abandoned the second interaction (pto_balance) at the request of the user. Because Amelia did what she was trained to do, the second interaction is scored as a `trained_performance` or `tp`.
> [!warning]  
>
> Remember that interactions have 2 default tags:
>
> -   `Score = tp`
> -   `Abandoned = true`
>
> Since there was no **terminateScoredInteraction*** *for Interaction ID 1 in the conversation example above, the default value of `Abandoned = True` remained.

# Create an Optimized BPN Process Flow
Once the Interaction script is added to a domain's script library, the next step is to import the six common BPNs which contain code to help tagging conversations. Then tasks which refer to these common BPNs are added to a BPN process flow, usually at the start and end points within a process.
## Set up Common BPNs
Using a set of common BPNs in a domain is a more efficient and scalable way to tag conversations for analysis than calling methods ad hoc within BPN Script tasks. Updates to scripts can be made in a centralized location to the common BPNs as needed for immediate use by all tagged BPN process flows.
To tag conversations for analysis, six additional BPNs must be imported to the domain. These should be placed into a common folder to group them by function and to make updates easier. To create a folder, right mouse-click over a folder on the left side of the BPN workspace to add a folder.
To import a BPN, right mouse-click over a folder on the left side of the BPN workspace to create a new blank BPN then click the wrench icon at the top left of the workspace to select Import from the dropdown list. Save the BPN then click the Deploy button to make the BPN active.
Table. Six Common BPNs

| BPN Name | Description |
| ----|----|
| flag_trained_optimization.bpmn | Need short descriptions here for each BPN |
| flag_untrained_performance.bpmn | Calls the method setInteractionScore with a value of 'up' to add the tag of "untrained performance" to the current Interaction.Sets the Abandoned flag to False.Signifies the end of the current interaction. |
| flag_untrained_opportunity.bpmn | Calls the method setInteractionScore with a value of 'uo' to add the tag of "untrained opportunity" to the current Interaction.Sets the Abandoned flag to False.Signifies the end of the current interaction. |
| terminate_scored_interaction.bpmn | Sets the Abandoned flag to False.Signifies the end of the current interaction.*note - default Interaction tag is 'tp' which will be applied to any interaction that ends with this BPN. |
| pre_escalate.bpmn | "Sweeper" style BPN that allows the developer to control adding tags to interactions that are outside of the pre-determined pathways.Ex: If a user talking to Amelia consistently sends utterances that do not trigger Intents or other sub-systems, eventually the pre_escalate sub-system will kick in, allowing the developer to add tags to an interaction before it is escalated to a human agent. |
| pre_close.bpmn | Calls the method writeInteractionsToMetrics which posts the Interaction array as a JSON object to the customMetric service via the method upsertMetric. |

> [!warning]  
>
> The Pre-Close BPN must be deployed and configured in the Domains workspace to export metrics tags to the conversation logs. While the Pre-Escalate BPN is optional, it is strongly recommended to use the logic tuned based on the system environment.
>
> To configure the domain, in the administration workspace, select the System Settings link on the left edge then click the Domains link to display a list of domains. Search or scroll to find the domain then click the notepad icon to edit the domain. In the Conversation Event Processes block in the domain edit workspace, select the correct Pre-Close Process and Pre-Escalate Process dropdown lists to select the correct BPNs.

## Create BPN Process Flow(s)
With the common BPNs imported to a domain, one or more BPN process flows can be created. Each BPN must start with a Script task called `Init` to execute the `initScoredInteractions` method in the Interact script with the following code:
**Script task code for first BPN task**
``` groovy
def main() {
    // Start script
    //LogUtils lu = new LogUtils(execution, log, 'init')
    //lu.startScript()
    // Create new scored interaction
    initScoredInteraction()
    // Get or create context map
    def context = transientVariableService.getVariable('context') ?: [:]
    //lu.logVar('context', context)
    // Get initial user utterance from transcript
    def initialUserUtterance = conversationService.getTranscriptUtterances().last().utterance()
    //lu.logVar('initialUserUtterance', initialUserUtterance)
    def initialUserUtteranceSequenceId = conversationService.getTranscriptUtterances().last().sequenceId()
    //lu.logVar('initialUserUtteranceSequenceId', initialUserUtteranceSequenceId)
    // Init map to hold data specific to this BPN
    def bpnData = [:]
    // Init flags
    bpnData.flags = [:]
    bpnData.flags.newGenerationFlag = false
    bpnData.flags.escalate = false
    bpnData.flags.noProductResults = true
    // Increment request count and set CSAT prompt flag
    context.'requestCount' = context.'requestCount' ? context.'requestCount' + 1 : 1
    log.info('requestCount: ' + context.'requestCount')
    bpnData.flags.csatPrompt = context.'requestCount' % 5 == 0
    log.info('csatPrompt flag: ' + bpnData.flags.csatPrompt)
    // Update context
    context.'sweeperCount' = 0
    context.'initialUserUtterance' = initialUserUtterance
    context.'initialUserUtteranceSequenceId' = initialUserUtteranceSequenceId
    context.'lastUserUtterance' = initialUserUtterance
    // Set execution vars
    execution.setVariable('bpnData', bpnData)
    // Set transient vars
    transientVariableService.addVariable('context', context)
    // End script 
    //lu.endScript()
}
// Execute main
main()
```
Before the terminating end of any BPN branch, the last task should be a Run the Workflow task that corresponds to the tag to export for the BPN branch.
For example, if Amelia goes down the happy path, end the branch with a `run the workflow terminate_scored_interaction` task, providing the tag of `tp` or `trained_performance`.
If Amelia goes down a non-optimal path where she was unable to help the user – but still triggered an Intent! –  end the branch with a `run the workflow flag_trained_opportunity` task.
Each BPN branch, tag, and how tags are defined depends on the domain of knowledge.
## Create Intents, Entities, and Models
At the same time BPN process flows are created and optimized, also create, test, and optimize any intents, entities, and models. This is the last step to prepare Amelia to generate tagged conversation logs.
# Engage Amelia in a Conversation
Once Amelia is trained, the next step is to talk with Amelia and trigger intents and generate tagged conversation data.
# Extract the Conversation Log with EsETL
The Elasticsearch ETL (EsETL) tool works either on a single computer for development or within a formal system architecture for production. The EsETL tool includes an embedded Metrics Extraction tool to extract conversation logs from Amelia instances which the EsETL tool prepares for analysis by visualization tools.
![](attachments/11944907/11944985.png)
Figure. Typical EsETL Tool System Architecture
## How EsETL Flattens Conversation Logs
To search and filter data in Kibana, which utilizes Lucerne Query Syntax, data in the Elasticsearch index must be as flat as possible. While Elasticsearch supports accessing objects in arrays, Kibana, Grafana, Tableau, and most visualization tools do not. JSON output from Amelia conversations includes embedded arrays. These arrays must be extracted and flattened while maintaining attribute associations at deeper levels of their data. The EsETL tool extracts arrays and maintains attribute associations.
Amelia's conversations use each conversation as a focal point, or center of the universe. For each conversation, arrays contain conversation data, slots by ID, goals by ID, contexts, and metrics. These arrays are mutually exclusive and tied together with unique IDs.
To work with the Lucerne Query Language and similar visualization tools, utterances are used as the focal point instead of conversations. Each utterance is indexed as an individual document or row, depending on terms used by a visualization tool. The result is a significantly flattened single JSON array used by Elasticsearch.
Because utterances are used as the focal point to process Amelia's conversations, every utterance must include top level data data found in the conversation array, for example, handle time, user_email, agent_email, and so on. Any calculated value also needs to exist as a unique value. For example, total_handle_time must uniquely exist for each conversation. Therefore, in a flattened Amelia conversation file, only one utterance in a conversation can hold top level metrics, usually Amelia's initial utterance in a conversation.
## Extract and Process Conversation Logs
The EsETL software can be requested from a Cognitive Project Lead.
> [!info]  
>
> Using this tool requires Python 3.6.4 or above on the executing laptop, server, or other machine. Additional Python modules may be required to use this tool depending on what exists on the executing machine.

The command usage for this tool closely mimics that of the MetEx tool.
**Export chats from single domain to Elasticsearch**
``` groovy
python3 elasticsearchimport.py -i '<amelia_location>' -u '<amelia_url>' -d '<domain>' -s '2018-10-01' -e '2018-10-23'
```
**Export chats from multiple domains to elasticsearch**
``` groovy
python3 elasticsearchimport.py -i '<amelia_location>' -u '<amelia_url>' -d '<domain domain domain>' -s '2018-10-01' -e '2018-10-23'
```
Table. EsETL Option Flags

| Option | Since Version | Description |
| ----|----|----|
| -i <value> | 0.1 | Name of the index to be created in Elasticsearch |
| -u <value> | 0.1 | URL of the Amelia instance |
| -d <values> | 0.1 | List of domains to export from (space delimited, must include at least 1 domain) |
| -s <value> | 0.1 | Start date to export from as YYYY-MM-DD |
| -e <value> | 0.1 | End date to export to as YYYY-MM-DD |

## Data Dictionary
A data dictionary will be provided shortly.
# Import the EsETL Output to a Visualization Tool
Metrics collected in the JSON array flattened by the EsETL tool can be aggregated in Kibana or similar tool. Any data indexed as a keyword type also can be created as a visualization. Data aggregations and visualizations can be collected and organized in a Kibana dashboard.
IPsoft currently follows this process internally for clients using Elasticsearch and Kibana tools. This process and tools are not officially validated and supported by IPsoft. There are many other tools that could be used to achieve the similar results.
## Attachments:
![](images/icons/bullet_blue.gif) [Interaction.groovy](attachments/11944907/11944937.groovy) (application/octet-stream)  
![](images/icons/bullet_blue.gif) [EsETL_6_Common_BPNs_2019-0425.zip](attachments/11944907/11944938.zip) (application/zip)  
![](images/icons/bullet_blue.gif) [create_ticket.bpmn](attachments/11944907/11944940.bpmn) (application/octet-stream)  
![](images/icons/bullet_blue.gif) [pto_balance.bpmn](attachments/11944907/11944941.bpmn) (application/octet-stream)  
![](images/icons/bullet_blue.gif) [Chat_ACE_Metrics_Presentation_0817.pdf](attachments/11944907/11944964.pdf) (application/pdf)  
![](images/icons/bullet_blue.gif) [image2019-4-25_13-26-25.png](attachments/11944907/11944968.png) (image/png)  
![](images/icons/bullet_blue.gif) [Chat_Analytics_MetEx_Flow_Prod.jpg](attachments/11944907/11944969.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2019-4-25_15-16-44.png](attachments/11944907/11944985.png) (image/png)  
