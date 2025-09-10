-   [Methods](#EscalationQueueService-Methods)
    -   [getNumberOfAvailableAgentsByQueueCode](#EscalationQueueService-getNumberOfAvailableAgentsByQueueCode)
    -   [getNumberOfAvailableAgentsByQueueName](#EscalationQueueService-getNumberOfAvailableAgentsByQueueName)
    -   [getAvailableAgentsByQueueCode](#EscalationQueueService-getAvailableAgentsByQueueCode)
    -   [getAvailableAgentsByQueueName](#EscalationQueueService-getAvailableAgentsByQueueName)
    -   [getNumberOfBusyAgentsByQueueCode](#EscalationQueueService-getNumberOfBusyAgentsByQueueCode)
    -   [getNumberOfBusyAgentsByQueueName (new 3.6.x)](#EscalationQueueService-getNumberOfBusyAgentsByQueueName(new3.6.x))
    -   [getNumberOfReadyAgentsByQueueCode (new 3.6.x)](#EscalationQueueService-getNumberOfReadyAgentsByQueueCode(new3.6.x))
    -   [getNumberOfReadyAgentsByQueueName (new 3.6.x)](#EscalationQueueService-getNumberOfReadyAgentsByQueueName(new3.6.x))
    -   [getNumberOfQueuedChatsByQueueCode (new 3.6.x)](#EscalationQueueService-getNumberOfQueuedChatsByQueueCode(new3.6.x))
    -   [getNumberOfQueuedChatsByQueueName (new 3.6.x)](#EscalationQueueService-getNumberOfQueuedChatsByQueueName(new3.6.x))
    -   [getNumberOfActiveChatsByQueueCode (new 3.6.x)](#EscalationQueueService-getNumberOfActiveChatsByQueueCode(new3.6.x))
    -   [getNumberOfActiveChatsByQueueName (new 3.6.x)](#EscalationQueueService-getNumberOfActiveChatsByQueueName(new3.6.x))
This service provides operations associated with the agent information of a given escalation queue. It is exposed as "escalationQueueService", to script tasks and libraries.
# Methods
## getNumberOfAvailableAgentsByQueueCode
    int getNumberOfAvailableAgentsByQueueCode(String queueCode)
Returns the number of available agents for the specified escalation queue code.

| Parameter | Description |
| ----|----|
| queueCode | The code of the Escalation Queue |
| value | The number of available agents |

## getNumberOfAvailableAgentsByQueueName
    int getqueueNumberOfAvailableAgentsByQueueName(String queueName)
Returns the number of available agents for the specified escalation queue name.

| Parameter | Description |
| ----|----|
| queueName | The name of the Escalation Queue |
| value | The number of available agents |

## getAvailableAgentsByQueueCode
    List<UserDto> getAvailableAgentsByQueueCode(String queueCode)
Returns the list of the available agents for the specified escalation queue code.

| Parameter | Description |
| ----|----|
| queueCode | The code of the Escalation Queue |

## getAvailableAgentsByQueueName
    List<UserDto> getAvailableAgentsByQueueName(String queueName)
Returns the list of the available agents for the specified escalation queue name.

| Parameter | Description |
| ----|----|
| queueName | The name of the Escalation Queue |

## getNumberOfBusyAgentsByQueueCode
    int getNumberOfBusyAgentsByQueueCode(String queueCode)
Returns the number of agents busy for the specified escalation queue code.

| Parameter | Definition |
| ----|----|
| queueCode | The code of the escalation queue |

## getNumberOfBusyAgentsByQueueName (new 3.6.x)
    int getNumberOfBusyAgentsByQueueName(String queueName)
Returns the number of busy agents for the specified escalation queue name.

| Parameter | Definition |
| ----|----|
| queueName | The name of the escalation queue |

## getNumberOfReadyAgentsByQueueCode (new 3.6.x)
    int getNumberOfReadyAgentsByQueueCode(String queueCode)
Returns the number of ready agents for the specified escalation queue code.

| Parameter | Definition |
| ----|----|
| queueCode | The code of the escalation queue |

## getNumberOfReadyAgentsByQueueName (new 3.6.x)
    int getNumberOfReadyAgentsByQueueName(String queueName)
Returns the number of ready agents for the specified escalation queue name.

| Parameter | Definition |
| ----|----|
| queueName | The name of the escalation queue |

## getNumberOfQueuedChatsByQueueCode (new 3.6.x)
    int getNumberOfQueuedChatsByQueueCode(String queueCode)
Returns the number of queued chat sessions for the specified escalation queue code.

| Parameter | Definition |
| ----|----|
| queueCode | The code of the escalation queue |

## getNumberOfQueuedChatsByQueueName (new 3.6.x)
    int getNumberOfQueuedChatsByQueueName(String queueName)
Returns the number of queued chat sessions for the specified escalation queue name.

| Parameter | Definition |
| ----|----|
| queueName | The name of the escalation queue |

## getNumberOfActiveChatsByQueueCode (new 3.6.x)
    int getNumberOfActiveChatsByQueueCode(String queueCode)
Returns the number of active (i.e., currently handled) chat sessions for the specified escalation queue code.

| Parameter | Definition |
| ----|----|
| queueCode | The code of the escalation queue |

## getNumberOfActiveChatsByQueueName (new 3.6.x)
    int getNumberOfActiveChatsByQueueName(String queueName)
Returns the number of active (i.e., currently handled) chat sessions for the specified escalation queue code.

| Parameter | Definition |
| ----|----|
| queueName | The name of the escalation queue |

