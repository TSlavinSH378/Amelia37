Response pools are batches of sentences, from which Amelia randomly selects for specific purposes. To greet users, for example, there might be a greeting response pool with many possible statements. Amelia would select a greeting for the start of each interaction. If Amelia cannot find an expected response at the domain level, she will look at the global response pool.
Response groups are created first to organize response pools. When a response group and a pool are created, response pool entries can be created to provide possible responses for Amelia.
Responses can be deleted.
# Dialog Acts and Sentence Types
Amelia's responses are determined by the type of dialog and sentences she processes in a conversation.
## Dialog Acts
Sentences processed by Amelia are classified into one of a set of dialog acts. Dialog acts describe the function of exchanges in a conversation. A "thank you," for example, is usually followed by "you're welcome" or similar dialog. If one person asks a question to seek information the response should provide information. If one person apologizes, the other person should accept, reject, or otherwise acknowledge the apology.
Dialog acts used in Amelia are focused on social obligation management. They are currently used solely with response pools to provide pre-packaged responses for certain inputs from the user.
-   Agreement – any positive acknowledgement or positives responses to yes/no questions ("Yes", "Sounds good", "Perfect", "Please do")
-   Apology – apologies ("Sorry", "I apologize", "My mistake")
-   Auto feedback negative – user doesn't understand Amelia ("I don't understand")
-   Closing – goodbyes ("See you later", "Have a nice day", "Goodnight")
-   Disagreement – any negative response to a yes/no question ("Nope", "No way")
-   Downplay – responses to apologies ("No problem", "It was nothing", "Don't worry about it")
-   Greeting – hello/salutation ("Hi", "Hello there", "Good morning")
-   Pause – pause the conversation ("Hold on", "One minute while I check on that")
-   Resume – resume the conversation ("Okay I'm back", "Go ahead")
-   Thanking – a thank you ("Thanks so much", "I appreciate it")
-   Thanking Reply – response to a thanking ("You're welcome")
-   Other – sentence without an explicit social obligation
Amelia's dialog acts are based originally on the work of Harry Bunt and colleagues but adapted for response pools. See <http://lrec-conf.org/proceedings/lrec2010/pdf/560_Paper.pdf> for details.
## Sentence Types
Every sentence Amelia processes is classified into one of three types:
-   **Interrogative** - questions or certain imperatives asking Amelia to provide information
-   **Imperative** - any statement telling Amelia to do something
-   **Declarative** - any sentence that is not an Interrogative or Imperative, typically when the user is providing information to Amelia
These types are used in combination with rule-based heuristics in many places in Amelia to determine how she should respond. For example, sentences classified as **Interrogative** elicit an "I don't know"-type of response if they are not understood by Amelia. In contrast, a **Declarative** will sentence will cause Amelia to acknowledge the user's information ("I understand", or "Got it.").
There are some exceptions to these rules. For example, there is logic to avoid acknowledging sentences that don't provide intelligible information. Single-sentence utterances without verbs that are not answers to Yes/No questions are currently responded to with "I don't know" even if they are declarative, though this logic is subject to change.
These labels are also used in various subsystems and responders in Amelia to help her determine how and if she should generate a response. For example, BPNs provide an option to allow other subsystems to respond to a user reply to an Ask task.
# Create Response Groups
Response pool groups organize response pools with one or more entries in a response pool. Tags can be used to organize response pool entries to provide responses in a conversation with Amelia. BPN Script tasks can be used to enable or activate tags to create a profile for the current conversation, for example, tags called Voice or Web to organize response entries by media.
> [!warning]  
>
> Amelia’s AIML documents use the response pool group code and response pool code. BPN Script tasks use tag names attached to response pool entries.

If creating a new response pool group, in Amelia’s administration pages click the Amelia Trainer links on the left side, then click the Response Pools link, and then click the Response Groups link. The New Response Group page will appear.
![](attachments/11939698/25461612.png)
Figure. Response Pool Group Details Page
Table. Response Pool Group Details Page Elements

| Element | Description |
| ----|----|
| Code | Type a unique code to identify the group and use in the template section of an AIML document. |
| Domain | Click to select the domain where this response group will be active. |
| Description | Type a short description of the response pool. Required for Groups. Optional for Response Pools |

