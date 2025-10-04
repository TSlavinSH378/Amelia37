{% version "3.x" %}
The custom user interface can display a multi-line data entry form in the conversation chat box. The form reduces the number of turns Amelia must make to collect information from users. Possible form options are defined in a BPN Script task, saved as a variable, and then referenced in an Ask task.
The form is limited to four fields, to ensure all fields can be seen on mobile devices. While collecting user first name, last name, email, and birth date are obvious uses for the multi-line form, each of the four fields can be customized. And the form can be displayed multiple times in a BPN by using process flows to evaluate user responses, for example, if the user answers Yes when Amelia asks if they have more data to enter.
However, this feature is not a replacement for conversation. Amelia is more than a talking form.
This multi-line feature works best for data types the user knows by memory, for example, name, email, address, and date of birth. The feature also is useful for tasks requiring entering multiple data points, for example, account creation.
This feature is not recommended for entering phrases or sentences or unrelated data points.
# How It Works
The code example below can be dropped into a Script task in a simple BPN to demonstrate how a multi-line form works. The Ask task Form data variable property also must be set to formInputData, the Script task variable output shown below in the code, or whatever variable name is used. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName `is the name of the simple BPN.
![](attachments/20809504/20809508.png)
Figure. Basic BPN to Display a Multi-Line Data Entry Form
The `define multi-line form` Script task above displays a multi-line form to enter basic demographic data.
![](attachments/20809504/20809513.png)
Figure. Default Multi-Line Data Entry Form
Completing the form then clicking the upward arrow icon to submit the form data executes the rest of the BPN.
![](attachments/20809504/20809509.png)
# The Script Task
To display a multi-line form in the conversation chat box, a BPN Script task defines JSON output then converts the output to a variable, formInputData in the example below, which is then referenced in an Ask task Form data variable property.
A Script task will display a form with this example code.
``` groovy
import groovy.json.JsonOutput
def jsonString = '''
    {
        "name": "multiLineInput",
        "formType": "form_only",
        "instructions": "Please choose one of the following",
        "fields": [
        {
          "name": "multiLineInput",
          "fieldType": "multiLineInput",
          "data": {
              "title": "My Form Title",
              "fields": [
                  {
                    "type": "text",
                    "name": "First Name",
                    "value": "",
                    "regex": "",
                    "errorMessage": "Invalid first name",
                    "required": true
                  },
                  {
                    "type": "text",
                    "name": "Last name",
                    "value": "",
                    "regex": "",
                    "errorMessage": "Invalid last name",
                    "required": true
                  },
                  {
                    "type": "email",
                    "name": "Email",
                    "value": "",
                    "regex": "^\\\\d{9}$",
                    "errorMessage": "Invalid email",
                    "required": true
                  },
                  {
                    "type": "date",
                    "name": "Birthday (MM-DD-YYYY)",
                    "value": "",
                    "regex": "",
                    "dateFormat": "MM-DD-YYYY",
                    "errorMessage": "Invalid birthday",
                    "required": false
                  }
                ]
          },
          "options": [],
          "selectionUtteranceMetadata": {
            "prefixSingle": "I select the field",
            "prefixMultiple": "I select the fields",
            "conjunction": "and"
          }
        },
        {
          "fieldType": "cancelButton"
        }
      ],
      "allowedUserInputs": "BOTH"
    }
    '''
