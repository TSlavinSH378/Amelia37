{% version "3.x" %}
This service allows for the creation and recovery of transient variables. It provides a separate scope for variables longer than 64kB. Such scope is accessible from script tasks via TransientVariableService.
The following operations are available from TransientVariableService. Transient variables are accessible across all processes executed during a conversation, and removed once the conversation is closed (by the user or due to timeout).
# Methods
## hasVariable
    boolean hasVariable(String name)
Determines whether a transient variable exists.

| Parameter | Definition |
| ----|----|
| name | Variable name |

## addVariable
    Object addVariable(String name, Object value)
Adds a variable to a process instance's transient variable scope.
Table. BpnTransientVariableService addVariable Parameters/Definitions

| Parameter | Definition |
| ----|----|
| name | Variable name |
| value | Variable value |

## addVariables
    Map<String, Object> addVariables(Map<String, Object> variables)
Adds multiple variables to a process instance's transient variable scope.
Table. BpnTransientVariableService addVariables Parameters/Definitions

| Parameter | Definition |
| ----|----|
| variables | Map of Object values, keyed by Strings |

## getVariable
    Object getVariable(String name)
Obtains the value of a variable associated with a process instance. Returns null if the variable does not exist.
Table. BpnTransientVariableService getVariable Parameters/Definitions

| Parameter | Definition |
| ----|----|
| name | Variable name |

## getVariables
    Map<String, Object> getVariables()
Obtains all variables associated with a process instance. The variables are enclosed in a Map of Object values, keyed by Strings.
## clearVariables
    void clearVariables()
Removes all variables associated with a process instance.
## clearVariables
void clearVariables(Long conversationId)
Removes all transient variables associated with a conversation.
{% /version %}
