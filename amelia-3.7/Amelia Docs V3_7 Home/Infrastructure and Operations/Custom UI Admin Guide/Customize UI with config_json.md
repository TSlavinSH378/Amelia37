# Customize Links, UI, and Functionality
<table class="wrapped relative-table confluenceTable" style="width: 91.7202%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 8%" />
<col style="width: 27%" />
<col style="width: 52%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh">Task</th>
<th class="confluenceTh">Config.json Version</th>
<th class="confluenceTh">Properties</th>
<th class="confluenceTh">Process</th>
</tr>
&#10;<tr class="odd">
<td colspan="4" class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-Add/HideLinks"><strong>Add/Hide Links</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-AddLiveAgentlink">Add Live Agent link</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">agent, hideAgentHelp, escalationBpn</td>
<td class="confluenceTd">Set agent to <code>true</code>, hideAgentHelp to <code>false</code>, and escalationBpn to the name of an escalation BPN.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-HideLiveAgentlink">Hide Live Agent link</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">agent, hideAgentHelp</td>
<td class="confluenceTd">Set agent to <code>false</code>, hideAgentHelp to <code>true</code>.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-AddFeedbacklink">Add Feedback link</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">feedback, feedbackBPN</td>
<td class="confluenceTd">Set feedback to <code>true</code> and feedbackBPN to the name of a BPN used to handle feedback.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-HideFeedbacklink">Hide Feedback link</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">feedback</td>
<td class="confluenceTd">Set feedback to <code>false</code>. The feedback link text can be updated with the <a href="#CustomizeUIwithconfig.json-customTranslation">customTranslation property</a>.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-AddaContactUslink">Add a Contact Us link</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">showMailLink, mailToLink</td>
<td class="confluenceTd">Set showMailLink to <code>true</code> to display a Contact Us link. Set mailToLink property to an appropriate email address. The Contact Us link text can be updated with the <a href="#CustomizeUIwithconfig.json-customTranslation">customTranslation property</a>.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-AddaPrivacyPolicylink">Add a Privacy Policy link</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">showPrivacyPolicy, privacyPolicyLink, privacyPolicyContent</td>
<td class="confluenceTd">Set showPrivacyPolicy to true to display a Privacy Policy link. Set privacyPolicyLink to an appropriate web URL. Add content to the privacyPolicyContent property, for example, <code>[ "My privacy", "policy", "content" ]</code>. The Privacy Policy link text can be updated with the <a href="#CustomizeUIwithconfig.json-customTranslation">customTranslation property</a>.</td>
</tr>
<tr class="even">
<td colspan="4" class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-UserInterface"><strong>User Interface</strong></h4></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-AlwaysHideTooltipAboveChatbox">Always Hide Tooltip Above Chatbox</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">tooltipAcknowledged</td>
<td class="confluenceTd">Set tooltipAcknowledged to <code>false</code> to hide the rectangle tooltip box immediately above the chatbox. To display the tooltip, set to true.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-UpdateBrowserTabTitleandFavicon">Update Browser Tab Title and Favicon</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">browserTabTitle, favicon</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Set browserTabTitle to a string value, for example, "Amelia" or "Company Name". The favicon value also can be set by adding the <code>favicon</code> property to the JSON file with a setting of a URL or base64 string.</p>
<p><img src="attachments/11946019/11946020.png" /></p>
<p>Figure. browserTabTitle set to "My Cool Site"</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-AddBlueFocusRinginChatInput">Add Blue Focus Ring in Chat Input</h5></td>
<td class="confluenceTd">5.13.0+</td>
<td class="confluenceTd">hideChatInputFocusRingColor</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>For accessibility, set hideChatInputFocusRingColor to <code>false</code> to display a blue line around the chat text area within the chatbox. The blue focus ring is hidden by default.</p>
<p><img src="attachments/11946019/11946021.png" /></p>
<p>Figure. hideChatInputFocusRingColor set to false</p>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-HideBlueFocusRinginChatInput">Hide Blue Focus Ring in Chat Input</h5></td>
<td class="confluenceTd">5.13.0+</td>
<td class="confluenceTd">hideChatInputFocusRingColor</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Set hideChatInputFocusRingColor to <code>true</code> to not display a blue line around the chat text area within the chatbox. The blue focus ring is hidden by default.</p>
<p><img src="attachments/11946019/11946022.png" /></p>
<p>Figure. hideChatInputFocusRingColor set to true</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-HideLoginandAnonymousAmeliaDomains">Hide Login and Anonymous Amelia Domains</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">hideLogin, showAnonymousDomains</td>
<td class="confluenceTd"><p>Set hideLogin to <code>false</code> and showAnonymousDomains to <code>true</code> to display the login box and list any domains that accept anonymous logins in the list of domains. User logs in at /Amelia/ui/BUNDLE_NAME/login.</p>
<p>Set hideLogin to <code>true</code> to display only a list of any domains that accept anonymous logins. User logs in at /Amelia/ui/BUNDLE_NAME/login. (Available 5.11.0+)</p>
<p>Set showAnonymousDomains to <code>false</code> to display the login box and hide any a list of any domains that accept anonymous logins. User logs in at /Amelia/ui/BUNDLE_NAME/login.</p>
<p>Set hideLogin to <code>true</code> and showAnonymousDomains to <code>false</code> to display a blank login page. This combination requires users to login through the /Amelia/admin URL then use a non-anonymous domain URL, for example, /Amelia/ui/BUNDLE_VERSION/?domainCode=NON_ANONYMOUS_AMELIA_DOMAIN_CODE. (Available 5.11.0+)</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-ToggleSecondsPropertyonChatTimestamp">Toggle Seconds Property on Chat Timestamp</h5></td>
<td class="confluenceTd">5.15.0+</td>
<td class="confluenceTd">showSecondsInTimeStamp</td>
<td class="confluenceTd">Set showSecondsInTimeStamp to <code>true</code> to display seconds in the timestamp in the chat conversation area, for example, HH:MM:SS. Set to <code>false</code> to display only the hour and minutes, for example, HH:MM.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-ScrolltoAmelia&#39;sFirstMessage">Scroll to Amelia's First Message</h5></td>
<td class="confluenceTd">5.14.0+</td>
<td class="confluenceTd">scrollToFirstOfAmeliaMessagesGroup</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Add scrollToFirstOfAmeliaMessagesGroup to the config.json file and set to <code>false</code> to display the latest of Amelia's messages, with older messages scrolled up out of view. Set to <code>true</code> to lock her first message at the top of the conversation area with new conversation scrolled up out of view.</p>
<p><img src="attachments/11946019/11946023.gif" /></p>
<p>Figure. scrollToFirstOfAmeliaMessagesGroup set to false</p>
<p><img src="attachments/11946019/11946024.gif" /></p>
<p>Figure. scrollToFirstOfAmeliaMessagesGroup set to true</p>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-Customizeselectbuttonsshape,color,andsize">Customize select buttons shape, color, and size</h5></td>
<td class="confluenceTd">5.18.4+</td>
<td class="confluenceTd"><p>radioSelectButtonOn, checkedSelectButtonColor, uncheckedSelectButtonColor, customizeOldStyleButtons, border, borderRadius</p></td>
<td class="confluenceTd"><p><code class="sourceCode javascript" style="text-align: left;">{</code><br />
<code class="sourceCode javascript" style="text-align: left;">    </code><code class="sourceCode javascript" style="text-align: left;">ui<span class="op">:</span> {</code><br />
<code class="sourceCode javascript" style="text-align: left;">        </code><code class="sourceCode javascript" style="text-align: left;">variables<span class="op">:</span> {</code><br />
<code class="sourceCode javascript" style="text-align: left;">            </code><code class="sourceCode javascript" style="text-align: left;">radioSelectButtonOn<span class="op">:</span> </code><code class="sourceCode javascript" style="text-align: left;"><span class="kw">true</span></code><code class="sourceCode javascript" style="text-align: left;"><span class="op">,</span></code><br />
<code class="sourceCode javascript" style="text-align: left;">            </code><code class="sourceCode javascript" style="text-align: left;">checkedSelectButtonColor<span class="op">:</span> </code><code class="sourceCode javascript" style="text-align: left;"><span class="st">&#39;orange&#39;</span></code><code class="sourceCode javascript" style="text-align: left;"><span class="op">,</span></code><br />
<code class="sourceCode javascript" style="text-align: left;">            </code><code class="sourceCode javascript" style="text-align: left;">uncheckedSelectButtonColor<span class="op">:</span> </code><code class="sourceCode javascript" style="text-align: left;"><span class="st">&#39;pink&#39;</span></code><code class="sourceCode javascript" style="text-align: left;"><span class="op">,</span></code><br />
<code class="sourceCode javascript" style="text-align: left;">            </code><code class="sourceCode javascript" style="text-align: left;">customizeOldStyleButtons<span class="op">:</span> {</code><br />
<code class="sourceCode javascript" style="text-align: left;">               </code><code class="sourceCode javascript" style="text-align: left;">border<span class="op">:</span> </code><code class="sourceCode javascript" style="text-align: left;"><span class="st">&#39;10px solid&#39;</span></code><code class="sourceCode javascript" style="text-align: left;"><span class="op">,</span></code><br />
<code class="sourceCode javascript" style="text-align: left;">               </code><code class="sourceCode javascript" style="text-align: left;">borderRadius<span class="op">:</span> </code><code class="sourceCode javascript" style="text-align: left;"><span class="st">&#39;8px&#39;</span></code><br />
<code class="sourceCode javascript" style="text-align: left;">            </code><code class="sourceCode javascript" style="text-align: left;">}</code><br />
<code class="sourceCode javascript" style="text-align: left;">        </code><code class="sourceCode javascript" style="text-align: left;">}</code><br />
<code class="sourceCode javascript" style="text-align: left;">    </code><code class="sourceCode javascript" style="text-align: left;">}</code><br />
<code class="sourceCode javascript" style="text-align: left;">}</code></p></td>
</tr>
<tr class="odd">
<td colspan="4" class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-Functionality"><strong>Functionality</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-Rejoinlastactiveconversationifuserreloadspage">Rejoin last active conversation if user reloads page</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">rejoin</td>
<td class="confluenceTd">Set rejoin to <code>true</code> to rejoin last active conversation if page is reloaded. Set to <code>false</code> or empty to start new conversation.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-EnableHotKeys">Enable Hot Keys</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">enableHotkeys</td>
<td class="confluenceTd">Set enableHotkeys to <code>true</code>. If set to true, Function+F5 resets the conversation and a . (period) triggers the microphone.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-EnableSpeechtoText(STT)">Enable Speech to Text (STT)</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">showMic, sttDelay</td>
<td class="confluenceTd"><div class="content-wrapper">
<blockquote>
<p>[!warning]<br />
</p>
<p>This functionality is only supported with modern Google Chrome web browsers.</p>
</blockquote>
<p> </p>
<p>Set showMic to <code>true</code> to display the Microphone icon on the right side of the chatbox. Set showMic to <code>false</code> to hide the Microphone icon. To add delay before an utterance is submitted to Amelia, add the JSON property sttDelay and set it to seconds, for example, <code>3000</code> for 3 seconds. <code>1500</code> or 1.5 seconds is the default.</p>
</div></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-EnableTexttoSpeech(TTS)">Enable Text to Speech (TTS)</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">speech</td>
<td class="confluenceTd"><div class="content-wrapper">
<blockquote>
<p>[!warning]<br />
</p>
<p>This functionality is not supported with the Internet Explorer 11 web browser.</p>
</blockquote>
<p> </p>
<p>Set speech to <code>true</code> to hear Amelia speak her text utterances in the default VW Julie voice in English. Set speech to <code>false</code> to stop hearing Amelia speak her utterances. Refer to the Text to Speech pages for more details.</p>
</div></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-GotoHiddenDomain">Go to Hidden Domain</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">includeHiddenDomains</td>
<td class="confluenceTd"><p>Set the includeHiddenDomains property to a defined URL that includes the domain code for the hidden domain, for example, <a href="PROTOCOL://DOMAIN/Amelia/ui/BUNDLE_NAME/?domainCode=HIDDEN_AMELIA_DOMAIN_CODE"><code>PROTOCOL://DOMAIN/Amelia/ui/BUNDLE_NAME/?domainCode=HIDDEN_AMELIA_DOMAIN_CODE</code></a>. This routes the user directly to a chat interface for the domain after a successful login.</p>
<p>Set the includeHiddenDomains property to <code>false</code> to display a list of domains to be selected after a successful login and before the chat interface appears.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-RequestUserAgentData">Request User Agent Data</h5></td>
<td class="confluenceTd">5.13.0+</td>
<td class="confluenceTd">sendUserAgent</td>
<td class="confluenceTd">Set sendUserAgent to <code>true</code>. The user data is sent by an initial conversation attribute and is available to BPN Script tasks with the execution.getCustomConversationAttribute("userAgent") and execution.getCustomConversationAttributesAsMap() methods.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-RequireConfirmationtoResetConversation">Require Confirmation to Reset Conversation</h5></td>
<td class="confluenceTd">5.14.0+</td>
<td class="confluenceTd">resetConfirmation</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Set resetConfirmation to <code>true</code> to display a popup with two buttons, Resume and Reset, when a conversation is reset.</p>
<blockquote>
<p>[!info]<br />
</p>
<p>Selecting the Reset button deletes all chat history.</p>
</blockquote>
<p><br />
</p>
</div></td>
</tr>
<tr class="odd">
<td colspan="4" class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-Google"><strong>Google</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-DisableGoogleAssetsCallsonPageLoad">Disable Google Assets Calls on Page Load</h5></td>
<td class="confluenceTd">5.16.0+</td>
<td class="confluenceTd">includeExternalAssets</td>
<td class="confluenceTd">Set to <code>true</code> to disable calls to the Google Maps and fonts API assets.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-AddGoogleAPIKey">Add Google API Key</h5></td>
<td class="confluenceTd">5.16.0+</td>
<td class="confluenceTd">googleApiKey</td>
<td class="confluenceTd">Add the Google API key to the config.json file for the Maps API used by the Geo Suggest feature.</td>
</tr>
</tbody>
</table>
# Properties and Settings
The config.json file has a number of properties used to configure the custom user interface.
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Property</th>
<th class="confluenceTh">Default Setting</th>
<th class="confluenceTh">Description</th>
</tr>
&#10;<tr class="odd">
<td colspan="3" class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-assets"><strong>assets</strong></h4></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-logo">logo</h5></td>
<td class="confluenceTd">""</td>
<td class="confluenceTd">A base64 string.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-avatar">avatar</h5></td>
<td class="confluenceTd">""</td>
<td class="confluenceTd">A base64 string.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-favicon">favicon</h5></td>
<td class="confluenceTd">""</td>
<td class="confluenceTd">Optional and must be added with a URL or base64 string as setting value.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-lightThemeActive">lightThemeActive</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-name">name</h5></td>
<td class="confluenceTd"><p>"Default Amelia Theme"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-deployed">deployed</h5></td>
<td class="confluenceTd"><p>0</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-dateCreated">dateCreated</h5></td>
<td class="confluenceTd"><p>"2017-11-08 11:56:16"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-allowAnonymous">allowAnonymous</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-speech">speech</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-hideAgentHelp">hideAgentHelp</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p>Default is false. To display a Live Agent link with the chat interface, also set agent property to true and define a BPN for the escalationBpn property.</p>
<p>When set to true and the agent property is set to false, the Live Agent link does not appear in the chat interface.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-logoutUrl">logoutUrl</h5></td>
<td class="confluenceTd"><p>""</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-SSOandAnonymous">SSOandAnonymous</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-ameliaV3">ameliaV3</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-tooltipAcknowledged">tooltipAcknowledged</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-escalationBpn">escalationBpn</h5></td>
<td class="confluenceTd"><p>"escalation"</p></td>
<td class="confluenceTd"><p>Define a BPN name for this property. To display a Live Agent link with the chat interface, also set agent property to true and hideAgentHelp property to false.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-menuInHeader">menuInHeader</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-chatNoteCollapse">chatNoteCollapse</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-language">language</h5></td>
<td class="confluenceTd"><p>"en"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-autoConnect">autoConnect</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-domainsMappedToLanguages">domainsMappedToLanguages</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-showSelectButtonsInChatLog">showSelectButtonsInChatLog</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-mic">mic</h5></td>
<td class="confluenceTd"><p>"micme"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-showMic">showMic</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-resetConversation">resetConversation</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">customFonts</td>
<td class="confluenceTd">[ ]</td>
<td class="confluenceTd">See Add Custom Fonts section below for details how to use this property.</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-logout">logout</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-agent">agent</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p>Default is true. To display a Live Agent link with the chat interface, also set hideAgentHelp property to false and define a BPN for the escalationBpn property.</p>
<p>When set to false and the hideAgentHelp property is set to true, the Live Agent link does not appear in the chat interface.</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-logoActive">logoActive</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td colspan="3" class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-ui"><strong>ui</strong></h4></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><div class="content-wrapper">
<h5 id="CustomizeUIwithconfig.json-customTranslationcustomTranslation">customTranslation</h5>
</div></td>
<td class="confluenceTd"><p><br />
</p></td>
<td class="confluenceTd"><p>Value is a JSON array to overwrite specific translated properties used to display text in the Customer UI, for example, the word(s) for login and logout. See <a href="#">Custom UI Translations</a> page for details.</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-showFeedback">showFeedback</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-notifierDisabled">notifierDisabled</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-avatarName">avatarName</h5></td>
<td class="confluenceTd"><p>"Amelia"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-avatarEnabled">avatarEnabled</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-headerDisabled">headerDisabled</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-particlesDisabled">particlesDisabled</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-bpnSelectDataValue">bpnSelectDataValue</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-headerLogoCentered">headerLogoCentered</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-showActiveConversations">showActiveConversations</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-emoticonsEnabled">emoticonsEnabled</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-feedbackBPN">feedbackBPN</h5></td>
<td class="confluenceTd"><p>"feedback_bpn"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-sessionModalCloseable">sessionModalCloseable</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-showPrivacyPolicy">showPrivacyPolicy</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-showSelectButtonsInChatLog.1">showSelectButtonsInChatLog</h5></td>
<td class="confluenceTd"><p>false</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td colspan="3" class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-variables"><strong>variables</strong></h4></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-primary">primary</h5></td>
<td class="confluenceTd"><p>"#20B2F9"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-primaryTextColor">primaryTextColor</h5></td>
<td class="confluenceTd"><p>"#000000"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-secondary">secondary</h5></td>
<td class="confluenceTd"><p>"#757575"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-secondaryTextColor">secondaryTextColor</h5></td>
<td class="confluenceTd"><p>"#FFF"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-backgroundColor">backgroundColor</h5></td>
<td class="confluenceTd"><p>"#FF"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-headerColor">headerColor</h5></td>
<td class="confluenceTd"><p>"#FF"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-avatarName.1">avatarName</h5></td>
<td class="confluenceTd"><p>"Amelia"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-name.1">name</h5></td>
<td class="confluenceTd"><p>"Default Amelia Theme"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-font">font</h5></td>
<td class="confluenceTd"><p>"Heebo"</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-changeDomain">changeDomain</h5></td>
<td class="confluenceTd"><p>true</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><h4 id="CustomizeUIwithconfig.json-initializeOptions">initializeOptions</h4></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Empty by default, this JSON object sets properties on launch of the custom UI application</td>
</tr>
<tr class="even">
<td class="confluenceTd"><h5 id="CustomizeUIwithconfig.json-domainCode">domainCode</h5></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">The domain can be set by URL or as the initial default for the application. The domain code is defined in Amelia's administration pages, in the Domains workspace found by clicking the System Settings then Domains links.</td>
</tr>
</tbody>
</table>
# Add Custom Fonts
To add a custom font for use in a custom user interface template, define the `customFonts` property in the config.json file, add CSS `@font-face` rules, then select the font from the configurator, as described in [Design with Configurator](Design%20with%20Configurator).
## Define the customFonts Property
The `customFonts` property in the config.json file can add custom fonts which appear in the configurator used to design and build the custom user interface. One or more fonts defined in the `customFonts` property will appear in a dropdown list of fonts in the configurator.
This property must be added to the config.json file for a UI Bundle.  The customFonts property is an array of objects containing the font's properties. Each font is enclosed in the object and defined with properties name and link. The link property must follow @font-face rules and WOFF2 format.
``` js
"customFonts": [
    {   
        "name": "fontName1",
        "link": "https://fonts.googleapis.com/css?family=fontName1:regular,bold,italic"
    },
    {
        "name": "Font Name2",
        "link": "https://fonts.googleapis.com/css?family=Font+Name2:regular,bold,italic"
    },
    {
        "name": "Dancing Script",
        "link": "https://fonts.googleapis.com/css?family=Dancing+Script:regular,bold,italic"
    }
]
```
## Add CSS @font-face Rules
CSS styles to call the fonts should adhere to @font-face rules and link to WOFF2 format files.
``` js
/* vietnamese */
@font-face {
  font-family: 'Dancing Script';
  font-style: normal;
  font-weight: 400;
  src: local('Dancing Script Regular'), local('DancingScript-Regular'), url(https://fonts.gstatic.com/s/dancingscript/v9/If2RXTr6YS-zF4S-kcSWSVi_szLviuEHiC4Wl-8.woff2) format('woff2');
  unicode-range: U+0102-0103, U+0110-0111, U+1EA0-1EF9, U+20AB;
}
/* latin-ext */
@font-face {
  font-family: 'Dancing Script';
  font-style: normal;
  font-weight: 400;
  src: local('Dancing Script Regular'), local('DancingScript-Regular'), url(https://fonts.gstatic.com/s/dancingscript/v9/If2RXTr6YS-zF4S-kcSWSVi_szLuiuEHiC4Wl-8.woff2) format('woff2');
  unicode-range: U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF;
}
/* latin */
@font-face {
  font-family: 'Dancing Script';
  font-style: normal;
  font-weight: 400;
  src: local('Dancing Script Regular'), local('DancingScript-Regular'), url(https://fonts.gstatic.com/s/dancingscript/v9/If2RXTr6YS-zF4S-kcSWSVi_szLgiuEHiC4W.woff2) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}
/* vietnamese */
@font-face {
  font-family: 'Dancing Script';
  font-style: normal;
  font-weight: 700;
  src: local('Dancing Script Bold'), local('DancingScript-Bold'), url(https://fonts.gstatic.com/s/dancingscript/v9/If2SXTr6YS-zF4S-kcSWSVi_szpbr_QlqiM8rebBwWg.woff2) format('woff2');
  unicode-range: U+0102-0103, U+0110-0111, U+1EA0-1EF9, U+20AB;
}
/* latin-ext */
@font-face {
  font-family: 'Dancing Script';
  font-style: normal;
  font-weight: 700;
  src: local('Dancing Script Bold'), local('DancingScript-Bold'), url(https://fonts.gstatic.com/s/dancingscript/v9/If2SXTr6YS-zF4S-kcSWSVi_szpbr_QkqiM8rebBwWg.woff2) format('woff2');
  unicode-range: U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF;
}
/* latin */
@font-face {
  font-family: 'Dancing Script';
  font-style: normal;
  font-weight: 700;
  src: local('Dancing Script Bold'), local('DancingScript-Bold'), url(https://fonts.gstatic.com/s/dancingscript/v9/If2SXTr6YS-zF4S-kcSWSVi_szpbr_QqqiM8rebB.woff2) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}
```
## Select the Custom Font in the Configurator
[Design with Configurator](Design%20with%20Configurator)
