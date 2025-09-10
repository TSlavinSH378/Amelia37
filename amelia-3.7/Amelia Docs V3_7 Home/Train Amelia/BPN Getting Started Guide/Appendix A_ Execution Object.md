-   [Process Instance Methods](#AppendixA:ExecutionObject-ProcessInstanceMethods)
    -   [getId()](#AppendixA:ExecutionObject-getId())
    -   [processDefinitionId()](#AppendixA:ExecutionObject-processDefinitionId())
    -   [parentProcessInstanceId()](#AppendixA:ExecutionObject-parentProcessInstanceId())
    -   [currentTaskInstanceId()](#AppendixA:ExecutionObject-currentTaskInstanceId())
    -   [conversationId()](#AppendixA:ExecutionObject-conversationId())
    -   [status()](#AppendixA:ExecutionObject-status())
-   [Process Variable Methods](#AppendixA:ExecutionObject-ProcessVariableMethods)
    -   [getVariable(key)](#AppendixA:ExecutionObject-getVariable(key))
    -   [getVariables()](#AppendixA:ExecutionObject-getVariables())
    -   [getVariablesAsMap()](#AppendixA:ExecutionObject-getVariablesAsMap())
    -   [getVariableNames()](#AppendixA:ExecutionObject-getVariableNames())
    -   [hasVariables()](#AppendixA:ExecutionObject-hasVariables())
    -   [containsVariable(key)](#AppendixA:ExecutionObject-containsVariable(key))
    -   [setVariable(key, value)](#AppendixA:ExecutionObject-setVariable(key,value))
    -   [setVariables(variables)](#AppendixA:ExecutionObject-setVariables(variables))
    -   [removeVariable(key)](#AppendixA:ExecutionObject-removeVariable(key))
    -   [removeVariables(keys)](#AppendixA:ExecutionObject-removeVariables(keys))
    -   [removeVariables()](#AppendixA:ExecutionObject-removeVariables())
-   [User Information Methods](#AppendixA:ExecutionObject-UserInformationMethods)
    -   [domainId()](#AppendixA:ExecutionObject-domainId())
    -   [domainCode()](#AppendixA:ExecutionObject-domainCode())
    -   [domainName()](#AppendixA:ExecutionObject-domainName())
    -   [userId()](#AppendixA:ExecutionObject-userId())
    -   [userDisplayName()](#AppendixA:ExecutionObject-userDisplayName())
    -   [isAnonymous()](#AppendixA:ExecutionObject-isAnonymous())
-   [Analytic Memory](#AppendixA:ExecutionObject-AnalyticMemory)
    -   [addAnalyticOutcome(name, datum)](#AppendixA:ExecutionObject-addAnalyticOutcome(name,datum))
The execution object provides access to a BPN process instance, variables, and user information. For example, the *containsVariable(string key)* method tests whether or not a variable of a given key name exists while the *userDisplayName()* method captures the full name of the current logged in user.
``` groovy
def varsIn =   execution.containsVariable('getId');
def userName = execution.userDisplayName();
execution.setVariable('varsIn', varsIn);
execution.setVariable('userName', userName);
```
In this example, the variables *varsIn* or *userName* could be displayed with a Say task or used with edge notation to determine the BPN process flow.
# Process Instance Methods
## getId()
    String getId()
Gets then returns the process instance ID.
## processDefinitionId()
    String processDefinitionId()
Gets then returns the process definition ID.
## parentProcessInstanceId()
    String parentProcessInstanceId()
For a child BPN, gets then returns the parent BPN process instance ID.
## currentTaskInstanceId()
    String currentTaskInstanceId()
Gets then returns the current task instance ID.
## conversationId()
    String conversationId()
Gets then returns the conversation ID.
## status()
    String status()
Gets then returns the current process instance status, ACTIVE or INACTIVE.
# Process Variable Methods
## getVariable(key)
    Object getVariable(String key)
Get variable by the variable name in a given process instance. The key parameter is the name of the variable. Returns the variable as an object.
## getVariables()
    Set<VariableInstance> getVariables()
Get all variables in a given process instance. A map of all variables associated with their variable names is returned.
## getVariablesAsMap()
    Map<String, Object> getVariablesAsMap()
Get all variables in a given process as a map. Returns a map of all variables associated with their keys.
## getVariableNames()
    Set<String> getVariableNames()
Get all variable names for the given process instance. Returns a set of all variable names.
## hasVariables()
    boolean hasVariables()
Tests if a given process instance has one or more variables. Returns true if the given process instance has at least one variable.
## containsVariable(key)
    boolean containsVariable(String key)
Tests if a given process instance has a variable associated with the given variable name key. Returns true if the process contains the variable.
## setVariable(key, value)
    void setVariable(String key, Object value)
Add a variable to a given process instance with a variable name key and value.
## setVariables(variables)
    void setVariables(Map<String, Object> variables)
Adds variables to a process instance.
## removeVariable(key)
    void removeVariable(String key)
Removes a variable name key in a given process instance.
## removeVariables(keys)
    void removeVariables(Set<String> keys)
Bulk removal of a set of variables based on variable name keys in a given process instance.
## removeVariables()
    void removeVariables()
Bulk removal of all variables in a given process instance.
# User Information Methods
## domainId()
    String domainId()
Returns the current domain ID.
## domainCode()
    String domainId()
Returns the current domain code.
## domainName()
    String domainId()
Returns the current domain name.
## userId()
    String userId()
Returns the user ID.
## userDisplayName()
    String userDisplayName()
Returns the user friendly username.
## isAnonymous()
    boolean isAnonymous()
Returns true if the current conversation is anonymous.
# Analytic Memory
## addAnalyticOutcome(name, datum)
    void addAnalyticOutcome(String name, AbstractDatum datum)
Adds the current outcome of a process from the Analytic Memory functionality to the current BPN process, for example, to test if a conversation is likely to succeed or fail based on analytics then route the conversation flow afterwards. name is the name of the outcome and datum is the value. Outcomes with the same name will update and replace the existing name value.
This functionality is to be added shortly with examples.