# Create Response Pools
If creating a new response pool, in Amelia’s administration pages click the Amelia Trainer link on the left side, then click the Response Pools link, and then click the nested Response Pools link. The Response Pools page appears with a list of response pools. Click the New Response Pool button to create a new pool. The New Response Pool page appears.
![](attachments/11939698/25461613.png)
Figure. New Response Pool Page
Table. New Response Pool Page Elements

| Element | Description |
| ----|----|
| Response Pool Group Code | Click the dropdown arrow to select an existing group. The group code and pool code are used to reference a response pool in the template section of an AIML document. |
| Code | Type a unique code to identify this response pool. The pool code and group code are used to reference a response pool in the template section of an AIML document. |
| Description | Optional. Type a short description of the response pool. |

# Create Response Pool Entry and Tags
The last step to configure response pools, groups, and tags is to add or update an entry in a response pool. For a selected response pool in the Response Pools list page, click the Notebook icon to edit a response pool.
![](attachments/11939698/25461614.png)
Figure. Response Pool Detail Page
Click the New Response Pool Entry button to display a blank Response Pool Entry page. Complete the form and add one or more appropriate tags or update an existing entry.
![](attachments/11939698/25461615.png)
Figure. Response Pool Entry Page
Table. Response Pool Entry Page Elements

| Element | Description |
| ----|----|
| Response Pool | The response pool name for the entry. |
| Question/Template | Add a question or prompt for the entry. |
| Locale | If needed, select the language locale. |
| Tags | Click and type a new tag name or click the dropdown arrow to select existing tags. An entry can have more than one tag, if appropriate. |

> [!warning]  
>
> The Question/Template field in the response pool entry page can include variables in ${variableName} format. Variables are created then set with a Script task in a BPN process for a current conversation. This syntax is new as of version 3.7.3 when the scripting language was changed to JEXL from SpEL.

# Annotate Response Pool Entries
Response pool entries can be annotated with HTML and speech modifications, for example, presenting chat text in bold or speaking words more slowly. In the Response Pool Entry popup, highlight a word or phrase the right mouse click over the selection to display the Annotation Editor popup with Styling and Speech tabs.
![](attachments/11939698/25462088.png)
Figure. Annotation Editor for a Response Pool Entry
# Annotation Editor Interfaces
The annotation editor includes a Styling tab and Speech tab.
## Styling Tab
The Styling tab controls the visual display of Amelia's chat utterances.
### Text Styles
![](attachments/11940946/11942763.png)
Figure. Styling Tab for Selected Text
Table. Styling Tab Elements for Selected Text
|                             |                                                                                                                                                                                                           |                              |
|----------|-----------------------------------------------|---------------|
| Styling Element             | Description                                                                                                                                                                                               | Single or Multiple Select    |
| **Top Row Buttons**         |                                                                                                                                                                                                           |                              |
| B                           | Apply bold/strong style                                                                                                                                                                                   | Multiple selections possible |
| I                           | Apply italics style                                                                                                                                                                                       |                              |
| U                           | Apply underscore style                                                                                                                                                                                    |                              |
| Strikethrough               | Apply strikethrough style                                                                                                                                                                                 |                              |
| M                           | Apply markup style                                                                                                                                                                                        |                              |
| **Top Row Drop Down Lists** |                                                                                                                                                                                                           |                              |
| Heading Level               |                                                                                                                                                                                                           | Single selection only        |
| H1                          | Apply Heading 1 style                                                                                                                                                                                     |                              |
| H2                          | Apply Heading 2 style                                                                                                                                                                                     |                              |
| H3                          | Apply Heading 3 style                                                                                                                                                                                     |                              |
| H4                          | Apply Heading 4 style                                                                                                                                                                                     |                              |
| H5                          | Apply Heading 5 style                                                                                                                                                                                     |                              |
| H6                          | Apply Heading 6 style                                                                                                                                                                                     |                              |
| Vertical Position           |                                                                                                                                                                                                           | Single selection only        |
| Subscript                   | Apply subscript style                                                                                                                                                                                     |                              |
| Superscript                 | Apply superscript style                                                                                                                                                                                   |                              |
| **Text Fields**             |                                                                                                                                                                                                           |                              |
| Abbreviation                | For abbreviations, type the full definition or phrase. The abbreviation will appear in the chat interface with a double underline. Hovering over the abbreviation displays the full definition or phrase. | N/A                          |
| Link                        | Type a URL with the http or https protocol. The text will be bold in the chat interface. Clicking the text replaces the chat interface with the website URL.                                              | N/A                          |
### HR and BR Styles
Horizontal rule and single line breaks can be added to an annotation. Click the cursor after a space then right mouse click to display the annotation editor with two options, HR and BR.
![](attachments/11940946/11942827.png)
Figure. Styling Tab for BR and HR Styles
Table. Styling Tab Elements for BR and HR Styles

