Amelia's integration service runs separately from Amelia, possibly located on another host or hosts, and allows her to interact with external systems. Integration flows are Apache Camel contexts created with Amelia V3 administration tools and deployed to these remote processes with gRPC, a universal remote procedure call standard.
The integration service unpacks the data received from an external system and deploys it in a Spring application separate from the parent context and any other flows running on the service. The integration service relies on Spring integration to handle RPC-style calls over RabbitMQ message broker and then internally hands off to Apache Camel to execute a request.
> [!warning]  
>
> The Integrations links in Amelia's administration pages are visible only if the Global Integration Designer role is assigned to a user account.

# Integrations Workspaces
The primary workspace used to create integrations is the flow design workspace. Properties and assets used by a flow can be created within the flow design workspace or individual Assets and Properties workspaces.
## Flow Design Workspace
Flows are found by clicking the Flows link at the top left of the Integration Home page. To create a flow, click the blue plus button on the right side of the Integration Flows page. A New Integration Service form page will appear with tools to design integration flows.
![](attachments/11940444/11940446.jpg)
Figure. Integration Flow Designer
The Integration Service page includes a flow edit property panel on the left side and a workspace on the right to create an integration either visually with drag and drop stencils or with Camel code. The visual design tools convert diagrams into Camel code. At the bottom right of the flow workspace are controls to toggle the view between a visual design tool and code source view.
Within the visual design workspace elements are placed into containers, starting with a default Integration Context and within it a Route container. Drag the computer mouse down and to the right to see these containers in the design workspace.
-   Clicking a container displays an x in the upper left of the container to delete it.
-   Drag Connector and Development stencils into a container as needed to build an integration flow. Once placed within an Integration Context or Route, click the stencil to display a properties panel to the right side of the workspace, for example, to configure an API URL.
-   Clicking a stencil in a container also displays a scissors icon, a curved connector arrow icon, and an x to the left, right, and top left of the stencil. Click the scissors icon to break all connections to the stencil. Click the wavy arrow icon and drag it to another stencil to connect them. Click the x to delete a stencil.
-   Click the Save icon in the flow properties panel on the left side of the workspace. If needed, toggle the folder icon at the top left of the workspace to display the panel and Save icon.
Flows use sets of properties. Every flow has one Internal Set, for properties only it can use. Flows may also add other shared Property Sets to their list of Property Sets. When a Flow has multiple sets, the last set in the list to contain a given property name will provide that value.
Lists of property sets can be assembled and the internal set adjusted. The properties Preview tab displays the final merged results. Property sets created with the Properties workspace are collections of properties shared with multiple flows through the Properties section of the flow edit form in the Flow Design Workspace.
The integration flow edit form also organizes jar files and other binary assets used by a flow. Assets are included in a jar file on deployment.
Table. Integration Flow Stencils
<table class="confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Stencil Icon</th>
<th class="confluenceTh">Stencil Name</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="3" class="confluenceTd"><strong>Integration Containers</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940447.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Integration Context</p>
</div></td>
<td class="confluenceTd">Creates an integration context container</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940448.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Route</p>
</div></td>
<td class="confluenceTd">Creates a route container</td>
</tr>
<tr class="even">
<td colspan="3" class="confluenceTd"><strong>Connectors</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940449.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>URL From</p>
</div></td>
<td class="confluenceTd">Set the URL from value and location within an integration flow</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940450.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>URL To</p>
</div></td>
<td class="confluenceTd">Set the URL to vlaue and location within an integration flow</td>
</tr>
<tr class="odd">
<td colspan="3" class="confluenceTd"><strong>Development</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940451.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Set Property</p>
</div></td>
<td class="confluenceTd">Sets a property with an expression, name, and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940452.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Set Header</p>
</div></td>
<td class="confluenceTd">Sets a header with an expression, name, and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940453.png" /></p>
</div></td>
<td class="confluenceTd">Choice</td>
<td class="confluenceTd">Defines when and otherwise conditions. Each has an expression and scheme language (constant, simple, groovy, or javascript).</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940454.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Print Log</p>
</div></td>
<td class="confluenceTd">Adds a print log condition with name, message, and status (DEBUG, ERROR, INFO, OFF, TRACE, and WARN)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940455.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Body Conversion</p>
</div></td>
<td class="confluenceTd">Default is java.lang.string</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940456.png" /></p>
</div></td>
<td class="confluenceTd">Delay</td>
<td class="confluenceTd">Set delay with an expression and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940457.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Generic</p>
</div></td>
<td class="confluenceTd">Set a node and edit the raw XML. The camel:replace tags and content within are placeholders to be replaced. Some XML may not be embeddable in certain contexts.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940458.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Script</p>
</div></td>
<td class="confluenceTd">Adds a script with the ability to set an expression, name, and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11940444/11940459.png" /></p>
</div></td>
<td class="confluenceTd">Transform</td>
<td class="confluenceTd">Converts a message from one format to another, or creates a new one, with Groovy or JavaScript before passing the message down the chain.</td>
</tr>
</tbody>
</table>
## Assets Workspace
The assets workspace is found by clicking the Assets link at the top left of the Integration Home page. The Integration Assets page will appear with a list of assets.
To create a new asset, click the plus ( + ) button at the top right of the assets workspace. The New Assets popup appears. Type the asset name, select the domain, and attach one or more files. Click the Submit button to upload the asset and update Amelia.
![](attachments/11940444/11940460.png)
Figure. New Assets Popup
## Properties Workspace
The properties workspace is found by clicking the Properties link at the top left of the Integration Home page.
To create a new property set, click the plus ( + ) icon at the top right of the properties workspace. The New Property Set page appears. Type the property set name and select the domain. Properties can be uploaded or click the Add Row button to manually add properties. Uploaded properties properties can replace or merge existing properties with the same name.
Property sets are collections of properties shared with multiple flows through the Properties section of the flow edit form in the Flow Design Workspace.
![](attachments/11940444/11940461.png)
Figure. New Property Set Form
# Create an Integration Flow
The API integrations are defined in the Amelia V3 administration pages. Click the Integrations Home link on the left side then click Integration Home to display the home page. To create an integration, at least configure one Host data and one or more Flows.
## Configure a Host
The first step is to configure a Host to make Amelia aware of one or more hosts that will run integration services. In many cases, the localhost integration service will run on the same host as Amelia V3 with the administrative port listening on port 4635. However, this is not automatically set.
From the Integrations workspace, click the Hosts link near the top of the page, then click the blue plus button at the top right to open a New Integration Service form.
To continue to configure an integration flow API or similar API, configure the localhost with this data. Click the Save icon at the top right of the form to save the host definition.
![](attachments/11940444/11940462.png)
Figure. Integration Host Form
Table. Integration Host Elements

