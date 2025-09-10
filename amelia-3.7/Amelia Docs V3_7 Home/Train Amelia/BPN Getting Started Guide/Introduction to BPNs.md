-   [BPN Model Types](#IntroductiontoBPNs-BPNModelTypes)
-   [BPN Elements](#IntroductiontoBPNs-BPNElements)
    -   [Events](#IntroductiontoBPNs-Events)
    -   [Tasks](#IntroductiontoBPNs-Tasks)
    -   [Gateways and Flows](#IntroductiontoBPNs-GatewaysandFlows)
    -   [Edge Notation](#IntroductiontoBPNs-EdgeNotation)
    -   [Scripting](#IntroductiontoBPNs-Scripting)
    -   [Integrations](#IntroductiontoBPNs-Integrations)
A Business Process Network (BPN) is a flexible and extensible way to guide Amelia's behavior in her interactions. They define a process flow needed to identify and resolve multiple goals and use cases. This is in addition to training Amelia's mind with relevant data to create a reasoning model to help her converse with people. BPNs map her process. Training gives her a model to use when evaluating responses from a conversation.
Amelia uses a BPN model based on the Business Process Model and Notation 2.0 (BPMN). By definition, Business Process Model and Notation helps businesses understand and document their internal procedures with graphical notation, as well as the ability to communicate these procedures in a standard.
# BPN Model Types
In Amelia V3, BPNs have several possible types.
-   **Deterministic** — A BPN model whose tasks are executed sequentially. Its elements may perform dialog management and branching logic such as ad-hoc forks, joins, and gateways.
-   **Headless** —  A BPN model whose tasks don’t use conversation, for example, the Ask or Say tasks. Script, Set, Unset tasks are allowed, as well as forking, join, and gateways.
The model type is set in the Properties Panel of a BPN model by clicking a blank area of the workspace, opening the panel, and selecting Type.
# BPN Elements
A BPN maps Amelia's responses to a user interaction as a process flow diagram. It is an organized set of Events, Tasks, and Gateways linked by Flows. BPNs also can integrate with backend systems to complete tasks.
-   **Events** dictate the start and end of the BPN execution.
-   **Tasks** define actions within the BPN to specify what Amelia should say, ask, and do.
-   **Gateways** branch the execution based on patterns matched by the outgoing flows.
-   **Flows** control the execution path of the BPN between the various events, tasks, and gateways.
-   **Edge notation** controls a BPN process flow based on data collected in a conversation and other factors.
-   **Scripting** captures or transforms data used within a BPN conversation.
-   **Integrations** use Tasks and other BPN elements to allow Amelia to retrieve and update data stored in backend systems.
## Events
BPNs have two possible Event types:
-   A **Start Event** begins the process flow diagram.
-   An **End Event** is the final step in a process flow diagram.
## Tasks
Tasks can include a variety of ways to define actions Amelia can take as she works through a process. A Say task, for example, is a task that instructs Amelia what to say to a user while the Set the Variable task defines a variable. Task properties can be set in a BPN, for example, to script Amelia's behavior, capture names and dates to store as entities, or present files to the user.
BPN models that include a Run the Workflow task to call another BPN are called wrapper BPNs. The BPN model called by a wrapper BPN is called a sub BPN. Larger process flows ideally should be broken down into multiple BPNs and linked together as appropriate with a Run the Workflow task.
## Gateways and Flows
Choices and process direction within a BPN can be defined with Gateways and Flows. Sequence flows show the execution order of a process while Default flows are followed only if none of the exit sequence flows conditions are met. There are currently three types of gateways used in BPNs:
-   **Exclusive Gateways** follow only one possible flow from a gateway
-   **Inclusive Gateways** allow all exit flow sequences if their conditions are met
-   **Parallel Gateways** fork the BPN process into multiple parallel processes executed at the same time.
## Edge Notation
In addition to flows and gateways, the direction of a BPN process can be controlled by notation between the edges of a task or gateway. For example, answering yes or no can determine two different paths in the process flow. The notation is based on basic Java notation and has been updated for Amelia V3 to be more concise and flexible.
## Scripting
BPNs allows for scripting complex functions and processes to be executed during a process flow, for example, to display invoice data within an HTML table. Groovy and JavaScript languages are currently supported. Within the scope of a script tasks, the execution object allows for interaction between the BPN and the script through the getVariable and setVariable methods. The BPN script editor includes a syntax check tool, as well as a tool to run and test a script. Amelia V3 also includes support for FreeMarker and tabular data to present data within a conversation.
## Integrations
BPNs can use script and tasks to connect to third party software systems to perform tasks within an Amelia interaction. Amelia V3 integrations use the Apache Camel standard to connect and interact with a wide variety of third party sources.
