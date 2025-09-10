The Semantic Documents workspace is available through the Semantic Memory link on the left side of Amelia's administration pages and the Semantic Documents link. The workspace includes space to specify the type of file, upload a file, and a list of previously uploaded files. Files uploaded display status, a green check mark or rotating circular arrow, and links to download or delete the file. A domain can be selected with a dropdown list at the top right of the interface, next to the navigation links.
![](attachments/28476789/28476790.jpg)
Figure. Semantic Memory Workspace
# Add to Amelia's Semantic Memory
Uploaded files can be in Excel XLSX (FAQs, Intent FAQs, Query Maps) or PDF (Manual) formats.
1.  Log in to the Amelia V3 administration pages and click Semantic Memory on the left navigation links.
2.  Click the Semnet Documents link under the Semantic Memory link. The workspace appears on the right side of the page. If needed, click the domain dropdown at the top right of the interface, next to the navigation links.
3.  In the workspace, select the document Type and the Replacement Policy in case the document file name already exists, Merge or Replace data.
4.  Click the folder icon upload button on the right side, then browse and select the file to upload.
5.  Click the Open button in the File Explorer to select the file. The file will be uploaded and processed into Amelia's memory. In the Status area to the right of the file details, a rotating circular arrow displays when the file is being processed. A green check mark appears when the file has been processed.
# Semantic Documents Examples
Amelia works with four types of content, frequently asked questions (FAQs), well curated documents called manuals, Intent FAQs, and Query Maps. These examples describe how to create the content to upload into Amelia's semantic memory.
## FAQs
In Amelia V3, FAQ files include two columns, the left column for the word Question or Answer and a second column with the question or answer utterance. Heading columns are not used. The file should include up to 10 but ideally 5 multiple paraphrases for questions and answers. Fewer questions are needed than in Amelia V2 because of her new paraphrase capabilities. FAQ files are saved in Excel XLSX format.
These sample FAQs clarify a few key points left unclear in the Manual example below. Note the different uses and placements of the words test, exercise, results, outcomes, and training in some questions and answers.
[Download Sample FAQ Excel File](attachments/11939867/11939872.xlsx)

|  |  |
| ----|----|
| Question | What are Klingons? |
| Question | Are Klingons dangerous? |
| Question | Do Klingons not hurt people? |
| Question | Are there peaceful Klingons? |
| Question | Would the Klingons let anyone rescue the Kobayashi Maru? |
| Answer | Klingons are dangerous members of a warlike humanoid alien species in the TV series Star Trek |
| Question | What are the possible outcomes of the Kobayashi Maru test? |
| Question | Is there any way to win the Kobayashi Maru training exercise? |
| Question | What happens if I try to rescue the Kobayashi Maru? |
| Question | What happens if I don't rescue the Kobayashi Maru? |
| Answer | There are two possible outcomes, the Kobayashi Maru is abandoned and lost or a rescue fails |
| Question | What is the purpose of the Kobayashi Maru exercise? |
| Question | What do people get from going through the training exercise? |
| Question | How are the results of the Kobayashi Maru training test used? |
| Answer | The exercise is a test of how people deal with failure in a no-win scenario. |

## Manuals
The ability to upload unstructured content into Amelia's memory is a new V3 feature. She processes well-curated information into a searchable resource to answer questions. The information may require editing and transformation to clarify key points. Images and tables, for example, currently cannot be read. Information can include many different sources, from Wikipedia to blog articles to procedure manuals, and much more. Manuals need to be in PDF format for uploading. For example, Microsoft Word can print to PDF files.
The sample manual is a lightly edited Wikipedia entry about a training exercise called the Kobayashi Maru from an episode in the Star Trek II: Wrath of Khan movie.
[Download the Sample PDF Manual](attachments/11939867/11939871.pdf)
## Intent FAQs
Intent FAQs are similar to FAQs with the ability to add an intent identifier to allow training a classifier model with the Amelia Trainer tools. The annotation framework may yield better results than the methods used to process FAQs, depending on the training corpus.
Once uploaded, each intent is created in the Intents page using the identifier specified in the Intent FAQs Excel file. Each question in the file also is added as a user utterance for each intent with the answer added as an Amelia utterance used in her conversation. A classifier model needs to be trained, using all the intents, then deployed for an intent FAQ to work.
Intent FAQ Excel files have three columns, a question or answer in the first left hand column, the question or answer in the center column, and the intent name as an identifier in the right side column.
[Download a Sample Intent FAQ Excel File](attachments/11939867/11939877.xlsx)

|  |  |  |
| ----|----|----|
| Question | What technology does Amelia use? | how_work |
| Question | What systems do you rely on to drive your decision making? |  |
| Question | How does your brain process information? |  |
| Question | How does your cpu brain deal with information? |  |
| Question | Can you explain Amelia's brain to me? |  |
| Answer | My brain operates using supervised learning, which ensures the error rate is minimal, and I am only doing things I am taught to. |  |
| Question | Would Amelia be classified as a chatbot? | chatbot |
| Question | Is Amelia a chatbot or a virtual assistant? |  |
| Question | Can Amelia be a chatbot? |  |
| Question | Can Amelia be used as a chatbot? |  |
| Answer | I prefer to introduce myself as a cognitive virtual agent. While chatbots use scripted dialog or recognized commands, I am a conversation driven AI solution able to integrate with complex systems and keep up with a natural human language at the same time. |  |
| Question | How different are you from other bots? | different |
| Question | How are you unique? |  |
| Question | What makes you different from other virtual agents? |  |
| Question | What distinguishes you from other AI assistants? |  |
| Answer | Other virtual agents struggle with context and can only process simple, short sentences. I can run business processes, monitor human emotional cues, and conduct multi-turn, non-scripted dialogues. |  |

## Query Maps
A query map uses labeled columns in an Excel file to provide answers Amelia can use to query data. For example, someone might ask what were the total current assets in 2017 and Amelia would use the query map to look up the answer.
[Download a Sample Query Map Excel File](attachments/11939867/11939875.xlsx)
![](attachments/28476789/28476791.png)
Figure. Example Query Map Excel File