| Host Element | Example | Description |
| ----|----|----|
| Name | localhost | A readable name for the host |
| Host | localhost | The FQDN of the host, as it can be reached from the Amelia V3 Instance itself. |
| Port | 4635 | The port upon which the;gRPC administrative service is running |
| Cluster |  | A host can optionally belong to a Cluster, defined elsewhere in the integration administration tools.; Clusters are for bulk operations so that a Flow can be deployed to or undeployed from multiple hosts at one time. |
| Description | Default localhost | Brief information about the Integration Host |
| Deleted/Disabled |  | A deleted/disabled host still exists in the system but is not eligible for any deployments. |
| Certificate |  | Visible only for an existing host record. Integration services declare themselves to Amelia on startup of the integration service. Services create their own certificates and send a public certificate to Amelia. Click the Certificate button to display a public certificate for a host. |
| Delete Certificate |  | Visible only for an existing host record. Click the Delete Certificate button to delete the public certificate generated by a service. Rebooting the integration service will cause the service to create their own certificates and send a new public certificate to Amelia. |

## Configure a Flow
To create a flow, click the Flows link at the top left of the Integration Home page. Click the blue plus sign at the top right of the page to display the Integration Service workspace. This workspace includes a form on the left side and designer tool on the right.
Complete the flow edit form, on the left side, as shown below to create a sample flow to pull data from Yahoo's weather API. Instructions below describe how to code the integration and call a flow from a BPN process model.
> [!warning]  
>
> Names for integration flows must be unique within each domain. Integration flows also are accessible to parent and child domains.
>
> The closest integration flow has the highest priority in cases where a parent or child domain has the same name for a flow. For example, if the global, parent, and current domains each have an integration flow named Weather, a BPN in the current domain will call the Weather flow from the current domain. If there is no Weather flow in the current domain, the BPN in the current domain would call the Weather flow defined in the parent domain.

![](attachments/11940444/11940446.jpg)
Figure. Configure the Integration Flow
Table. Integration Flow Form Elements

| Flow Element | Example | Description |
| ----|----|----|
| Name | YahooWeather | A readable name for the flow, which can be changed after creation. No spaces between words are allowed. Must be unique within the current selected domain. |
| Code | yahoo_weather | An alternate key for the flow, immutable after creation.; This value must be unique within the current selected domain. Code names also cannot be edited once created. |
| Domain |  | Every flow must belong to one Amelia Domain |
| Description | Pull weather data from Yahoo | Brief information about the Integration Flow |
| Assets |  | Binary elements that should be included in a flow.; These assets will be included in the jar file assembled for deployment. Click the plus sign to the right of the Assets dropdown list to add assets to a specific domain. |
| Property | {{password}} | Create one or more properties to handle data, for example, usernames and passwords. Properties can be encrypted or plain text. Sensitive data should always be defined as an encrypted property, not passed any other way. |

