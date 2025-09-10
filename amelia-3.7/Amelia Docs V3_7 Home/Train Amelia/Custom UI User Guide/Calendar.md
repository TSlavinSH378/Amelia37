-   [Pick a Single Date](#Calendar-PickaSingleDate)
-   [Pick a Date Range](#Calendar-PickaDateRange)
    -   [Default](#Calendar-Default)
    -   [Block Days Before and After Specific Dates](#Calendar-BlockDaysBeforeandAfterSpecificDates)
    -   [Block Days Before a Specific Date](#Calendar-BlockDaysBeforeaSpecificDate)
    -   [Block Days After a Specific Date](#Calendar-BlockDaysAfteraSpecificDate)
    -   [Block Days After Today's Date](#Calendar-BlockDaysAfterToday'sDate)
    -   [Block Specific Dates](#Calendar-BlockSpecificDates)
The custom user interface can display a calendar in the conversation chat box. Possible calendar options are defined in a BPN Script task, saved as a variable, and then referenced in an Ask task.
The code examples below can be dropped into a Script task in a simple BPN to demonstrate how they work. The Ask task Form data variable property also must be set to formInputData, the Script task variable output shown below, or whatever variable name is used. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName `is the name of the simple BPN.
![](attachments/20809426/20809492.png)
Figure. Basic BPN to Display a Calendar
The define calendar Script task above displays the default two-month calendar to select a single date.
Figure. Default Two-Month Calendar Display
Selecting a date then clicking the upward arrow icon to submit the date executes the rest of the BPN.
![](attachments/20809426/20809502.png)
Figure. Output from Selecting a Date
There are many options to display the calendar, for example, the date format, as well as picking one date or a date range and blocking users from selecting dates before or after specific dates.
# Pick a Single Date
To display a calendar in the conversation chat box, a BPN Script task defines JSON output then converts the output to a variable, formInputData, which is then referenced in an Ask task Form data variable property.
A Script task will display a two-month calendar with this example code with the ability to pick then submit a single date.
``` groovy
import groovy.json.JsonOutput
def jsonString = '''
    {
      "name": "datePickerForm",
      "formType": "form_only",
      "instructions": "Please choose one of the following",
      "fields": [
        {
          "name": "datePickerField",
          "fieldType": "datePicker",
          "data": {
            "datePickerType": "dateSingle",
            "dateFormat": "DD-MM-YYYY"
          },
          "options": [],
          "selectionUtteranceMetadata": {
            "prefixSingle": "I select the date",
            "prefixMultiple": "I select the dates",
            "conjunction": "and"
          }
        }
      ],
      "allowedUserInputs": "FORM_ONLY"
    }
    '''
jsonString = JsonOutput.toJson(jsonString)
execution.setVariable("formInputData", jsonString)
```
# Pick a Date Range
There are a number of options for users to select a date range with the custom user interface. The default example provides the full Script task used to define the form. Other options only affect the JSON `data` object definition, as shown below, and can swap out the default data object definition.
> [!warning]  
>
> The variable output that contains the JSON definition, `formInputData` in the example below, also must be set in the Ask task Form data variable property to display the calendar in the conversation chat box.

## Default
To display a calendar in the conversation chat box, a BPN Script task defines JSON output then converts the output to a variable, formInputData, which is then referenced in an Ask task property, Form data variable.
A Script task will display a two-month calendar with this example code with the ability to pick then submit a date range.
``` groovy
import groovy.json.JsonOutput
def jsonString = '''
    {
      "name": "datePickerForm",
      "formType": "form_only",
      "instructions": "Please choose one of the following",
      "fields": [
        {
          "name": "datePickerField",
          "fieldType": "datePicker",
          "data": {
            "datePickerType": "dateRange",
            "dateFormat": "DD-MM-YYYY"
          },
          "options": [],
          "selectionUtteranceMetadata": {
            "prefixSingle": "I select the date",
            "prefixMultiple": "I select the dates",
            "conjunction": "and"
          }
        }
      ],
      "allowedUserInputs": "FORM_ONLY"
    }
    '''
jsonString = JsonOutput.toJson(jsonString)
execution.setVariable("formInputData", jsonString)
```
## Block Days Before and After Specific Dates
Use this data object to replace the default data object definition of the default date range example above.
``` groovy
    "data": {
      "datePickerType": "dateRange",
      "dateFormat": "DD-MM-YYYY",
      "dateRangeStart": "YYYY-MM-DD",
      "dateRangeEnd": "YYYY-MM-DD"
    }
```
## Block Days Before a Specific Date
Use this data object to replace the default data object definition of the default date range example above.
``` groovy
    "data": {
      "datePickerType": "dateRange",
      "dateFormat": "DD-MM-YYYY",
      "dateRangeStart": "YYYY-MM-DD"
    }
```
## Block Days After a Specific Date
Use this data object to replace the default data object definition of the default date range example above.
``` groovy
    "data": {
      "datePickerType": "dateRange",
      "dateFormat": "DD-MM-YYYY",
      "dateRangeEnd": "YYYY-MM-DD"
    }
```
## Block Days After Today's Date
Use this data object to replace the default data object definition of the default date range example above.
``` groovy
    "data": {
      "datePickerType": "dateRange",
      "dateFormat": "DD-MM-YYYY",
      "dontAllowDateBeforeToday": true
    }
```
## Block Specific Dates
Use this data object to replace the default data object definition of the default date range example above.
``` groovy
    "data": {
      "datePickerType": "dateRange",
      "dateFormat": "DD-MM-YYYY",
      "blockedDays": [
        "YYYY-MM-DD",
        "YYYY-MM-DD"
      ]
    }
```
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-7-24_13-2-22.png](attachments/20809426/20809492.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-24_13-14-22.png](attachments/20809426/20809495.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-24_13-16-24.png](attachments/20809426/20809496.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-24_14-16-39.png](attachments/20809426/20809502.png) (image/png)  
