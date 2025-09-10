-   [Create Tests](#EddieAutomatedTestTool-CreateTests)
    -   [Replay vs. Load Tests](#EddieAutomatedTestTool-Replayvs.LoadTests)
    -   [Creating a New Replay Test](#EddieAutomatedTestTool-CreatingaNewReplayTest)
    -   [Handing multi-line responses from Amelia](#EddieAutomatedTestTool-Handingmulti-lineresponsesfromAmelia)
    -   [Creating a New Load Test](#EddieAutomatedTestTool-CreatingaNewLoadTest)
    -   [Test Form Fields](#EddieAutomatedTestTool-TestFormFields)
        -   [Test Type](#EddieAutomatedTestTool-TestType)
        -   [Test Name](#EddieAutomatedTestTool-TestName)
        -   [Max Concurrent](#EddieAutomatedTestTool-MaxConcurrent)
        -   [Instance](#EddieAutomatedTestTool-Instance)
        -   [HumanWait](#EddieAutomatedTestTool-HumanWait)
        -   [Conversations](#EddieAutomatedTestTool-Conversations)
        -   [Utterance Pairs](#EddieAutomatedTestTool-UtterancePairs)
        -   [Selector LOAD ONLY](#EddieAutomatedTestTool-SelectorLOADONLY)
        -   [Max chats LOAD ONLY](#EddieAutomatedTestTool-MaxchatsLOADONLY)
        -   [Ramp Config LOAD ONLY](#EddieAutomatedTestTool-RampConfigLOADONLY)
    -   [Exporting a test](#EddieAutomatedTestTool-Exportingatest)
    -   [Importing a test](#EddieAutomatedTestTool-Importingatest)
-   [Dashboard](#EddieAutomatedTestTool-Dashboard)
    -   [Recent Tests](#EddieAutomatedTestTool-RecentTests)
    -   [Recent Load Tests](#EddieAutomatedTestTool-RecentLoadTests)
    -   [Test Details](#EddieAutomatedTestTool-TestDetails)
# Create Tests
From the `Create Tests` page you can create new tests, export a test as a replay file, or import previously saved replay files for testing.
## Replay vs. Load Tests
There are two types of tests - Replay and Load.
-   Replay tests are designed to test conversations and use cases from an Amelia instance. These are the most common type of tests and most users will only create Replay tests.
-   Load tests are designed to stress-test an Amelia instance with multiple conversations at the same time, rather than test the use-cases themselves. These tests require an elevated level of permissions to create.
## Creating a New Replay Test
The steps below are meant to be a quick-start guide. For detailed information on what each field in the test creation form means, see the test fields table  
Before submitting a test to be run, you may want to export the test as a replay file to ensure you have a backup of your test.
1.  Click `Create Test` on the navigation menu
2.  Enter a Test Name (it is *highly* recommended this name be unique for each test)
3.  Set a Max Concurrent value, this allows you to run multiple conversation use cases at the same time.
4.  Enter the Instance information:
    1.  Give the instance a Name (this is meant to be a user-friendly name, and is only used to make reading results easier to parse)
    2.  Enter the instance URL (This must be an Amelia URL that ends in */Amelia*).
    3.  Enter a Username. This is the user account used by Eddie when connecting to the Amelia instance. Some instances allow anonymous chat sessions, in which case use the default user *anonymous*
    4.  Enter the Password for the given `Username`. If using the *anonymous*, no password is required.
    5.  Set the Version number of Amelia to be tested (default is version *3*).
    6.  Enter the Domain Code of the domain to be tested.  
        Note: The `domain code` may differ from the `domain name` used for display in the Amelia interface
5.  Fill out the HumanWait section. This define how long Eddie will wait between utterances while testing.   
    Note: if you're unsure what this section is, you can just use the default values
    1.  Set the Interval Type
        -   Millisecond
        -   Second  
            default
        -   Minute
    2.  Set the Minimum interval to wait before sending an utterance to Amelia
    3.  Set the Maximum interval to wait before sending an utterance to Amelia
6.  Create one or more Conversations to test for a use-case using 
    1.  Enter a Name for the conversation.   
        Note: it is best to give a unique name for each conversation
    2.  Enter the Domain Code where the conversation will take place on the Amelia instance (this will almost always be the same domain code defined in the `Instance` section).
    3.  Set the Timeout period, in seconds, to wait for the conversation to complete. If exceeded the test will be terminated and marked as timed out (using the default timeout is recommended).
    4.  Click the  button to add an Utterance Pair. Each utterance pair consists of the user question/statement and the expected response from Amelia. Each utterance pair represents a step in the conversation. Each pair runs in the order which is defined in the test form.   
        Note: If Amelia has a multi-line response to a user utterance, create a new utterance pair for each line after the first one, leaving the user utterance empty. See the Multi-line Amelia Responses section for details.
        1.  Enter User Utterance - the questions or statement the user would say to amelia.  
            Note: The first pair question should always be blank for the initial Amelia utterance
        2.  Define the type of Operation used to compare Amelia's response against the Expected Answer to determine success or failure.
        3.  Click the  button to add an expected answers. You can add multiple if there is variation in the conversation.
        4.  Set if you want to Negate the operation - causing the oposite of the defined operation/expected answer to be considered successful .
        5.  Set the Timeout in seconds to wait before the response is considered timed out.
7.  Next, click the  button to export a replay copy of your test to your hard drive (this step is not required, but it is *highly*recommended to keep backups of your tests).
8.  Click  to launch your test into the Eddie test queue.  
    Note: if you have made any errors in formatting the system will tell you
## Handing multi-line responses from Amelia
Sometimes Amelia will respond with multi-line statements. Each line in Amelia's response should have it's own utterance pair, even if there is no correlating user utterance.
The following conversation only needs **one utterance pair**, as there is only one response from Amelia:

|  |  |
| ----|----|
| User: | I'm having trouble logging into my account. |
| Amelia: | No problem. What is your 4 digit extension? |

Whereas this conversation would need **two utterance pairs**. One with the user utterance and expected answer for "Sorry to hear that", and another with an empty user utterance and an expected answer for "What is your 4 digit extension?".

|  |  |
| ----|----|
| User: | I'm having trouble logging into my account. |
| Amelia: | Sorry to hear that. |
| Amelia: | What is your 4 digit extension? |

> [!info]  
>
> If only one utterance pair was created for this conversation, the correct expected answer would be "Sorry to hear that. What is your 4 digit extension?"

## Creating a New Load Test
The steps below are meant to be a quick-start guide. For detailed information on what each field in the test creation form means, see the test fields table.
> [!info]  
>
> Load testing requires elevated permissions and may not be available depending on your user roles.
> [!info]  
>
> Before submitting a test to be run, you may want to export the test as a load file to ensure you have a backup of your test.

1.  Click `Create Test` on the navigation menu
2.  From the *Test Type* drop down select *Load*
3.  Enter a Test Name (it is *highly* recommended this name be unique for each test)
4.  Enter the Instance information:
    1.  Give the instance a Name (this is meant to be a user-friendly name, and is only used to make reading results easier to parse)
    2.  Enter the instance URL (This must be an Amelia URL that ends in */Amelia*).
    3.  Enter a Username. This is the user account used by Eddie when connecting to the Amelia instance. Some instances allow anonymous chat sessions, in which case use the default user *anonymous*
    4.  Enter the Password for the given `Username`. If using the *anonymous*, no password is required.
    5.  Set the Version number of Amelia to be tested (default is version *3*).
    6.  Enter the Domain Code of the domain to be tested.  
        Note: The `domain code` may differ from the `domain name` used for display in the Amelia interface.
5.  Pick the Selector to control the order of test execution.
6.  Enter a Max Chats value to set how many conversations will run during the test.
7.  Enter the Ramp Up configuration information. This defines how Eddie will ramp up the load test from 0 conversations until reaching the target value. This allows you to slowly apply load over time if you choose.
    1.  Enter the Concurrent Chats the load test should reach.
    2.  Enter the Chat Ratio the load test should increase by until reaching Concurrent Chats.
    3.  Enter the Time Ratio the load test should wait before increasing the number of active chats.
    4.  Set the Time Type
        -   Millisecond
        -   Second  
            default
        -   Minute
8.  Enter the Ramp Down configuration information. This defines how Eddie will ramp down the load test from the max concurrent chats.
    1.  Enter the Concurrent Chats the load test should reach, this should always be zero
    2.  Enter the Chat Ratio the load test should decrease by until reaching Concurrent Chats.
    3.  Enter the Time Ratio the load test should wait before decreasing the number of active chats.
    4.  Set the Time Type
        -   Millisecond
        -   Second  
            default
        -   Minute
9.  Fill out the HumanWait section. This define how long Eddie will wait between utterances while testing.  
    Note: if you're unsure what this section is, you can just use the default values
    1.  Set the Interval Type
        -   Millisecond
        -   Second  
            default
        -   Minute
    2.  Set the Minimum interval to wait before sending an utterance to Amelia
    3.  Set the Maximum interval to wait before sending an utterance to Amelia
10. Create one or more Conversations to test for a use-case using 
    1.  Optionally enter the Weight of each conversation. This is used with Selector type *random* to pick more or less of a use case.
    2.  Set the timeout period, in seconds, to wait for the conversation to complete. If exceeded the test will be terminated and marked as timed out (using the default timeout is recommended).
    3.  Click the  button to add an Utterance Pair. Each utterance pair consists of the user question/statement and the expected response from Amelia. Each utterance pair represents a step in the conversation. Each pair runs in the order which is defined in the test form.
        1.  Enter User Utterance - the questions or statement the user would say to Aamelia.  
            Note: The first pair question should always be blank for the initial Amelia utterance
        2.  Define the type of Operation used to compare Amelia's response against the Expected Answer to determine success or failure.
        3.  Click the  button to add an Expected Answers. You can add multiple if there is variation in the conversation.
        4.  Set if you want to Negate the operation - causing the opposite of the defined operation/expected answer to be considered successful .
        5.  Set the Timeout in seconds to wait before the response is considered timed out.
11. Next, click the  button to export a load copy of your test to your hard drive (this step is not required, but it is *highly* recommended to keep backups of your tests).
12. Click  to launch your load test into the Eddie test queue.  
    Note: if you have made any errors in formatting the system will tell you
## Test Form Fields
Most tests are simple, but some require complexity. For this reason, the test creation form allows you to override default settings for some of the more complex test settings. Below are details for each field in the replay and load test creation forms.
### Test Type
The type of test being created

| Replay |
| ----|
| The default test type used to test conversations |
| This test type is used to stress test an Amelia instance and should never be used to test conversations or use cases. Load tests are covered in detail in the;Creating a new load test section. |

### Test Name
The user-friendly test name.
> [!warning]  
>
> Always use unique, easily identifiable names for each test. This will make the test easy to find on the dashboard and ensure unique names for the exported replay files.

### Max Concurrent
The maximum number of conversations to run concurrently for a given test. If you are testing multiple conversations this can enable the overall test to finish faster up to a max of 10 concurrent chats. In tests were use cases must be executed one at a time in order you can set the value to 1.
### Instance
The Amelia instance you will be testing.
<table class="wrapped confluenceTable">
<tbody>
<tr class="odd">
<th class="confluenceTh">Name</th>
<td class="confluenceTd">The user-friendly name for the instance</td>
</tr>
<tr class="even">
<th class="confluenceTh">URL</th>
<td class="confluenceTd"><div class="content-wrapper">
<p>The instance URL. (This must be an Amelia URL that ends in <em>/Amelia</em>).</p>
<div class="table-wrap">
<pre class="table"><code>| Example URLs |
| ----|
| http://amelia.client.com/Amelia |
| http://amelia.client.com/Amelia/ |
| http://amelia.client.com/ |</code></pre>
</div>
<p><br />
</p>
</div></td>
</tr>
<tr class="odd">
<th class="confluenceTh">Username</th>
<td class="confluenceTd">This is the user account used by Eddie when connecting to the Amelia instance. Some instances allow anonymous chat sessions, in which case use the default user <em>anonymous</em></td>
</tr>
<tr class="even">
<th class="confluenceTh">Password</th>
<td class="confluenceTd">Enter the <code>Password</code> for the given <code>Username</code>. If using the <em>anonymous</em>, no password is required.</td>
</tr>
<tr class="odd">
<th class="confluenceTh">Version</th>
<td class="confluenceTd">The version of Amelia being tested</td>
</tr>
<tr class="even">
<th class="confluenceTh">Domain Code</th>
<td class="confluenceTd">The <code>domain code</code> of the domain to be tested against on the Amelia instance. Note: The <code>domain code</code> may be different from the <code>domain name</code> displayed in the Amelia interface. If you are unsure what the correct <code>domain code</code> is, ask you Amelia administrator.</td>
</tr>
</tbody>
</table>
### HumanWait
The `Human Wait` controls are used to simulate human-like responds times when sending utterances to Amelia during a test. The delay will be a randomly selected value between the two defined values.
> [!warning]  
>
> Human wait times are not counted against utterance response times.


| IntervalType |
| ----|
| MillisecondSeconddefaultMinute |
| The minimum interval to wait before replying to Amelia. |
| The maximum interval to wait before replying to Amelia. |

### Conversations
Clicking the  button in the `Conversations` section will create a new conversation for the test. One test can have multiple conversations.
> [!warning]  
>
> It is *strongly* recommended you create conversations relevant to the purpose of the test. Each conversation should reflect a different path for the same use case. This will make it possible to efficiently test in the future as new conversational paths are added to a use case.


| Conversation Weight LOAD ONLY |
| ----|
| The numerical weight that will be used when;Selector Random is used. Tests with a higher weight will be run more often. |
| The user-friendly name of the conversation.Note:;It is very important to make names unique for each conversation. This is necessary to make the test results readable. |
| This domain code to be tested on the Amelia instance.Note:;This will almost always be the same as the Domain Code given when filling in the instance information. Although, there are rare cases where a multiple domains need to be tested from the same test. |
| The number of seconds to wait for a response from the Amelia instance before considering the conversation timed out.Note:;It is recommended to leave this at it's default value. Entering a high timeout can take up Eddie resources if the Amelia instance is having network issues or if changes to a BPN have caused an error. |

### Utterance Pairs
The utterance pairs, consisting of an utterance from Eddie and the expected response(s) from Amelia, will be executed in the order they are defined.
> [!warning]  
>
> Only make conversations as long as they *need* to be. If your Amelia instance is setup to allow endless conversation, across multiple use-cases, it is best to make a separate test for each use-case.


| User Utterance |
| ----|
| The User question or statement to be said to Amelia.Note:;The first pair question should always be blank for the initial Amelia utterance |
| The compare operation to be made when evaluating Amelia's response to the;Expected AnswersMatches

Accepts regex patterns to match against the expected answer(s)
Equals
Tests for a string match, but does accept `*` on word boundaries.
Contains
Checks if Amelia's response contains the given word or phrase
Similar
Tests for similarity by checking Amelia's response against the given word/phrase for a jaccard index of 70% or above.
\| \| Accepts regex patterns to match against the expected answer(s) \| \| Tests for a string match, but does accept;`*` on word boundaries. \| \| Checks if Amelia's response contains the given word or phrase \| \| Tests for similarity by checking Amelia's response against the given word/phrase for a;jaccard index of 70% or above. \| \| Clicking the; to add an expected answer to test for from Amelia. Each user utterance can have multiple expected answers. The expected answers can be string matches or regex patterns depending on the operation selected above. Only one of the expected answers need to match for the QA pair to be considered passing. \| \| Set if the defined;operation should be negated when testing (i.e., consider the opposite of the operation a success).  
<u>Example:</u>  
Setting negate to `true` for an `equals` operation for the expected answer `Hello there` will consider the response `General Kenobi` a success. \| \| The number of seconds to wait before a response is considered timed out.
Note:;if a response times out all following utterance pairs will be marked failed and the test will be completed.
\|
### Selector <span class="small">LOAD ONLY</span>
The selector option is used to define in what order the load test will execute use cases. This option is required but only takes effect if more than one conversation is defined.

| Ordered |
| ----|
| Conversation execute in the order they were defined in a loop. |
| Conversation execute in a weighted random order. |

### Max chats <span class="small">LOAD ONLY</span>
The number of conversations that will be executed during the load test.
### Ramp Config <span class="small">LOAD ONLY</span>
Ramp configuration allow for controlled increase and decrease of load over time.

| Concurrent Chats |
| ----|
| The target number of concurrent chats for the ramp configuration. The is the value Eddie will attempt to reach during the ramp periods. |
| The number of chats that will be added or removed during the period. |
| The amount of ms/sec/min paused until the next ramp is executed. |
| The unit of time that will be used in the ramp periods.MillisecondSeconddefaultMinute |

## Exporting a test
Exporting a test to a replay or load file will ensure that you can quickly and easily rerun and update tests when needed.
1.  First, fill out the test creation form using the quick-start instructions.
2.  After the test information has been filled in, click the  button on the form. This will prompt you to save the replay/load file to your hard drive.
## Importing a test
You can import a replay or load file into the UI for modification, or launch the imported file to be tested immediately
1.  Click `Create Test` from the navigation menu
2.  Then click the  button on the test creation page
3.  Click , navigate to the desired replay file, and \[open\]
4.  Next you have two possible options:
    1.  If you want to edit, update, or just look at the test's contents, click the  button. This will import the contents of the replay file into the test creation form
    2.  If you would like to immediate launch a test from the replay file, click the  button. This will queue a new test to be run based on the contents of the replay file.
# Dashboard
The dashboard gives a quick overview of the most recently run tests. Each test listed is linked to a detailed view, if the summary isn't enough. On the dashboard there are two lists - one for the running or completed replay tests and another for the load tests.
## Recent Tests
At the top level of the dashboard, is a list of the most recent tests load run within Eddie. This list broken out into several columns:

| ID |
| ----|
| The unique ID assigned to the test. (Multiple tests can have the same name, but each test will always have a unique ID) |
| The name of give to a test. Although you can give multiple tests the same name, it is;highly recommended that you give each test a uniquely identifiable name. |
| One-Shot

Test has only one conversation
Multi-test
Test has multiple conversations
\| \| Test has only one conversation \| \| Test has multiple conversations \| \|
|          |                                                                                                                                                                                    |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Finished | The test has finished running                                                                                                                                                      |
| Running  | The test is currently running. This status will display how many conversations have been tested out of the total number of conversations in the test (e.g.,;*Running (10 of 20)*). |
\| \| The test has finished running \| \| The test is currently running. This status will display how many conversations have been tested out of the total number of conversations in the test (e.g.,;*Running (10 of 20)*). \| \| Whether the test passed/failed and the score percentage. \| \| The name of the client associated with the instance URL used (administrators can register clients in Eddie) \| \| The instance URL against which the test was run \| \| The user who created the test \|
## Recent Load Tests
At the top level of the dashboard, is a list of the most recent load tests run within Eddie. This list broken out into several columns:
> [!info]  
>
> Only users with elevated privileges to create load tests will see the list of completed/running load tests.


| ID |
| ----|
| The unique ID assigned to the test. (Multiple tests can have the same name, but each test will always have a unique ID) |
| The name of give to a test. Although you can give multiple tests the same name, it is;highly recommended that you give each test a uniquely identifiable name. |
| Finished

The test has finished running
Running
The test is currently running
Hung/Failed
The test has exceed the maximum timeout and did not finish correctly. This can happen when the Amelia instance fails in the middle of a load test.
\| \| The test has finished running \| \| The test is currently running \| \| The test has exceed the maximum timeout and did not finish correctly. This can happen when the Amelia instance fails in the middle of a load test. \| \| How many tests have been completed in the load test so far. \| \| The name of the client associated with the instance URL used (administrators can register clients in Eddie) \| \| The instance URL against which the test was run \| \| The user who created the test \|
## Test Details
> [!info]  
>
> To view details of a test, click the test's ID link from the dashboard list

On a test's details page, you can see information about the Amelia instance tested against, when the test was run, it's overall score, and detailed list of each conversation tested. To view details on the utterance pairs tested, click on a conversation in the list - this will expand to reveal the user utterance, the expected answer, Amelia's actual answer, whether the utterance pair passed, and other information.
If a conversation failed, a red error box will appear underneath the failed conversation in the list. Click on the conversation to find where the conversation failed.
