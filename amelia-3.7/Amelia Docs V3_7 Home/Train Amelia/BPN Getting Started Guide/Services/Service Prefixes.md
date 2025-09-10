Amelia V3 includes a notation system called service prefixes with a service:function() syntax. Service prefixes include a range of possible actions, for example, to capture and evaluate a user choice in a BPN with the bpn service prefix using bpn:choice() syntax.
Service prefixes are used in the Expression setting field in the Properties Panel for process flow lines.
# bpn: Functions
## choice
    bpn:choice(string... options)
bpn:choice('red')
Allows for the specification of a choice. This predicate takes one or more text values as argument. These values may be characters, words, or sentences.
## otherwise
    bpn:otherwise()
bpn:otherwise()
Allows for the specification of an outgoing edge that is followed if all of the other outgoing edges off of the same task cannot be followed. There are two equivalent ways to designate an edge as otherwise or default, use the edge expression bpn:otherwise() or mark the edge as a default flow. Where bpn:choice() finds valid options, bpn:otherwise() accepts all invalid options.
## attempts
    bpn:attempts()
bpn:attempts() == 2
Allows the number of attempts to execute the task to be used in an edge expression. Returns the number of consecutive attempts to execute the current task. 
# ctx: Functions
Refer to [Context Service](Context%20Service) for details.
# response: Functions
-   Predicates and functions available under the “response:” namespace will match only against the user’s response.
-   If an ask task has CONFIRM or ALWAYS_ASK behavior, "response:" predicates may be used on its outgoing transition.
-   In a stochastic BPN, response:value().matches("yes") is used instead of the slot:yes() service prefix as well as response:value().matches("no") for slot:no() and response:value().matches("idk") for slot:idk().
Response functions include a number of methods to evaluate equality or check for a value. The matches method can include regular expressions, for example,  response:value().matches(‘(?i)pizza’) to match case insensitive responses pizza or Pizza.
-   contains(String)
-   containsAny(String)
-   endsWith(String)
-   equal(String)
-   fuzzy(String, Double)
-   hasDigits()
-   hasLetters()
-   hasLettersAndDigits()
-   hasSpace()
-   idk()
-   in(String)
-   isAlphaNumeric()
-   isDecimal()
-   isInteger()
-   isNumber()
-   levenshteinDistance(String, Double)
-   like(String)
-   matches(String)
-   no()
-   startsWith(String)
-   yes()
## equal
    response:equal(string... option)
response:equal('red')
## value
    response:value(string... option)
response:value.matches('red')
Obtains the last utterance provided by the user in response to a question posed by an Ask task. Returns a string.
# slot: Functions
Entity slot functions obtain the normalized value of a slot for the current task. If a slot does not exist, Amelia will escalate. An entity model must be trained if the slot datum type is TEXT. In addition, the namespace references of slots and responses cannot be mixed when evaluating edges of the same task.
## equal
    slot:equal(string... option)
slot:equal('red')
## value
    slot:value(string... option)
slot:value.matches('red')
Obtains the normalized value of the slot instance associated with the current task. If called on a nonexistent slot, an escalation will occur.
Return types:
-   String for "text" slots.
-   Long for "integer" slots.
-   BigDecimal for "decimal" slots.
-   LocalDate for "date" slots.
-   LocalTime for "time slots.
-   Google Range\<T\> for rangeable slots.
The entity slot value has a number of methods available for evaluation. Most methods return boolean values.
-   contains(String)
-   containsAny(String)
-   containsNone(String)
-   endsWith(String)
-   equal(String)
-   fuzzy(String, Double)
-   get() –\> returns SlotInstance
-   hasDigits()
-   hasLetters()
-   hasLettersAndDigits()
-   hasLettersOrDigits()
-   hasSpace()
-   idk()
-   in(String)
-   isAlphaNumeric()
-   isDecimal()
-   isInteger()
-   isNotPresent()
-   isPresent()
-   isNumber()
-   levenshteinDistance(String, Double)
-   like(String)
-   matches(String)
-   no()
-   startsWith(String)
-   text() -\> returns String
-   value() -\> returns Object
-   yes()
## yes
    slot:yes()
slot:yes()
Evaluates to true if the response is affirmative, e.g., "yup", "yeah", "sure". In a stochastic BPN, response:value().matches("yes") is used instead of the slot:yes() service prefix.
## no
    slot:no()
slot:no()
Evaluates to true if the response is negative. e.g., "nope", "nah", "n". In a stochastic BPN, response:value().matches("no") for slot:no() service prefix.
## idk
    slot:idk()
slot:idk()
Evaluates to true if the response is "I don't know" or equivalent, e.g., "dunno", "idk", "not sure", "no idea". In a stochastic BPN, response:value().matches("idk") for slot:idk() service prefix.
## isPresent
    slot:isPresent()
slot:isPresent()
Use if the slot absolutely must be filled in response to an Ask task before the BPN process can continue.
# qty: Functions
The quantity (qty) prefix exposes functions to format the value of a slot. 
## format(String slotCode)
    format(String slotCode)
**Purpose**: Formats the latest slot instance of the slot code provided using the default formatter for the datum type of the object held by the slot instance.
**Parameters**:  
Takes the slot code as a parameter
## format(String slotCode, Formatters.\<FormatterType\>
    format(String slotCode, Formatters.<FormatterType>)
**Purpose**: Formats the latest slot instance of the slot code provided using the formatter, name of which is provided in the method call.
**Parameters**:  
Takes the slot code as the first parameter  
The second parameter is the Formatter to use to format the value
> [!warning]  
>
> To read more about Formatters, refer to [Appendix D: Formatters](Appendix%20D_%20Formatters) in the Amelia Trainer guide.

## format(String slotCode, Formatters.\<FormatterType\>, TimeZones.\<TimeZone\>)
    format(String slotCode, Formatters.<FormatterType>, TimeZones.<timeZone>)
**Purpose**: Formats the latest slot instance of the slot code provided using the formatter, name of which is provided in the method call. The time zone provided in the method is the one in which the datum value would be formatted in.
**Parameters**  
Takes the slot code as the first parameter  
The second parameter is the Formatter to use to format the value  
The third parameter is the TimeZone, the value needs to be formatted in.
> [!warning]  
>
> To read more about Formatters, refer to [Appendix D: Formatters](Appendix%20D_%20Formatters) in the Amelia Trainer guide. Time zones are listed in [Appendix E: Time Zones](Appendix%20E_%20Time%20Zones) of the same guide.

# tabularDataService: Functions
Tabular Data grammar, query operator, conditional operators, and other details are in the [Tabular Data](https://docs.ipsoft.com/display/AmeliaDocsV3/Script+Tasks#ScriptTasks-TabularDataTabularDataSources) section of the [Script Tasks](Script%20Tasks) page.
# Operators
A full set of operators can be used with ctx:, response:, bpn:, and slot: service prefixes to define task edge notation conditions for flow lines. As with Amelia V2, only slots can be used to define edge notation from gateways. Edge conditions are defined in the Expression setting field of the flow line Properties Panel.
    ctx:slot('roomNumber').value()!=null
    ctx:slot('roomNumber').value()==null
    slot:value()==10
    slot:value()!=10
    slot:value()>10
    slot:value()>=250
    slot:value()<2
    slot:value()<=500
Operators also can be concatenated with no spaces and the namespaces repeated. Or is a double pipe (\|\|) while And is a double ampersand (&&).
`slot:equal('14')||slot:equal("15")`
