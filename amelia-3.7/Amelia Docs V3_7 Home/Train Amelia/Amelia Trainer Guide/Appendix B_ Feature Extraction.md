{% version "3.x" %}
# Overview
While quality and quantity of data is crucial to training Amelia, feature engineering is equally or more important. Feature engineering uses domain knowledge of the data to create features – attributes used to build a numeric representation of each data point that emphasizes and distinguishes their differences – ideal to solve a specific problem with machine learning.
For example, a mapping gazetteer of US state names with all possible variations would have state as a feature to solve the problem of helping Amelia identify all variations people might use to describe a state. If AL and Alabama are single word tokens mapped to a feature in a file, Amelia can identify AL refers to a US state and connects to the state of Alabama.
A sample US state gazetteer CSV file might have an id, key, and state structure where key is a feature called STATE.
``` text
id,key,state
1,STATE,ak
2,STATE,al
3,STATE,ala.
4,STATE,alabama
5,STATE,alaska
...
```
This example file maps state names and acronyms to a common STATE feature as a key. Instead of relying on each word as a feature, Amelia has an important clue that ak, al, and alabama are single word tokens that represent US states.
## Extracting Features
In many cases, extracting features can be split into two activities:
-   Identify context within the input text
-   Extract useful features over those contexts
For example, if the input text is "I want to book a flight," all six individual words in the text are contexts: I, want, to, book, a, flight. Extracting each word as a feature yields the same output.
## Context
In some cases, we might give significance to words in particular contexts. For example, if we tag each single word token in a sentence with a label, the words to the left and right of the current word likely should be treated differently from each other. A set of features could be extracted specifically for each token. In this situation, the current token or focus is important.

| Input Sentence | Context Type | Contexts | Extraction Function | Extracted Features |
| ----|----|----|----|----|
| I want to book a flight | Unigram | (I) (want) (to) (book) (a) (flight) | Identity | I, want, to, book, a, flight |
| What is the Current Time? | Bigram | (What, is) (is, the) (the, Current) (Current, Time) (time, ?) | Lowercase (concatenate) | what|is, is|the, the|current, current|time, time|? |
| We are going to NYC | Bigram | (We, are) (are, going) (going, to) (to, NYC) | Lemma (concatenate) | we|be, be|go, go|to, to|NYC |

The current token or focus can be used to reference, for example, with a +1 or -1, the offset to the immediate right and left of the current token. References that yield an empty result are marked out of bounds (OOB) or the end (X).

| Input Token | Context Type | Contexts (offset:result) | Extraction Function | Extracted Features (offset:result) |
| ----|----|----|----|----|
| My name is John Doe | Left/Right tokens | (-1:OOB) (+1:name) | Part-of-speech | -1:X, +1:NOUN |
| My name is John Doe | Left/Right tokens | (-1:My) (+1:is) | Part-of-speech | -1:DET, +1:VERB |
| My name is John Doe | Left/Right tokens | (-1:name) (+1:John) | Part-of-speech | -1:NOUN, +1:PROPN |
| My name is John Doe | Left/Right tokens | (-1:is) (+1:Doe) | Part-of-speech | -1:VERB, +1:PROPN |
| My name is John Doe | Left/Right tokens | (-1:John) (+1:OOB) | Part-of-speech | -1:PROPN, +1:X |

