Once the integration flow and host details have been configured, call the service from within a BPN process flow.
![](attachments/11939862/11939863.png)
Figure. Simple BPN to Retrieve API Output
# Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it getWeather. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Retrieve API Output

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started! | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | run the integration flow yahoo_weather | yahoo_weather is the Code setting from the Integration Flows page for the Yahoo Weather flow. |
| 3 | parse response | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 4 | say temperature is ${temp} degrees in Nome, Alaska. | Display output from the variable set in the script |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
# A Script to Retrieve API Output
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 3 in the table above. Note *parser.parseText* in this script parses a text representation of the API output as a string which, in turn, allows retrieval of data within the JSON data structure. Otherwise, data is returned as a Groovy LazyMap object by default.
``` groovy
import groovy.json.JsonSlurper;
def temp = "no temp"
def bodyAsString = execution.getVariable("body")
if (bodyAsString != null) {
    def parser = new JsonSlurper()
         def output = parser.parseText(bodyAsString)
         temp = output.query.results.channel.item.condition.temp
}
execution.setVariable("temp", temp)
execution.setVariable("output", output)
```
The document structure – query.results.channel.item.condition.temp – used to define the temp variable in this script is derived from analysis of the XML output from the [Yahoo Weather URL](https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22nome%2C%20ak%22)&format=json&diagnostics=true&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys&callback=) used in the integration flow. The output can be displayed during tests with a Say task in the BPN – for example, say ${output} – if the variable is set, as shown in the last line of the code.
# Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages..
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the getJokes workflow by typing this command in the chat interface:
    ``` bash
    run the workflow getWeather
    ```
3.  Amelia displays the conversation transcript and an object of transcript utterances.
