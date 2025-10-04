{% version "3.x" %}
Working with models requires juggling large amounts of precious and evolving data. To stay in control of this data and preserve any formatting, data must be managed and curated in a reasonably disciplined way. This avoids potential double work and time-consuming clean-ups. To work efficiently and smartly with this data, it's helpful to know a few techniques to search in the data and read it.
# Organization and Version Control
The data we use is distributed across various files. They should be organized in a sensible way that helps us keep the data clean, and allows us to cooperate on the data and maintain version control.
## Data Sets Organization
Data should be organized in a set of files to give a good overview of the data, indicate what utterance data a model is trained and validated with, and makes it easy to navigate inside the data.
This organization is crucial to analyze and understand the performance of an intent model. Because Amelia is not a data management application, this is typically best done outside Amelia. A simple file structure with three files each for training and validation works best.
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 15%" />
<col style="width: 20%" />
<col style="width: 64%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh" style="width: 87.0px">Training Data Files</th>
<th class="confluenceTh" style="width: 95.0px">Validation Data Files</th>
<th class="confluenceTh" style="width: 971.0px">Comment</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd" style="text-align: left; width: 87.0px;">Intent training data</td>
<td class="confluenceTd" style="text-align: left; width: 95.0px;">Intent Validation Data</td>
<td class="confluenceTd" style="text-align: left; width: 971.0px;">Because all intent data is labeled with the intent name, and easily organized within a single file, it makes sense to keep intent data in one place. Separate files for each intent can become unmanageable with dozens of files.</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: left; width: 87.0px;">Negative in-domain training data</td>
<td class="confluenceTd" style="text-align: left; width: 95.0px;">Negative in-domain validation data</td>
<td rowspan="2" class="confluenceTd" style="width: 971.0px"><p>Negative data does not have labels. There's no good way to distinguish in-domain data from out-of-domain data in a single file. To avoid mixing up in-domain and out-of-domain negative data, it's better to keep them in separate files.</p>
<p>There's a few reasons for this: First, parts of the in-domain negative data may at some point become intent data, if building out Amelia skills for those parts happens. It will be easier to locate in-domain negative data when it's not mixed up with all the out-of-domain negative data. Second, it can be useful to understand how the model performs on in-domain negative data compared to out-of-domain negative data. This is only possible if these two data sets are kept distinct and apart.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: left; width: 87.0px;">Negative out-of-domain training data</td>
<td class="confluenceTd" style="text-align: left; width: 95.0px;">Negative out-of-domain validation data</td>
</tr>
</tbody>
</table>
## Maintain Master Data Sets
Given the amount and delicacy of data, it's important to maintain master files. A high risk of confusion is possible if versions of data exists in various places, circulating as attachments between various team members. A git repository or source control works best with a structured process to change data contents.
## Version Control of the Data and Models
Always keep prior versions of data available. This can be to compare our current data with the data of a former iteration or to roll back to a former iteration in case mistakes are made or change decisions reversed. As with organizing data sets, this is most efficiently done outside Amelia, ideally in a git repository.
-   Maintain versions of at least every data iteration that results in an updated intent model. This ensures versions are saved with reasonable frequency with the ability to trace exactly what data went with what version of a model.
-   Also maintain the content of any file in alphabetical order. It's easier to get an overview of the content of the file, especially an intent file with labels. It also simplifies comparisons across different versions of the same file.
-   Save trained models. Because models are saved in Amelia, it is not necessary to save models outside Amelia unless all files are stored in one place. In that case, export each trained model from Amelia.
# Content Management
Inside individual data files, it's important to see a high level view of the file data, scan data efficiently, and make edits to the data. This should be done with high efficiency and low risk of breaking the data formatting.
## Text Editors vs Spreadsheets vs Data Management Tools
It can be up to personal preference what application best serves those purposes. Usually it comes down to either a text editor (Notepad++, Sublime, etc), a spreadsheet (Microsoft Excel, Google Sheets) or in some cases a dedicated data management tool.
### Text Editors
Text editors are designed to understand large amounts of structured text easily, search and replace within the text, and reorganize it. Although model data files aren't as structured as lines of code, they still are structured files organized around lines and tab separation.
So for reading, analyzing and changing data, text editors have a number of tools to work efficiently on the data. In the screenshot below, notice how the Sublime text editor color coded the columns in the file (based on tab separation), aligned the columns (based on tab separation), and highlighted the rows containing the search term visa in the third column (using a regex search).
![](attachments/20808369/20808712.png)
### Spreadsheets
Spreadsheets are also designed for structured data but primarily for numbers and smaller chunks of text, and with a focus on performing actions based on relations between cells (like calculating). In terms of reading, analyzing, and changing data, spreadsheets are arguably inferior to a text editor.
For annotation and filtering purposes, however, spreadsheets can be preferable. Spreadsheets allow data validation and auto-complete. For example, with a set of 200 utterances that needs annotation, misspellings can be eliminated by validating against a list intent labels, in combination with auto-complete, reducing the need to type out the entire label. Filtering is of course a core functionality in any spreadsheet.
That said, text editors can do auto-complete by tabbing out strings and a regex search in a text editor can filter out whatever is needed in text editors.
### Data Management Tools
Data management tools like [OpenRefine](http://openrefine.org/) are tailor-made for various forms of data management. These often require more effort to use out-of-the-gate, as there's a learning process for understanding how to use them. Once familiar with them though, they can be powerful tools.
## Preserving and Checking Formatting
When data sets are uploaded in Amelia, they are read based on formatting rules. For intent data, this formatting is the tab separation between the intent label and the utterance, as well as in line breaks. If data sets that don't follow these rules, for example with an extra tab or a wayward line break, they won't work. Working with data will sometimes accidentally break the data in this way. To check the formatting of an intent file, regex search in a data file:
``` groovy
^\w+\t[^\t]+$
```
The number of hits for this search should match the number of lines in a file. If it doesn't it usually means a tab is missing or there is a tab too many on some line. If so, search a bit up and down the doc, to find out where the hit number doesn't match the line number to find the culprit.
This searches for double line breaks and should have zero matches. If there are any matches, check it out and remove the excess line break.
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
