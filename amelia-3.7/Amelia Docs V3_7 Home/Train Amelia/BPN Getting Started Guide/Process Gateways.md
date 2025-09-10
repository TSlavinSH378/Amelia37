Gateways direct BPN process flows by testing values against variables. The variables are created through integrations and Script tasks or are captured by slot entities from user responses to Ask tasks.
Gateways allow for branching in the execution of a BPN based on specified criteria.
-   Exclusive gateways follow only one possible flow away from the gateway
-   Inclusive gateways allow execution of more than one path if more than one condition is met
-   Parallel gateways fork BPN execution to multiple branches at the same time.
> [!warning]  
>
> Gateways must be named in BPNs or a *Gateway is anonymous* message will appear when the BPN is deployed. To name a gateway, double-click the gateway icon and type a name in the text box that appears.

# Exclusive Gateways
Exclusive Gateways are the most common gateway used in BPN flows. The execution of the BPN can only follow one possible flow from the Exclusive Gateway. If none of the conditions of exit sequence flows are met and no default flow exists, Amelia will display an error.
The example below moves to default flow, income greater than 10000. When the value of income_level is less or equal to the default value, it would proceed to another flow.
![](attachments/11939550/11939555.png)
Figure. BPN Example of Exclusive Gateway with Default Flow and Alternate Paths
# Inclusive Gateways
Inclusive Gateways allow for the execution of all exit sequence flows if their conditions are met. As this could fork the execution of the BPN, the different branches of the inclusive gateways must be joined back together with another inclusive gateway. Failing to include the joining inclusive gateway will cause an error. This BPN triggers two flows as both are true.
![](attachments/11939550/11939554.png)
Figure. BPN Example of Inclusive Gateway with Two Flows that Trigger
# Parallel Gateways
Parallel Gateways fork the execution of the BPN to multiple branches. Each branch will be executed simultaneously. All branches must be joined together by another parallel gateway before the BPN execution can complete. Failing to include the joining parallel gateway will cause an error.
In the parallel gateway below, there is a say Lemma and an integration flow both executed in the same time.
![](attachments/11939550/11939551.png)
Figure. BPN Parallel Gateway Example
# Loop Example
Gateways and Flows can be used to create a loop within BPN executions. This can be useful to allow the user to revisit a question that they answered incorrectly. To create a loop, first set a variable, such as loopcount1, to 0. See below for the example loop.
![](attachments/11939550/11939553.png)
Figure. BPN Flow Loop Example
This loop allows the user to input their annual income. If the income is between 1114 and 1000000, the normal BPN flow will continue. However, if it is too small or too large, the BPN flow cannot continue. Instead of simply escalating immediately, the loop allows the user one chance to retype their income in case a mistake was made. If the user still inputs a number outside of the accepted range on the second pass through the loop, Amelia will now escalate to an agent.
# Gateway Operators and Expressions
Edge notation on a flow from a gateway can use a number of relational operators to evaluate criteria. Strings used in evaluations should be surrounded by double quotes. Flow expressions are set in the Expression field of the Properties Panel for a selected flow.
Table. Gateway Operators and Expressions
|                          |                  |     |
|--------------------------|:----------------:|:---:|
| Name                     |     Operator     |     |
| Equal To                 |        ==        | eq  |
| Greater Than             |        \>        | gt  |
| Less Than                |        \<        | lt  |
| Not Equal To             |        !=        | ne  |
| Less Than or Equal To    |       \<=        | le  |
| Greater Than or Equal To |       \>=        | ge  |
| And                      |        &&        | and |
| Or                       |       \|\|       | or  |
| Not Empty                | !empty *varName* |     |
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-1-5_10-22-11.png](attachments/11939550/11939551.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-5_10-14-40.png](attachments/11939550/11939552.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-3_12-21-50.png](attachments/11939550/11939553.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-3_12-21-4.png](attachments/11939550/11939554.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-3_12-20-43.png](attachments/11939550/11939555.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_16-14-31.png](attachments/11939550/11939556.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_16-14-8.png](attachments/11939550/11939557.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_16-13-42.png](attachments/11939550/11939558.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-27_16-13-16.png](attachments/11939550/11939559.png) (image/png)  
