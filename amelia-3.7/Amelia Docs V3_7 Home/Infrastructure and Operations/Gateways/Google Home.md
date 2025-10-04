{% version "3.x" %}
The Amelia Google Home Gateway allows users to have a conversation with Amelia through Google Home devices and devices running Google Assistant, such as mobile phones.  
In addition to handling conversational questions and responses to and from Amelia, the gateway can also be directed to stream audio files to the Google Home device.  The audio files can be downloaded from Amelia (retrieved from Content Manager) or, preferably, streamed from an external media server.  
Download and use this form to collect client configuration details:  IPsoft-Amelia-GoogleHome-Gateway-Client-Information-1.0.pdf
In order to communicate with the Amelia gateway, an Actions on Google project and a Dialogflow Agent need to be created and deployed. To create the required action and agent a Google Cloud Platform account is required. Login to your Google Cloud Platform account and navigate to the Actions Console:  [https://console.actions.google.com](https://console.actions.google.com/). Follow the instructions below to setup Amelia and a Google Home speaker.
> [!warning]  
>
> This guide does not cover the required steps necessary to deploy the action for use by the general public.  Refer to Google's documentation for this information.

# Create a New Actions Project
1.  On the main page of the Actions Console, click New project.  
    ![](attachments/25461077/25461079.png)  
    Figure. Google Home Actions Page  
2.  Give the project a distinctive name and click Create project.  
    ![](attachments/25461077/25461080.png)  
    Figure. New Project Popup  
3.  Choose to build a Conversational experience in the bottom right section of the Welcome page.  
    ![](attachments/25461077/25461081.png)  
    Figure. Google Home Project Welcome Page
# Build the Action and Create the Dialogflow Agent
1.  After the project has been created, add an action from the Actions Console.  In the middle of the screen open Build your Action and click Add Action(s).  
    ![](attachments/25461077/25461082.png)  
    Figure. Google Home Actions Console  
2.  Click Add a first action.  
    ![](attachments/25461077/25461083.png)  
    Figure. Add Action Button  
3.  Choose Custom Intent from the left hand menu then click Build to display the Dialogflow console.  
    ![](attachments/25461077/25461084.png)  
    Figure. Build Button  
4.  In the Dialogflow console, give the agent a distinct name and click Create.  
    ![](attachments/25461077/25461085.png)  
    Figure. Give Agent a Name
# Import Amelia Specific Settings
After creating the agent in Dialogflow, import Amelia specific settings (Intents) into the agent.
1.  Go to the Agent's settings by clicking the gear icon next to the agent's name, in the upper left of the screen.  
    ![](attachments/25461077/25461088.png)  
    Figure. Agent Settings Screen  
2.  On the settings page click Export and Import in the upper middle of the screen.  
    ![](attachments/25461077/25461090.png)  
    Figure. Export and Import Link at Top of Middle of Screen  
3.  Click the RESTORE FROM ZIP button.  
    ![](attachments/25461077/25461091.png)  
    Figure. RESTORE FROM ZIP Button  
4.  Upload the Amelia Agent zip file (supplied by IPsoft) into the page.  
    ![](attachments/25461077/25461092.png)  
    Figure. Upload Agent Popup  
5.  Type RESTORE and click RESTORE to upload the zip file.  
    ![](attachments/25461077/25461093.png)  
    Figure. Upload Zip File  
6.  Click Done to complete the import.  
    ![](http://dtools.ipsoft.com/confluence/download/attachments/119046995/m_DialogflowClickDone.png)  
    Figure. Complete the Import Process  
7.  This is how the Dialogflow console (with Intents selected) should appear after the zip file has been imported.  
    ![](attachments/25461077/25461094.png)  
    Figure. Dialogflow Console with Intents Selected
> [!info]  
>
> With the exception of configuring the Fulfillment webhook, and possibly adding additional language support, no other modifications to this agent are required or suggested.

# Configure Fulfillment to Communicate with the Gateway
1.  To connect the Dialogflow Agent to the Amelia gateway, select Fulfillment from the left hand menu.  
    ![](attachments/25461077/25461096.png)  
    Figure. Fulfillment Screen  
2.  To enable a Webhook, click the Disabled button to toggle Enabled in the upper right portion of the page.  
    ![](attachments/25461077/25461097.png)  
    Figure. Enable Webhook  
3.  Add this information to the Webhook configuration.  
    Table. Webhook Configuration Settings  
    |            |                                                                                                                                    |
    |------------|------------------------------------------------------------------------------------------------------------------------------------|
    | Setting    | Description                                                                                                                        |
    | URL        | Enter the URL for Amelia in this format:  https://your-amelia-instance/Amelia/google/request                                       |
    | HEADERS    |                                                                                                                                    |
    | App-Name   | The value MUST be the same value used for the Display Name of the action specified in the Actions Console (see below for details)  |
    | App-Number | The value MUST be the value of the Project Number as assigned in the Google Cloud Platform for the project (see below for details) |
4.  Click the Save button, at the bottom right of the screen, to save changes.
# Finding Required Values for the Fulfillment Headers
1.  To find the Display Name required for the App-Name header value, navigate to the Actions Console ([https://console.actions.google.com](https://console.actions.google.com/)) and select Invocation from the left hand menu (under the Develop tab).  
    ![](attachments/25461077/25461098.png)  
    Figure. Find the Display Name  
    Enter the Display name from the above page into the App-Name header value on the Fulfillment page.  
    > [!warning]  
    >
    > The Display name is also the Invocation name used to invoke the action
2.  To find the Project Number required for the App-Number header value, navigate to the Google Cloud Platform Dashboard (<https://console.cloud.google.com/home/dashboard>) and select this project, if there are multiple projects.  
    ![](attachments/25461077/25461099.png)  
    Figure. Find Project Number  
3.  Enter the Project number from the Project info tab into the App-Number header value on the Fulfillment page.
# Test the Action Using the Simulator
Once the gateway is configured for this action and is running on the target host, test the integration using the Actions Console Simulator.
1.  To invoke the simulator, from the Dialogflow console click See how it works in Google Assistant on the right hand side of the page.  
    ![](attachments/25461077/25461100.png)  
    Figure. The See How It Works in Google Assistant Link  
2.  From the simulator, type text to simulate user utterances to communicate with Amelia.  
    ![](attachments/25461077/25461101.png)  
    Figure. Communicate with Amelia in Simulator
# Test the Action Using a Google Home Device or Google Assistant
To test outside the simulator, a Google Home device or a mobile phone or other device running Google Assistant is needed. This device and/or Google Assistant MUST be configured to connect to Google with the same account used to build this action on the Actions Console. Alternatively, deploy an Alpha release of the Action and invite up to 20 people to test on their own devices.  Refer to Google's documentation on how to deploy an Alpha release.
Once configured, use the invocation name defined in the Actions Console to start and test conversations with Amelia.
-   Hey Google, talk to ClientName Amelia
-   Ok Google, ask ClientName Amelia to play podcast episode one
Run at least one test from the simulator before accessing the action from a Google Home or Google Assistant device. Running from the simulator will update the action on Google so that it can be found by your test device.
> [!warning]  
>
> Refer to Google's documentation regarding the steps required to deploy the action for use by the general public.

{% /version %}
