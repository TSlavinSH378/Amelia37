The Context Service provides access to slot entity and intent operations within a BPN for Script tasks and libraries.
-   Predicates and functions available under the “slot:” namespace will match only against the value of the slot associated with the task.
-   The outgoing transitions of a task and expressions on edge transitions should not mix references to the namespaces “slot:” and “response:”
-   If a task has a slot reference, "response:” references must not be allowed on its outgoing transitions.
-   If a task does not have a slot reference, “slot:” references must not be allowed on its outgoing transitions.
-   If an Ask task has its Properties Panel Ask behavior (1st pass) and Ask behavior (subsequent) settings set to Confirm or Always Ask, "slot:" predicates may be used on its outgoing transition.
-   If an Ask task has its Properties Panel Ask behavior (1st pass) and Ask behavior (subsequent) settings set to Ignore if Responded, only “slot:value() …” predicates are acceptable on its outgoing transitions. Whether or not the task in question will be ignored upon the existence of a slot instance depends on the existence of the slot itself.
-   If an Ask task has its Properties Panel Ask behavior (1st pass) and Ask behavior (subsequent) settings set to Ignore if Responded, and is associated with a slot definition, and a slot instance is defined for it, and the value of the slot instance does not satisfy any of the outgoing transitions, then the BPN engine must re-elicit the task with a sentence like "The value of x is not acceptable, please provide something like x, y, or z"
# Slot Entity Methods
## latestSlots
    Set<SlotInstanceDto> latestSlots();
ctx:latestSlots()  
contextService.latestSlots()
Obtains the slots elicited after the last user utterance.
## slots
    Set<SlotInstanceDto> slots();
ctx:slots()  
contextService.slots()
Obtains elicited slots associated with the current context.
## newSlots
    List<SlotInstanceDto> newSlots()
Slot instances that have been elicited for the first time over the last user response.
## modifiedSlots
    List<SlotInstanceDto> modifiedSlots()
Slot instances that have been elicited over the last utterance, but one or more instances already existed in the current context.
## oldSlots
    List<SlotInstanceDto> oldSlots()
Slot instances that have not been elicited or updated over the last user utterance.
## slots (by slot code)
    List<SlotInstanceDto> slots(String slotCode)
Obtains elicited slots associated with the current context by its code.
    Parameters:
-   slotCode: code of the slot (definition) whose instances is being obtained.
Return:
-   List of slots.
## hasSlot
    boolean hasSlot(String slotCode)
ctx:hasSlot('fullName')  
contextService.hasSlot('fullName')
Determines whether a slot was elicited.
Parameters:
-   slotCode: code of the slot (definition) whose instance existence is being tested.
Return:
-   *true* if the slot exists in the current context.
## latestSlot
    DatumDecorator latestSlot(String slotCode)
Obtains the value of a slot by its code.
**Parameters:**
-   slotCode: code of the slot (definition) whose instance value is being obtained.
**Return:**
-   DatumDecorator.
## hasNewSlotsForCode
    boolean hasNewSlotsForCode(String slotCode)
Determines whether at least one of the first time elicited slots are associated with a slot definition.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   *true* if there is at least one of the first time elicited slots are associated with a slot definition.
## newSlotsForCode
    Set<SlotInstanceDto> newSlotsForCode(String slotCode)
Obtains all the first time elicited slots that are associated with a slot definition.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   Set of slots.
## hasModifiedSlotsForCode
    boolean hasModifiedSlotsForCode(String slotCode)
Determines whether at least one of the newly elicited slots are associated with a slot definition and one or more slot instances already existed in the current context.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   *true* if there is at least one of the newly elicited slots are associated with a slot definition.
## intentHistory
    Set<IntentInstanceDto> intentHistory()
Retrieves the history of triggered intents throughout the conversation. Returns a set of intent instances, preserving the original order.
``` groovy
def intents = contextService.intentHistory()
                .collect { intent -> "$intent.intent.name" }
                .join(', ');
execution.setVariable('intents', intents);
```
## modifiedSlotsForCode
    Set<SlotInstanceDto> modifiedSlotsForCode(String slotCode)
