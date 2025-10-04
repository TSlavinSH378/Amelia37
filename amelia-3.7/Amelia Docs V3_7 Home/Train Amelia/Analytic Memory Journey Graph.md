{% version "3.x" %}
The Analytic Memory page displays Journey Analytics which show the conversation and resolution flows as Amelia handles conversations. The flow diagram begins with the number of conversations on the left then evolves to include conversations Amelia covered and conversations she escalated. Above the flow diagram are graphs to show her performance over a designated time period. Mouse over a line node in the top graphs to display counts.
The AUTHORITY_JOURNEY_VIEW authority is required to view the graph. This authority is included in the Admin, Agent, Agent Supervisor, Knowledge Designer, Power User, and RBAC Administrator roles.
The BPN Graph button is not active currently.
![](attachments/11939882/25460793.png)
Figure. Sample Journey Analytics Page
Each node in the conversation and resolution journey includes **Average Handle Time** in hh:mm:ss, **Average Quality of Service score** from -1 to 1, and counts for **BPNs** and **Intents**. Clicking these elements displays a panel on the right side with detailed graphs for the selected node in the conversation flow. Click the X at the top right of the node detail panel to close the panel.
![](attachments/11939882/25460791.png)
Figure. Sample Journey Analytics Page with Node Detail Panel
At the top right of the Journey Analytics page are display options used to filter conversation flow data.
Table. Journey Analytics Dropdown Options

| Option | Description |
| ----|----|
| Search | Display conversation flows for a selected conversation identifier |
| Domains | Select a domain or all domains to display conversation flows for the domain(s). All Domains is default. |
| Date Range | Select a date or date range to display conversation flows. Options are Today, Yesterday, Week to Date, Last Week, Month to Date, and Last Month, as well as years, quarters, and months based on log data stored in the Amelia instance. Today is default. |
| Data Type | Select a specific type of data to filter conversation flows. Options are Intent, Agent, BPN, and None. Selecting Intent, Agent, or BPN displays a second dropdown list of all available choices for that type of data. None is the default filter option; all data is used to display conversation flows. |

{% /version %}
