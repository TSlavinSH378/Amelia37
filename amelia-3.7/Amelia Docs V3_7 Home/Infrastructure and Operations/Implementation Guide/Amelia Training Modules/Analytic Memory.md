Amelia's Analytic Memory trains a predictive model used to steer conversations based on their correlation to the model. The predictive model is different from the reasoning models Amelia uses to engage in conversation.
Entities are created and connected to a series of Ask tasks in a BPN to gather data related to the predictive model. Answers to the Ask tasks feed into the model. A BPN Script task can evaluate how the current conversation responses compare to the predictive model then route the conversation based on the evaluation results.
For example, a predictive model for credit card issuance could use age, debt, and bank balance to predict whether or not credit would be extended. The model would use an existing data set to train Amelia how to predict a successful credit extension as well as no extension of credit. Amelia would ask questions about age, debt, and bank balance and use the responses to predict where the current conversation answers fall in relation to the predictive model. In addition, the answers from the current conversation would be incorporated into the predictive model to refine the model.
The initial existing data set might indicate someone age 23 with high student loan debt and a low bank balance would likely not be extended credit while a person age 44 with low debt and a higher bank balance would be extended credit. The predictive model might predict low age, high debt, and low bank balance would fail to gain credit while the opposite would succeed.The Analytic Memory feature allows Amelia to understand these dynamics and steer a conversation based on what the person says and what the model predicts.
The process to create, train, and deploy a predictive model with Analytic Memory follows these steps:
1.  Prepare a predictive model data set
2.  Create a predictive model
3.  Analyze and train the model
4.  Define the outcome variable
5.  Create Entities
6.  Create the BPN model to work with the predictive model
Each of these steps are described in detail in the [Analytic Memory Journey Graph](Analytic%20Memory%20Journey%20Graph).
