The custom user interface can display a basic survey in the conversation chat box. Survey options are stars, emoji, and numbers. Possible survey options are defined in a BPN Script task, saved as a variable, and then referenced in an Ask task.
Survey results can be mined from conversation logs or captured with a Script task, for example, to integrate with a third party tool that collects survey data.
The code examples below can be dropped into a Script task in a simple BPN to demonstrate how they work. The Ask task Form data variable property also must be set to formInputData, the Script task variable output shown below, or whatever variable name is used. Once the BPN is saved and deployed, type run the workflow BPNName in the custom user interface chat box, where BPNName is the name of the simple BPN.
Figure. Basic BPN to Display a Survey
# Survey Options
There are three options for the basic survey: emojis, numbers, and stars.
Figure. Example Survey Options
# Script Task
To display a survey in the conversation chat box, a BPN Script task defines JSON output then converts the output to a variable, formInputData, which is then referenced in an Ask task property.
A Script task will display a survey with this example code. Properties are described below the code.
``` groovy
import groovy.json.JsonOutput
def jsonString = '''
    {
      "name": "surveyEmojiForm",
      "formType": "form_only",
      "instructions": "Please choose one of the following",
      "fields": [
        {
          "name": "surveyEmojiField",
          "fieldType": "Survey",
          "data": {
            "surveyType": "emojis",
            "surveyData": [
                {"label": "devastated", "value": "devastated"},
                {"label": "sad", "value": "sad"},
                {"label": "neutral", "value": "neutral"},
                {"label": "happy", "value": "happy"},
                {"label": "excited", "value": "excited"}
            ]
          },
          "options": [],
          "selectionUtteranceMetadata": {
            "prefixSingle": "I select the date",
            "prefixMultiple": "I select the emojis",
            "conjunction": "and"
          }
        }
      ],
      "selectionUtteranceMetadata": {
        "staticUtterance": "",
        "conjunction": "and"
      },
      "allowedUserInputs": "FORM_ONLY"
    }
    '''
jsonString = JsonOutput.toJson(jsonString)
execution.setVariable("formInputData", jsonString)
```
Table. Survey Properties

| Property | Description |
| ----|----|
| surveyType | emojis, stars, or numbers |
| surveyData | Each of the five possible options include label and value key:value pairs. See below for examples for the stars and numbers survey options. |

The `data` JSON structure for numbers and stars differs slightly from emojis.
**Stars**
``` groovy
          "data": {
            "surveyType": "stars",
            "surveyData": [
                {"label": "1", "value": 1},
                {"label": "2", "value": 2},
                {"label": "3", "value": 3},
                {"label": "4", "value": 4},
                {"label": "5", "value": 5}
            ]
          },
```
**Numbers**
``` groovy
          "data": {
            "surveyType": "numbers",
            "surveyData": [
                {"label": "bad", "value": 1},
                {"label": "ok", "value": 2},
                {"label": "good", "value": 3},
                {"label": "better", "value": 4},
                {"label": "great", "value": 5}
            ]
          },
```
# Ask Task
Once the survey is defined with JSON in a Script task and turned into a variable, formInputData, the Ask task Form Data Variable property must be set to the formInputData variable name.
Figure. Ask Task Form Data Variable Property
# Survey Display
The basic survey appears in the conversation chat box. Click a survey option then click the up arrow at the right of the chat box, or press the Enter key, to select the option.  
Figure. Example Survey in Conversation Chat Box
Figure. Example Survey Result Output
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-7-19_10-45-48.png](attachments/20809407/20809408.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_11-6-2.png](attachments/20809407/20809409.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_11-13-23.png](attachments/20809407/20809410.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_11-20-58.png](attachments/20809407/20809411.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_11-59-56.png](attachments/20809407/20809412.png) (image/png)  