jsonString = JsonOutput.toJson(jsonString)
execution.setVariable("formInputData", jsonString)
```
The multi-line JSON payload has a number of properties. The software expects the instructions, selectionUtteranceMetadata, and allowedUserInputs properties must be present. The fieldType and name properties are used different ways, as shown above.
Table. Basic Multi-Line Properties
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Property</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">formType</td>
<td class="confluenceTd"><p>FORM_ONLY, BOTH. Should match the allowedUserInputs property.</p>
<div class="table-wrap">
<pre class="table"><code>| Option | Description |
| ----|----|
| form_only | Display only the form and disable the chat input box |
| both | Display the form and enable the chat input box. Clicking into the chat box erases any data entered in the form. Allows users to change their mind and converse with Amelia. |</code></pre>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">title</td>
<td class="confluenceTd">Optional. Displays a title at the top of the multi-line form.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">fields</td>
<td class="confluenceTd">Up to four fields are allowed.<br />
&#10;<div class="table-wrap">
<table class="wrapped confluenceTable">
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Option</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd">type</td>
<td class="confluenceTd">Options are text, password, email, date. The password value triggers data masking for any sensitive data, for example, Social Security and bank account numbers.</td>
</tr>
<tr class="even">
<td class="confluenceTd">name</td>
<td class="confluenceTd">Appears in the top of a field, for example, First Name or Password</td>
</tr>
<tr class="odd">
<td class="confluenceTd">value</td>
<td class="confluenceTd">Optional. Example value.</td>
</tr>
<tr class="even">
<td class="confluenceTd">regex</td>
<td class="confluenceTd">Optional. A regular expression to use to validate data entered in the field. 
<blockquote>
<p>[!warning]<br />
</p>
<p>This field uses basic regexes that may not meet enterprise security requirements. If needed, use a stronger regex definition that matches any enterprise security requirements.</p>
</blockquote>
<p> </p>
<div class="table-wrap">
<pre class="table"><code>| Data Type | Default Regex |
| ----|----|
| Text | /[a-zA-Z]{1,10}$/ |
| Password | /[a-zA-Z0-9]{1,10}$/ |
| Email | /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/ |</code></pre>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd">dateFormat</td>
<td class="confluenceTd">Appears when type is date. Format is a combination of MM, DD, and YYYY values.</td>
</tr>
<tr class="even">
<td class="confluenceTd">errorMessage</td>
<td class="confluenceTd">Message to display when user enters data incorrectly</td>
</tr>
<tr class="odd">
<td class="confluenceTd">required</td>
<td class="confluenceTd">Options are true or false</td>
</tr>
</tbody>
</table>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd">fieldType</td>
<td class="confluenceTd">Optional when used for the Cancel button. cancelButton displays an X icon at the top left of the form. When clicked, the form disappears. Otherwise, fieldType repeats the value for the name property.</td>
</tr>
<tr class="odd">
<td class="confluenceTd">allowedUserInputs</td>
<td class="confluenceTd">FORM_ONLY, BOTH. Should match the formType property.</td>
</tr>
</tbody>
</table>
# Features
The multi-line form includes a number of features activated with JSON name:value pairs and objects, as shown in the code example above.
## Field Types
There are four available field types set with the `fieldType` property:
-   Text
-   Password
-   Email
-   Date
## Turn Chat Input On or Off
To enable or disable the chat input box when the multi-line form displays, use the `allowedUserInputs` and `formType` properties and set their values to either `form_only` (disables the chat input box) or `both` (enables the chat input box and the multi-line form). Enabling both allows the user to change their mind and continue their conversation with Amelia, for example, if they have a question.
When the chat input box and multi-line form are both enabled, clicking the chat input box erases any data entered in the form.
## Add Cancel Button
To add a cancel button to the multi-line form, add a `fieldType` property and set the value to `cancelButton`. This should be the last JSON object in the `fields` object.
## Input Validation and Error Messages
To validate data entered into a field, use the `regex` property to define a regular expression value to be used for validation. Error messages can be set with the `errorMessage` property.
## Mandatory and Optional Fields
To set a field as mandatory or optional, set the `required` property to true (mandatory) or false (optional).
## Mask Sensitive Data
To mask sensitive data, use `password` as the value for the `property` type used to define one of the four input fields. Each character entered in the field will be masked with an asterisk. An eye icon also will appear to the right of the field and, when clicked and held down, will display the entry in plain text.
## Form Title
To display a title at the top of the multi-line form, use the `title` property set as the first entry in the data JSON object.
{% /version %}
