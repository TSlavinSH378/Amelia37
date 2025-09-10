This exercise uses the FAQs and Manual to demonstrate how well Amelia uses these inputs to create a semantic memory.
1.  Upload the PDF manual
2.  Use the conversation area to test Amelia's knowledge of the PDF manual content
3.  Upload the FAQ Excel file
4.  Test Amelia's ability to clarify knowledge using FAQs and the PDF manual
# Manual
To demonstrate Amelia's semantic memory, begin by uploading only the manual. The PDF document has a number of unclear topics, for example, the possible outcomes of the Kobayashi Maru training test. However, if you ask her what is the Kobayashi Maru, she answers correctly, as shown below: it's a training exercise in a fictional universe. She'll also correctly tell you whether or not Captain Kirk took the test, how many times, and other basic questions.
Asking what are the possible outcomes of the training exercise, however, reveals she doesn't completely understand the question. The answer is in the Wikipedia text but it is obscured and garbled by other data of similar weight about the same topic. A real life example of a manual, of course, would have more focus and clarity.
Once the PDF manual is uploaded to Amelia's semantic memory, use the top right dropdown navigation links to select Mind and open a web browser tab with the main conversation area. If needed, click the Mind link at the top right of the conversation page to display the Mind panel with her internal processes.
Then click the Semantic Memory tab at the top right, as shown below. This displays a semantic memory workspace on the right side with a Debug area below. Click the plus sign at the top right of the Debug area to open it.
As questions and utterances from the conversation flow back and forth, each appears in the bottom of the Debug area with a plus sign on the far right. Click the plus sign to toggle the display of the Initial Context, Pre-Processors, and Sub-Systems used by Amelia to respond. Click on one of the three headings to displays its contents. The Debug area also can be scrolled to see all utterances.
![](attachments/28476795/28476796.jpg)
Figure. Mind Semantic Memory Workspace Using PDF Manual Only
In this example, the SemnetDoc semantic network sub-system is used repeatedly to answer questions instead of other systems Amelia uses.
> [!info]  
>
> The screen shot above shows results with only the sample manual PDF file uploaded. Adding the FAQ can and often will change Amelia's responses. The data set used to train Amelia should be checked frequently as data is added.

# FAQs
Finally, upload the FAQs Excel spreadsheet with questions and answers about the Kobayashi Maru training exercise. Once uploaded, ask Amelia questions from the FAQ spreadsheet as well as paraphrased versions of the questions. Adjust questions and answers as needed to cover the most common questions people might ask.
Also note the Debug information about sub-systems Amelia uses to answer FAQ questions. The FAQ sub-system is used to respond, not SemnetDoc. Also note the SemnetDoc response is accurate to some degree but includes extra characters. Amelia is able to choose the correct FAQ in her semantic memory despite a mostly accurate but incomplete response based on the uploaded manual.
![](attachments/28476795/28476797.jpg)
Figure. Mind Semantic Memory Workspace Using FAQs and Manual