### Configure Flows with Stencils and Designer View
The Flows workspace includes a visual design tool to create integration flows with configurable drag and drop stencils.
The default Flows workspace includes a Route nested in an Integration Context. The route includes two stencils, one to start the flow (*URL From*) and one to receive any data collected from the route (*URL To*).
This demonstration adds two stencils to the default route, a *URL To* stencil followed by a *Body* stencil. The XML output can be examined at this Yahoo Weather URL: <https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22nome%2C%20ak%22)&format=json&diagnostics=true&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys&callback=>
![](attachments/11940444/11940463.png)
Figure. Default Flows Workspace with Nested Route in an Integration Context
1.  Click to select the default *URL To* stencil in the Route and drag the stencil to the far right. This will make room to drop other stencils while preserving the default code included in the stencil.
2.  Select a *URL To* stencil from the Stencil column in the designer then drag it between the two default stencils. Drop it near the default *URL From* stencil.
3.  With the new *URL To* stencil selected, copy/paste this API URL in the Properties field on the right side of the workspace:
    ``` text
    https4://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22nome%2C%20ak%22)&format=json&diagnostics=true&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys&callback=
    ```
    > [!warning]  
    >
    > Note the use of https4 is not a typographical error. In the Camel language, https4 is a language-specific syntax to refer to the Apache https4 client software. For other projects, use http4 or https4 as appropriate.
    ![](attachments/11940444/11940464.png)  
    Figure. Drag Default *URL To* Stencil to Right  
4.  Select the arrow that connects the default *URL From* stencil to the default *URL To* stencil. The arrow head turns orange. Drag the arrow back until the new *URL To* stencil is outlined in orange. This connects the default *URL From* stencil to the new *URL To* stencil. If needed, delete the original arrow and click the curved connector arrow icon to the right of the original *URL From* stencil and drag the icon to the new *URL To* stencil with the Yahoo Weather URL in its Properties field.
    ![](attachments/11940444/11940465.jpg)
    Figure. Select the Arrow Connecting Default Stencils
5.  Select a *Body* stencil from the Stencil column in the designer then drag it between the new *URL To* stencil and the original *URL To* stencil.
6.  Select the new *Body* stencil and confirm the properties Type is java.lang.String.
    ![](attachments/11940444/11940466.jpg)
    Figure. Drag *Body* Stencil between *URL To* Stencils
7.  The next step is to connect isolated stencils in the route. Select the curved connector arrow on the right edge of the new *URL To* stencil. It turns red. Click the red arrow and drag to connect to the new *Body* stencil until it is outlined in orange.
    Click the new *Body* stencil, select the curved connector arrow on the right edge then drag to connect to the default *URL To* stencil until it is outlined in orange.
    ![](attachments/11940444/11940467.jpg)
    Figure. Connect Stencils with Connect Arrow
8.  With default and new stencils connected in sequence, select the default *URL To* stencil and update the variable values for the *URL To* moveToOutboundVariables property. The *body* variable is the JSON output Yahoo returns. Amelia converts the data into a Groovy LazyMap object.  
    > [!warning]  
    >
    > \_body\_ in this code is variable notation unique to Amelia, not a typo.
    ``` text
    bean:varpop?method=moveToOutboundVariables('_body_')
    ```
    ![](attachments/11940444/11940468.jpg)
    Figure. Update Default *URL To* Value for moveToOutboundVariables
9.  Click the Folder icon at the top left of the Flows workspace to display the Save icon and flow details. Click the Save icon to save the flow.
### Configure Flows with Code and Source View
Integration flows also can be created with Camel code using the Flow workspace. The Designer View automatically updates to translate the code into configured stencils and connectors.
In the Flows designer, click Source View at the bottom right and paste in this code to define a Camel flow for Yahoo's weather API:
> [!warning]  
>
> Camel code must have a camel:from statement with id set to mainRouteStart and the uri set to direct:start. Amelia looks for direct:start to begin the integration flow.

