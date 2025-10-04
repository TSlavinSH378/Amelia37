{% version "3.x" %}
Amelia's utterances can be annotated for style and speech, for example, highlighting with bold part of an utterance or changing the pitch. This feature applies to BPN Say and Ask tasks, response pools, entities, and Answer FAQs. The tool appears with a right mouse-click after a cursor is positioned in an edit field or text is highlighted. See the Annotation Editor Interfaces section below for details about annotation editor settings.
# Ask and Say Tasks
With an Ask or Say task, double-click the task to open then highlight a portion of text then right mouse-click to open the annotation tool. For Ask tasks, the double quote marks cannot be annotated, only content in between.
![](attachments/11940946/11942763.png)
Figure. Annotation Tool for Ask or Say Tasks
See the Annotation Editor Interfaces section below for details about annotation tool settings.
# Entity Amelia Asks Utterances
With the Amelia Asks utterances, included as part of an entity, click the pencil icon to the right of the utterance to display the question in an edit field. Highlight all or part of the question then right mouse-click to open the annotation tool.
![](attachments/11940946/11942766.png)
Figure. Annotation Tool for the Amelia Ask Utterances
See the Annotation Editor Interfaces section below for details about annotation tool settings.
# Edit an Annotation
Open a BPN Say or Ask task, response pool, entity, or Answer FAQs with an annotation. Position the cursor in annotated text then right mouse click to display the edit menu. Click Edit Annotation to display the Annotation Editor popup.
![](attachments/11940946/11942774.png)
Figure. Annotation Edit Menu
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

{% /version %}