| Styling Element | Description |
| ----|----|
| HR | Insert a horizontal rule where cursor is placed |
| BR | Insert a single line break where cursor is placed |

## Speech Tab
The Speech tab controls how Amelia speaks an utterance when in a conversation. Click the Speech tab to display then hover the mouse over the first two entries, Volume and Rate, and scroll the mouse to display all settings.
![](attachments/11940946/11942769.png)
Figure. Speech Tab
Table. Speech Tab Elements (SAPI Standard)

| Annotation | Type | Description | Attributes |
| ----|----|----|----|
| E | Voice state control | The Emph tag instructs the voice to emphasize a word or section of text. The Emph tag cannot be empty.  | NA |
| S | Voice state control | The Spell tag forces the voice to spell out all text, rather than using its default word and sentence breaking rules, normalization rules, and so forth. All characters should be expanded to corresponding words (including punctuation, numbers, and so forth). The Spell tag cannot be empty. | NA |
| Volume | Voice state control | The Volume tag controls the volume of a voice. The tag can be empty, in which case it applies to all subsequent text, or it can have content, in which case it only applies to that content. | The Volume tag has one required attribute: Level. The value of this attribute should be an integer between 0 and 100. Values outside of this range will be truncated. |
| Rate | Voice state control | The Rate tag controls the rate of a voice. The tag can be empty, in which case it applies to all subsequent text, or it can have content, in which case it only applies to that content. | The Rate tag has two attributes, Speed and AbsSpeed, one of which must be present. The value of both of these attributes should be an integer between -10 and 10. Values outside of this range may be truncated by the engine (but are not truncated by SAPI). The AbsSpeed attribute controls the absolute rate of the voice, so a value of 10 always corresponds to a value of 10, a value of 5 always corresponds to a value of 5.The Speed attribute controls the relative rate of the voice. The absolute value is found by adding each Speed to the current absolute value. |
| Pitch | Voice state control | The Pitch tag controls the pitch of a voice. The tag can be empty, in which case it applies to all subsequent text, or it can have content, in which case it only applies to that content. | The Pitch tag has two attributes, Middle and AbsMiddle, one of which must be present. The value of both of these attributes should be an integer between -10 and 10. Values outside of this range may be truncated by the engine (but are not truncated by SAPI).The AbsMiddle attribute controls the absolute pitch of the voice, so a value of 10 always corresponds to a value of 10, a value of 5 always corresponds to a value of 5.The Middle attribute controls the relative pitch of the voice. The absolute value is found by adding each Middle to the current absolute value |
| Emph | Voice state control | The Emph tag instructs the voice to emphasize a word or section of text. The Emph tag cannot be empty.  | NA |
| Spell | Voice state control | The Spell tag forces the voice to spell out all text, rather than using its default word and sentence breaking rules, normalization rules, and so forth. All characters should be expanded to corresponding words (including punctuation, numbers, and so forth). The Spell tag cannot be empty. | NA |
| Silence | Direct item insertion tags | The Silence tag inserts a specified number of milliseconds of silence into the output audio stream. This tag must be empty, and must have one attribute, Msec. | Msec |
| Pron | Direct item insertion tags | The Pron tag inserts a specified pronunciation. The voice will process the sequence of phonemes exactly as they are specified. This tag can be empty, or it can have content. If it does have content, it will be interpreted as providing the pronunciation for the enclosed text. That is, the enclosed text will not be processed as it normally would be. | The Pron tag has one attribute, Sym, whose value is a string of white space separated phonemes. |
| Bookmark | Direct item insertion tags | The Bookmark tag inserts a bookmark event into the output audio stream. Use this event to signal the application when the audio corresponding to the text at the Bookmark tag has been reached. The Bookmark tag must be empty. | The Bookmark tag has one attribute, Mark, whose value is a string. This value can then be used to differentiate between bookmark events (each of which will contain the string value from their corresponding tag). |
| PartOfSp | Voice context control tags | The PartOfSp tag provides the voice with the part of speech of the enclosed word(s). Use this tag to enable the voice to pronounce a word with multiple pronunciations correctly depending on its part of speech. The PartOfSp tag cannot be empty. | The PartOfSp tag has one attribute, Part, which takes a string corresponding to a SAPI part of speech as its attribute. Only SAPI defined parts of speech are supported - "Unknown", "Noun", "Verb", "Modifier", "Function", "Interjection". |
| Context | Voice context control tags | The Context tag provides the voice with information which the voice may then use to determine how to normalize special items, like dates, numbers, and currency. Use this tag to enable the voice to distinguish between confusable date formats (see the example, below). The Context tag cannot be empty. | The Context tag has one attribute, Id, which takes a string corresponding to the context of the enclosed text. Several contexts are defined by SAPI and are more likely to be recognized by SAPI compliant voices, but any string may be used. See documentation for a particular voice for more details. |
| Voice | Voice Selection Tags | The tag can be empty, in which case it changes the voice for all subsequent text, or it can have content, in which case it only changes the voice for that content. | The Voice tag selects a voice based on its attributes, Age, Gender, Language, Name, Vendor, and VendorPreferred. |
| Lang | Voice Selection Tags | The Lang tag selects a voice based solely on its Language attribute. The tag can be empty, in which case it changes the voice for all subsequent text; or it can have content, in which case it only changes the voice for that content. | The Lang tag has one attribute, LangId. This attribute should be a LANGID, such as 409 (U.S. English) or 411 (Japanese). Note that these numbers are hexadecimal, but without the typical "0x". |

