-   [Text Messages](#SlackGatewayFeatures-TextMessages)
-   [Send Files to User](#SlackGatewayFeatures-SendFilestoUser)
-   [Quick Reply Options](#SlackGatewayFeatures-QuickReplyOptions)
-   [Get Information with Dialog Box](#SlackGatewayFeatures-GetInformationwithDialogBox)
**Table. Slack Gateway Features**
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Feature</th>
<th class="confluenceTh">Amelia Versions</th>
<th class="confluenceTh">Details</th>
</tr>
&#10;<tr class="odd">
<td class="confluenceTd"><h4 id="SlackGatewayFeatures-TextMessages">Text Messages</h4></td>
<td class="confluenceTd">All</td>
<td class="confluenceTd">Normal text message conversation is supported.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h4 id="SlackGatewayFeatures-SendFilestoUser">Send Files to User</h4></td>
<td class="confluenceTd">3.5.3+</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Amelia can send file to user, all the file formats which are supported by <a href="https://docs.ipsoft.com/display/AmeliaDocsV37/BPN+Tasks#BPNTasks-PresentTask">Present lemma</a>, are supported. <strong>Maximum file size limit is 1 Mb.</strong></p>
<div class="table-wrap">
<pre class="table"><code>| Image | PDF | Video |
| ----|----|----|
|  |  |  |</code></pre>
</div>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h4 id="SlackGatewayFeatures-QuickReplyOptions">Quick Reply Options</h4></td>
<td class="confluenceTd">3.5.4, 3.6.x, 3.7.x</td>
<td class="confluenceTd"><div class="content-wrapper">
<p><a href="Slack%20API">Set up the Slack App for Quick Reply feature.</a><br />
Quick reply options are coming from Amelia, generated from a BPN using FormInputData. The fieldType determines how the quick reply options are displayed, using buttons or using dropdown box. <strong>Currently slack allows only single selection of the option</strong>.<br />
To display as buttons, use fieldType "singleSelection" and to display as dropdown, use fieldType "multipleSelection".<br />
Once one of the given options is selected, the quick reply options message will be replaced by the selected option text.</p>
<div class="table-wrap">
<pre class="table"><code>| Using Buttons | Using DropDown |
| ----|----|
|  |  |</code></pre>
</div>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h4 id="SlackGatewayFeatures-GetInformationwithDialogBox">Get Information with Dialog Box</h4></td>
<td class="confluenceTd">3.5.4, 3.6.x, 3.7.1+</td>
<td class="confluenceTd"><div class="content-wrapper">
<p><a href="Slack%20API">Set up the Slack App for Dialog box.</a><br />
Apps can invoke dialogs after users interact with <a href="https://api.slack.com/docs/message-buttons">message buttons</a> or <a href="https://api.slack.com/docs/message-menus">message menus</a>. Each interaction will include a <code>trigger_id</code>, a kind of short-lived pointer to interaction.  <br />
We can use FormInputData to create a dialog box. The form type will be MultiLineInput.<br />
Supported field types are:  text, email, number, tel. Slack doesn't support <strong>password</strong> or <strong>date</strong> field type yet. <br />
The response will be sent back as a JSON, containing field name and the value, to the Request URL associated with your Slack app.</p>
</div></td>
</tr>
</tbody>
</table>
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-6-6_12-41-22.png](attachments/20807870/20807872.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-6-6_12-41-54.png](attachments/20807870/20807873.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-6-6_12-42-29.png](attachments/20807870/20807874.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-6-6_12-43-35.png](attachments/20807870/20807875.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-6-6_12-44-20.png](attachments/20807870/20807876.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-6-6_12-45-27.png](attachments/20807870/20807877.png) (image/png)  
