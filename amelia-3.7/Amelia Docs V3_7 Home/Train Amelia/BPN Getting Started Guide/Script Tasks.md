-   [Script Task BPN and Console Interfaces](#ScriptTasks-ScriptTaskBPNandConsoleInterfaces)
    -   [Script Task Icons](#ScriptTasks-ScriptTaskIcons)
    -   [Script Editor](#ScriptTasks-ScriptEditor)
    -   [Check the Syntax of a Script Task](#ScriptTasks-ChecktheSyntaxofaScriptTask)
-   [Send Integration Messages with a Script Task](#ScriptTasks-SendIntegrationMessageswithaScriptTask)
-   [Scripting Services](#ScriptTasks-ScriptingServices)
-   [Script Library Workspace](#ScriptTasks-ScriptLibraryWorkspace)
-   [Best Practice Error Catching](#ScriptTasks-BestPracticeErrorCatching)
-   [Advanced Variable Usage](#ScriptTasks-AdvancedVariableUsage)
-   [Reference Documents](#ScriptTasks-ReferenceDocuments)
-   [FreeMarker to Display Dynamic Data](#ScriptTasks-FreeMarkertoDisplayDynamicData)
    -   [Create a Bucket in Process Memory](#ScriptTasks-CreateaBucketinProcessMemory)
    -   [Create the HTML Template](#ScriptTasks-CreatetheHTMLTemplate)
    -   [Create a BPN](#ScriptTasks-CreateaBPN)
        -   [Create the BPN](#ScriptTasks-CreatetheBPN)
        -   [A Script to Generate Data for Template](#ScriptTasks-AScripttoGenerateDataforTemplate)
        -   [Interact with Amelia](#ScriptTasks-InteractwithAmelia)
-   [Tabular Data Sources](#ScriptTasks-TabularDataTabularDataSources)
    -   [File Rules](#ScriptTasks-FileRules)
    -   [File Content Rules](#ScriptTasks-FileContentRules)
    -   [Upload a Data Source](#ScriptTasks-UploadaDataSource)
    -   [Edit Tabular Data](#ScriptTasks-EditTabularData)
    -   [Query Tabular Data](#ScriptTasks-QueryTabularData)
        -   [Query Operator](#ScriptTasks-QueryOperator)
        -   [Conditional Operators](#ScriptTasks-ConditionalOperators)
        -   [Ordering Tabular Data Queries](#ScriptTasks-OrderingTabularDataQueries)
        -   [Return Value Operators](#ScriptTasks-ReturnValueOperators)
        -   [Evaluating Output](#ScriptTasks-EvaluatingOutput)
    -   [Create a BPN](#ScriptTasks-CreateaBPN.1)
        -   [Upload Tabular Data](#ScriptTasks-UploadTabularData)
        -   [Create a Slot Entity](#ScriptTasks-CreateaSlotEntity)
        -   [Create the BPN](#ScriptTasks-CreatetheBPN.1)
        -   [A Script to Retrieve Tabular Data](#ScriptTasks-AScripttoRetrieveTabularData)
        -   [Interact with Amelia](#ScriptTasks-InteractwithAmelia.1)
Script tasks allow complex functions and processes to be executed during a BPN process in a conversation. Two languages are currently supported: Groovy and Javascript.
In the scope of the script task, the execution object allows for interaction between the BPN and the script through the methods getVariable and setVariable. As the supported scripting languages are compliant with the [JSR-223 specification](https://www.jcp.org/en/jsr/detail?id=223), converting the example provided in Groovy to JS is a fairly simple task.
# Script Task BPN and Console Interfaces
Script tasks use the task icons to define the script and access the script editor.
## Script Task Icons
Within the BPN workspace, click once on a Task to display the task tool icons, as shown below.
![](attachments/11939477/25461131.jpg)
Figure. Basic BPN Task Tools to Create Script Tasks and Set Properties
The Change Task Type wrench icon sets the type, Task or Script.  To create a Script task, click the wrench icon and select Script Task.
The Edit Script document icon opens a script editor where scripts can be written in Groovy or JavaScript. When a Task is selected, click the Properties Panel to toggle display of configuration options based on the task.
## Script Editor
When the Edit Script icon is clicked, the Script Editor appears.
![](attachments/11939477/11939478.png)
Figure. Script Editor Interface
The Script Editor is a text editor with a number of features to write and test code.
Table. Script Editor Interface Elements

| Element | Description |
| ----|----|
| Save | This button toggles on and off, active and inactive, based on whether or not changes have been made in the Text Editor. |
| Check Syntax | When clicked, the Console at the bottom of the editor displays a pass or no pass message with details. |
| Language | Select Groovy or JavaScript. Groovy is enabled by default. JavaScript is enabled by setting the amelia.bpn.scripting.javascript.enabled=true in both the amelia-engine-service and amelia-admin-web file files. |
| Import User Libraries | Select one or more script libraries created with the Script Library in the Process Memory administration pages.Scripts display based on the Language selected, Groovy or JavaScript.
When a script is selected for import, the script name appears below the dropdown list. To remove a selected script to import, click the x next to the script name. |
| Text Editor | Type code in the center area with numbered lines. |
| Console | Displays results of clicking the Check Syntax button, either Syntax check passed or detailed message(s). |
| Save and Close | Click to save and close the Script Editor |
| Close | Click to close without saving edits. |

## Check the Syntax of a Script Task
To check the syntax of a Script task, click the Check Syntax button near the top of the editor. The results display in the Console area at the bottom of the editor, either *Syntax check passed* or detailed messages.
# Send Integration Messages with a Script Task
Prior to Amelia 3.6, a Send task conveyed a data payload to Amelia’s user interface, for example, to display data in a chat note. The syntax was send the integration message payload_var_name.
The new messageService eliminates the need for a Send task. A Script task builds the payload, as before, then the sendIntegrationMessage method sends the data to the user interface.
``` groovy
def buildIntegrationMessage() {
    return sectionBuilder.create()
      .title("Address #1")
      .name("address_1")
      .addSubSection()
        .title("Mailing Address")
        .name("mailingAddress")
        .newSectionField()
          .name("line1")
          .value("40 Wall Street")
          .label("Street")
          .backToSection()
      .backToParentSection()
      .build()
}
def payload = buildIntegrationMessage()
messageService.sendIntegrationMessage(payload.toJsonString())
```
# Scripting Services
Amelia V3 includes scripting services to handle variables, log data, create multimedia objects, retrieve conversation data, and other tasks. Services are available from Script tasks and the Script Library. The [Services](Services) pages describe most or all of these services.
Table. Scripting Services

| Service/Object | Handle | Description |
| ----|----|----|
| Content management service | cmService | BPN script tasks and libraries can manipulate assets of Amelia's content manager. |
| Context service | contextService | Exposes operations for accessing slots, intents, and other items of current context. |
| Conversation service | conversationService | Exposes conversation-related operations. |
| Escalation Queue service | escalationQueueService | Exposes operations associated with the agent information of a given escalation queue. |
| Execution | execution | Current process instance and respective convenience operations. |
| Form input data builder | formInputDataBuilder | BPN script tasks/libraries construct form input data for the custom UI. |
| Integration message section builder | sectionBuilder | BPN script tasks/libraries construct integration message data for custom UI. |
| Integration Service | integrationService | Provides integration flow related operations to BPN script tasks and libraries. |
| Logging service | log | Script task/library friendly logger. Events supposed to be appended to application's log/relayed to section of Mind. |
| Message Service | messageService | Message related operations |
| Quantity service | quantityService | Normalization/formatting operations. |
| Tabular data service | tabularDataService | Script tasks/libraries manipulate & query tables uploaded as CSV. |
| Text service | textService | Text manipulation and matching operations not available in Groovy/JavaScript scripting engines. |
| Transient variable service | transientVariableService | Allow script tasks and libraries to manipulate transient variables. |
| User service | userService | Extract user data associated with the current conversation. |

# Script Library Workspace
Amelia V3 includes the ability to share scripts used by script tasks in multiple BPN models within a domain. To access the script library workspace, click the Process Memory link on the left side of Amelia administration pages then click Script Library. A script editor appears in the Scripts workspace.
Scripts can be saved in the Script Tree folders on the left side of the Scripts workspace. Any script created in the workspace for a specified domain is available to any Script task in any BPN in the domain. And scripts in the library can be imported into other library scripts.
To add a script or folder in the Scripts workspace, right mouse-click over the Root folder or any subfolder and select Add Folder, Add Script, Rename Folder, or Delete Folder. To open, rename, or remove a script, right mouse-click over the script and select Open, Rename, or Remove.
Math and other Groovy or JavaScript libraries can be stored in the script library and work similar to importing libraries in scripts. To use a method for these libraries, directly call the method with the required parameters.
> [!warning]  
>
> Strings must be escaped with single quotes, not double quotes, in the script editor.
> [!info]  
>
> Always test before using a BPN that uses a script library. The script libraries may have been modified. If a script library is modified, the linked BPNs need to be tested and modified as needed. 

![](attachments/11939477/25461130.png)
Figure. Script Library Workspace
Table. Script Library Workspace Elements

| Script Library Workspace Element | Description |
| ----|----|
| Top Navigation | Click tabs to Save a script or Check Syntax of a script and display results in Console below. Scripts also can be imported from files or exported as files. |
| Language | Groovy is the default language. |
| Import User Libraries | Click to display then select from a dropdown list of shared scripts. |
| Code Editor | Includes syntax highlighting and line numbers. |
| Console | Check Syntax results display here. |
| Script Tree | Displays the folders and scripts. Double-click a folder or script name to display folders and models. Click the Script Tree title to toggle the area open or closed. Search script or folder names with the Search box at the top of this area. |

# Best Practice Error Catching
Remember to catch your errors, and even present them as a variable available within the BPN process.
``` bash
try {
    //your script code here
} catch (Exception e) {
    def script_error = e.getMessage()
    log.error(execution, script_error)
    execution.setVariable("script_error", script_error)
}
```
# Advanced Variable Usage
To create complex objects with Groovy with access through EL (Java EE 6: Expression Language) in a BPN, create a map object or array using Groovy in a Script Task and then export this map object or array as a variable in your workflow.
**Script Task (Groovy)**
``` groovy
def theMap = [color: "red", type: "golf-cart", id: "ABC123"]
def theList = ["abc123", "xyz123", "def456"]
execution.setVariable("vehicleABC", theMap)
execution.setVariable("idList", theList)
```
Access these objects in in BPN tasks as shown in the table below.  This is useful if there are a large number of values linked to a single item and you want to access them using attributes rather than create a large number of individual variables. It is also possible to use arrays in a similar fashion. This is especially convenient with a looping flow to iterate over a list.  Use the counter variable name in place of a numerical index.
Table. Example Usage of Advanced Variables
|                                    |           |                                                                              |                                             |
|------------------------------------|-----------|------------------------------------------------------------------------------|---------------------------------------------|
| Purpose                            | Task Type | Task Text                                                                    | Amelia Display Output                       |
| Access attributes in a map         | Say       | say "My vehicle is the color ${vehicleABC\['color'\]}"                       | "My vehicle is the color red"               |
|                                    | Say       | say "The vehicle is a ${vehicleABC\['type'\]} with id ${vehicleABC\['id'\]}" | "The vehicle is a golf-cart with id ABC123" |
| Access values in a list            | Say       | say "Available id's are ${idList\[0\]}, ${idList\[1\]} and ${idList\[2\]}"   | "Available id's are abc123 xyz123 def456"   |
| Use a counter variable as an index | Set       | set the variable counter to 0                                                | "The first id is abc123"                    |
|                                    | Say       | say "The first id is ${idList\[counter\]}"                                   |                                             |
# Reference Documents
-   Groovy: <http://groovy-lang.org/single-page-documentation.html>
-   JavaScript (Rhino): <https://developer.mozilla.org/en-US/docs/Mozilla/Projects/Rhino/Documentation>
-   JSR 223 Specification: <https://www.jcp.org/en/jsr/detail?id=223>
# FreeMarker to Display Dynamic Data
Amelia V3 includes a template engine that enables her to present dynamically generated content within the conversation area. The template is created and stored in a Process Memory bucket and holds layout code. A BPN generates data dynamically and makes it available as one or more variables for use within the HTML template.
The template engine is Apache FreeMarker, a Java library to generate text output based on templates and dynamic data.  Templates are written in FreeMarker Template Language (FTL), a simple specialized language. Data is created with a full featured language. Output can be HTML web pages, emails, configuration files, source code, and so on. More information about FreeMarker is at [http://freemarker.org](http://freemarker.org/).
This demonstration creates a Process Memory bucket, an HTML template resource, and a BPN to integrate data dynamically with the HTML template resource.
## Create a Bucket in Process Memory
1.  In the Amelia V3 administration pages, click Process Memory then the Content Management link. The Buckets workspace appears. If necessary, click the domain dropdown list at the top right and select a domain.
2.  Click the Create button near the top left of the workspace. The Create New Bucket popup appears.
3.  Type newbucket for the name, lower case. Click Create to create then save a new bucket.
4.  Click newbucket in the list of buckets in the workspace. The newbucket page appears.
## Create the HTML Template
1.  Click the Create Document button near the top of the newbucket page. The Create New Document popup appears.
2.  Type htmlPage for the name. Click Create to create then save a blank HTML file.
3.  Click htmlPage in the list of document names. The HTML editor page appears.
4.  Copy then paste the FreeMarker template code below into the HTML editor. Click Save to save the htmlPage resource.
Note the variables *nameOfUser* and *users* in the template code are created in the BPN script task, as described below. The #if and #list code are examples of FreeMarker directive code.
``` xml
<p>Hello Welcome ${userName}&nbsp;<#if userName=='Your Name'>, this conditional works</#if></p>
<p>${userName}</p>
<table border="1" cellpadding="1" cellspacing="1" style="width:500px">
<thead>
<tr>
<th scope="col">Name</th>
<th scope="col">Age</th>
<th scope="col">Job Title</th>
</tr>
</thead>
<tbody><#list users as user>
<tr>
<td>${user.name}</td>
<td>${user.age}</td>
<td>${user.jobTitle}</td>
</tr>
</#list>
</tbody>
</table>
```
## Create a BPN
Once the Process Memory bucket and htmlPage resource template are created, the next step is to create a BPN to generate data for the template.
![](attachments/11939477/25461133.png)
Figure. showFreeMarker BPN
### Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it showFreeMarker. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Generate/Integrate Data for FreeMarker Output

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started! | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | generate data for templates | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | present htmlPage.html from newbucket | integrates output from Step 3 with the htmlPage resource template in the newbucket bucket |
| 4 | say goodbye | exit the BPN |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
### A Script to Generate Data for Template
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above. The two variables set – *userName* and *users* – are used in the htmlPage FreeMarker template to provide data for display in the template.
``` groovy
def userName = execution.userDisplayName();
def users = [];
for (def i = 0; i < 10; i++) {
    def tempUser = ['name': 'user'+i, 'age': i+20, jobTitle:'JobTitle'+i];
    users.push(tempUser);
}
execution.setVariable('userName', userName);
execution.setVariable("users", users);
```
### Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the showFreeMarker workflow by typing this command in the chat interface:
    ``` bash
    run the workflow showFreeMarker
    ```
3.  Amelia displays user data within the FreeMarker template.
# Tabular Data Sources
Amelia V3 includes the ability to provide BPNs with data in CSV table format for quick searches to retrieve data. For example, postal code data or details about insurance plans. The tabular data is stored in Amelia's database but exists apart from her natural language processing and other features.
![](attachments/11939477/11942865.jpg)
Figure. Tabular Data Workspace
Table. Tabular Data Workspace Elements

| Element | Description |
| ----|----|
|  | Click to download the tabular data file. |
|  | Click to delete the tabular data file. |
|  | Click to display all data from the file, including both meta data and file data with the ability to edit file name, domain, and column data types. |
|  | Click to edit the tabular data file. Opening a file to edit starts a fifteen minute clock countdown that locks the file from editing by others. |
|  | Click to replace the tabular data file with a new uploaded file. This button opens a popup to upload a file that will overwrite and update the existing tabular data file. |

## File Rules
-   The size of the file should not exceed 20 MB
-   The file should not be a corrupted file
-   The file size should be more than 0 bytes
-   The name of the file should be unique with respect to existing tables per domain
-   If you have an Excel file, please save it as a (comma\|tab\|semi-colon\|pipe) separated file before uploading
## File Content Rules
-   The file should contain data, a blank file would not be uploaded
-   Headers for columns are mandatory
-   There should exist at least one row other than the header row in the file
-   The number of delimiters in each row should be the same
-   In cases where your data contains a delimiter, please either remove the delimiter or qualify those values with a text qualifier (single-quote\|double-quote)
-   Do not explicitly add double/single quotes to String related columns. The service can identify the type of the columns based on the data contained
-   Each column has data of same type. Example: If the first row has data of type Integer, please make sure that all the following rows have Integer data for that column
-   Empty fields in the first row would be treated as String type. Please make sure that your first row is completely populated
-   Character support - UTF-8
-   No two columns should have the same name
## Upload a Data Source
To manage tabular data, click the Process Memory link in Amelia's administration pages, click the Tabular Data link to display the Tabular Service workspace. Data sources are listed by domain. To upload a data source, click the Import new file button at the top right of the workspace. The import file wizard appears.
> [!warning]  
>
> Tabular data files upload to the domain selected at the top right of the interface. Confirm the correct domain is selected.

The first step is to select the data source file to upload. Upload a file then click the Next button to continue.
![](attachments/11939477/11939485.png)
Figure. Step 1 of Tabular Data Import File Wizard
The second step is to select the delimiter used in the file (Comma, Tab, Semi-Colon, Pipe), and any single quote or double quote text qualifier used to identify text entries in the file. Click the Next button to continue.
![](attachments/11939477/11939486.png)
Figure. Step 2 of Tabular Data Import File Wizard
The third step is to validate the column types, for example, Integer, Double, or String. Click the Next button to continue.
![](attachments/11939477/11939487.png)
Figure. Step 3 of Tabular Data Import File Wizard
The fourth and final step is confirm the summary and click the Okay button to upload the data source file.
![](attachments/11939477/11939488.png)
Figure. Step 4 of Tabular Data Import File Wizard
Invalid files are deleted from the database. Use the error message(s) to correct the file and upload again.
## Edit Tabular Data
In the Tabular Data workspace, visible after clicking Process Memory link then the Tabular Data link, click the Edit Data note icon to the far right of a data source listing. The Edit Tabular Data workspace appears. Opening a file to edit starts a fifteen minute lock process to edit the file. Click the Add New Row, Undo Changes, or Finish Editing buttons as needed.
![](attachments/11939477/11939490.png)
Figure. Edit Tabular Data Workspace
## Query Tabular Data
Amelia V3 provides a flexible and dynamic expression language to create complex queries on the fly to query the tabular data table. The language uses a syntax that follows Fluent interface to promote readability of the queries and ease of use. Read more about Fluent interface here at Wikipedia: <https://en.wikipedia.org/wiki/Fluent_interface> and Martin Fowler's website: <https://martinfowler.com/bliki/FluentInterface.html>.
### Query Operator
For Script tasks, the query operator is most commonly used. The query operator takes a minimum of one parameter, the name of the table to query. Following the table name, one can append any number of legit column names separated with a comma. These column will be the ones that are eventually projected.
    tabularDataService.query('tableName', 'columnName1', 'columnName2', ...)
> [!warning]  
>
> The default name of the table is the same as the name of the file uploaded to the admin portal. The table name can be changed at a later point and that name used to query the tabular data entity.

Query operators also can append conditional and ordering operators to filter and organize results available within a Script task.
**Tabular Service Query Example**
``` java
tabularDataService.query('realestate','beds','baths')
    .is('beds','2')
    .isNot('baths','1')
    .in('type','Condo','Residential')
    .sortAsc('beds')
    .sortDesc('baths')
    .first()['baths']==2
```
### Conditional Operators
The operations supported by the tabular service have been derived from the generic operations that are typically performed using Filters in an Excel sheet or in SQL queries. Also note empty parameters in a query can cause execution errors.
Table.  Tabular Data Conditional Operators

| Query Operator | Description |
| ----|----|
| is | The is operator is similar to an equals operation and it takes two parameters.;
The first parameter is the column name you want to compare the value in and the second parameter is the value itself. |
| isNot | The isNot operator is similar to a not equals operation and it takes two parameters.;
The first parameter is the column name you want to compare the value in and the second parameter is the value itself. |
| in | The in operator is similar to the IN operation in SQL and it takes a minimum of two parameters.;
The first parameter is the column name you want to compare the value in. There can be any number of parameters following the first parameter. 
All the rows that satisfy at least one parameter would be returned. |
| notIn | The notIn operator is similar to the NOT IN operation in SQL and it takes a minimum of two parameters.;
The first parameter is the column name you want to compare the value in. There can be any number of parameters following the first parameter. 
All the rows that satisfy at least one parameter would be returned. |
| isGt | The isGt operator is similar to the '>' operator in most programming languages and it takes two parameters.The first parameter is the column name you want to compare the value in and the second parameter is the value itself. |
| isGte | The gte operator is similar to the '>=' operator in most programming languages and it takes two parameters.The first parameter is the column name you want to compare the value in and the second parameter is the value itself. |
| isLt | The less operator is similar to the '<' operator in most programming languages and it takes two parameters.The first parameter is the column name you want to compare the value in and the second parameter is the value itself. |
| isLte | The lte operator is similar to the '<=' operator in most programming languages and it takes two parameters.The first parameter is the column name you want to compare the value in and the second parameter is the value itself. |
| like | The like operator is similar to the like operator in used in SQL queries. The function takes only two parameters and can only compare one value at a time. The first parameter to the function is the column name you want to compare the value in adn the second parameter is the String value itself.Two wildcareds are supported while comparing the values, '%' (percent) for any characters and '?' (question mark) for matching one value at the character positiion.Examples: like("appName", "bitlocker%")
like("appName", "bitlocker")
like("appName", "bitlock?r") |
| likeAny | The likeAny operator is similar to the like operator and can be used to compare String values. The function takes at least two parameters and can compare multiple values at the same time. The first parameter to the function is the column name you want to compare the value in and the all parameters following are the String values.Two wildcareds are supported while comparing the values, '%' (percent) for any characters and '?' (question mark) for matching one value at the character positiion.Examples: like("appName", "bitlocker%", "windows", "?p", "ameliav3.2")
like("appName", "bitlocker")
like("appName", "bitlock?r") |
| sortAsc | The sortAsc operator sorts the column passed as parameter in ascending order. |
| sortDesc | The sortDesc operator sorts the column passed as parameter in descending order. |

**Tabular Service Query Example**
``` java
tabular:query('realestate','beds','baths')
    .is('beds',2)
    .isNot('baths',1)
    .in('type','Condo','Residential')
    .sortAsc('beds')
    .sortDesc('baths')
    .first().get('baths')==2
```
### Ordering Tabular Data Queries
The output can be ordered ascending and descending by columns, much similar to SQL order by operation. Two operators, sortAsc and sortDesc are provided for the same.
In order to sort multiple columns in sequence (in different sort order), write the sortAsc and sortDesc queries one after another with column names specified. The service will execute the commands sequentially and hence sort accordingly.
**Tabular Service Query Example**
``` java
tabular:query('realestate','beds','baths')
    .is('beds',2)
    .isNot('baths',1)
    .in('type','Condo','Residential')
    .sortAsc('beds')
    .sortDesc('baths')
    .first().get('baths')==2
```
 In this example, the table realestate is sorted first by beds in ascending and then by baths descending.
### Return Value Operators
Table. Tabular Data Return Value Operators

| Return Operator | Description |
| ----|----|
| first | Returns the first row that satisfies the query criteria. |
| last | Returns the last row that satisfies the query criteria. |
| list | Returns all the rows that satisfy the query criteria. |
| first(N) | Returns the first N rows that satisfy the query criteria. N should be an integer. |
| last(N) | Returns the last N rows that satisfy the query criteria. N should be an integer. |
| index(N) | Returns the row at index N out of rows that satisfy the query criteria. N should be an integer. |

Array notation can be used to access the values provided by the queries to the evaluation criteria. The table name for querying is the same as the name of the file uploaded unless it is changed explicitly.
**Tabular Service Query Example**
``` java
tabular:query('realestate','beds','baths')
    .is('beds',2)
    .isNot('baths',1)
    .in('type','Condo','Residential')
    .sortAsc('beds')
    .sortDesc('baths')
    .first()['baths']==2
```
### Evaluating Output
Tabular data query output values can be accessed with array notation. Also note the table name to query is the same as the name of the uploaded file.
## Create a BPN
This exercise describes how to use Tabular Data and queries as part of a BPN process.
![](attachments/11939477/11939499.png)
Figure. movieCosts BPN Model
### Upload Tabular Data
From the Amelia V3 administration pages, click the Process Knowledge link and then the Tabular Data link.
1.  Click the Upload icon at the bottom right of the import file wizard, above the inactive Next button. Upload the [moviecosts.csv](attachments/11939477/11939498.csv) file.
2.  Select the Domain from the dropdown list in the Domain Selection of the wizard. The green Next button becomes active.
3.  Click the green Next button to import, validate, and process the tabular file. The results display on the next screen.
4.  Click the green Finish button to upload the file.
Invalid files are deleted from the database. Use the error message(s) to correct the file and upload again.
If you have questions, for example, about file format, refer to the [Tabular Data section](https://docs.ipsoft.com/display/AmeliaDocsV3/Script+Tasks#ScriptTasks-TabularDataSources) directly above.
### Create a Slot Entity
The first step is to create a slot entity called *cost*. From the Amelia V3 administration pages, click the Amelia Trainer link on the left navigation and the Entities link under it. The Entities workspace appears. Select the domain, located at the top left near the logo, then in the top section of the workspace fill out name and code as *cost*, with Datum Type as Integer, and a short description. Click the Add New Entity button to save.
When the new entitiy appears in the middle section of the Entities workspace, in a list, click the edit icon to the left of the icon name. The entity detail page appears. In the Questions input field at the bottom left of the Entity Overview page, type in a question, for example, How much do you want to spend on a movie? Click the Add button to add and save the question. Click the Save button at the top right of the Entity Overview page to save the updated slot entity.
### Create the BPN
The next step is to create a BPN that can use the new entity cost. In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it movieCosts. Save the new model then build each of the BPN tasks as described below.
Table. Specifications to Create movieCosts BPN Model

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started! | Let the user know the BPN workflow has started and initialize Amelia. |
| 2 | ask for the slot cost | Click the task and select the Properties Panel tab on the right edge of the workspace.Select a question previously defined for this entity in the Question setting dropdown. |
| 3 | pull movie by cost | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 4 | say ${movieChoice} costs ${movieCost} dollars | display data retrieved from the tabular data source with user input. |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
### A Script to Retrieve Tabular Data
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 3 in the table above. The file name and first element of the tabularDataService.query call must be the same, *moviecosts*.
``` groovy
def movieCost = contextService.latestSlot('cost')
def formattedValueCost = quantityService.format(movieCost, Formatters.INTEGER)
def movieChoice = tabularDataService.query('moviecosts','release_date','title','cost').is('cost',formattedValueCost).first()['title'];
execution.setVariable("movieChoice", movieChoice)
execution.setVariable("movieCost", formattedValueCost)
```
### Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the right edge of the Mind panel.
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the movieCosts workflow by typing this command in the chat interface:
    ``` bash
    run the workflow movieCosts
    ```
3.  Amelia asks for a price. Enter an integer, for example, 3 or 10 or 6. Amelia will complete the last task in the BPN model.
## Attachments:
![](images/icons/bullet_blue.gif) [image2017-9-22_16-42-21.png](attachments/11939477/11939478.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_15-4-36.png](attachments/11939477/11939479.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_15-4-13.png](attachments/11939477/11939480.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_15-3-52.png](attachments/11939477/11939481.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_15-3-30.png](attachments/11939477/11939482.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-tabular-data-workspace-3.5.10.jpg](attachments/11939477/11939483.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-9-27_14-51-54.png](attachments/11939477/11939484.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_14-32-2.png](attachments/11939477/11939485.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_14-29-39.png](attachments/11939477/11939486.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_14-28-36.png](attachments/11939477/11939487.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-27_14-27-28.png](attachments/11939477/11939488.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-19_13-7-20.png](attachments/11939477/11939489.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-23_16-54-22.png](attachments/11939477/11939490.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-23_16-27-41.png](attachments/11939477/11939491.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-23_16-23-50.png](attachments/11939477/11939492.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-23_16-22-31.png](attachments/11939477/11939493.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-23_16-21-34.png](attachments/11939477/11939494.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-23_15-43-26.png](attachments/11939477/11939495.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-4-20_17-8-52.png](attachments/11939477/11939496.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-5_14-7-51.png](attachments/11939477/11939497.png) (image/png)  
![](images/icons/bullet_blue.gif) [moviecosts.csv](attachments/11939477/11939498.csv) (text/csv)  
![](images/icons/bullet_blue.gif) [image2017-12-20_14-15-52.png](attachments/11939477/11939499.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-26_15-4-10.png](attachments/11939477/11939500.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-43-11.png](attachments/11939477/11939501.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-22_16-42-46.png](attachments/11939477/11939502.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_9-47-53.png](attachments/11939477/11942860.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_9-48-30.png](attachments/11939477/11942861.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_9-48-59.png](attachments/11939477/11942862.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_9-49-31.png](attachments/11939477/11942863.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-3-12_9-49-54.png](attachments/11939477/11942864.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-tabular-data-workspace-3.8.0.jpg](attachments/11939477/11942865.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2019-9-24_12-40-51.png](attachments/11939477/25461128.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-24_12-49-34.png](attachments/11939477/25461130.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-script-task-tools-3.7.37.jpg](attachments/11939477/25461131.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2019-9-24_13-54-31.png](attachments/11939477/25461133.png) (image/png)  
