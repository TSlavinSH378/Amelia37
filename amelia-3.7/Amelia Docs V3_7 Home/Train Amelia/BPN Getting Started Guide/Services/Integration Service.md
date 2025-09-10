The `integrationService` service provides integration flow related operations to BPN Script tasks and libraries. Many times a Run the Integration Flow task is followed by a Script task used to parse output from the preceding task. The Integration Service allows a Script task to interact with integration flows directly and adapt data, in some cases without any limitations of a BPN task.
# Methods
## runSynchronously(String flowName)
    void runSynchronously(@NonNull String flowName)
Runs the specified integration flow automatically, building the context from all variables in the current execution to the integration flow.  
Once the integration flow execution is complete, the resulting variables will automatically overwrite the ones found in the current execution.
> [!warning]  
>
> Depending on the number of variables held in the current process instance, this method will be slow.

Table. runSynchronously Parameters/Definitions

| Parameter | Definition |
| ----|----|
| flowName | Name of the integration flow |

## Map runSynchronously(String flowName, Map context)
    void runSynchronously(@NonNull String flowName)
Runs the specified integration flow, solely using the specified context as input, and returning the integration flow execution outcome in a map without automatically overwriting process instance variable(s).
Returns the integration flow execution outcome.
> [!warning]  
>
> This operation is significantly faster when the current process instance handles a large number of variables (more than 10).

Table. Map\<String, Object\> runSynchronously Parameters/Definitions

| Parameter | Definition |
| ----|----|
| flowName | Name of the integration flow |
| context | Context for the integration flow execution |

# Examples
To call the integrationService with only the flow name and no context:
``` groovy
integrationService.runSynchronously('multiply')
```
This example might include Camel code in the flow that sets a property `result` and JavaScript to use the Camel `exchange` method to return a value available within the BPN context for tasks to use:
``` groovy
<setProperty propertyName="result">
<javaScript>var result=exchange.getProperty('x')*2;result</javaScript>
</setProperty>
```
In this example, `runSynchronously` calls the flow and passes a Groovy HashMap with a single value. The result is assigned to a single variable `sum` which is available within the BPN context for tasks to use:
``` groovy
def outgoingVariable = execution.getVariable('response');
def outgoingVariableMap = new HashMap();
outgoingVariableMap.put('x', outgoingVariable)
def incomingVariableMap = integrationService.runSynchronously('multiply', outgoingVariableMap)
execution.setVariable('sum', incomingVariableMap.get('result'));
```