Obtains all newly elicited slots that are associated with a slot definition and one or more instances already existed in the current context.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   Set of slots.
## hasLatestSlotsForCode
    boolean hasLatestSlotsForCode(String slotCode)
Determines whether at least one of the newly elicited slots are associated with a slot definition.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   *true* if there is at least one of the newly elicited slots are associated with a slot definition.
## latestSlotsForCode
    Set<SlotInstanceDto> latestSlotsForCode(String slotCode)
Obtains all newly elicited slots that are associated with a slot definition.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   Set of slots.
## hasOldSlotsForCode
    boolean hasOldSlotsForCode(String slotCode)
Determines whether at least one slot that is associated with a slot definition but has not been created or updated over the last utterance.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   *true* if there is at least one slot that is associated with a slot definition.
## oldSlotsForCode
    Set<SlotInstanceDto> oldSlotsForCode(String slotCode)
Obtains all slots that are associated with a slot definition but have not been created or updated over the last utterance.
**Parameters:**
-   slotCode: code of the slot (definition) whose instances is being obtained.
**Return:**
-   Set of slots.
# Slot Entity Data Types
These data types are used by slot-related operations. All fields are only accessible via accessors, e.g., to obtain the *datum* field from a *SlotInstanceDto* object in Groovy, use "def value = slotEntity.datum()".
## Definition
The slot definition is represented internally by the class Slot.
## Instance
The slot instance is represented internally by the class SlotInstanceDto.
## Fields
All fields are accessible with accessors, for example, to access the datum field use *contextService.latestSlot(slotCode).datumType()*.

| Field | Description |
| ----|----|
| slotInstanceId | UUID |
| slotId | UUID |
| datum | Populated DatumDecorator object |
| value | The value held by the Datum object The value returned would be different based on the type of DatumDecorator object returned. |
| datumType | The type of datum |

# Intent Methods
## triggeredIntent
    IntentInstanceDto triggeredIntent()
ctx:triggeredIntent()  
contextService.triggeredIntent().intent().code()  
execution.setVariable("triggeredIntent", contextService.triggeredIntent())
The currently triggered or running intent, if existing.
Return:
-   The running intent, or *null* if none.
## processIntents
    IntentDto processIntents()
All intents that point to the BPN process in context and are visible from the current domain.
**Return:**
-   A set of intent definitions, which may be empty.
## isCurrentProcessTargetedByIntent
    boolean isCurrentProcessTargetedByIntent(String intentCode);
ctx:isCurrentProcessTargetedByIntent()  
contextService.isCurrentProcessTargetedByIntent()  
execution.setVariable("isTriggeredByIntent", contextService.isCurrentProcessTargetedByIntent("mortgage_help"))
All intents that point to the BPN process in context and are visible from the current domain.
Parameters:
-   intentCode: Code of the intent definition whose instance may have been used to trigger the current BPN execution.
Return:
-   *true* if the current process instance was kicked off by the specified intent
# Intent Data Types
These data types are used by intent-related operations. All fields are only accessible via accessors, e.g., to obtain the *datum* field from a *SlotInstanceDto* object in Groovy, use "def value = slotInstance.datum()".
## Definition
The slot definition is represented internally by the class IntentDto. All fields are accessible with accessors.

| Field | Description |
| ----|----|
| id | UUID |
| code | String |
| name | String |
| actionType | EXECUTE_BPN, ECHO_GOAL |
| actionSystemData | String, BPN model name |

## Instance
The intentinstance is represented internally by the class IntentInstanceDto.
## Fields
All fields are accessible with accessors.

| Field | Description |
| ----|----|
| id | UUID |
| intent | IntentDto |

# Examples
This example demonstrates the use of the intent-related operations provided by *contextService*.
``` groovy
execution.setVariable("triggeredIntent", contextService.triggeredIntent())
execution.setVariable("processIntents", contextService.processIntents().collect { it.code() })
execution.setVariable("isTriggeredByIntent", contextService.isCurrentProcessTargetedByIntent("mortgage_help"))
```