Notice the extracted part-of-speech features and how the contexts are distinguished with their offsets. This technique enables a machine learning model to assign weights to the same word appearing in different positions. The bag-of-words approach, in contrast, treats a text as a bag filled with each word in the text and each word will always have the same impact in a model.
Amelia V3 includes a feature framework to create features to train reasoning models. Features used to train a model are uploaded through the Tabular Data workspace in Amelia V3's administration pages. Once uploaded, a Feature Editor is available in the Annotate workspace to use features, tokens, offsets, and other techniques to train Amelia.
# Create a Feature Resource File
Currently, feature resource files must be in CSV file format and uploaded through the Tabular Data workspace. Files must meet [the file format requirements](https://docs.ipsoft.com/display/AmeliaDocsV3/Script+Tasks#ScriptTasks-TabularDataSources) for that service.
# Upload a Feature Resource File
Feature resource files are uploaded within the Tabular Data file workspace, in this demonstration the [states.csv](attachments/11939753/11939771.csv) file.
1.  Click the Process Memory link in Amelia V3's administration pages. Then click the Tabular Data link to display the Tabular Service workspace.
2.  Click the Import New File button at the top right of the Tabular Data workspace. The Import File workspace appears.
3.  Select a domain where to place the feature resource file.
4.  Click the upload icon to display the file browser. Search for the feature resource file and click the Open button to upload the selected file.
5.  Click the Next button to continue. If the file is a duplicate, Amelia V3 will alert you.
6.  Click the Finish button to finish the import process.
# Annotate Training Data
The next step is to annotate training data. This demonstration annotates data for an entity model. However, the process is the same for an intent model, except as noted.
## Import a File to Annotate
The [state-examples.txt](attachments/11939753/11939772.txt) file includes bits of US state-related utterances to annotate.
1.  Click the Amelia Trainer link in Amelia V3's administration pages. Then click the Annotate link to display the Annotate workspace.
2.  Click the Import tab to display the Import Settings panel on the right side of the workspace. Click the folder icon to display a file explorer then find the state-examples.txt file and click the Open button to upload the selected file. The utterances will load in the Annotate workspace.
## Annotate File
1.  Select a state name in the utterances to display a list of entities. If state is not listed as an entity, type *state* in the input field to create an entity that can map to the feature loaded with the Tabular Data workspace. Repeat tagging state names and acronyms with the *state* entity for other US state related tokens in the utterances.  
    ![](attachments/11939753/11939758.png)  
    Figure. Highlight Text then Select the State Entity  
2.  When all tokens are tagged as entities, click the Save As icon at the top right of the workspace.
3.  Click the Train tab and Train Entities popup to display the Train Entity Models panel on the right side of the workspace. Alternately, Train Intents could be selected to train an intent model and use the Feature Editor.  
    ![](attachments/11939753/11939768.png)  
    Figure. Select Train Entities
# Train an Entity Model
For this demonstration, the next step is to train an entity model to show how to use the Feature Editor. Alternately, an Intent model could be trained and include the Feature Editor.
1.  Once a file is imported and annotated, use the Train Entity Models panel to type in a model name or upgrade a model.
2.  Select the Include entity list utterances toggle slider and state-examples.txt file.  
    ![](attachments/11939753/11939757.png)  
    Figure. Select state-examples.txt File  
3.  Amelia's Feature Editor is available in the Training Entity Models panel by clicking the *Use custom features* toggle slider to display the Edit Features button. Pre-processors are available in the Feature Editor when training intents or if the *Spanless entity classifier* toggle slider is selected when training entities or when training intents with the Train Intent Models panel.  
    ![](attachments/11939753/11939756.png)
    Figure. Train Entity Models Panel  
4.  Use the Feature Editor to define features. See the next section for details about how to use the Feature Editor.
5.  Click the Train Entity Model button at the bottom of the panel to start training.
6.  Click the Dashboard link at the left, under the Amelia Trainer link, to see the trained entity model listed. Click the statistics icons to the right of the model name to evaluate the results of training.
# Use Feature Editor
The Feature Editor is designed to edit and test feature configuration in real time, before training a model. Configured features and, if appropriate, preprocessors will be used to train a model. The editor provides a subset of functionality provided through XML file configurations. For most cases, however, the editor is sufficient. The editor also allows visual insight into what features are extracted with a configuration which, in turn, helps do debug and improve results.
The Feature Editor is available by clicking the toggle slider *Use custom features* in the Train Entity Models and Train Intent Models panels. While sample formatters and pre-processors are included, editor tools can create many variations.
## Model Feature Editor Default Interface
When the Open feature editor button in the Train panel, the Model Feature Editor displays as a popup. Preprocessors will appear if training intents or Spanless entity classifier is selected in the Training Entity Models panel.
![](attachments/11939753/11939755.png)
Figure. Model Features Editor with Spanless entity classifier Selected
Table. Model Features Editor Elements

| Element | Description |
| ----|----|
| Features | Add, edit and delete features, the core of the feature extraction pipeline |
| Preprocessors | Add, edit and delete preprocessors, which are used before feature extraction even begins to preprocess the input text |
| Interactive Tester | Enter test utterances and see the resulting extracted features given the current feature pipeline. Results are shown directly below as labels. Values extracted are on the left of a label with the feature name to the right. |

## Edit Feature Interface
The edit feature interface appears when Add Feature or an existing feature is clicked in the default interface.
![](attachments/11939753/11939754.png)
Figure. Edit Feature Interface of the Model Features Editor
Table. Edit Feature Interface Elements

| Element | Description |
| ----|----|
| Feature Name | Identifier that must be unique, and must be composed of ASCII characters with no spaces. Using a pre-existing name will overwrite the previous feature with that name. |
| Context Type | The context in the input text over which the feature will be extractedUnigrams;– bag-of-words in the input utterance (order is not taken into consideration)Bigrams – bag-of-bigrams (subsequences of two words) in the input utteranceSyntactic bigrams – in a syntactic parse of the input, rather than use sequential bigrams, use bigrams from child tokens to their heads: I am flying to Memphis → (I flying), (am flying), (to Memphis), (Memphis flying)Subjects – syntactic subjects in a parse of the input: John threw the ball → JohnObjects – syntactic objects in the parse of the input: John threw the ball → ball |
| Collocation offsets |  |
| Extractor | Type of extractor to apply to the input context. Specifies what is actually extracted from each word as a feature.Word;– Original, unmodified text of the input wordLemma – Base form of the word after morphological analysis (Lemmatization)Lookup – Selecting Lookup displays a second dropdown list for Lookup Type and Table, Input Column, and Output Column, both below the Extractor dropdown. Use two columns from tabular service to map from the output of an extractor (keys from the input column) onto a value in the output column. There are three Lookup Type options.Exact matching – as it sounds, only finds a match if the input text exactly matches the value in the input columnRegex matching – presupposes that the input columns are regular expressions–then matches the input text using each regular expression to find a matchApproximate matching – uses Levenshtein distance (default threshold of 1) to determine if there is a match. For example, with an input value New York, New Yirk would be considered to be a match.Fallback Lookup – Similar to lookup, but when no match is found fallback to the output of the base extractor (instead of outputting a blank feature)Prediction History |
| Check for Negation | Wraps the extractor in a negation extractor, which checks to see if the context is negated in any way. |
| Table/Input Column/Output Column | Used by lookup-based extractors to specifiy a mapping from inputs onto outputs. Refers to tables in Tabular Service. |
| Preprocessors | List of string functions applied to the output of the extractor. Click the input field to display a dropdown list of options.Ignore Digits;– replace every continuous string of digits with a hashtag/pound symbol: 34.00 → #.#Lowercase – simply lowercase each letter in every wordNormalize Digits – replace every digit in a word with a hashtag/pound symbol: 34.00 → ##.##Normalize Unicode – replace unicode characters with their normalized ASCII form: ésta → estaNormalize Words - Extract only shape of words based on capitalization and/or digitsExtract Prefix – extract only the first two characters of the input: IPsoft → IPExtract Suffix – extract only the last three characters of the input: IPsoft → oft |

## Edit Preprocessor Interface
The edit feature interface appears when Add Preprocessor or an existing preprocessor is clicked in the default interface.
![](attachments/11939753/11939762.png)
Figure. Edit Preprocessor Interface of the Model Features Editor
Table. Edit Preprocessor Elements

| Element | Description |
| ----|----|
| Preprocessor Type | Stopword Filter;– removes provided words from the input text before extracting features. There are some good lists available here: https://www.ranks.nl/stopwords. Use stopwords with caution, and be sparing, as they rarely improve performance on intent detection, but can often hurt performance.Punctuation Filter – removes punctuation matching a given regular expression at the end of the input sequence. This only removes sentence-final punctuation–if you want to remove punctuation within the sentence, use Stopword Filter.  |
| Punctuation regex / Stopword List | Depending on Preprocessor Type selected, an input field appears for the appropriate data to be entered. |

# Custom Feature Templates
In addition to the Feature Editor interface, feature extraction also can be defined with an XML file called a feature template. The file can be uploaded as part of training a reasoning model. Amelia uses the feature template to identify patterns within user utterances. Testing a user utterance to match the pattern, however, is done with edge notation from a BPN model task.
Feature templates are built with context factories, extractors, and processors called with a range of XML tags, as described in this section.
## Context Factories
Features are specified in two steps. The first step identifies the context while the second applies feature functions over the contexts.
Contexts are an ordered collection of tokens, for example, a complete sentence or a single word token. Contexts are captured with Context Factories. There are many Context Factories, for example, to capture sub-sequences of tokens in the current instance (NgramContextFactory) or syntactic neighbors (DepNgramContextFactory).
There are two types of Context Factories, SequenceContextFactories for sequence-level classification tasks and FocusContextFactories to use a single token as a focus, as well as the sequence containing the token. Context factories generally are used in sequence tagging tasks where each individual token becomes a classification instance over which to extract features.
### Sequence Contexts
Sequence contexts are used most frequently in sentence-level classification tasks (sequence classification). In sentence-level classification, features are extracted across the entire sequence as a single classification instance. These tasks are distinct from sequence tagging tasks, where each token in the sequence is individually classified.
#### **NgramContext **
The most common context for sequence classification tasks. Extract subsequences of a specified length of words within the sentence. N-grams of length 1 and 2 correspond to unigrams and bigrams respectively. These are frequently used in text classification tasks.
``` text
<Feature name="bigram">
 <NgramContext length="2"/>
 <MapExtractor key="lemma"/>
</Feature>
```
    John loves donuts in the morning → [bigram:John_love, bigram:love_donut, bigram:donut_in, bigram:in_the, bigram:the_morning]
#### **DepNgramContext**
Extract syntactic dependency path-based n-grams in a sentence.
``` text
<Feature name="dep_bigram">
 <DepNgramContext length="2"/>
 <MapExtractor key="lemma"/>
</Feature>
```
    John doesn't really love donuts in the morning ->
    dep_bigram: John_love, dep_bigram:does_love, dep_bigram:not_love, dep_bigram:really_love, dep_bigram:donut_love, dep_bigram:morning_love, dep_bigram:the_morning, dep_bigram:in_morning
**![](attachments/11939753/11939759.png)**
Figure. DepNgramContext Example Diagrammed
#### **QuestionFocusContext**
When classifying questions, this context can be useful for identifying the "focus" of the question as a feature.
``` text
<Feature name="QF">
 <QuestionFocusContext/>
 <MapExtractor key="form"/>
</Feature>
```
    Which country has the highest GDP? -> QF:country
    What year did Mussolini seize power in Italy? -> QF:year
For "how much/many"-type questions, it returns foci for the adjective modifier of the focus as well as focus itself.
    How much fiber should you have per day? -> QF:QFQ:much, QF:QFE:fiber
    How many liters in a gallon? -> QF:QFQ:many, QF:QFE:liters
#### **DepRelContext **
Sometimes it can be useful to select features for a specific set of dependency relations.
``` text
<Feature name="subj-obj">
 <DepRelContext rels="nsubj,dobj"/>
 <MapExtractor key="form"/>
</Feature>
```
    I want to order a pizza -> subj-obj:I, subj-obj:pizza
![](attachments/11939753/11939760.png)
Figure. DepRelContext Example Diagrammed
#### **SequenceIdentityContext**
This context outputs the entire sentence/sequence of tokens as a context. This is useful when looking for keywords/phrases across the entire sentence (see [KeyPhraseExtractor](#AppendixB:FeatureExtraction-KeyPhraseExtractor)).
``` text
<Feature name="keywords">
 <SequenceIdentityContext/>
 <KeyPhraseExtractor>
 <MapExtractor key="form"/>
 <Gazetteer resource="food_gaz"/>
 </KeyPhraseExtractor>
</Feature>
```
### Focus Contexts
These contexts are useful for sequence tagging tasks like entity tagging where one extracts features over each token in the input sequence.
Note that this is different than sequence classification like intent detection, where features are extracted across the entire sentence. In such a task, useful contexts might be the previous token and the following token. The CollocationalContext context factory takes an offset – for example, "-2,-1" – and captures the token offset by that amount -- for example, the 2 tokens to the left -- from the current token. If the current sequence is "My employee id# is 12315" and the current token is "12315", the context \["id#", "is"\] would be captured.
#### **FocusIdentityContext**
Returns the current focus token as a context.
``` text
<Feature name="focus">
 <FocusIdentityContext/>
 <MapExtractor key="form"/>
</Feature>
```
    Hello   → Focus:Hello
    world   → Focus:world
    !       → Focus:!
#### **CollocationalContext**
Used to specify contexts relative the focus token. Given an integer offset *k* and focus token with index *i*, extract a token at index (k + i). When i is negative, extract tokens to the left, and when positive, extract tokens to the right. When i is 0, this is equivalent to the FocusIdentityContext.
This context factory also can be used to capture multi-token contexts relative to the focus. If given a list of integer offsets, it will return a context containing a token at each of the corresponding offsets.
``` text
<Feature name="word_-1">
 <CollocationalContext offset="-1"/>
 <MapExtractor key="form"/>
</Feature>
```
    I       → word_-1:#OOB
    want    → word_-1:I
    a       → word_-1:want
    cheese  → word_-1:a
    pizza   → word_-1:cheese
(#OOB is a token used when extracting a feature from a context that is **O**ut **O**f **B**ounds).
``` text
<Feature name="word_-1_-2">
 <CollocationalContext offset="-1,-2"/>
 <MapExtractor key="form"/>
</Feature>
```
    I       → word_-1_-2:#OOB_#OOB
    want    → word_-1_-2:I_#OOB
    a       → word_-1_-2:want_I
    cheese  → word_-1_-2:a_want
    pizza   → word_-1_-2:cheese_a
## Extractors
Extractors are the second component of a feature extractor, the first being a context factory. Extractors take a context output from a context factory as input, perform a function or composition of functions on those contexts, then returns the results as features.
### **MapExtractor**
Extracts features from a predefined set of attributes associated with the tokens in the provided context. These include **form** (raw text), **lemma** (base form), **pos** (part-of-speech tag), **cpos** (coarse-grained pos-tag) and **dep** (dependency parse label). When a gazetteer is applied as a preprocessor, the keys in the gazetteer are also available as keys for this feature.
``` text
<Feature name="unigram">
 <NgramContext length="1"/>
 <MapExtractor key="cpos"/>
</Feature>
```
    I want to order a pizza -> unigram:PRON, unigram:VERB, unigram:PART, unigram:VERB, unigram:DET, unigram:NOUN
When a context contains multiple tokens – for example, as for n-grams, with n \> 1 -- the results of the extraction are concatenated together.
``` text
<Feature name="bigram">
 <NgramContext length="2"/>
 <MapExtractor key="pos"/>
</Feature>
```
    I want to order a pizza -> 2gram:PRP_VBP, 2gram:VBP_TO, 2gram:TO_VB, 2gram:VB_DT, 2gram:DT_NN

| MapExtractor Keys | key | description |
| ----|----|----|
| form | original text of token | John, ran, 3, miles |
| lemma | base form of token | John, run, 3, mile |
| pos | part-of-speech tag (language-specific) | NNP, VBD, CD, NNS |
| cpos | universal part-of-speech tag (coarse-grained) | PROPN, VERB, NUM, NOUN |
| dep | head label in syntactic dependency parse | nsubj, root, nummod, dobj |

![](attachments/11939753/11939761.png)
Figure. MapExtractor Diagrammed
### **NegationExtractor**
This extractor wraps a base extractor, for example, as a map extractor. If the context word has negative polarity (is negated in some way), the base extraction is marked as being negated.
``` text
<Feature name="word">
 <NgramContext length="1"/>
 <NegationExtractor>
 <MapExtractor key="form"/>
 </NegationExtractor>
</Feature>
```
    Do not cancel my policy -> word:do word:not word:neg:cancel word:my word:policy
### **GazetteerExtractor**
Used to extract features corresponding to a particular gazetteer, given by the "gaz" attribute, which references a gazetteer defined earlier.
``` text
<Feature name="state_gaz">
 <FocusIdentityContext/>
 <GazetteerExtractor gaz="us_states"/>
</Feature>
```
    I      -> O
    live   -> O
    in     -> O
    Rhode  -> state_gaz:B-STATE
    Island -> state_gaz:I-STATE
### **KeyPhraseExtractor**
This extractor applies a base extractor to the full input context then attempts to locate all phrases defined in a given gazetteer. If the phrase is located, the key is returned as a feature.
*states_gaz* contents:
    VALID      Alabama
    INVALID    Alaska
    VALID      Arizona
    ...
    VALID      West Virginia
    VALID      Wisconsin
    INVALID    Wyoming
``` text
<Feature name="state">
 <SequenceIdentityContext/>
 <KeyPhraseExtractor>
 <MapExtractor key="form"/>
 <Gazetteer resource="us_states"/>
 </KeyPhraseExtractor>
</Feature>
```
    I live in Alaska. -> state:INVALID
### **StringFunctionExtractor**
Performs one of a number of predefined string functions to the output of a base extractor. These functions include lowercasing the input, extracting affixes/suffixes of words, normalizing digits, or other forms of normalization.
``` text
<Feature name="shape">
 <FocusIdentityContext/>
 <StringFunctionExtractor>
 <!-- MR stands for "Merge Repeats" OPC (One per character) and KPR (Kleene plus) are also available -->
 <ShapeFunction type="OPC"/>
 <MapExtractor key="form"/>
 </StringFunctionExtractor>
</Feature>
```
    My             shape: Xx
    invoice        shape: x
    number         shape: x
    is             shape: x
    xasd1231asd123 shape: xdxd
SequentialStringFunction applies a sequence of string functions.
``` text
<Feature name="word">
 <NgramContext length="1"/>
 <StringFunctionExtractor name="form_extractor">
 <SequentialFunction>
 <DigitNormalizingFunction type="MR"/>
 <LowerCaseFunction/>
 </SequentialFunction>
 <MapExtractor key="form"/>
 </StringFunctionExtractor>
</Feature>
```
    I OWE $ 142.00 -> word:i, word:owe word:$ word:#.#
## Processors
Processors do some form of pre-processing over the input instances prior to feature extraction. Gazetteers are a common processor that labels matching tokens with corresponding gazetteer categories.
### Gazetteers
Gazetteers are lists of words, for example, locations, names, product types, etc. Each list corresponds to a particular type.
They are used in feature extraction by matching entries in each list with some level annotation in the target instance, for example, text, lower-cased tokens, and lemmas.  
In the sentence, "John lives in New York and works at Chase," a gazetteer containing locations might identify "New York" as a location. Similarly, a gazetteer containing company names might identify "Chase" as a company.
Gazetteers require a resource to be pre-defined in the Resources element. A gazetteer can then be applied as a processor using the GazetteerProcessor element, which takes an extractor to convert the input text to a format consistent with the gazetteer, and the *Gazetteer* itself, which takes a resource pointing to the key of a pre-defined resource.
``` text
<Resources>
 <Resource key="gaz" path="path/to/gaz.txt"/>
</Resources>
<Processors>
 <GazetteerProcessor>
 <StringFunctionExtractor>
 <LowerCaseFunction/>
 <MapExtractor key="form"/>
 </StringFunctionExtractor>
 <Gazetteer resource="gaz"/>
 </GazetteerProcessor>
</Processors>
```
    In this example, a gazetteer identified as "gaz" is defined and initialized from the provided path. An extractor that takes the text of each word and lowercases it preprocesses the input text, then passes the result to the gazetteer, which attempts to look up each entry in the gazetteer. If a match is found, it adds the corresponding key to the token, which can then be used later during feature extraction.
#### Gazetteer Types
Currently there are 3 types of gazetteers offered, Exact, Regex, and Approximate Matching.
##### **Exact**
Only matches when the annotation text exactly equals the gazetteer entry. This correspond to the above example:
``` text
 <Gazetteer resource="gaz"/>
```
##### **Regex**
Instead of strings, gazetteer entries are regular expressions which are compiled and used to match against the input text.
``` text
<RegexGazetteer resource="dict"/>
```
    An example dictionary accepted by a regex gazetteer:
    PHONE   ((\+?\d)?[-. ]?(\([ ]?\d{3}[ ]?\)|\d{3})[-. ]?)?\d{3} *[-.]? *\d{4}
    7DIGIT  \d{7}
    9DIGIT \d{9}
    10DIGIT    \d{10}
    EMAIL  [^\s@]+@[^\s@]+\.[^\s@]+
##### **Approximate Matching**
Uses Levenshtein distance to approximately match gazetteer entries with target annotations. Matches only happen when the distance between target annotation and a gazetteer entry is below a manually set threshold.
``` text
<ApproximateGazetteer resource="dict" threshold="1"/>
```
    Threshold corresponds to the maximum-accepted Levenshtein distance. "New Yirk" would match a gazetteer entry with key "New York" in this example.
#### Usage
Gazetteers can be used in different ways. In one approach, they can be used as a key-phrase extractor, that simply return gazetteer matches as an unordered "bag of words" (see [KeyPhraseExtractor](#AppendixB:FeatureExtraction-KeyPhraseExtractor)).
They can also be used as annotations, which can be extracted with arbitrary contexts (see [GazetteerExtractor](#AppendixB:FeatureExtraction-GazetteerExtractor)). For example, one could extract gazetteer-annotated labels over unigrams, bigrams or trigrams. Using a location gazetteer with key "LOC", given the sentence "He left New York for California", bigrams would be "O O", "O B-LOC", "B-LOC I-LOC", "I-LOC O" and "O B-LOC". This can be especially useful for slot extraction/sequence tagging. For example, if extracting the browser type as a slot, a useful gazetteer might simply be a list of browsers or aliases of browsers:
        BROWSER    chrome
        BROWSER    firefox
        BROWSER    internet explorer
        BROWSER    ie
        BROWSER    safari
        BROWSER    edge
        BROWSER    chromium
        ...
### Chunking Processor
Chunking processors can be used to re-label annotations on tokens with different chunking strategies. For example, if tokens are labeled with named entity labels:
    John   PERSON
    lives  O
    in     O
    New    LOCATION
    York   LOCATION
A chunking processor, given the label key and chunking strategy (e.g. BIO or BESIO - <https://en.wikipedia.org/wiki/Inside_Outside_Beginning>), could relabel this as:
    John   S-PERSON
    lives  O
    in     O
    New    B-LOCATION
    York   E-LOCATION
This approach can often improve performance in sequence tagging/slot filling tasks.
#### Begin - Inside - Out
*Begin* corresponds to the first token of the entity and *Inside* is used for any non-*Begin* entity. *Out* is the label used for all non-entity tokens.
``` text
<Processors>
 <ChunkingProcessor key="gold" chunkType="BIO"/>
</Processors>
```
#### Begin - End - Single - Inside - Out
*Single* corresponds to entities that only have a single token. *End* corresponds to the last token in the entity.
``` text
<Processors>
 <ChunkingProcessor key="gold" chunkType="BESIO"/>
</Processors>
```
#### Inside - Out
``` text
<Processors>
 <ChunkingProcessor key="gold" chunkType="IO"/>
</Processors>
```
## Feature Template Examples
The feature extraction framework specifies feature extraction pipelines as XML descriptor files called feature templates. These files are uploaded into Amelia V3 and stored along with the trained model parameters to allow for dynamic creation of the feature extraction pipelines at runtime.
### Simple Tagger Example
**Simple Tagger Example**
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<ClassifierTemplate xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                    xsi:noNamespaceSchemaLocation="ClassifierTemplate.xsd">
    <!-- instanceType indicates the feature extraction approach (sparse for linear classifiers vs. dense for DNNs) -->
    <!-- modelType indicates which classification algorithm to use -->
    <ClassifierProperties instanceType="VECTOR"/>
    <Processors>
        <ChunkingProcessor key="gold" chunkType="BIO"/>
    </Processors>
    <!-- You can define extractors here, which you can later refer to by the "name" attribute using "ref=...".
    This is useful if you reuse the same extractor over different contexts, so you don't need to keep re-defining them. -->
    <Extractors>
        <StringFunctionExtractor name="lemma_extractor">
            <SequentialFunction>
                <DigitNormalizingFunction/>
                <LowerCaseFunction/>
            </SequentialFunction>
            <MapExtractor key="lemma"/>
        </StringFunctionExtractor>
    </Extractors>
    <!--Focus Features are features extracted on a per-token basis-->
    <FocusFeatures>
        <Feature name="win_-2">
            <CollocationalContext offset="-2"/>
            <Extractor ref="lemma_extractor"/>
        </Feature>
        <Feature name="win_-1">
            <CollocationalContext offset="-1"/>
            <Extractor ref="lemma_extractor"/>
        </Feature>
        <Feature name="win_0">
            <CollocationalContext offset="0"/>
            <Extractor ref="lemma_extractor"/>
        </Feature>
        <Feature name="win_1">
            <CollocationalContext offset="1"/>
            <Extractor ref="lemma_extractor"/>
        </Feature>
        <Feature name="win_2">
            <CollocationalContext offset="2"/>
            <Extractor ref="lemma_extractor"/>
        </Feature>
        <Feature name="win_-2_pred_form">
            <CollocationalContext offset="-2"/>
            <PredictionExtractor/>
        </Feature>
        <Feature name="win_-1_pred_form">
            <CollocationalContext offset="-1"/>
            <PredictionExtractor/>
        </Feature>
    </FocusFeatures>
</ClassifierTemplate>
```
### Simple Intent Classifier Example
**Simple Intent Classifier Example**
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<ClassifierTemplate xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                    xsi:noNamespaceSchemaLocation="ClassifierTemplate.xsd">
    <!-- instanceType indicates the feature extraction approach (sparse for linear classifiers vs. dense for DNNs) -->
    <!-- modelType indicates which classification algorithm to use -->
    <ClassifierProperties instanceType="VECTOR"/>
    <!-- You can define extractors here, which you can later refer to by the "name" attribute using "ref=...".
    This is useful if you reuse the same extractor over different contexts, so you don't need to keep re-defining them. -->
    <Extractors>
        <StringFunctionExtractor name="lemma_extractor">
            <SequentialFunction>
                <DigitNormalizingFunction/>
                <LowerCaseFunction/>
            </SequentialFunction>
            <MapExtractor key="lemma"/>
        </StringFunctionExtractor>
    </Extractors>
    <SequenceFeatures>
        <Feature name="unigrams">
            <NgramContext length="1"/>
            <Extractor ref="lemma_extractor"/>
        </Feature>
        <Feature name="bigrams">
            <NgramContext length="2"/>
            <Extractor ref="lemma_extractor"/>
        </Feature>
    </SequenceFeatures>
</ClassifierTemplate>
```
### Named Entity Tagging Example
(See [Appendix B: Feature Extraction](Appendix%20B_%20Feature%20Extraction) and [Appendix B: Feature Extraction](Appendix%20B_%20Feature%20Extraction) for example resources).
**Named Entity Tagging Example**
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<ClassifierTemplate xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                    xsi:noNamespaceSchemaLocation="ClassifierTemplate.xsd">
    <!-- instanceType indicates the feature extraction approach (sparse for linear classifiers vs. dense for DNNs) -->
    <!-- modelType indicates which classification algorithm to use -->
    <ClassifierProperties instanceType="VECTOR" modelType="CrfSuite"/>
    <!-- Specify tab-separated files here, in the format name<tab>value:
        STATE   Alabama
        STATE   Alaska
        ...
        COUNTRY United States of America
        COUNTRY USA
        COUNTRY Canada
        COUNTRY Mexico
    -->
    <Resources>
        <Resource key="gazetteer" path="entity-lists.txt"/>
        <!-- resources are read as tsv files with keys in the first column and values in the second column by default. since this
        cluster file has values in the second column, we need to reverse it when reading it-->
        <Resource key="brown" path="brown-clusters.txt" reverse="1"/>
    </Resources>
    <Processors>
        <!-- a pre-processor used to pre-annotate each token with matching gazetteer entries -->
        <GazetteerProcessor chunkType="BESIO">
            <MapExtractor key="form"/>
            <Gazetteer resource="gazetteer"/>
        </GazetteerProcessor>
        <!-- pre-processes the labels of tokens to a particular chunking type (e.g. BIO, IO or BESIO) -->
        <ChunkingProcessor key="gold" chunkType="BESIO"/>
    </Processors>
    <Extractors>
        <MapExtractor name="form_extractor" key="form"/>
        <!-- extracts the text of a word, normalizing the digits like 12/11/2013 to ##/##/#### or $3.23 to $#.## -->
        <StringFunctionExtractor name="normalized">
            <SequentialFunction>
                <DigitNormalizingFunction/>
            </SequentialFunction>
            <Extractor ref="form_extractor"/>
        </StringFunctionExtractor>
        <!-- extracts Brown cluster features for each word, where present -->
        <BrownClusterExtractor name="browncls" resource="brown">
            <Extractor ref="form_extractor"/>
        </BrownClusterExtractor>
        <ConjunctionExtractor name="pred_conj">
            <PredictionExtractor/>
            <Extractor ref="normalized"/>
        </ConjunctionExtractor>
        <Aggregate name="win">
            <!-- extracts a feature for the capitalization shape of each word -->
            <StringFunctionExtractor>
                <ShapeFunction type="OPC"/>
                <Extractor ref="form_extractor"/>
            </StringFunctionExtractor>
            <Extractor ref="browncls"/>
            <!-- gazetteer extractor that only returns features when they are present -->
            <GazetteerExtractor gaz="gazetteer"/>
            <Extractor ref="normalized"/>
            <!-- part-of-speech tag-->
            <MapExtractor key="pos"/>
        </Aggregate>
        <!-- extract prefixes and affixes of each (digit-normalized) word -->
        <Aggregate name="suffix">
            <StringFunctionExtractor>
                <AffixFunction type="Suffix" length="1"/>
                <Extractor ref="normalized"/>
            </StringFunctionExtractor>
            <StringFunctionExtractor>
                <AffixFunction type="Suffix" length="2"/>
                <Extractor ref="normalized"/>
            </StringFunctionExtractor>
            <StringFunctionExtractor>
                <AffixFunction type="Suffix" length="3"/>
                <Extractor ref="normalized"/>
            </StringFunctionExtractor>
            <StringFunctionExtractor>
                <AffixFunction type="Suffix" length="4"/>
                <Extractor ref="normalized"/>
            </StringFunctionExtractor>
        </Aggregate>
        <Aggregate name="prefix">
            <StringFunctionExtractor>
                <AffixFunction type="Prefix" length="3"/>
                <Extractor ref="normalized"/>
            </StringFunctionExtractor>
            <StringFunctionExtractor>
                <AffixFunction type="Prefix" length="4"/>
                <Extractor ref="normalized"/>
            </StringFunctionExtractor>
        </Aggregate>
    </Extractors>
    <!--Features extracted on a per-token basis-->
    <FocusFeatures>
        <!-- FOCUS TOKEN FEATURES -->
        <Feature name="focus_shape">
            <FocusIdentityContext/>
            <StringFunctionExtractor>
                <CapsFunction/>
                <Extractor ref="form_extractor"/>
            </StringFunctionExtractor>
        </Feature>
        <!-- AFFIX FEATURES -->
        <Feature name="focus_suffix">
            <FocusIdentityContext/>
            <Extractor ref="suffix"/>
        </Feature>
        <Feature name="focus_prefix">
            <FocusIdentityContext/>
            <Extractor ref="prefix"/>
        </Feature>
        <!-- COLLOCATIONAL FEATURES -->
        <Feature name="win_-2_pred">
            <CollocationalContext offset="-2"/>
            <Extractor ref="pred_conj"/>
        </Feature>
        <Feature name="win_-1_pred">
            <CollocationalContext offset="-1"/>
            <Extractor ref="pred_conj"/>
        </Feature>
        <Feature name="win_-2_-1_pred_form">
            <CollocationalContext offset="-2,-1"/>
            <PredictionExtractor/>
        </Feature>
        <Feature name="win_-2_pred_form">
            <CollocationalContext offset="-2"/>
            <PredictionExtractor/>
        </Feature>
        <Feature name="win_-1_pred_form">
            <CollocationalContext offset="-1"/>
            <PredictionExtractor/>
        </Feature>
        <Feature name="win_-2">
            <CollocationalContext offset="-2"/>
            <Extractor ref="win"/>
        </Feature>
        <Feature name="win_-1">
            <CollocationalContext offset="-1"/>
            <Extractor ref="win"/>
        </Feature>
        <Feature name="win_0">
            <CollocationalContext offset="0"/>
            <Extractor ref="win"/>
        </Feature>
        <Feature name="win_1">
            <CollocationalContext offset="1"/>
            <Extractor ref="win"/>
        </Feature>
        <Feature name="win_2">
            <CollocationalContext offset="2"/>
            <Extractor ref="win"/>
        </Feature>
    </FocusFeatures>
</ClassifierTemplate>
```
### Question Classification Example
**Question Classification Example**
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<ClassifierTemplate xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="ClassifierTemplate.xsd">
    <!-- Indicates the type of features to extract: "VECTOR" is used for everything besides DNNs which use "DNN" -->
    <ClassifierProperties instanceType="VECTOR"/>
    <!-- Specify tab-separated files here, in the format name<tab>value:
        STATE   Alabama
        STATE   Alaska
        ...
        COUNTRY United States of America
        COUNTRY USA
        COUNTRY Canada
        COUNTRY Mexico
    -->
    <Resources>
        <Resource key="word_lists" path="word-lists.txt"/>
        <Resource key="brown" path="brown-clusters.txt" reverse="1"/>
    </Resources>
    <!-- Define pre-processors here, such as gazetteers, which annotate incoming tokens with categories defined in a resource file. -->
    <Processors>
        <!-- Gazetteer processor, which uses a resource defined above. -->
        <GazetteerProcessor chunkType="IO">
            <!-- extractor that produces a string value for each token in the input to apply the gazetteer against -->
            <MapExtractor key="form"/>
            <!-- uses the resource "word_lists" defined above -->
            <Gazetteer resource="word_lists"/>
        </GazetteerProcessor>
    </Processors>
    <!-- You can define extractors here, which you can later refer to by the "name" attribute using "ref=...".
    This is useful if you reuse the same extractor over different contexts, so you don't need to keep re-defining them. -->
    <Extractors>
        <StringFunctionExtractor name="normalized">
            <SequentialFunction>
                <LowerCaseFunction/>
                <DigitNormalizingFunction/>
            </SequentialFunction>
            <MapExtractor key="lemma"/>
        </StringFunctionExtractor>
    </Extractors>
    <!-- Features extracted across the input sequence (e.g. sentence or utterance) -->
    <SequenceFeatures>
        <!-- unigram and bigram features -->
        <Feature name="unigram_form">
            <!-- context is the first field defined (here we are using 1-gram contexts, or "unigrams") -->
            <NgramContext length="1"/>
            <!-- the extractor is the second field. here we are referencing the predefined extractor "normalized"
            You could also define a new extractor here just for this context. -->
            <Extractor ref="normalized"/>
        </Feature>
        <Feature name="bigram_form">
            <NgramContext length="2"/>
            <Extractor ref="normalized"/>
        </Feature>
        <!-- question focus features: both of these use the question focus as a context,
        e.g. "which [president]..." or "what [country]"-->
        <Feature name="qf_form">
            <QuestionFocusContext/>
            <Extractor ref="normalized"/>
        </Feature>
        <Feature name="qf_list">
            <QuestionFocusContext/>
            <KeyPhraseExtractor>
                <MapExtractor key="form"/>
                <Gazetteer resource="word_lists"/>
            </KeyPhraseExtractor>
        </Feature>
        <!-- key phrase features over word lists. if a phrase in the provided list appears in the sequence,
        we extract the corresponding key as a feature -->
        <Feature name="key_phrase">
            <SequenceIdentityContext/>
            <KeyPhraseExtractor>
                <MapExtractor key="form"/>
                <Gazetteer resource="word_lists"/>
            </KeyPhraseExtractor>
        </Feature>
    </SequenceFeatures>
</ClassifierTemplate>
```
## Uploading Feature Templates
In the Annotate workspace in the Amelia Trainer pages of Amelia V3 administration pages, when the Train Intent Models panel is displayed, click the Use custom features toggle slider then click the folder icon to find then upload the feature template file.
# Test Feature Engineering Output
When a model is trained with the Annotate workspace and deployed with the Dashboard, click the Entities link or Intents link under the Amelia Trainer link to display the Entities or Intents workspace. At the bottom of the workspace is a simple test facility. Select the newly trained model from a dropdown list and enter sample utterances to confirm they trigger the new model.
{% /version %}
