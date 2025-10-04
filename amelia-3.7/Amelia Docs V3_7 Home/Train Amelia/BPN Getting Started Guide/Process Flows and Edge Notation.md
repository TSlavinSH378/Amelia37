{% version "3.x" %}
Process flows are single direction paths from the edge of a task or gateway to the next element in a BPN. Gateways organize branching of multiple single direction flows in a BPN with specified conditions for each flow line. Gateways and Flows allow for choices to be made in the execution of a BPN based on Amelia's interactions with a person.
# Flow Types
Flow types include Sequence Flows and Default Flows. Sequence flows include all paths from task edges and gateways. Default flows are defined for situations where multiple paths are possible from a task edge or gateway.
![](attachments/11939503/11939505.png)
Figure. BPN Sequence Flow and Default Flow Examples
## Sequence Flows
Flows from task edges may or may not include conditions to evaluate what path the BPN process should take next. Sequence flows exiting from gateways must have a condition expression also called edge notation.
## Default Flows
Default flows from a task edge or gateway are followed only if none of the conditions of one or more exit sequence flows are met. A default flow is indicated by a vertical line near the start of the flow line.
To select a flow line as a default flow, hover the mouse anywhere on the line but the middle and click the yellow dot to display the wrench Change Type icon. Click the wrench icon and select Default Flow.
![](attachments/11939503/11939504.png)
Figure. BPN Sequence Flow and Default Flow Examples
# Edge Notation and Flow Routing
Flow lines can include conditions to determine whether or not they should be followed. In Amelia V3, the ability to define conditions has been simplified and improved. The Properties Panel for flow lines includes both Name and Expression fields. The Name appears near the flow line while the Expression is the condition to be met in order for the flow line to be followed during a BPN process.
Edges and gateways with flow lines that have edge notation also must include either a default flow line or specify an otherwise condition with bpn:otherwise() edge notation for one flow line. To set a default flow line, select a flow near its end points to display the wrench and garbage can icons. Click the wrench icon and select Default Flow from the popup.
![](attachments/11939503/11939507.png)
Figure. Flow Line Edge Notation Properties
The conditions set in the Expression field are called edge notation because their flow lines transition from one task or gateway edge to another.
> [!warning]  
>
> Ask task and Gateway edges operate differently. Because Ask tasks capture user input from a conversation with Amelia, they have a wider range of dialogue-related context available than gateways. For example, the outbound process flow from an Ask task can evaluate the slot code retrieved by the Ask task. A gateway evaluating the same slot code would be out of context.

# Service Prefixes
Amelia V3 includes a notation system called service prefixes with a service:function() syntax. Service prefixes include a range of possible actions, for example, to capture and evaluate a user choice in a BPN with the bpn service prefix using bpn:choice() syntax.
Service prefixes are used in the Expression setting field in the Properties Panel for process flow lines. Refer to [Service Prefixes](Service%20Prefixes) for details about service prefixes.
{% /version %}