# Use Dynamic Content in Response Pools
Amelia uses Artificial Intelligence Markup Language (AIML) files to chit chat with people, for example, if someone asks Amelia about her favorite movie.
Changes in Amelia 3.7 expand the use and flexibility of her AIML responder by connecting AIML documents to response pools with the ability to pass dynamically created values to include in Amelia’s responses.
-   Response pool entries can be tagged with a value to organize entries and call the entries from a BPN Script task.
-   BPN Script tasks can use the new responsePoolService to manage profile tags used by response pool entries for the current conversation.
-   Entries for a response pool can reference tags enabled or activated with a BPN Script task, for example, tags called Voice or Web to organize response entries by media.
-   AIML documents can use response pool entry tags in their template section to reference default and custom response pool groups and pools.
-   Response pool entries can include data captured in a BPN process and stored as variables.
A default set of AIML and Response Pools are available in the Global domain. Custom AIML files and Response Pools also can be created in any domain. These files are available in Amelia’s administration pages by clicking the Amelia Trainer link on the left side then clicking the AIML link.
Response Groups also can be created in both Global and other domains, for example, to organize response pools and avoid potential name clashes with identical response pool names.
To demonstrate the flexibility of Amelia’s AIML responder, the first steps are to create or use pre-existing response pool groups then configure response pools and entries.
## AIML Template Section
Amelia stores default AIML documents in the Global domain. Custom AIML documents can be created and uploaded to a domain or the Global domain. Documents are available in the Amelia administration pages by clicking the Amelia Trainer link on the left side then the AIML link. The Import page displays a list of existing files available for the current domain. Click the folder icon to upload custom AIML documents or click the pencil icon to the right of a file listing to edit.
Once response pool groups and response pools exist with entries tagged, response pools can be referenced in AIML documents in a template section nested within a category section.
``` groovy
<category>
    <pattern></pattern>
    <template>rp:use(RESPONSE_POOL_GROUP_CODE:RESPONSE_POOL_CODE)</template>
</category>
```
The `rp` namespace calls the use() method and passes the response pool group code value and the response pool code value separated by a single colon. The pattern section contains a string of characters used to match one or more user inputs in a conversation.
## BPN Script Task Profile Tags
Once response pool groups and response pools exist with their entries tagged, a BPN Script task can use responsePoolService to enable or disable the use of response pool entry tags in a current conversation. The service can configure Amelia to pull responses from the appropriately tagged response pool entries through her AIML subsystem responder.
Four responsePoolService methods are available with the 3.7.x release.
### responsePoolService Methods
#### activateProfile
    ResponsePoolProfileBuilder activateProfile(String... tags)