``` bash
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:camel="http://camel.apache.org/schema/spring" xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans-4.2.xsd
 http://camel.apache.org/schema/spring
 http://camel.apache.org/schema/spring/camel-spring.xsd
">
    <!-- add a comment -->
    <camel:camelContext id="mainContext">
        <camel:route id="route1">
            <camel:description layoutX="40" layoutY="200" layoutWidth="560" layoutHeight="340"/>
            <camel:from id="mainRouteStart" uri="direct:start">
                <camel:description layoutX="50" layoutY="250" layoutWidth="120" layoutHeight="120"/>
            </camel:from>
            <!-- you can also use other languages such as groovy, ognl, mvel, javascript etc. -->
            <camel:to id="c4e63689-785e-4541-a927-0e0cc98241c6" uri="https4://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22nome%2C%20ak%22)&amp;format=json&amp;diagnostics=true&amp;env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys&amp;callback=">
                <camel:description layoutX="200" layoutY="250" layoutWidth="120" layoutHeight="120"/>
            </camel:to>
            <camel:convertBodyTo type="java.lang.String" id="d97f9150-aab8-11e7-a0a5-1d4f80ae85b9">
                <camel:description layoutX="345" layoutY="250" layoutWidth="120" layoutHeight="120"/>
            </camel:convertBodyTo>
            <camel:to uri="bean:varpop?method=moveToOutboundVariables(&apos;_body_&apos;)" id="dde7ef60-a795-11e7-9c6e-b5575ac44e3c">
                <camel:description layoutX="480" layoutY="250" layoutWidth="120" layoutHeight="120"/>
            </camel:to>
        </camel:route>
    </camel:camelContext>
</beans>
```
There are several details to note in the code above.
-   The default namespace wrapper is spring, \<beans ...\>\</beans\>, and the Apache *camel:* tags must be namespaced between the spring tags.
-   The camel:description tags preserve the layout details for the flow editor, specifically the x,y positions of stencil icons used to define a flow in the designer. These tags are ignored during flow execution.
-   The camel:to uri setting uses http4 which is not a typographical error. In the Camel language, http4 is a language-specific syntax to refer to the Apache http4 client software. For other projects, use http4 or https4 as appropriate.
-   The returned data is converted to a string with the convertBodyTo setting.
-   The returned data output is sent to a Spring bean method moveToOutboundVariables to make the data available within a BPN process.
-   The *id* values are unique to the code block. Nothing outside of the integration flow design tool will refer to them. As with camel:description tags, id values are regenerated if deleted.
These Camel Components are currently included in the integration service:
-   Camel core components
-   HTTP4: <http://camel.apache.org/http4.html>
-   Email: <http://camel.apache.org/mail.html>
-   Ldap: <http://camel.apache.org/ldap.html>
-   Jdbc: <http://camel.apache.org/jdbc.html>   (mysql driver is present)
-   Printer: <http://camel.apache.org/printer.html>
-   Spring-ldap <http://camel.apache.org/spring-ldap.html>
-   FTP <http://camel.apache.org/ftp.html>
-   SMPP <http://camel.apache.org/smpp.html>
-   ServiceNow <http://camel.apache.org/servicenow.html>
Click the Designer View at the bottom right to display the code as stencil blocks. Reposition stencils and resize containers, if needed, to make the flow more understandable.
![](attachments/11940444/11940469.png)
Figure. Integration Flow Design for Yahoo Weather API
In this example, the *URL From* stencil at the top left flows to a *URL To* stencil which calls the Yahoo weather API. The stencil then flows to a *Body* stencil and a final *URL To* stencil which passes the API output a Spring integration that makes any data available to the BPN process that calls this integration flow.
To save the demonstration flow code, click the Folder icon at the top left of the Flows workspace to display the Save icon and flow details. Click the Save icon to save the flow.
## Deploy Integration Service
Once a flow and host are defined, click the Service Deploy tab near the top of the Integrations Home page. To create a deployment, click the plus sign near to top right of the workspace. The Integration Service Deployment popup appears. Select the Flow name and, as appropriate, the Hosts to Deploy in the popup. Click the Run button to deploy.
> [!warning]  
>
> The integration service only allows one flow code name – set when creating a flow – for all domains within an Amelia instance. Attempting to deploy an integration flow with a code name in one domain when it exists in another domain will generate an error. The error message will include a Confirm action check box in the Integration Service Deployment popup. Clicking the Confirm action check box will override the block, deploying two flows in one instance with the same name and possibly introducing errors.

