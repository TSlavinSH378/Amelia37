-   [Types of Grammars](#Grammars-TypesofGrammars)
-   [Grammar Workspace](#Grammars-GrammarWorkspace)
-   [Create Grammars](#Grammars-CreateGrammars)
-   [Import Grammars](#Grammars-ImportGrammars)
    -   [File Format](#Grammars-FileFormat)
    -   [Upload Grammar Files](#Grammars-UploadGrammarFiles)
-   [Setup Intents and Entities](#Grammars-SetupIntentsandEntities)
    -   [Manual Setup](#Grammars-ManualSetup)
        -   [Intents](#Grammars-Intents)
        -   [Entities](#Grammars-Entities)
    -   [Automatic Creation of Intents and Entities](#Grammars-AutomaticCreationofIntentsandEntities)
-   [Edit Grammars](#Grammars-EditGrammars)
-   [Export Grammars](#Grammars-ExportGrammars)
-   [Parser Behavior for Unknown Words/Tokens](#Grammars-ParserBehaviorforUnknownWords/Tokens)
-   [Grammar Notation](#Grammars-GrammarNotation)
    -   [Notation Basics](#Grammars-NotationBasics)
        -   [Reserved Key Words](#Grammars-ReservedKeyWords)
        -   [Dropped Symbols](#Grammars-DroppedSymbols)
        -   [Contractions](#Grammars-Contractions)
        -   [Macros and Repetitions](#Grammars-MacrosandRepetitions)
        -   [Global Macros](#Grammars-GlobalMacros)
        -   [Non-terminals](#Grammars-Non-terminals)
        -   [Pre-terminals](#Grammars-Pre-terminals)
        -   [Negation Syntax](#Grammars-NegationSyntax)
        -   [Attributes](#Grammars-Attributes)
        -   [Goal Priorities](#Grammars-GoalPriorities)
        -   [Multi-choice Slots with Variations](#Grammars-Multi-choiceSlotswithVariations)
    -   [Regular Expressions](#Grammars-RegularExpressions)
        -   [Working with Regex and Reserved Keywords](#Grammars-WorkingwithRegexandReservedKeywords)
        -   [Predefined Regular Expression Patterns](#Grammars-PredefinedRegularExpressionPatterns)
        -   [Example of Reusing Predefined Regexes and Generic Grammars](#Grammars-ExampleofReusingPredefinedRegexesandGenericGrammars)
    -   [Grammar Notation Best Practices](#Grammars-GrammarNotationBestPractices)
        -   [Use Natural Speech](#Grammars-UseNaturalSpeech)
        -   [Work with Regex and Reserved Keywords](#Grammars-WorkwithRegexandReservedKeywords)
        -   [Use Logical Negations](#Grammars-UseLogicalNegations)
        -   [Group with Pre-terminals](#Grammars-GroupwithPre-terminals)
        -   [Use Grammars for Inferences](#Grammars-UseGrammarsforInferences)
        -   [Avoid Useless Definitions](#Grammars-AvoidUselessDefinitions)
        -   [Avoid Not Restricting $ANY_ALL](#Grammars-AvoidNotRestricting$ANY_ALL)
Grammars are sets of rewriting rules that represent Natural Language patterns concisely, for example, the unconstructed casual way people talk. Grammars help Amelia use natural language to recognize the user’s goal intent (Intents) and data (Entities) needed to address their intent.
Business Process Networks (BPNs) use grammars to help provide Amelia with structure to follow processes, not only the rote question and answer structure of FAQs but also more complex processes with multiple paths and outcomes.
Amelia can capture and understand hundreds of thousands of user utterances by combining grammars into patterns that represent semantics constructs and meanings. These semantics constructs are represented by grammars are called Language Units and they can be of intent or entity type.
Some examples to show how Amelia uses language units to understand Natural Language:
-   I want to reserve a hotel in Paris from 10/10/2018 to 10/20/2018.
**\[Goal\].**hotelReservation
**\[NearLocation\].\[Location\].**Paris
**\[FromDate\].\[Date\].**10/10/2018
**\[ToDate\].\[Date\].**10/20/2018
-   I want to check the status of my bill.
**\[Goal\].**checkBillStatus
-   I want to check the status of bill \# ABC987134
**\[Goal\]**.checkBillStatus
**\[BillNumber\]**.ABC987134
Grammars use natural language, special notation, and regular expressions to define language units for Amelia to process and use. They provide an extremely precise method to extract intents and entities because they rely on rules rather than quality and amount of training data.
In Amelia V3, grammars are significantly improved. Grammars exported from Amelia V2 to Amelia V3 can be used with minimal issues.
# Types of Grammars
Grammars help Amelia determine user intent. They're written in natural language with the help of notation, keywords, regular expressions, and pre-defined elements.
Amelia works with goal and slot grammars:
-   **Goal grammars** define user intent, often with reference to expected data and utterances required to meet the intent and goal. "I lost my hotel bill. Can you send me a copy?" is an example of a goal grammar utterance.
-   **Slot grammars** define data needed to meet a goal. The most common slot grammars are used to fill in information, for example, to retrieve and send a hotel bill, slots might include the name of the hotel, dates of a stay, and an email address.
# Grammar Workspace
Amelia's administration interface includes a workspace to import and export grammars. Select the Amelia Trainer link to display then click the Grammars link.
![](attachments/11939678/11939681.jpg)
Figure. Grammars Workspace
Click the Revision History icon to display a popup with the history of a selected grammar.
![](attachments/11939678/11939685.png)
Figure. Grammar Revision History Popup
# Create Grammars
Click the Create new Grammar button at the top right of the Grammars workspace to create a new grammar. The Add Grammar workspace appears.
![](attachments/11939678/11941067.png)
Figure. The Create new Grammar Button
![](attachments/11939678/11941068.png)
Figure. Add Grammar Workspace
# Import Grammars
For Amelia to associate the contents of a grammar file with utterances, grammar files must be structured in XML format then connected with related intents and entities. While grammar files can be imported in the Amelia V2 format, the import process converts the files into the current V3 format.
## File Format
Grammar files are in XML format with file names less than 128 characters and use only letter, number, hyphen, and underscore characters. The \<grammar\>\</grammar\> section can be edited in the Grammars workspace. In this example, slotfood is the terminal name for the grammar. A sample file slotfood_text.xml can be downloaded [here](attachments/11939678/11939689.xml).
``` groovy
<grammars domain="Test">
  <grammar type="SLOT" name="meal">[slotfood]
                (pizza)
            ;
   </grammar>
</grammars>
```
Table. Grammar XML File Structure

| Element | Description |
| ----|----|
| type | SLOT or GOAL. GOAL creates intents. SLOT creates entities. |
| name | Name of the grammar |
| grammar | Use <![CDATA[ ...content here... ]]> to define the grammar content |
| [ intententityname ] | The intent (GOAL) or entity (SLOT) name is in square brackets immediately after the initial <grammar> tag definition. |

## Upload Grammar Files
To upload a grammar file, click the Upload button in the Import Grammar File box in the Grammar workspace. Then use the file explorer popup to navigate to a file and upload.
# Setup Intents and Entities
Grammars are connected to intents and entities either manually or automatically with the New Entity tab in the Entity workspace and the New Intent tab in the Intent workspace.
## Manual Setup
Each grammar file can be connected to an entity and intent.
### Intents
For intents, use the Select intent grammar dropdown at the bottom of the add or edit intent form.
![](attachments/11939678/11939680.png)
Figure. Grammar Connection on Intent Form
### Entities
For entities, click the New Entity tab in the Entity workspace to first create an entity with the CUSTOM_DATUM type.
1.  Type an entity code in the Code field.  
    > [!warning]  
    >
    > The entity code must be the same as the terminal name used in the selected grammar. In the XML code example above, the terminal name is slotfood.
2.  Select CUSTOM_DATUM from the Datum type dropdown list. The Custom Entity Settings form appears below.
3.  Select Grammars from the Custom entity type dropdown list.
4.  Select an option from the Extract/Normalization dropdown list. Select an option from the Fallback Strategy dropdown list.
5.  Select the grammar name from the Grammar dropdown list.
The grammar-related Custom Entity Settings options are described in a table below.
![](attachments/11939678/11939682.png)
Figure. Grammar Custom Entity Settings on Entity Form
Table. Grammar Custom Entity Settings
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 85%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Setting</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">Custom entity type</td>
<td class="confluenceTd">Specifies the general entity normalization/extraction approach. Options are Grammars or Tabular Data Lookup.</td>
</tr>
<tr class="even">
<td class="confluenceTd">Extract/Normalize</td>
<td class="confluenceTd"><p>Specifies whether to normalize, extract, or perform both using a normalizer. For example, if using a trained entity tagger, the resulting spans can be normalized when using the Normalize Only option.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| Normalize | Only normalize the entity. Requires training an entity extractor. |
| Normalize and Extract | Extract and normalize results using a normalizer. |
| Extract Only | Use a lookup to extract values but do not perform normalization. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd">Rollback strategy</td>
<td class="confluenceTd"><p>Provides a default normalized value when an entity is extracted but cannot be normalized.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| None | Don&#39;t extract entities that cannot be normalized. |
| Provided | Use specified input as the fallback normalized value. |
| Original | Use the original un-normalized matched text. |</code></pre>
</div>
<p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">Grammar</td>
<td class="confluenceTd">Select a slot grammar to use to extract/normalize this entity.</td>
</tr>
</tbody>
</table>
## Automatic Creation of Intents and Entities
Entities and intents also can be connected with a grammar with the New Intent tab in the Intent workspace and New Entity tab in the Entity workspace. Both tabs display a slideout panel with an Import from Grammars button, located at the bottom of the panel. Clicking the Import from Grammars button will create a new intent and new entity configured to work with a selected grammar.
If this example grammar file were uploaded with the Grammars workspace, then:
-   Clicking the Import from Grammars button in the Add Intents tab in the Intents workspace, the goal grammar would create an intent with the name billDiscrepancy
-   Clicking the Import from Grammars button in the Add Entities tab in the Entities workspace, the slot grammar would create an entity with the name and code set to yesNoAlt.
``` groovy
<grammars domain="Test">
  <grammar type="GOAL" name="hotel_billing_discrepancy">[_billDiscrepancy]
                (i have a billing discrepancy)
                (i need to discuss *an ISSUE with *a billing SITUATION)
                (billing issue)
            ISSUE
                (problem)
                (refund)
                (credit)
            SITUATION
                (discrepancy)
                (issue)
                (over charge)
            ;</grammar>
  <grammar type="SLOT" name="yesNoAlt">[yesNoAlt]
                (yip)
            ;</grammar>
</grammars>
```
> [!warning]  
>
> The entity code and grammar terminal name must be synchronized manually if one or the other is changed after setup.
> [!warning]  
>
> If the grammar is defined as type=SLOT for the lu parameter, only an entity will be created automatically.

# Edit Grammars
Once a grammar is uploaded and listed in the Grammars box in the workspace, click the Notepad edit icon to the left of a grammar name to edit the file.
![](attachments/11939678/11939679.png)
Figure. Edit Grammar Form
# Export Grammars
In the Grammars workspace, click the Export button in the Export Grammar File box to download a single XML file of all grammars for the current domain. The exported file is in the V3 grammar format with the domain_name_grammar.xml as the file name, where domain_name is the name of the domain. For the example below, the file name would be Test_grammar.xml.
``` groovy
<grammars domain="Test">
  <grammar type="GOAL" name="hotel_billing_discrepancy">[_billDiscrepancy]
                (i have a billing discrepancy)
                (i need to discuss *an ISSUE with *a billing SITUATION)
                (billing issue)
            ISSUE
                (problem)
                (refund)
                (credit)
            SITUATION
                (discrepancy)
                (issue)
                (over charge)
            ;</grammar>
  <grammar type="SLOT" name="room_type_slot">[room_Type_Slot]
                ([_single])
                ([_double])
            ;
            [_single]
                (one bed)
                (king)
                (single)
                (single bed)
                (single room)
                (large bed)
            ;
            [_double]
                (two beds)
                (queen)
                (double)
                (double beds)
                (queen beds)
                (double room)
            ;</grammar>
  <grammar type="SLOT" name="new_york_tourist_spot">[newYorkTouristSpot]
                (brooklyn bridge)
                (battery park)
                (ellis island)
                (statue *of liberty)
                (museum *of natural history)
                (museum of modern art)
                (museum of $ANY $ANY)
                (central park)
                (*the highline)
                (times square)
                (broadway)
                (*the whitney *museum)
                (wall street)
            ;</grammar>
  <grammar type="SLOT" name="choice_of_food_type">[typeOfFoodChoice]
                (*mushroom pizza *pie)
                (salad)
                (bread)
                (hamburger)
            ;</grammar>
  <grammar type="GOAL" name="room_test">[_roomtest]
                (!>car)
                (!>table)
            ;</grammar>
  <grammar type="SLOT" name="yesNoAlt">[yesNoAlt]
                (yip)
            ;</grammar>
</grammars>
```
# Parser Behavior for Unknown Words/Tokens
For every space-separated token in the user utterance, the parser will check if the token either:
1.  Exists as a regular word used anywhere in any grammar files.
2.  Is matchable by a #define custom regex.
Any token that does not fulfill either of these two criteria will be ignored during preprocessing. Any unknown tokens or out-of-grammar tokens, symbolized by question marks in the table below, will not be read by the grammar parser. In practice, they will always match. See [Grammar Notation](#Grammars-GrammarNotation) below for the notation and matching logic used in these examples.
``` bash
#define roomNumber [0-9]{4}  # matches any 4-digit number.
[roomNumber]
       (my room number roomNumber)
;
[_reserveAHotel]
       (reserve a hotel)
;
```
Table. Grammar Parser Behavior for Unknown Words

| Original Utterance | Preprocessed Utterance | Result |
| ----|----|----|
| I want to reserve a hotel | ? ? ? reserve a hotel; (assuming 'i', 'want', 'to' do not exist in any other grammar files)  | MATCH |
| I want to reserve a great hotel | ? ? ? reserve a ? hotel ;(assuming  'i', 'want', 'to', 'great' do not exist in any grammar files) | MATCH |
| My room 123456 number is 1067 | my room ? number ? 1067 (assuming '123456', 'is', do not exist in any grammar files. '1067' matches #define roomNumber hence not ignored) | MATCH |
| My gigantic room number a 1067 | my ? room number a 1067 (assuming 'gigantic' undefined. 'a' is defined in grammar files in [_reserveAHotel] hence not ignored.) | NO MATCH |

Every grammar entry for a domain is concatenated as one big string to build the parser. As the grammar grows, the words dictionary gets bigger and that's when \*$ANY becomes necessary to ignore words that exist in the dictionary already.
Therefore, write patterns as explicitly as possible, especially goals grammars, and don't get limited to write all the patterns variations in one line.
This example is bad practice because the pattern ends up looking like a regular expression.
``` bash
[_reserveAHotel]
     (reserve *a *an *hotel [RoomType])
;
```
This example is good practice because the pattern has been split into two lines and use $ANY when possible.
``` bash
[_reserveAHotel]
     (reserve *$ANY hotel)
     (reserve *$ANY [RoomType])
;
```
# Grammar Notation
Grammar notation consist of two symbol types:
1.  **Terminal Symbols**– literal symbols which may appear in the outputs of the production rules of a formal grammar and which cannot be changed using the rules of the grammar.
2.  **Non-terminal symbols**– those symbols which can be replaced.
The notation and syntax used in grammars follow these rules:
Table. Grammar Syntax Rules, Definitions, and Examples

| Syntax Name | Definition | Example |
| ----|----|----|
| Terminals | Lower case strings |  |
| Non-Terminals | Calls to other grammars are enclosed in square brackets [ ] |  |
| Macros (Local) | Upper case strings | SOFTWARE |
| Macros (Global) | Wrapped in square brackets with @ symbol prefix | [ @software ] |
| * | 0 or 1 repetitions of the item |  |
| + | 1 or more repetitions of the item |  |

> [!info]  
>
> **NOTE:  
> **All grammar definitions must begin with a frame definition using \[ \] (square brackets) and end with a ; (semi-colon) on a new line. A grammar can include multiple frames.

## Notation Basics
### Reserved Key Words
In Lynx grammars, these reserved keywords are used in special cases:
Table. Grammar Reserved Key Words

| Reserved Keyword | Description |
| ----|----|
| #define regexKey regexPattern | Allows creation of custom regex patterns |
| $ANY | Matches any (space delimited) single token that is anywhere in the grammar |
| $ANY_ALL | Matches any tokens anywhere in the grammar, no matter how many, in what order, or whether divided by tokens that are not in the grammar |
| $PERSON | Matches any Person Named Entity, as defined by Stanford's Named Entity Recognizer (NER) |
| $ORG | Matches any Organization Named Entity, as defined by Stanford's Named Entity Recognizer (NER) |
| $LOCATION | Matches any Location Named Entity, as defined by Stanford's Named Entity Recognizer (NER) |

**  
**
**$ANY, $ANY_ALL Example**
In this example, we use $ANY to ignore stop-words (words that have no meaning by themselves, e.g., a, my, to, the).  Note: \*$ANY is also allowed to indicate that is optional.
``` bash
[_hotelReservation]
    (WANT $ANY reserve *$ANY hotel)    # Only matches if stopwords are listed in grammar, otherwise no match
    (WANT *to reserve *a hotel)        # Assuming the line above covers variations with "to" and "a", this line in the grammar is redundant, as it's more efficiently covered by the line above
    (WANT $ANY_ALL reserve *a suite)   # $ANY_ALL should only be used for loose patterns
    WANT
        (want)
        (need)
;                                      # Grammar is closed with a semicolon
```
**$PERSON, $ORG, $LOCATION Example**
This patterns can be used to match on person names, organizations and locations as recognized by the Stanford Named Entity Recognizer (NER) classifier.
``` bash
[PrefName]               # For the input: "Call me John Doe",
    (call me $PERSON)    # This pattern will yield: [PrefName].[Person].John Doe
;                        # Grammar is closed with a semicolon
```
``` bash
[WorksAt]                # For the input: "I work at IPsoft"
    (*i work at $ORG)    # This pattern will yield: [WorksAt].[Organization].IPsoft
;                        # Grammar is closed with a semicolon
```
``` bash
[NearLocation]           # For the input: "Find me places near NY."
    (near $LOCATION)     # This pattern will yield: [NearLocation].[Location].NY
;                        # Grammar is closed with a semicolon
```
### Dropped Symbols
These characters are stripped before processing grammars and, therefore, should not be used in writing grammars.
Table. Grammar Dropped Symbols

| Unicode/ASCII | Example | Name |
| ----|----|----|
| ASCII 0027 | ' | Single Quote |
| ASCII 0022 | " | Double Quotation Mark |
| \u201C | “ | Left Double Quotation Mark |
| \u201D | ” | Right Double Quotation Mark |
| \u2018 | ‘ | Left Single Quotation Mark |
| \u2019 | ’ | Right Single Quotation Mark |
| ASCII 0063 | ? | Question Mark |
| ASCII 007C | | | Vertical Line |
| ASCII 003B | ; | Semicolon |
| ASCII 0028 | ( | Left Parenthesis |
| ASCII 0029 | ) | Right Parenthesis |
| ASCII 005B | [ | Left Square Bracket |
| ASCII 005D | ] | Right Square Bracket |
| ASCII 002C | , | Comma |
| ASCII 003C | < | Less-Than Sign |
| ASCII 003E | > | Greater-Than Sign |
| ASCII 007B | { | Left Curly Bracket |
| ASCII 007D | } | Right Curly Bracket |

### Contractions
When dealing with contractions, use root words with the contracted letters separated by a space from other letters in the word. For example:
Table. Grammar Contractions Syntax
|                  |           |                     |          |
|------------------|-----------|---------------------|----------|
| With Apostrophes |           | Without Apostrophes |          |
| I can’t          | (i ca nt) | I cant              | (i cant) |
| I won’t          | (i wo nt) | I wont              | (i wont) |
> [!warning]  
>
> With contractions, the space does not go where the single quote was removed.

### Macros and Repetitions
Macros (uppercase strings) are regular rewrite rules that redefine a pattern inside a grammar definition. For example, in this example the slot grammars INSTALL and SOFTWARE are local macros used within the \_installSoftware goal grammar:
``` bash
[_installSoftware]            # "install a software" goal grammar
    (INSTALL *a SOFTWARE)     # INSTALL and SOFTWARE are macros (they start with uppercase)
INSTALL                       # Rewrite rule for INSTALL
    (install)
    (download)
    (setup)
SOFTWARE                      # Rewrite rule for SOFTWARE
    (software)
    (app)
    (application)
;
```
### Global Macros
However, if slot grammars SOFTWARE and INSTALL will be reused across multiple grammar definitions, create them as global macros. It might be useful to store global macros into a single grammar to make maintenance easier. Global macros are defined as individual grammar definition that start with @ symbol prefix:
``` bash
[_installSoftware]                   # "install a software" goal grammar
    ([@install] *a [@software])      # [@install] and [@software] are global macros refs (they start with @)
;
[_uninstallSoftware]                 # "install a software" goal grammar
    ([@uninstall] *a [@software])    # [@install] and [@software] are global macros refs (they start with @)
;
[@install]
    (install)
    (download)
    (setup)
;
[@uninstall]
    (uninstall)
    (remove)
;
[@software]
    (software)
    (app)
    (application)
;
```
### Non-terminals
Names enclosed in square brackets – ** \[ \] –** are non-terminals, calls to other grammars, for example:
**\[hotel_request\]**
If non-terminal starts with lower-case it won’t be returned in output but it will be used to match the pattern.
### Pre-terminals
Pre-terminals are non-terminals whose name begins with an underscore. The name of the pre-terminal rather than its content is used in extracted output. In this example, Amelia would output \_retainedProfit instead of using possible goal grammar names "retained profit" or "retained":
``` bash
 [IncomeSource]
    ([_retainedprofit])
    ([_rentalincome])
    ([_salaryIncome])
;
[_retainedprofit]
    (retained profit)
    (retained)
    (profit)
;
[_rentalincome]
    (rental income)
    (land property)
    (land income)
    (property income)
;
[_salaryIncome]
    (salary income)
    (working income)
    (employment income)
;
```
Possible Outputs:
-   \[IncomeSource\].retainedProfit
-   \[IncomeSource\].rentalIncome
-   \[IncomeSource\].salaryIncome
### Negation Syntax
Table. Grammar Negation Syntax

| Syntax | Description |
| ----|----|
| ! | Deprecated. Please substitute with <! or !> |
| <! ... | Changed to Look-behind negation |
| !> ... | Changed to Look-ahead negation |
| <<! ... | New syntax for Infinite look-behind negation |
| !>> ... | New syntax for Infinite look-ahead negation |
| + ;... | Removed |
| +* ... | Removed |

**Examples**
*Not "JUNK" ahead of "hi there"*
``` bash
[_Slot1]
        (hi there !>JUNK)
JUNK
        (junk)
        (garbage)
;
```
Matches: 
        "hi there"  
        "hi there. how are you?"
No Match:   
        "hi there junk"  
        "hi there garbage how are you?"  
*Not "JUNK" before "goodbye there"*
``` bash
[_Slot2]
        (<!JUNK goodbye there)
JUNK
        (junk)
        (garbage)
;
```
Matches: 
        "goodbye there"  
        "goodbye there. how are you?"  
        "goodbye there junk"
No Match:   
        "junk goodbye there"  
        "garbage goodbye there how are you?"
*Matching a text only if there is no in-grammar token anywhere in the utterance before or after POLICY:*
``` bash
[_Slot3]
         (<!$ANY POLICY !>$ANY)
POLICY
         (policy)
         (insurance)
;
```
Matches: 
         "policy"  
         "insurance"
These two statements will not match only if "vehicle" is in the grammar. If "vehicle" is not in the grammar, it will still match:  
         "vehicle policy"  
         "insurance vehicle"
*No "DONT" **ANYWHERE** before "need help"*
``` bash
[_Slot4]
         (<<!DONT need help)
DONT
         (do not)
         (does not)
         (dont)
;
```
Matches: 
         "I need help"  
         "I not do need help"
No Match:   
         "I do not need help"  
         "I do not know what is the date today, and I need help."  
*No "DONT" within 4 words behind "require help"*
``` bash
[_Slot5]
         (<!DONT_3 require help)
DONT_3
         (DONT [@any3])
DONT
         (do not)
         (does not)
         (dont)
;
[@any3]
         (*$ANY *$ANY *$ANY)
;
```
Matches:
        "I do not know what is the date today, and I require help."  
        "dont foo1 foo2 foo3 foo4 require help"
No Match:  
        "I do not really require help"  
         "dont foo1 foo2 foo3 require help"  
         "do not foo1 foo2 foo3 require help"
**Limitations**
Currently grammar negation syntax is not able to **negate** entire classes of named entities (NE) using $ORG, $PERSON, or $LOCATION. To negate a specific named entity such as "canada", you also must negate "$LOCATION" for it to successfully negate "canada".
Example:
``` bash
[_Slot6]
         (good morning !>AMERICA)
AMERICA
         ($LOCATION)
         (america)
;
```
Matches:
         "good morning"  
         "good morning canada"
No Match:  
         "good morning america"
### Attributes
Grammars include syntax to assign optional attributes to specific slots or pre-terminals including goals.
``` bash
#attributes(normalizedValue = "Lync")
[_lync]
    (skype $ANY *BIZ)
    (lync)
BIZ
    (business)
    (biz)
;
```
**Supported Attributes**
Table. Grammar Attributes Syntax

| Attribute Name | Description | Values Accepted | Target | Example |
| ----|----|----|----|----|
| normalizedValue | Used for normalization of categorical grammars (i.e., pre-terminals). The value overrides the preterminal name and allows for spaces, symbols, foreign language or custom capitalization. This normalization is applied right before SLU runs a BPN and in Ask lemmas of the language unit type. | A non-empty string. | Pre-terminals | [ApplicationName]    

        ([_excel]); 
    #attributes (normalizedValue = "MS. Excel")  
    [_excel]
        (*ms excel)
    ;
\| \| matchStyle \|
Changes the behavior of the parser for matching on a specific slot. The GREEDY match style indicates the parser to continue matching on a specific slot until all the possible values are matched even if there are duplicates. Also, slots of the GREEDY type will be passed to BPN variables as a collection or list.
\| GREEDY, DEFAULT \| Slots \|
    #attributes(matchStyle = GREEDY)[ASlot] # A random slot with three different categorical patterns
         ([_pattern1]) 
         ([_pattern2])
         ([_pattern3])
    ;
    # 'p1' is first defined here. 
    # The default parser matching style will stop considering 
    # other patterns once it finds one pattern.
    [_pattern1] 
         (p1)
    ;
    [_pattern2]
         (p2)
    ;
    # 'p1' Is a duplicated pattern that also exists in [_pattern1]
    [_pattern3]
         (p1)  
    ;
**Input**:   "p1"
**Output**:  "\[ASlot\].pattern1    \[ASlot\].pattern3" 
\| \| priority \| Goal Priorities for SLU \| \| Goal pre-terminals \| \| \| onInterrogative \| Goals annotated with onInterrogative = true will only be triggered if the sentence type is interrogative. Notice that it will not be effective for multi-sentence utterances. Defaults to false. \| true, false \| Goal pre-terminals \|
#attributes (onInterrogative = true)\[\_userQuestions\]  
(amelia)  
;
**Input**: "Amelia?"
**Output**: "\[Goal\].userQuestions"
**Input**: "Amelia..."
**Output**: 'No parse'
\| \|
confirm
\| If confirm = false, SLU won't confirm a single goal if it was resolved from a principal slot. Defaults to true. \| true or false \| Goal preterminals \|
#attributes (confirm = false)\[\_getAQuote\]  
(want \*to get a quote)  
;
\| \|
choiceName
\|
An optional behavior to default slot questions to similarity when no grammar is matched. Should only be used for multi-choice slot questions, not numeric slots such as Dates, SSN, PhoneNumber, and so on. Generates one or more utterances from Amelia, ordered by slot, using the choiceName value(s), when no grammar is matched based on the user utterance.
\| A non-empty string \| Slot preterminals \|
    [PolicyCancelSlot]   ([_cancel_howto_1])
       ([_reinstate_1])
    ;
    #attributes(choiceName="how to cancel a policy")
    [_cancel_howto_1]
       (how to cancel)
    ;
    #attributes(choiceName="reinstating a policy")
    [_reinstate_1]
       (reinstate)
    ;
\|
### Goal Priorities
Goal priorities allow for modification of the SLU's goal clarification behavior by giving precedence to goals that have higher priority. It is optional and all goals have same priority unless they are modified.
The priority attribute is an integer set by an implementation engineer. The default value for each goal is 0. If the default priority values are not changed, SLU will have goal clarifications. If there is a priority assigned for the goals that exist in an utterance, the clarification will be skipped and the goal of the conversation will be assigned to the goal with the higher priority.
For example, the utterance, "I want to get a quote but I am having difficulty accessing the contents of the drop down box." has two goals, **Getting a quote** and **Technical Issue.**
For this example, let's assume that **Getting a quote** goal has priority 5 and **Technical Issue **has priority 10. SLU will directly continue with **Technical issue** goal since it has higher priority.
If the priorities were not modified, SLU would ask a clarification, for example, asking, "Are you trying to get a quote or solve a technical issue?"
In a goal grammar, write the #attributes line above its corresponding goal.
``` bash
#attributes (priority = 15)
[_statusOfInvoice]
      (check status $ANY  invoice)
;
```
Attributes have these properties:
-   They are optional
-   Negative priority values can be assigned, for example, #attributes (priority = -10)
-   The range of priority values is −2,147,483,648 to 2,147,483,647
-   The default value of goal priority is 0. A lower or higher priority can be set for goals. 
If Lynx and classifiers are used in addition to grammars, singly or both together, then these configuration options are available:
-   If using only Lynx, use the priority attribute if needed.
-   If using only classifiers, do not use priority. Knowledge such as priority is extracted from classifier utterances.
-   If using both Lynx and classifiers, use the priority attribute if needed. Otherwise, unless Lynx ( can capture multiple goals per user utterance) and Classifier (can capture single goal per user utterance) recognize exactly same content for the goals, not having priorities will create clarification.
### Multi-choice Slots with Variations
Grammar notation can be used as variations to handle a broad range of possible natural language utterances.
**Not Recommended**
In this example, the local macro LYNC is a slot grammar with only a few possible utterances to trigger its use within the Application grammar:
``` bash
[Application]
    (LYNC)
    (microsoftoffice)
LYNC
    (lync)
    (skypefor biz)
;
```
**  
Recommended**
In this example, the Application grammar will be triggered by \_lync and \_msOffice grammars, for example, "Microsoft Office" and "MS Office":
``` bash
[Application]
    ([_lync])
    ([_msOffice])
;
[_lync]
    (lync)
    (skype *for BIZ)
BIZ
    (business)
    (biz)
;
[_msOffice]
    (MS office)
MS
    (ms)
    (microsoft)
    (msoft)
;
```
## Regular Expressions
Amelia includes a set of generic regular expression (regex) patterns and grammars which can be reused within new grammars.
### Working with Regex and Reserved Keywords
When writing grammars, regular expressions are defined as a comment at the top of the statements. For example, acronymsRegex\[A-Z\]{2-3} is defined within a comment then used in the slot grammar WorkAt:
``` bash
#define acronymsRegex[A-Z]{2,3}       #keep in mind the regex/terminals are not case sensitive
[WorkAt]
    (iwork at $ORG)
    (iWork $ANY_ALL acronymsRegex)
Work
    (work)
    (get a living)
;
```
Possible Output
-   \[WorkAt\].\[Organization\].IPsoft
-   \[WorkAt\].ABC
### Predefined Regular Expression Patterns
Common regular expression patterns are available when writing grammars:
Table. Grammar Pre-Defined Regular Expression Patterns

| Regex Pattern Name | Description |
| ----|----|
| alphaNumeric | Any 6 digits alphanumeric string. E.g., ABC123 |
| ssnPattern | Any Social Security Number. E.g., 123-12-1234 |
| maybeSsnPattern | A numeric token of 9 numbers. E.g. 987654321 |
| currencyPattern | Any 1 to 10 digits ;number followed/preceded by a $, €, or £ sign |
| timePattern | Any time pattern. E.g., 10:00:00 |
| dateTimePattern | Any simple mm/dd/yyyy date format |
| partialDatePattern | Simple dates that follow month/day structure. E.g., 12/31 |
| comprehensiveDatePattern | Most common date patterns. E.g., 01/15/2015, 1/15/2015, 2015-15-01 |
| comprehensiveDatePatternExtension | Simple dates that follow day/month/year structure. E.g., 01/jan/2015, 01 jan 2015, 31/12/2015 |
| shortNumberPattern | Any single 1 to 6 digits number |
| longNumberPattern | Any 6 to 30 digits number |
| integerPattern | Numeric tokens of one or more characters. E.g. 1, -14, 753951 |
| phoneNumberPattern | Any U.S. phone number |
| ipAddressPattern | Any IP address |
| decimalNumberPattern | Any decimal value. E.g., 12.75 |
| emailAddressPattern | Any email address |
| integerPattern | Any sequence of digits |
| urlPattern | Any full URL. E.g., http://ipsoft.com/ or https://ipsoft.com |
| domainPattern | Any domain name. E.g., amelia.ipsoft.com |

### Example of Reusing Predefined Regexes and Generic Grammars
These three generic slot grammar examples use regex to define new higher level slots:
``` bash
[InvoiceDate]                             # We can create a new slot that is a special case of date
    (invoice *date *is [Date])            # Example using the generic pre-defined grammar [Date]
    (invoice *date *is dateTimePattern)   # Example using the pre-defined regex pattern directly also works
; 
```
``` bash
[WifeDob]                    # Wife date of birth is another slot that can be defined
    (wife DOB *is [Date])    # Example using the generic pre-defined grammar [Date]
;
DOB
    (date of birth)
    (birthday)
    (dob)
;
```
``` bash
#define invoiceIdPattern REF[a-z0-9]{5,}    # Note: Custom regular expressions are case insensitive
[InvoiceId]                                 # We want to match on a declarative or invoice id pattern regex
    (invoice id *is alphaNumeric)           # The user's declarative plus any alphaNumeric pattern
    (invoiceIdPattern)                      # The specific invoice id pattern
;  
```
## Grammar Notation Best Practices
There are optimal ways to write grammars for Amelia, for example, using natural speech and pre-defined keywords and regex patterns wherever possible.
### Use Natural Speech
Create your patterns close to natural speech, so that when engineers read it, thet will get the idea at a glance. For example, a good practice is to write meaningful patterns and not just abstract or vague representations:
Good Practice: (ACCESS \*a \*my EMAIL)
Bad Practice:    (VERB \*$ANY \*$ANY TOPIC)
### Work with Regex and Reserved Keywords
Regex should only be done for simple pattern matching and should not replace grammar syntax.
To capture the cases the Named Entity Recognizer (NER) fails, we can use a custom regex to get the value:
``` bash
#define acronymsRegex [A-Z]{2,3}    #Note regex/terminals are not case sensitive
[WorksAt]
    (i Work at $ORG)                # Here we use the standard $ORG keyword
    (i Work at acronymsRegex)       # We can use a custom regex for when NER fails
Work
    (work)
    (make a living)
;
```
Example Output
-   **\[WorksAt\].\[Organization\]**.IPsoft
-   **\[WorksAt\]**.ABC
### Use Logical Negations
Logical negations help us enhance the semantics of the grammar when needed, by making sure that negated patterns don’t match on special cases.  In the example below, we are only interested in matching to the person’s preferred name when it’s not negated.
**Recommended**
``` bash
[preferredname]
    (*you $ANY <![@cannot] call me $PERSON)    #only matches when [@cannot] does NOT exist.
;
```
**Not Recommended**
``` bash
[not_preferredname]
    (you [@cannot] call me $PERSON)    #only matches when [@cannot] exists.
;
```
### Group with Pre-terminals
Pre-terminals let us group patterns into certain groups, especially when there are many ways to express something. For example, “Lync” and “Skype for Business” both mean “Lync” from an IT Service Desk agent’s perspective.
Good Practice: Group the patterns that have many variations with pre-terminals.
``` bash
[ApplicationName]
     ([_lync])        # We use pre-terminals to capture the many variations of Lync and Office
     ([_msOffice])
;
[_lync]
     (lync)
     (skype *for BIZ)
BIZ
     (business)
     (biz)
;
[_msOffice]
     (MS office)
MS
     (ms)
     (microsoft)
     (msoft)
;
```
Bad practice: It can get parsed as "**\[Application\]**.skype of biz" or "**\[Application\]**.lync"
``` bash
[Application]
     (LYNC)
     (microsoft office)
LYNC
     (lync)
     (skype for biz)
;
```
### Use Grammars for Inferences
Grammars can also be used for inference rules. For example, in a scenario where we have the following job roles: sole trader, director, salaried. Some basic inference rules can be pre-defined to capture whether or not a person is self-employed.
``` bash
[JobRoles]               # grammars for job roles slot
     ([_soleTrader])
     ([_director])
     ([_salaried])
;
[_soleTrader]
     (sole trader)
     (trades alone)
;
[_director]
     (director)
     (owns *$ANY company)
;
[_salaried]
     (works for the company)
     (under salary)
;
```
``` bash
[SelfEmployedBoolean]     #Now we can use grammars to define simple rules
     ([_selfEmployedTrue])
     ([_selfEmployedFalse])
;
[_selfEmployedTrue]
     (i own my own business)
     ([_soleTrader])     # Sole traders and directors are self-employed by definition
     ([_director])
;
[_selfEmployedFalse]
     ([_salaried])
     (employed)
;
```
### Avoid Useless Definitions
Grammar definitions can overuse parsing resources and cause overmatching. In this example, definitions 1 and 2 are identical but definition 1 has more restrictions, additionally requiring the parser to deal with the word go. Because there will never be a case where definition 1 can match a text and definition 2 cannot, definition 1 doesn't help increase the number of user utterances that can be matched by this slot.
``` bash
[Slot1]
   (let me go) # definition 1
   (let me)    # definition 2
;
```
The parser tries to match every definition with the user utterance, one at a time. In the worst case scenario, the parser tries all possible definitions. Trying definitions that don't add value is a waste of time. In this case, "let me go" is just 3 short words. The performance impact is minimal. 
However, the following real example demonstrates the same principle as above, but with much more significant impact on parse-times.
``` bash
[@gettingRefunded]
   ([@want] $ANY_ALL [@refund]) # Definition 1: same as definition 2, but additionally requiring [@want] to appear somewhere before.
   ([@refund])                  # Definition 2
   ([@refund] [@any3] [@money]) # Definition 3: same as definition 2, but additionally requiring [@money] to appear somewhere after with at most 3 random words in the middle.
   ([@money] back)              # Definition 4
   ([@get] [@money] back)       # Definition 5: same as definition 4, but additionally requiring [@get] to appear immediately before.
;
```
Because slot grammars can generate **hundreds of lines** of regular expressions, this definition could waste significant parser time.
### Avoid Not Restricting $ANY_ALL
Having $ANY_ALL on the ends of a definition like the above can lead to overmatching, too many collisions, and wasting parser time. 
``` bash
[Slot1]
   (check insurance $ANY_ALL)
;
```
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-11-20_16-7-4.png](attachments/11939678/11939679.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-11-20_16-5-51.png](attachments/11939678/11939680.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-grammars-workspace-3.6.4.jpg](attachments/11939678/11939681.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-9-20_17-0-10.png](attachments/11939678/11939682.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-20_17-0-1.png](attachments/11939678/11939683.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-grammars-intent-edit-3.5.9.jpg](attachments/11939678/11939684.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-9-20_16-41-18.png](attachments/11939678/11939685.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-grammars-workspace-3.5.9.jpg](attachments/11939678/11939686.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia-v3-grammars-entity-edit-3.4.8.jpg](attachments/11939678/11939687.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-5-9_14-49-50.png](attachments/11939678/11939688.png) (image/png)  
![](images/icons/bullet_blue.gif) [slotfood_test.xml](attachments/11939678/11939689.xml) (text/xml)  
![](images/icons/bullet_blue.gif) [amelia-v3-grammars-intent-edit-3.4.8.jpg](attachments/11939678/11939690.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia-v3-grammars-workspace-3.4.8.jpg](attachments/11939678/11939691.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2019-1-16_16-32-26.png](attachments/11939678/11941067.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-1-16_16-35-4.png](attachments/11939678/11941068.png) (image/png)  
