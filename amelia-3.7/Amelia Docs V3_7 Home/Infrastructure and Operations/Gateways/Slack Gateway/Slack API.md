# Slack API URLs
-   -   **Real Time Messaging Api** - <https://api.slack.com/rtm>  
    -   **Send a file to user** - <https://api.slack.com/methods/files.upload>  
    -   **Quick reply buttons** - <https://api.slack.com/docs/message-buttons>  
    -   **Quick reply dropdown** - <https://api.slack.com/docs/message-menus>  
    -   **Interacting with Dialog box** - <https://api.slack.com/dialogs>  
    -   **Slash Commands** - <https://api.slack.com/slash-commands>
# Setting up Slack App for Quick Reply Buttons, Dropdown and Dialog
1.  Create an app at https://api.slack.com/apps/new if needed.
2.  Log into Slack → Navigate to Build → Your apps → Select the app -\> find the app's Interactive Components section.  
    ![](attachments/20807833/20807834.png)  
3.  Turn On the Interactive Components  
4.  Configure Request URL. Only configure one Request URL for the application. It will receive actions from all clicks happening throughout messages with buttons the app has produced, across all channels and workspaces. It's a master dispatch station for interactivity. The URL must be the hostname of Amelia followed by slack, for example, https://myameliaurl.com/Amelia/slack  
5.  Save Changes.
> [!warning]  
>
> Changes on the Amelia host are required and HAproxy also needs to be modified.  Instructions can be found here: HAproxy changes for Slack Quick Reply