![](attachments/11940444/11940470.png)
Figure. Integration Service Deployment Pop-Up
# Create a BPN Process Flow
Once the integration flow and host details have been configured, call the service from within a BPN process flow.
![](attachments/11940444/11940445.png)
Figure. Simple BPN to Retrieve API Output
## Create the BPN
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
## A Script to Retrieve API Output
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
The document structure – query.results.channel.item.condition.temp – used to define the temp variable in this script is derived from analysis of the XML output from the [Yahoo Weather URL](https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22nome%2C%20ak%22)&format=json&diagnostics=true&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys&callback=) used in the integration flow. The output can be displayed during tests with a Say task in the BPN – for example, say ${output} – if the variable is set, as shown in the last line of the code.
## Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages..
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the getJokes workflow by typing this command in the chat interface:
    ``` bash
    run the workflow getWeather
    ```
3.  Amelia displays the conversation transcript and an object of transcript utterances.
# Camel Integration Examples
These examples show how to use Camel in the Source View of the Integration Flow workspace to implement key functionality.
## Database Integration
### Camel Code
> [!note]  
>
>     <?xml version="1.0" encoding="UTF-8"?>
>     <beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:camel="http://camel.apache.org/schema/spring" xsi:schemaLocation="http://www.springframework.org/schema/beans
>               http://www.springframework.org/schema/beans/spring-beans-4.2.xsd
>               http://camel.apache.org/schema/spring
>               http://camel.apache.org/schema/spring/camel-spring.xsd
>     ">
>         <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
>             <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
>             <property name="url" value="jdbc:mysql://${dbHost}:${dbPort}/${dbName}"/>
>             <property name="username" value="${dbUser}"/>
>             <property name="password" value="${dbPass}"/>
>         </bean>
>         <camel:camelContext id="mainContext">
>             <camel:route id="route1">
>                 <camel:description layoutX="20" layoutY="20" layoutWidth="970" layoutHeight="640"/>
>                 <camel:from id="mainRouteStart" uri="direct:start">
>                     <camel:description layoutX="20" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:from>
>                 <camel:log message="running $simple{property.sqlStatement}" loggingLevel="INFO" id="c-eb630da6-1b69-49fb-afa1-f1e6eb217523">
>                     <camel:description layoutX="150" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:log>
>                 <camel:setBody id="c-50b78bf5-3733-456b-a349-e45c1aac3972">
>                     <camel:description layoutX="150" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                     <camel:simple id="c-635da76f-8821-4fa4-bbb7-b64e5ad46245">
>                         ${exchangeProperty.sqlStatement}
>                     </camel:simple>
>                 </camel:setBody>
>                 <camel:to uri="jdbc:dataSource" id="c-632e3dd5-9fd8-4c16-ad9d-938857b292ab">
>                     <camel:description layoutX="280" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:to>
>                 <camel:convertBodyTo type="java.lang.String" id="c-7f9d92c9-e573-4b8b-81e5-3f1f9006b1e7">
>                     <camel:description layoutX="670" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:convertBodyTo>
>                 <camel:log message="body is ${body.getClass()} ${body}." loggingLevel="INFO" id="c-7c71ae3b-0e1d-4dcb-bf8e-f5ae1d0c837c">
>                     <camel:description layoutX="810" layoutY="150" layoutWidth="120" layoutHeight="120"/>
>                 </camel:log>
>                 <camel:setProperty propertyName="sqlResponse" id="ee9b7a0d-aa03-11e7-a861-fdebea8f0396">
>                     <camel:description layoutX="740" layoutY="330" layoutWidth="120" layoutHeight="120"/>
>                     <camel:simple id="ee9b7a0e-aa03-11e7-a861-fdebea8f0396"><![CDATA[${body}]]></camel:simple>
>                 </camel:setProperty>
>                 <camel:to uri="bean:varpop?method=moveToOutboundVariables(&apos;sqlResponse&apos;)" id="c-ef1c4903-a2e6-4c65-b9aa-25d602680310">
>                     <camel:description layoutX="20" layoutY="470" layoutWidth="120" layoutHeight="120"/>
>                 </camel:to>
>             </camel:route>
>         </camel:camelContext>
>     </beans>

### Required Flow Properties

| Property | Example Value | Description |
| ----|----|----|
| dbHost

\|
utility01.ams1.amelia.ipcenter.com
\| Hostname of server where database lives \| \|
    dbPort
\| 3306 \| Port to access database instance \| \|
    dbName
\| banking \| Name of the database \| \|
    dbUser
\| amelia \| Username used to access the database \| \|
    dbPassword
\| password \| Password used to access the databse \|
### Required Exchange Properties

| Property | Example Value | Description |
| ----|----|----|
| sqlStatement

\| select \* from Termijnbedrag where CONTRACTREKENINGNUMMER=004000001882; \| SQL query to run against the databse \|
### Returned Variables

| Variable | Value | Description |
| ----|----|----|
| sqlResponse | Array of maps for each table row returned | The result set or result code of the sql statement |

