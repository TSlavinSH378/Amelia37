When an agent joins a conversation and the user is away from the conversation tab, the custom UI will display push notifications if the pushNotificationDisabled setting is set to false in the UI Bundles workspace. The first push notification will prompt the user to allow or block notifications.
The agent has joined notification pops up every 30 seconds if the user is not focused on the conversation browser tab. If the user starts typing in the chat input to respond to an agent notification popup, the popups will stop appearing.
> [!warning]  
>
> Popup notification functionality is not available for the Microsoft IE11 web browser and earlier. See <https://developer.mozilla.org/en-US/docs/Web/API/notification> for details.

# Notifications Display
When an agent joins a conversation, notification appears differently based upon the web browser used to chat with Amelia.
## Chrome Web Browsers
A Chrome browser displays a popup in the right corner of the browser window whether or not the conversation tab is open.
![](attachments/25462177/25462194.png)
Figure. Example of Agent Has Joined Popup in Chrome Browser
## Microsoft Edge Web Browser
With the Microsoft Edge web browser in Windows 10, the conversation tab displays an Agent has joined message and a popup appears in the lower right corner.
![](attachments/25462177/25462195.png)
Figure. Example of Agent Has Joined Tab in Microsoft Edge Browser
Notifications on Microsoft Edge can also behaves like Internet Explorer and/or push notifications. Simply pin Edge url link into taskbar through Edge's settings menu.
![](attachments/25462177/25462199.png)
Figure. Select the Pin This Page to the Taskbar Setting for Edge Browsers
## Internet Explorer Web Browsers
> [!warning]  
>
> Popup notification functionality is not available for the Microsoft IE11 web browser and earlier. See <https://developer.mozilla.org/en-US/docs/Web/API/notification> for details.

However, notifications on Microsoft Internet Explorer can be configured to flash in the taskbar when a URL link of the page is pinned to the taskbar.
To pin onto taskbar, simply drag the icon (refer to image below) next to the URL into the taskbar.
![](attachments/25462177/25462197.png)
Figure. Pinning to Task Bar: Click URL Icon
![](attachments/25462177/25462198.png)
Figure. Pinning to Task Bar: Drag URL Icon to Task Bar
# Enable or Disable Notifications
Notifications can be enabled or disabled with the pushNotificationDisabled setting. The UI Bundles workspaces, available by clicking the System Settings link on the left side of the Amelia administration pages, include the ability to define the Config Json settings for any custom UI bundle. Notifications cannot be set with the custom UI configurator interface.
To enable notifications, set the pushNotificationDisabled setting to false. To disable notifications, set the pushNotificationDisabled setting to true.
![](attachments/25462177/25462200.png)
Figure. Add or Edit the pushNotificationDisabled Setting
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-10-24_9-28-19.png](attachments/25462177/25462182.png) (image/png)  
![](images/icons/bullet_blue.gif) [agentJoinsRecording.gif](attachments/25462177/25462184.gif) (image/gif)  
![](images/icons/bullet_blue.gif) [agentJoinsRecording.gif](attachments/25462177/25462183.gif) (image/gif)  
![](images/icons/bullet_blue.gif) [image2019-10-24_10-7-27.png](attachments/25462177/25462186.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-24_11-57-2.png](attachments/25462177/25462194.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-24_12-17-28.png](attachments/25462177/25462195.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-24_12-24-46.png](attachments/25462177/25462196.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-24_12-28-30.png](attachments/25462177/25462197.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-24_12-30-2.png](attachments/25462177/25462198.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-24_12-38-53.png](attachments/25462177/25462199.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-24_12-43-8.png](attachments/25462177/25462200.png) (image/png)  