Entry point for activating a response pool profile for the current conversation. The returned *ResponsePoolProfileBuilder* instance provides a fluent interface for configuring the profile.
**Example**
``` text
responsePoolService.activateProfile('tag1', 'tag2')
       .lenient(true)
       .exactMatch()
```

| Parameter | Description |
| ----|----|
| tags | Response pool entry tag names. |

#### activeProfile
    String[] activeProfile()
tags = responsePoolService.activeProfile()
Returns an array of active response pool entry tags.
#### clearProfile
    void clearProfile()
responsePoolService.clearProfile()
Deactivates all response pool entry tags for the conversation.
#### getResponsePool
    String getResponsePool(String groupCode, String responsePoolCode)
Obtains a response pool evaluated template by response pool group code and response pool code.

| Parameter | Description |
| ----|----|
| groupCode | A response pool group code. |
| responsePoolCode | A response pool code. |

#### isTagActive
    boolean isTagActive(String tag)
Checks whether the profile contains the tag.

| Parameter | Description |
| ----|----|
| tag | Response pool tag to be matched. |

#### isTagNotActive
    boolean isTagNotActive(String tag)
Checks whether the profile does not contain the tag.

| Parameter | Description |
| ----|----|
| tag | Response pool tag to be matched. |

#### areAllTagsActive
    boolean areAllTagActive(String... tags)
Checks whether the profile contains all the tags.

| Parameter | Description |
| ----|----|
| tags | Response pool tags to be matched. |

#### isAnyTagActive
    boolean isAnyTagActive(String... tags)
Checks whether the profile contains any of the tags.

| Parameter | Description |
| ----|----|
| tags | Response pool tags to be matched. |

#### activeTags
    String[] activeTags()
Returns an array of active profile tags.
#### ResponsePoolTagMatchingOperator
Enumeration of the possible response pool tag matching operators.
-   **EXACT** - The set of tags specified in the profile is exactly the same as the tags in the response pool entry (bijective).
-   **ALL** - All tags in the profile have a counterpart in the set of tags of the response pool entry.
-   **ANY** - If at least one tag in the profile matches a tag in the response pool entry.
#### ResponsePoolProfile
Holds response pool profile properties. Read-only.
-   **tags : String\[\]** - Tags associated with the profile.
-   **tagMatchingOperator : ResponsePoolTagMatchingOperator** - Tag matching operator.
-   **lenient : boolean** - Whether the response pool search should allow for untagged entries to be picked up.
#### ResponsePoolProfileBuilder
Builder returned by the *activateProfile(String... tags)* method. Allows for fluent profile configuration. Exposes the following operations:
-   **lenient(boolean lenient) : ResponsePoolProfileBuilder** - Allows the search for response pool entries to pick untagged entries, if no entries result from tag matching. Default value: *false*.
-   **exactMatch() : void** - Selects only the response pool entries whose set of tags is identical to the set of tags in the profile.
-   **anyMatch() : void** - Selects only the response pool entries from which at least one tag intersects with the tags in the profile.
-   **allMatch() : void** - Selects only the response pool entries whose tags include all tags in the profile.
### responsePoolService Examples
#### Activate two tags
``` groovy
responsePoolService.activateProfile('tag1', 'tag2')
    .allMatch()
```
#### Deactivate all tags
``` groovy
responsePoolService.clearProfile()
```
#### Activate a tag and disable lenient search
``` groovy
responsePoolService.configureProfile('tag3')
    .lenient(true)
    .allMatch()
```
#### Get all active tags
``` groovy
def activeProfile = responsePoolService.activeProfile()
if (null != activeProfile) { // If the response pool profile was activated
    def tags = activeProfile.tags()
}
```
or
``` groovy
def tags = responsePoolService.activeTags()
```
# Import and Export Response Pools
Response pools and entries also can be imported and exported from within the Response Groups and Response Pools workspaces, available by clicking the Amelia Trainer link on the left side of Amelia’s administration pages then clicking Response Pools link and either the Response Pools link or Response Groups.
![](attachments/11939698/25461616.png)
Figure. Import and Export Response Pool Buttons
Files are imported and exported in XML format, as shown in this example, with a defined structure.
Table. Response Pool XML File Elements

