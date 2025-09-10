Amelia's integration service runs separately from Amelia, possibly located on another host or hosts, and allows her to interact with external systems. Integration flows are Apache Camel contexts created with Amelia V3 administration tools and deployed to these remote processes with gRPC, a universal remote procedure call standard.
The integration service unpacks the data received from an external system and deploys it in a Spring application separate from the parent context and any other flows running on the service. The integration service relies on Spring integration to handle RPC-style calls over RabbitMQ message broker and then internally hands off to Apache Camel to execute a request.
> [!warning]  
>
> The Integrations links in Amelia's administration pages are visible only if the Global Integration Designer role is assigned to a user account.

The primary workspace used to create integrations is the flow design workspace. Properties and assets used by a flow can be created within the flow design workspace or individual Assets and Properties workspaces.
# Flow Design Workspace
Flows are found by clicking the Flows link at the top left of the Integration Home page. To create a flow, click the blue plus button on the right side of the Integration Flows page. A New Integration Service form page will appear with tools to design integration flows.
![](attachments/11939827/11939842.jpg)
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
<table class="wrapped confluenceTable">
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
<p><img src="attachments/11939827/11939846.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Integration Context</p>
</div></td>
<td class="confluenceTd">Creates an integration context container</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939828.png" /></p>
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
<p><img src="attachments/11939827/11939829.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>URL From</p>
</div></td>
<td class="confluenceTd">Set the URL from value and location within an integration flow</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939830.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>URL To</p>
</div></td>
<td class="confluenceTd">Set the URL to value and location within an integration flow</td>
</tr>
<tr class="odd">
<td colspan="3" class="confluenceTd"><strong>Development</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939831.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Set Property</p>
</div></td>
<td class="confluenceTd">Sets a property with an expression, name, and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939832.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Set Header</p>
</div></td>
<td class="confluenceTd">Sets a header with an expression, name, and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939833.png" /></p>
</div></td>
<td class="confluenceTd">Choice</td>
<td class="confluenceTd">Defines when and otherwise conditions. Each has an expression and scheme language (constant, simple, groovy, or javascript).</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939834.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Print Log</p>
</div></td>
<td class="confluenceTd">Adds a print log condition with name, message, and status (DEBUG, ERROR, INFO, OFF, TRACE, and WARN)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939835.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Body Conversion</p>
</div></td>
<td class="confluenceTd">Default is java.lang.string</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939836.png" /></p>
</div></td>
<td class="confluenceTd">Delay</td>
<td class="confluenceTd">Set delay with an expression and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939837.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Generic</p>
</div></td>
<td class="confluenceTd">Set a node and edit the raw XML. The camel:replace tags and content within are placeholders to be replaced. Some XML may not be embeddable in certain contexts.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939838.png" /></p>
</div></td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Script</p>
</div></td>
<td class="confluenceTd">Adds a script with the ability to set an expression, name, and language (constant, simple, groovy, or javascript)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><div class="content-wrapper">
<p><img src="attachments/11939827/11939839.png" /></p>
</div></td>
<td class="confluenceTd">Transform</td>
<td class="confluenceTd">Converts a message from one format to another, or creates a new one, with Groovy or JavaScript before passing the message down the chain.</td>
</tr>
</tbody>
</table>
# Assets Workspace
The assets workspace is found by clicking the Assets link at the top left of the Integration Home page. The Integration Assets page will appear with a list of assets.
To create a new asset, click the plus ( + ) button at the top right of the assets workspace. The New Assets popup appears. Type the asset name, select the domain, and attach one or more files. Click the Submit button to upload the asset and update Amelia.
![](attachments/11939827/11939844.png)
Figure. New Assets Popup
# Properties Workspace
The properties workspace is found by clicking the Properties link at the top left of the Integration Home page.
To create a new property set, click the plus ( + ) icon at the top right of the properties workspace. The New Property Set page appears. Type the property set name and select the domain. Properties can be uploaded or click the Add Row button to manually add properties. Uploaded properties properties can replace or merge existing properties with the same name.
Property sets are collections of properties shared with multiple flows through the Properties section of the flow edit form in the Flow Design Workspace.
![](attachments/11939827/11939843.png)
Figure. New Property Set Form
