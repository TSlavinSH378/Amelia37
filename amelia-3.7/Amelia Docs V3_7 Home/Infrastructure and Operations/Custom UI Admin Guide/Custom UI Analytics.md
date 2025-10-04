{% version "3.x" %}
As of Custom UI version 5.5.1, it is possible to capture analytics data for the custom user interface. JavaScript code is passed with the **customJS** parameter in the config.json file.
Refer to [Custom UI Bundles](Custom%20UI%20Bundles) page for details about configuring a custom user interface and [Customize UI with config.json](Customize%20UI%20with%20config_json) for details about the config.json file.
Analytics data can be sent with an external script to receive data or without an external script.
# External Script to Process Data
Data can be processed with an external script adapted to receive data in a structured format. Code used to collect data is pretty printed then minified before being added to the **customJS** parameter in the config.json file.
1.  Create a script file to receive analytics data. The script includes a **sendAnalytics** function and receives values for **eventType**, **conversationId**, **sessionId**, **agentName**, and **domainCode** wrapped in a **data** value. These values are sent when **resetConversation** or **closedConversation** events happen in the custom user interface.  
    For example, this JavaScript code creates a **sendAnalytics** function and writes to Amelia's **console.log** function.  
    ``` groovy
    function sendAnalytics (data) {
        // My analytics code below to process s, type, src values ...
        console.log('data', data);
    }
    ```
2.  Pretty print the JavaScript code used to collect data.  
    ``` groovy
    var s = document.createElement('script');
    s.type = 'text/javascript';
    s.src = 'http://somedomain.com/somescript';
    document.head.appendChild(s);
    ```
3.  Minify the pretty print JavaScript code. Then add it to the **customJS** property in the config.json file.  
    ``` groovy
    {
      "customJS": "(() => {var s = document.createElement('script');s.type = 'text/javascript';s.src = 'http://somedomain.com/somescript';document.head.appendChild(s);})();"
    }
    ```
# No External Script to Process Data
If there is no external analytics file to process data, the **customJS** parameter is set to receive data using Amelia's **console.log** functionality.
``` groovy
{
  "customJS": "window.sendAnalytics = function (data) {console.log('data', data);};"
}
```
# Example to Collect Clicked Links
This code collects any custom user interface links clicked by the user. JavaScript is used to capture URLs with data collected and sent with the **customJS** property in the config.json file.
1.  Create a JavaScript function **getClick** to create a list to capture data about links clicked.  
    ``` groovy
    <script type="text/javascript">
    var list = []; 
    function getClick(url) {
        console.log(url);
        list.push(url);
        console.log(list);
    }
    </script>
    ```
2.  Pretty print the JavaScript function.  
    ``` groovy
    var s = document.createElement('script');
    s.type = 'text/javascript';
    s.text = 'var list = []; function getClick(url) {console.log(url); list.push(url); console.log(list);}';
    document.head.appendChild(s);
    ```
3.  Minify the pretty print JavaScript code. Then add it to the **customJS** property in the config.json file.  
    ``` groovy
    {
    "customJS": "(() => {var s = document.createElement('script');s.type = 'text/javascript';s.text = 'var list = []; function getClick(url) {console.log(url);list.push(url);console.log(list);}';document.head.appendChild(s);})();"
    }
    ```
{% /version %}