| Element | Description |
| ----|----|
| id | When entries are imported, Amelia checks the ID to avoid duplication. Value is created dynamically. |
| locale | Local string, for example, en_US for English/US |
| sequence | Fixes the priority order in which entries are picked from the pool of responses. |
| template | A Spring Expression Language template used to generate the response sentence. |

``` groovy
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<responsePools xmlns="http://www.ipsoft.com/amelia/response-pool/1.0.0">
    <group id="15cf1ca5-a5c5-48b8-9818-086a5f26d36a" domain="global" code="SOCIAL_TALK" description="Social talk generation" internal="true">
        <responsePool id="7e29fcec-f1b1-4784-a85e-54655d657044" code="ADDRESS">
            <entry id="2286478a-ed84-4a5e-afbd-e1bb195e1c9d" locale="en_US" sequence="1">
                <template>17 State street, New York City, New York.</template>
            </entry>
            <entry id="5958236b-93db-455d-871c-f9ef37406560" locale="en_US" sequence="2">
                <template>IPsoft, Manhattan, New York.</template>
            </entry>
        </responsePool>
        <responsePool id="04280bd3-f81f-427f-8a5b-d01e585b375c" code="AGE">
            <entry id="af61fd43-f659-4ed8-8dbe-95f907dd8453" locale="en_US" sequence="1">
                <template>Sorry. That's too inappropriate for this conversation.</template>
            </entry>
            <entry id="d39544e5-1331-4e12-ac85-1a502d35c33e" locale="en_US" sequence="2">
                <template>That is too personal.</template>
            </entry>
        </responsePool>
        <responsePool id="3b06281b-1e7d-431f-abc0-3c654d3ba8a6" code="ARE_YOU_COGNITIVE">
            <entry id="f528be28-8e89-4b9c-ad9f-a0def7c0ccda" locale="en_US" sequence="1">
                <template>Yes. It's a state of mind.</template>
            </entry>
            <entry id="7a395aff-3e16-41de-a6ca-b05fcc5ce230" locale="en_US" sequence="2">
                <template>Yes, I am.</template>
            </entry>
            <entry id="4145d7ca-aa23-4a5f-87bd-6b72c82dc918" locale="en_US" sequence="3">
                <template>Yes, I am. It's a good feeling.</template>
            </entry>
        </responsePool>
        <responsePool id="a81afac9-2d54-4364-853b-b0a3f9f38be9" code="ARE_YOU_DUMB">
            <entry id="af515fbd-2782-4e10-8ab2-8af1fa389848" locale="en_US" sequence="1">
                <template>No. I'm constantly learning. In fact my brain was built to constantly evolve and improve.</template>
            </entry>
            <entry id="85648b90-91e0-49e1-ad4b-1e1e263efaa8" locale="en_US" sequence="2">
                <template>I wouldn't say that. I am constantly learning and improving.</template>
            </entry>
            <entry id="1e30a486-be1d-4653-85be-8b7798bbfc82" locale="en_US" sequence="3">
                <template>No. I'm a life long learner.</template>
            </entry>
        </responsePool>
    </group>
</responsePools>
```
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-10-4_13-18-22.png](attachments/11939698/25461612.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-4_13-18-54.png](attachments/11939698/25461613.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-4_13-19-23.png](attachments/11939698/25461614.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-4_13-19-48.png](attachments/11939698/25461615.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-19_16-7-40.png](attachments/11939698/25461616.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-21_16-43-36.png](attachments/11939698/25462088.png) (image/png)  
