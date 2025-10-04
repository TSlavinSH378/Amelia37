{% version "3.x" %}
> [!warning]  
>
> Clients who need the JavaScript SDK should contact their Engagement Manager or Cognitive Project Lead to request access to the Java SDK artifact files through IPsoft's public Artifactory site.

AmeliaChat is a pure Javascript client for Amelia User Chats, with minimal dependencies, so that developers can use their own choice of frameworks to roll a custom user interface.  An AmeliaChat instance works with the core concept of Amelia Messages.  A chat is instantiated, and then can use methods to begin/end a chat, and to send messages to Amelia.  The instance can also register javascript listeners to respond to messages incoming from Amelia
# Changes
Starting with Version 3.7, the AmeliaV3 javascript client offers support for multiple conversations at the same time, as well as subscriptions for escalations and push conversations.  This involved some API incompatibilities.  While every effort is being made to ensure that the SDK will work against older versions of Amelia, the signature of methods and events have changed, so that the context of the conversation is passed out where appropriate.  As examples:
``` js
//Pre 3.7 style -- single conversation only
OutboundTextMessage event fired with (sdk, messageType, messageBody, headers);
//3.7 and up -- with the conversation context
OutboundTextMessage event fired with (sdk, conversation, messageType, messageBody, headers
```
Many methods will also change, requiring a conversation sessionId along with to identify to the SDK which conversation the client is attempting to interact.  These will be appended to the end of the existing methods, so that, if nothing is provided, the SDK will choose whatever conversation is currently in the foreground, making it easier for single conversation clients to transition.
TBD: Method description
TBD: Client responsibilities in tracking conversations
# Dependencies
AmeliaChat uses [Stomp](https://github.com/jmesnil/stomp-websocket) over [SockJS](https://github.com/sockjs/sockjs-client) for its underlying communication.  Together, these provide a publish/subscribe mechanism over web sockets if available, and via web polling if not.  It also makes use of dropzone.js for cross-browser drag and drop uploading of files.  These dependencies must be included and fully loaded before an AmeliaChat is instantiated.  This should be done by including the \<script/\> tags normally and creating a chat instance when the document is loaded.  AmeliaChat also relies on audio5.js and Queue.js to provide text-to-speech capabilities.  The SDK can be obtained as a webjar or as an npm module in our artifactory, or the files can be extracted and included as in a standard web page.
# Chatting with Amelia
Amelia works with the concept of Messages passed back and forth between a user in a browser and the intelligent agent on the server.  AmeliaChat allows the creation of custom UIs to chat with this intelligent agent.  Custom UIs interact with the agent by invoking methods on it to send input, and registering listeners to Messages to handle communication back from Amelia.  Strictly speaking, listeners are not required, but any Message that does not have listeners will effectively be ignored by your application, resulting in reduced or broken functionality.  For example, if you do not register a listener for WolframAlphaFinalMessage, then any response from Amelia that is informed by WolframAlpha will still be sent to the browser, but silently dropped by your application.
## Proxying Requirements
At this time, the javascript SDK does not allow cross-domain chats; therefore, your application must look to the browser to be served from the same domain as Amelia itself.   By example:

| Amelia Domain | Web Page User is On | Works? |
| ----|----|----|
| https://amelia.ipsoft.com/ | https://amelia.ipsoft.com/test.html | YES |
| https://amelia.ipsoft.com/ | http://amelia.ipsoft.com/test.html | NO |
| https://amelia.ipsoft.com/ | https://some.client.com/test.html | NO |
| https://some.client.com/ | https://some.client.com/test.html | YES |

If the page the user is on is not from the same scheme/host/port as Amelia, the browser sandbox and Amelia will disallow the request.
If you are creating a client-specific app to run on the same environment, contact IPsoft for the ports the application should serve from; this application should be proxied by the same web server in front of Amelia to hand off as appropriate.  If you are working in a different environment, but can proxy requests from https://some.client.com/Amelia/\* to https://amelia.ipsoft.com/Amelia/\* so that it all appears the same to the browser, it may work, though you will have to take into account other considerations per-instance, such as SSO considerations.  Consult your web server documentation on how to proxy accordingly.
The UIUX team has a [configurable custom chat overlay](Create%20a%20Custom%20Chat%20Overlay) using an iframe mechanism that is suitable for placement on other sites, as well.
## Beginning a Chat, Anonymously or Logged In
Prior to Amelia 3.7, an **autoConnect** parameter was recommended to initiate conversations automatically upon a page load or login.  In response to demands for more fine-grained control, this has been largely supplanted in favor of an **appReady** even which is fired when the SDK has completed its opening tasks to signal to the client code do do what it will.  autoConnect is still present, but should be considered deprecated, and may be removed in a future release.
### Using appReady
``` js
var ameliaChat = new AmeliaChat({
    allowAnonymous: true,
    listeners: {
       appReady: myAppReadyFunction
    }
});
```
where myAppReadyFunction would be something the client code has defined that might start a conversation, or perform another task, based on its own decisions.  It is an extra step compared to autoConnect, but offers far more control for the SDK-using application.
### Using autoConnect (deprecated)
When you begin a session with AmeliaChat, two configuration options are paramount:
``` js
var ameliaChat = new AmeliaChat({
    autoConnect:true,
    allowAnonymous: true
});
```
When you initialize AmeliaChat, two configuration options are paramount when determining how users will first get to your system. 
1.  autoConnect - if true, AmeliaChat will attempt to create a session and start a conversation immediately, without any user interaction
2.  allowAnonymous: if true, absent any logged-in user AmeliaChat will ask Amelia to create an anonymous user and start an anonymous chat.  If the Amelia instance has no domains configured to allow anonymous users, a sessionFail event will be thrown
These two options combine to give you the following set of possibilities:
<table class="relative-table wrapped confluenceTable" style="width: 73.5411%;">
<colgroup>
<col style="width: 13%" />
<col style="width: 39%" />
<col style="width: 46%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh"><br />
</th>
<th class="confluenceTh">autoConnect:true</th>
<th class="confluenceTh">autoConnect:false</th>
</tr>
&#10;<tr class="odd">
<th class="confluenceTh">allowAnonymous:true</th>
<td class="confluenceTd"><ol>
<li>on page load, try to start a conversation immediately
<ol>
<li>if there is a logged in user, use that user</li>
<li>If no logged in user, create an anonymous user
<ol>
<li>If Amelia disallows anonymous users, throw sessionFail event</li>
</ol></li>
</ol></li>
</ol>
<p><strong>RECOMMENDED WHEN:</strong> You want chats to begin as soon as possible, and do not need user authentication or information</p></td>
<td class="confluenceTd"><ol>
<li>On page load, do nothing</li>
<li>When user calls ameliaChat.newConversation(), create a conversation
<ol>
<li>if there is a logged in user, use that user</li>
<li>if no logged in user, create an anonymous user
<ol>
<li>If Amelia disallows anonymous users, throw sessionFail event</li>
</ol></li>
</ol></li>
</ol>
<p><strong>RECOMMENDED WHEN:</strong> You do not need user information, but also do not need to load the chat until the user expressly asks for it</p></td>
</tr>
<tr class="even">
<th class="confluenceTh">alllowAnonymous:false</th>
<td class="confluenceTd"><ol>
<li>on page load, try to start a conversation immediately
<ol>
<li>If there is a logged in user, use that user</li>
<li>if no logged in user, fire a loginRequired event without starting a chat</li>
</ol></li>
<li>When a user calls a.login() with a proper type, login that user in, and, if successful, start achat</li>
</ol>
<p><strong>RECOMMENDED WHEN:</strong> You exclusively use an ajax login type, want a chat to begin as soon as possible, but want to force a login if none is present</p></td>
<td class="confluenceTd"><ol>
<li>On page load, do nothing</li>
<li>When the user calls ameliaameliaChat.newConversation(), try to create a conversation
<ol>
<li>If there is a logged in user, use that user</li>
<li>if no logged in user, fire a loginRequired event without starting a chat</li>
<li>When a user calls a.login() with a proper type, login that user in, and, if successful, start a chat</li>
</ol></li>
</ol>
<p><strong>RECOMMENDED WHEN:</strong> You exclusively use an ajax login type and do not need to load the chat until the user expressly asks for it</p></td>
</tr>
</tbody>
</table>
At the successful conclusion of any of these paths, Amelia will query the available domains, and can start  a new **USER** conversation.  You still have some control over the domain choice, however, using the domainCode config attribute:

| domainCode | result |
| ----|----|
| not present | Will fetch all domains the user can see. If there is only one domain, it will be chosen and the conversation will start. If more than two domains are returned, the domainFetch event will be fired to client code, which can use that to display a picker as required, just as in the _manual case |
| _automatic | same as above |
| _manual | Will fetch all visible domains from the server, and then fire a domainFetch event with all domains, and will NOT start a conversation. The client code can use this list to create a selection widget, and then at the end of its process, must callchat.setDomainCode(domainCode);chat.newConversation(); |
| anyothercode | Any other code is presumed to be an exact domainCode desired, and it will be used unless the user in question has no access. If the user has no access or there is no such domain, an error event will be fired |

If at the conclusion of the domain selection process, if no domains are available, or if the domain is invalid or inaccessible, a domainFail event will be thrown
Keep in mind that all through this process, Amelia will not accept input; therefore, it is a good idea for your user widgets to start with chat input visually and otherwise disabled; the **inputEnabled** message will fire when Amelia is ready, and you can listen for that event to enable the UI for your user.
The concept of messages and listeners is crucial to Amelia.  While the above code will get you to the point of establishing a conversation, your application code must use the methods supplied to speak with Amelia and register listeners to handle the messages Amelia will be sending to you.  These listeners can be registered at configuration time or added later; there is not as of yet a facility to deregister listeners, so avoid attaching listeners to transient DOM elements.  (There is one exception: if autoConnect is true, listeners for all events regarding session, conversation, and login status need to be registered in the AmeliaChat constructor, or else the messages will be sent before your code is ready to receive them.)  Especially if you use your own framework, consider creating your own thin point of contact in your own framework's choice of event bus/framework, and have your individual DOM elements respond to that point of contact.  This will allow you to leverage the lifecycle services of your preferred framework.
## Example: A Complete Simple Chat Only Client
``` js
var updateChat = function(source, conversation, messageType, msgBody, headers) {
    if (msgBody.messageText) {
        if (headers['X-Amelia-Self-Echo'] === 'true') {
            $("#chat_div").chatbox("option", "boxManager").userMsg(msgBody.fromUserDisplayName,  msgBody.messageText, true);
        } else {
            $("#chat_div").chatbox("option", "boxManager").ameliaMsg(msgBody.fromUserDisplayName,  msgBody.messageText);
        }
    }
    createForm(source, conversation, messageType, msgBody, headers);
};
var endAndDisable = function(source, conversation, messageType, msgBody, headers) {
    updateChat(source, conversation, messageType, msgBody, headers);
    $("#newConvBtn").prop("disabled", false);
    $("#endConvBtn").prop("disabled", true);
    $('textarea.ui-chatbox-input-box').prop("disabled", true);
    $('textarea.ui-chatbox-input-box').addClass('ui-state-disabled');
}
var a = new AmeliaChat({
    autoConnect:true,
    allowAnonymous:true,
    listeners: {
        inputEnabled:function(source, conversation, messageType, options) {
            $('textarea.ui-chatbox-input-box').prop("disabled", false);
            $('textarea.ui-chatbox-input-box').removeClass('ui-state-disabled');
            $('textarea.ui-chatbox-input-box').focus();
        },
        inputDisabled:function(source, conversation, messageType, options) {
            $('textarea.ui-chatbox-input-box').prop("disabled", true);
            $('textarea.ui-chatbox-input-box').addClass('ui-state-disabled');
        },
        OutboundTextMessage: updateChat,
        OutboundEchoMessage: updateChat,
        OutboundConversationClosedMessage: endAndDisable,
        OutboundSessionClosedMessage:  endAndDisable
    }
});
var box = $("#chat_div").chatbox({
    id:"user",
    user:{key : "value"},
    title : "Conversation ",
    messageSent : function(id, user, msg) {
        if(user == 'amelia'){
                //$("#chat_div").chatbox("option", "boxManager").ameliaMsg(id, msg);
        }else{
                //$("#chat_div").chatbox("option", "boxManager").userMsg(id, msg);
            a.ask(msg);
        }
    }
});
```
![](attachments/11940105/11940110.png)
The above code is enough to conduct a simple chat messages in Amelia.  (It will not support form or integration data, which are discussed later.)  This application uses jQuery's chatbox plugin to run their chat.  We can see from the initializer that autoConnect is set to true, which means a conversation will be established immediately.  The first thing to happen in a conversation is that Amelia will greet the user. This arrives as an OutboundTextMessage, and two events are fired:
1.  inputEnabled (because input had been disabled.  inputEnabled/inputDisabled are not fired on every message, but only in response to changes in that status.) .
2.  OutboundTextMessage
The listener for inputEnabled sets some properties on the chat box and gives it focus, so that the user may type.  The listener for OutboundTextMessage calls a shared function, updateChat, which will place text in the chat window.  Please note the decision around **headers\['X-Amelia-Self-Echo'\]**, as it is a crucial point to Amelia.  When a user submits chat to Amelia, Amelia will echo that chat back to the user.  This provides feedback in the case of certain complicated operations, but it also allows clean up and sanitization of input.  As a rule, if you are sending messages to Amelia, you should **not** place input into the chatbox directly.  Wait for the echoed message, and place it accordingly.  You can see this in the second block, which is entirely jQuery chatbox-based.  Where normally the chatbox would be updated directly, those lines are commented out.   Instead, there is one line referencing back to Amelia: a.ask(msg);  This line will submit the user's input to Amelia.  The users's response will be echoed, and Amelia's response will be placed in the chat, by the updateChat method.
# Configuration Options
AmeliaChat can optionally be provided configuration options in JSON format:
**Configuration Example**
``` js
var ameliaChat = new AmeliaChat({
    autoConnect:true,
    domainCode: "anon"
});
```
The following configuration options are supported:

| Name | Description | Notes |
| ----|----|----|
| autoConnect | If true, will initialize and connect a chat immediately. If false, chat will not begin until a new conversation has been requested. Defaults to false |  |
| allowAnonymous | If true, will ask Amelia to create an anonymous user if there is no already logged-in user. If false, a loginRequired message will be sent, and the chat will not be enabled until a login has occurred. Defaults to false |  |
| domainCode | One of three options:_automatic. the JS client will select a domain from the list of domains the user can access. If there are more than two, a domainFail message will be sent. If there are two, and one is global, the other will be picked, unless the other is hidden. (If no non-global, non-hidden domains are present, a domainFail message will be sent.) If there is one, it will be selected, unless it is hidden_manual. the JS client will fetch all domains the user can access, and pass them out in a domainFetch event. The listener is responsible for setting up some manner of selecting a domain code, and starting the conversation manually.All other values are treated as domainCodes, and are used as such.If in any case a missing, invalid, or otherwise inaccessible domainCode is chosen, a domainFail message is sent |  |
| listeners | A JSON object of elements and callback functions listening to messages arrive from Amelia. See addEventListeners for format |  |
| speech | if true, Amelia will speak if the browser supports it. Defaults to false |  |
| mic | either an HTML element or the id of one. If the browser supports WebkitSpeechRecognition (e.g. Chrome on desktop), this icon will be given a click event to start/stop speech recognition. Beta feature; will be documented more thoroughly once support can be widened |  |
| initialBpnVariablesinitialConversationVariables | These two are aliases for each other. Both provide a means to pass variables to the kickoff bpn of a conversation. They can take two forms:Object.Object Format
initialConversationVariables: {name:value, processName:"mybpn"};

A standard javascript objet of keys and values. Note that the values will be passed in as strings, and the backend BPN must be able to interpret them.
Function
**Function format**
``` js
initialConversationVariables: function() { return {name:value, processName:"mybpn"}; }
```
A function that returns a hash.
If no config property is supplied, then the query string will be examined for any parameter beginning with 'bpn\_'
\| \| \| initialConversationAttributes \|
This parameter will specify initial conversation attributes when a conversation begins. Conversation attributes differ from bpn/conversation variables in that conversationAttributes are good for the duration of a conversation, and can be changed during the conversation, whereas bpn/conversation variables exist in the scope of the bpn only. This can also take two forms:
**Object Form**
``` js
initialConversationAttributes: { name: value}
```
A standard javascript objet of keys and values. Note that the values will be passed in as strings, and the backend must be able to interpret them.
**Function Form**
``` js
initialConversationAttributes: function() { return { name: value }; } 
```
A function that returns a hash. If no config property is supplied, then the query string will be examined for any parameter beginning with 'attrib\_' These values can be changed over the course of a converstion by calling the setCustomConversationAttribute method.
\| \| \| fetchSpeech, playSpeech \|
These two options are only used if speech:true is specified, and they allow an application to specify their own TTS provider while still utilizing the SDK for parsing and queueing of what speech needs to be spoken aloud. If they are undefined, the SDK will use the default Amelia internal speech implementation. If defined, they must both be functions, and are interdependent; one without the other will not work, and if they do not agree on their dataformat, they will not work. Specify as follows:
**Custom TTS**
``` js
/**
  * Fetch audio to be played at the appropriate time based on the tts parameters handed from the SDK
  * @param tts - the tts object handed out from the SDK.  It will have two properties, text and voice.
  *  { text:'Hello, how are you today?', voice: 'VW Julie'}
  * @param chat - the SDK instance itself
**/
fetchSpeech: function(tts, chat) {
    myCustomAudioFetcher(tts.text, {
        success: function(data) {
            //This is *required* at some point in this method, as it enqueues the actual audio to play later, in the playSpeech method
            chat.addFetchedAudio(tts, data);
        });
    }
},
/**
  * Play the enqueued audio.  Note that toPlay here should correspond to the data from the fetchSpeech method.  If playSpeech cannot understand the data
  * returned by fetchSpeech, playback will not occur, and may throw an error
  * @param toPlay - the audio structure to play, must expect the same data enqueued in fetchSpeech
  * @param chat - the SDK instance itself
  */
playSpeech: function(toPlay, chat) {
   //this will force the SDK to fire the 'speakstart' event, so that any application can respond to the beginning of the audio playback regardless of TTS implementation
   chat.onFetchedAudioPlayStart(); 
   //assuming the custom audio player fires an event when its playback is done 
   myCustomAudioPlayer.play(toPlay, {
      onplayend: function() {
          //This will do some internal housekeeping, as well as fire the 'speakend' event so that any application can respond to the end of audio playback regardless of TTS implementation
          chat.onFetchedAudioPlayEnd();
      });
}
```
\| since 3.1.8 \|
One element that is currently not configurable is the fileUpload widget.  If you plan on using file upload, make sure you have a div with the id fileUpload on your page.
# Breaking Changes from Previous Versions
Amelia  introduced the ability for one user interface to handle multiple conversations at the same time.  To support this, many methods have a "sessionId" attribute indicating the conversation, and events have a "conversation" argument to provide context information.  This requires the client code to keep track of the conversation which currently appiles.
# Methods
Methods are used to begin/end a conversation, as well as to pass messages from the User to Amelia.
## action
**action**
``` js
 /**
 * Submit an integration action to Amelia, which will run a named bpn with the provided arguments, along with either
 *    a static message defined in SubmissionUtteranceMetadata or a custom message provided to the method
 *
 * @param processName - the name of the BPN process to run
 * @param processVariables - the arguments to pass to that BPN process
 * @param sessionId - the conversationSessionId of the conversation to which this action should be submitted.
 * @param submissionMetadata - a SubmissionUtteranceMetadata object, with a staticUtterance property.  Can come from
 *         BPN naturally, but only the staticUtterance is supported { staticUtterance: "Please run this"}
 * @param message a custom message to send.  If present, overrides anything in the submissionMetadata
 */
chat.action = function(processName, processVariables, sessionId, submissionMetadata, message);
```
action is discussed in more detail in [Handling Integrations](#AmeliaV3JavascriptSDK-V3.7+-handlingintegrations)
## addEventListener
**addEventListener**
``` js
/**
 * Add a listener to the chat
 * @param event {string} the name of the event to listen
 * @param recipient {sting} the object listening to the event, will be bound as "this" in the function
 * @param fn {function} the function to call when the event is received.  Arguments are:
 *    source - the ameliaChat instance that fired the event
 *    messageType - the name of the messageType fired
 *    msgBody - the body of the message
 *    headers - the headers of the message
 */
chat.addEventListener = function(event, recipient, fn);
//example - updated a jquery chatbox with the text message coming from Amelia
chat.addEventListener("OutboundTextMessage", chatbox, function(source, conversation, messageType, msgBody, headers) {
    $("#chat_div").chatbox("option", "boxManager").ameliaMsg(msgBody.fromUserDisplayName,  msgBody.messageText);
});
```
## addEventListeners
**addEventListeners**
``` js
/**
 * Add multiple listeners to the chat at once; takes many different formats
 * @param - many types, see separate docs
 */
var a = new AmeliaChat();
//Format #1 - event, recipient, fn
a.addEventListeners(event, recipient, fn) //same as addEventListener(event, recipient, fn);
var updateChat =  function(source, conversation, messageType, msgBody, headers) {
    $("#chat_div").chatbox("option", "boxManager").ameliaMsg(msgBody.fromUserDisplayName,  msgBody.messageText);
});
//Format #2 - config object
//each key is the name of a message fired, and each value can be either a function, a config object, or an array of config objects
a.addEventListeners({
    //function style; functions executed in scope of the ameliaChat instance
    OutboundTextMessage: updateChat,
    //config object style
    conversationStart: {
        element: document.getElementById('status'), //the scope of the callback function; if not defined, will be the ameliaChat instance
        fn: function(source, conversation, messageType, msgBody, headers) {
            this.innerHTML.append(msgBody.messageText);
        }
    },
    //array of config objects style; can contain both function and config objects
    OutboundConversationClosedMessage:[
    function(source, conversation, messageType, msgBody, headers) {
        alert('good bye');
    }, {
        element:favicon,
        fn: function(source, conversation, messageType, msgBody, headers) {
            favicon.badge(0);
        }
    ]    
});
```
## ask
**ask**
``` js
/**
 * Send a user text message to amelia and updates the chat's timeOfLastMessage
 * @param text {string} the text to send to Amelia
 * @param sessionId {string} the id of the conversationSession to which this text should be sent.  If omitted, the SDK will attempt to send to the foreground conversation
 * @param attribuets {object} an optional hash of attributes to include with the utterance
 */
chat.ask = function(text, sessionId, attributes);
var a = new AmeliaChat();
a.ask("How much wood could a woodchuck chuck if a woodchuck could chuck wood?
```
## clearChatHistory - removed
**clearChatHistory**
``` js
/**
 * clear the chat history -- since AmeliaChat does not maintain a client side history, this has no effect internally, but
 * fires an event that other components can listen to and react
 * @event chatHistoryClear
 * @removed
 */
chat.clearChatHistory = function();
var a = new AmeliaChat();
a.clearChatHistory();
this event is no longer fired
```
## endConversation
**endConversation**
``` js
/**
 * ends a conversation
 * @param attributes {object} a hash of attributes to send while closing the conversation
 * @param sessionId the id of the conversation session to end
 */
chat.endConversation=function(attributes, sessionId);
var a = new AmeliaChat();
a.endConversation();
```
## fireEvent
**fireEvent**
``` js
/**
 * fires an event, with the AmeliaChat instance as the first argument, and 2...n arguments to this function
 * as the arguments in the fired event.  Not often used by client code, but used by plugins to wire their events to Amelia's
 * @param event {string} the name of the event to fire
 */
chat.fireEvent=function(event);
var a = new AmeliaChat();
a.fireEvent("customevent", foo, bar, bar); 
```
## getConversationId
**getConversationId**
``` js
/**
 * Gets the conversationId of the chat, if a chat is underway
 */
chat.getConversationId=function();
var a = new AmeliaChat();
a.getConversationId();
```
## getDomainCode
**getConversationId**
``` js
/**
 * Gets the domain code of the current foreground conversation, or undefined if no conversation is open
 */
chat.getDomainCode=function();
var a = new AmeliaChat();
a.getDomainCode();
```
## getLanguageCode
**getLanguageCode**
``` js
/**
 * Gets the language code of the chat or current foreground conversation
 */
chat.getLanguageCode=function();
var a = new AmeliaChat();
a.getLanguageCode();
```
## getSessionId
**getSessionId**
``` js
/**
 * Gets the sessionId of the current foreground conversation
 */
chat.getSessionId=function();
var a = new AmeliaChat();
a.getSessionId();
```
## getTimeOfLastMessage
**getTimeOfLastMessage**
``` js
/**
 * Gets the time of the last message sent to/from the chat
 * @param sessionId the id of a conversation session
 */
chat.getTimeOfLastMessage=function(sessionId);
var a = new AmeliaChat();
a.getTimeOfLastMessage();
```
## getUserInterface
**getUserInterface**
``` js
/**
 * Gets the userInterface of the chat, currently only WEB_USER
 */
chat.getUserInterface=function();
var a = new AmeliaChat();
a.getUserInterface();
```
## login
**login**
``` js
/**
 * attempts to log in a user
 *
 * @param options an object containing a username and a password
 */
chat.login=function(options);
// all logins will immediately terminate any current chat and disable input
var a = new AmeliaChat();
a.login({username:"greg.ludington@ipsoft.com", password:"imn0tt3ll1ngu"})
```
## logout
**logout**
``` js
/**
 * attempts to log out a user
 *
 * @param options and object containing a type, and parameters appropriate to its type
 */
chat.logout=function(options);
var a = new AmeliaChat();
a.logout();
//Note that this logs the user out of an Amelia session, but will not initiate any logout of the host web application or any related domain
```
## mute
**mute**
``` js
/**
 * Silences Amelia's speaking.  Only has an effect if speech was true in the config
 */
chat.mute=function();
var a = new AmeliaChat();
a.mute();
```
## newConversation
**newConversation**
``` js
/**
 * Starts a new conversation, initializing the connection if necessary
 * @param options {object} optional options with which to start the conversation
 */
chat.newConversation=function(options);
var a = new AmeliaChat();
a.newConversation();
```
## registerPlugin/registerPlugins
A **plugin** is a single object that can be registered with the SDK to pass events back and forth between external code and the SDK.  It is functionally not much different between registering multiple listeners to SDK events, but creating them as a single plugin object may allow for simpler organization of client code.  The plugin itself must contain this single method:
``` js
plugin.registerChatPlugin = function (chat) {}
```
This single method will be called, with the SDK as its argument, when the plugin is registered.  Inside this method, the plugin can initialize itself, and establish any listeners or method calls to the SDK.  Registering the plugin can be done in one of two ways:
**Registering a Plugin**
``` js
//First way, as part of the config object:
var sdk = new AmeliaChat({
    plugins: plugin
})
//or 
var sdk = new AmeliaChat({
    plugins: [plugin1, plugin2]
})
//Second way, by calling a method
var sdk = new AmeliaChat({});
sdk.registerPlugin(plugin);
sdk.registerPlugins([plugin1, plugin2]);
```
The major difference between these two methods is that if you configure through the initial config object, the plugin will be active at the time initialization events are fired out from the SDK.  If you call a **registerPlugin **method, that is not guaranteed, and will depend on the order of operations of the client code.
## setDomainCode
**getConversationId**
``` js
/**
 * Sets the domainCode of the next chat, if the user has access to it
 * Throws a domainFail event if the user cannot access this domain
 */
chat.getConversationId=function();
var a = new AmeliaChat({autoConnect:false});
a.setDomainCode('domain');
a.newConversation();
```
## say
alias for ask
## submit - requires Amelia Core 3.2+
**submit**
``` js
/**
 * submits a form
 *
 * @param form - required; either an html form containing all widgets or a JSON object to submit
 * @param formInputData - required; the full formInputData object used to create this form
 * @param sessionId - the id of a conversation session to which this applies
 * @param message - optional, a text message to be the user utterance when the form is submitted; if omitted, one will be built from the formInputData
 *      and the elements defined in the BPN
 */
chat.submit = function(form, formInputData, sessionId, message)
a.submit(this.form, formInputData); //will submit to Amelia with the contents of all form inputs, except for image, button, and submit types
a.submit(this.form, formInputData, "I selected these options"); //with optional explicit message
a.submit({"carMake":['Camry', 'Celica']}, formInputData); //will submit this JSON directly; using this form, the client code is responsible for assembling the JSON in the proper format.
```
## setCustomConversationAttributes - requires Amelia Core 3.5+
**submit**
``` js
  /**
* sends conversation attributes
* @param attributes a set of key/value pairs to set on a conversation
   */
  chat.sendCustomConversationAttributes = function(attributes);
var a = new AmeliaChat();
a.setCustomConversationAttributes({"name":"value", "othername":"othervalue"});
```
## unmute
**mute**
``` js
/**
 * Allows Amelia to speak again.  Only has an effect if speech was true in the config
 */
chat.unmute=function();
var a = new AmeliaChat();
a.unmute();
```
# Messages
Listeners registered in the config object or via an addEventListener allow the client code to respond to messages coming in from Amelia.  The following messages are supported with the javascript client
## Amelia Messages
Amelia Messages are standard output sent directly from the server as a step in a conversation.  All Amelia messages are fired with the following callback signature:
**Standard Callback Format**
``` js
messageType:function(source, conversation, messageType, messageBody, headers);
with the arguments:
    source: the AmeliaChat instance that fired the message
    conversation: the conversation from which this message was fired
    messageType: the type of the message being fired -- this will correspond to the name of the handling method
    messageBody: a JSON object containing the contents of the message
    headers: a JSON object containing the headers of the message
```
### messageBody
A messageBody is a json object representing the actual message.  The typical format is as follows
**messageBody**
``` js
{
    attributes:{ ... },                                         //a JSON object that differs between message types.  Will not be necessary to use in most cases.
    conversationId:"K7YY67KOYAIAA-1"                          //the conversation id 
    fromUserDisplayName:"Amelia"                              //the name of the Amelia user responding
    id:"9f3a5697-e51d-486a-9a40-f576babc2b78"                 //the id of the message
    inResponseToMessageId:"8cde97-e51d-486a-9a40-f576babc2b78"    //the id of the message this is a direct response to, if a response
    messageText:"It's a pleasure to meet you."                   //the text of the message
    messageType:"OutboundTextMessage"                         //the type of the message
    sourceClass:"LoginSocialTalkStage"                            //the generator of this comment
    sourceSessionId:"bb6c8272-d8aa-4c11-98f6-b50e60296303"        //the id of the session
}
```
Additional elements of the message body may include:
-   formInputData - This will contain the BPN-driven semantic definition of a form in JSON format, for which custom javascript can be written to parse and layout.  See [handling forms](#AmeliaV3JavascriptSDK-V3.7+-handlingforms) for more detail.  This can be part of any text message coming from Amelia
-   integrationMessageData - This will contain the BPN-drive semantic definition of a more freeform widget in JSON format, for which custom javascript can be written to parse and layout.  See [handing integrations](#AmeliaV3JavascriptSDK-V3.7+-handlingintegrations) for more detail.  This will only be in an OutboundIntegrationMessage
-   headers
Headers contain metadata around the message being sent:
**headers**
``` js
{
  "X-Amelia-Session-Mode": "USER",
  "X-Amelia-Source-User-Type": "Amelia",
  "X-Amelia-Conversation-Id": "K7YY67KOYAIAA-1",
  "X-Amelia-Message-Type": "OutboundTextMessage",
  "X-Amelia-Self-Echo": "false",
  "X-Amelia-Clock-Skew": "364",
  "X-Amelia-Session-Id": "bb6c8272-d8aa-4c11-98f6-b50e60296303",
  "X-Amelia-Input-Enabled": "false",
  "X-Amelia-Debug-Message": "false",
  "X-Amelia-Message-Id": "9f3a5697-e51d-486a-9a40-f576babc2b78",
  "X-Amelia-Timestamp": "1510859471179"
}
```
Most headers are either internal details, or already reflected in the body object, and will not be used by authors.  Authors should concentrate on working through the fired events, but the headers, as well as the messageBody, are both passed to messages in case the author has reason to use them at a lower level.
This list contains the most relevant messages, and may not be exhaustive.  As more messages are added to Amelia, they will be passed through the SDK to clients automatically.
### OutboundTextMessage
OutboundTextMessage will fire when Amelia says text at the conclusion of a typical process. This is typically the type of message you want to echo into your chat UI.
**OutboundFinalTextMessage**
``` groovy
var a = new AmeliaChat({
    listeners: {
        OutboundTextMessage:function(source, conversation, messageType, messageBody, headers) {
            // if text is present, add to the box
            if (msgBody.messageText) {
                $("#chat_div").chatbox("option", "boxManager").ameliaMsg(msgBody.fromUserDisplayName,  msgBody.messageText);
            }
        }
    }
});
```
OutBoundTextMessage may have a formInputData attribute, which can be used to construct custom form widgets.  See the section on [Handling Forms](#AmeliaV3JavascriptSDK-V3.7+-handlingforms) for details.
### OutboundEchoMessage
An echo of a user response.  Used to populate the user side of a chat; client side code should rely on echo messages rather than populating the chat box immediately.
**OutboundEchoMessage**
``` js
var a = new AmeliaChat({
    OutboundEchoMessage:function(source, conversation, messageType, messageBody, headers) {
        udpateUserChat(messageBody.messageText);
    }
});
```
### OutboundAgentSessionChangedMessage
A message sent when a new agent takes over the chat, typically when a human agent takes over for Amelia
**OutboundEchoMessage**
``` js
var a = new AmeliaChat({
    listeners: {
        OutboundAgentSessionChangedMessage:function(source, conversation, messageType, messageBody, headers) {
            $("#chat_div").chatbox("option", "boxManager").ameliaMsg(msgBody.fromUserDisplayName,  msgBody.messageText);
        }
    }
});
```
### OutboundConversationClosedMessage
A message Amelia sends when the conversation is closed.  It does **not** end the session, but it does signal the close and end of the current conversation in the session:
**OutboundConversationClosedMessage**
``` js
var a = new AmeliaChat({
    listeners: {
        OutboundConversationClosedMessage:function(source, conversation, messageType, messageBody, headers) {
            alert('Thank you for the conversation');
        }
    }
});
```
### OutboundSessionClosedMessage
A message Amelia sends when the user session is closed.  It will contain some messageText, so you may use it to update the chat box as well as to inform other components of your UI that the session has terminated.  Using jqueryui as an example:
**OutboundSessionClosedMessage**
``` js
var a = new AmeliaChat({
    listeners: {
        OutboundSessionClosedMessage:function(source, conversation, messageType, messageBody, headers) {
            //Disable input, the session is closed
            $('textarea.ui-chatbox-input-box').prop("disabled", true);
        }
    }
});
```
### OutboundFormInputMessage
OutboundFormInputMessage will fire when Amelia requests the assembly of a custom form to submit input back to the server.  See [Handling Forms](#AmeliaV3JavascriptSDK-V3.7+-handlingforms)
(Deprecated) formInputData can be present in any message as an attribute, negating the need for this custom message, though it is currently here for compatibility purposes
**OutboundFormInputMessage**
``` js
var a = new AmeliaChat({
    listeners: {
        OutboundFormInputMessage(source, conversation, messageType, messageBody, headers) {
            //this will have one special attribute, formInputData, that will contain all elements needed to assemble a widget
            var atts = msgBody.attributes.formInputData;
            createForm(atts);
        }
    }
});
```
### OutboundIntegrationMessage
OutboundIntegrationMessage will fire when Amelia requests the assembly of a section widgets for working with another system.  See [Handling Integrations](#AmeliaV3JavascriptSDK-V3.7+-handlingintegrations)
**OutboundFormInputMessage**
``` js
var a = new AmeliaChat({
    listeners: {
        OutboundIntegrationMessage(source, conversation, messageType, messageBody, headers) {
            //this will have one special attribute, integrationMessageData, that will contain all elements needed to assemble a widget
            var atts = msgBody.attributes.integrationMessageData;
            createIntegrationSection(atts);
        }
    }
});
```
### OutboundPresentMessage
An OutboundPresentMessage will fire when Amelia is presenting some content which may be shown or downloaded
**OutboundFormInputMessage**
``` js
var a = new AmeliaChat({
    OutboundPresentMessage(source, conversation, messageType, messageBody, headers) {
        //this will have one special attribute, resourceToPresent, that will contain information needed to display the element
        var res = msgBody.resourceToPresent
        showResource(res);
    }
});
```
#### Downloading Resources after OutboundPresentMessage
The resourceToPresent item in OutboundPresentMessage does not contain the content itself, but rather enough information for the user interface to present the content.  Example:
**Example resourceToPresent**
``` js
//example resourceToPresent in an OutboundPresentMessage:
{
...rest of message,
  "resourceToPresent": {
    "objectId": null,
    "bucketName": "test",
    "filename": "ack.png",
    "label": null,
    "description": null,
    "byteCount": "20485",
    "fileSize": "20 kB",
    "previewStyle": "INLINE_AND_POPUP",
    "download": "DOWNLOAD_YES",
    "documentStyle": "INHERIT",
    "displayResourceDetails": "YES",
    "processInstanceId": "5b5cfe06-e1e8-47f8-869c-984653db2b47",
    "url": "blob:https://localhost/8eaca37c-928e-4ec7-8f84-0d9a0cc81255" //not send from Amelia, but the SDK will add this on before delivering the message
  }
}
```
The crucial elements here are **download**, **bucketName, filename**, and **processInstanceId**, as they allow downloading from from Amelia's content management system.  The SDK does this for you, and adds a blob url that a browser may use to directly display or present download links.  Other items in this resourceToPresent object are suggestions the BPN author has provided on how to present the content, but it is up to the UI code to choose to follow those hints.
## Non Amelia Messages
These messages are not fired directly by the server, but rather fired by javascript SDK in response to specific events from the client or translated from the server
### appInit
**on connect**
``` js
/**
 * Fired when the application initializes, before any conversation or even login
 *    source - the AmeliaChat instance that fired the event
 *    appConfig - the server side configuration of the application, including the user if one already present, though the user may be overwritten is login is subsequently called
 */
appInit(source, appConfig)
var a = new AmeliaChat({
    listeners: {
        appInit: function(source, appConfig) {
            console.log("application configuration received", appConfig);
        }
    }
});
```
### appReady
**on connect**
``` js
/**
 * Fired when app has finished initialzing and can accept new commands, either after load or after a login
 *    source - the AmeliaChat instance that fired the event
 */
appReady()
var a = new AmeliaChat({
    appready: function(source) {
        console.log("ready");
    }
});
```
### languageChange
**languageChange**
``` js
/**
 * Fired when a message from Amelia has triggered a change in the current language
 *    source - the AmeliaChat instance that fired the event
 *    newLang - the new language
 *    oldLang - the old language
 *
 * @since 1.2.0
 */
langaugeChange(source, newLang, oldLand)
var a = new AmeliaChat({
    listeners: {
        messageReceived: function(source, message) {
            console.log("raw message received from Amelia");
            console.log(message);
        }
    }
});
```
### messageReceived
**messageReceived**
``` js
/**
 * Fired when a standard Amelia message is received from the server.  Not recommended for production use, but can aid in development
 *    source - the AmeliaChat instance that fired the event
 *    message - the raw message returned from Amelia
 */
messageReceived(source, message)
var a = new AmeliaChat(
    listeners: {
        messageReceived: function(source, message) {
            console.log("raw message received from Amelia");
            console.log(message);
        }
    }
});
```
### chatHistoryClear
**chatHistoryClear**
``` js
/**
 * Fired when the user invoked clearChatHistory method.  Does nothing internally, as AmeliaChat maintains no internal history, but
 * other elements can listen to this event and respond
 *    source - the AmeliaChat instance that fired the event
 */
chatHistoryClear(source)
var a = new AmeliaChat({
    listeners: {
        chatHistoryClear: {
            element: document.getElementId('chatpane'),
            fn: function(source, message) {
                this.innerHTML = '';
            }   
        }
    }
});
```
### loginFail
**loginFail**
``` js
/**
 * Fired when the a login attempt fails.  Typically fires only in response to ajax login failures, though full page
 * logins can fire this if not all required parameters are present
 *   source - the AmeliaChat instance that fired the event
 *   message - the code of the error returned
 *   options - an object containing information relevant to the specific error code
 */
loginFail(source, message, options)
var a = new AmeliaChat({
    listeners: {
        loginFail: function(source, message, options) {
            alert("log in first");
        }
    }
a.login({type:"INTERNAL"});
//will fire a loginFail with message MISSING_OPTIONS
```
### loginSuccess
**loginSuccess**
``` js
/**
 * Fired when the a login attempt succeeds.  Only fired by ajax login methods, currently only INTERNAL
 * logins can fire this if not all required parameters are present
 *   source - the AmeliaChat instance that fired the event
 *   message - the code of the error returned
 *   options - an object containing information relevant to the specific error code
 */
loginSuccess(source, message, options)
var a = new AmeliaChat({
    listeners: {
        loginSuccess: function(source, message, options) {
            $('#loginbtn').hide();
            $('#logoutbtn').show();
        }
    }
});
```
### loginRequired
**loginRequired**
``` js
/**
 * Fired when the a chat initialization is attempted when the AmeliaChat instance is not configured to allow anonymous chats
 *    source - the AmeliaChat instance that fired the event
 */
loginRequired(source)
var a = new AmeliaChat({
    autoConnect:true,
    allowAnonymous: false
    listeners: {
        loginRequired: function(source) {
            alert("log in first");
            console.error(authSystems);
        }
    }
});
// These objects can be passed in the login method -- minimally, the correct loginPath and redirect boolean are required.
// code, name, and description are not required in the login method, but a UI may wish to use them to make display choices
```
### logout
**loginRequired**
``` js
/**
 * Fired when an ajax logout completes
 *    source - the AmeliaChat instance that fired the event
 */
logout(source)
 var a = new AmeliaChat({
    listeners: {
        loginSuccess: function(source, message, options) {
            $('#loginbtn').show();
            $('#logoutbtn').hide();
        }
    }
});
```
### sessionFail
**sessionFail**
``` js
/**
 * Fired when the anonymous session cannot be created
 *    source - the AmeliaChat instance that fired the event
 *    status - the http status code of the failed response
 *    statusText - the http status text of the failed response
 *    responseText - the body text of the response
 */
sessionFail(source, status, statusText, responseText)
var a = new AmeliaChat({
    listeners: {
        sessionFail: function(source, status, statusText, responseText) {
            alert('unable to start session ' + statusText + '[' + status + ']');
        }
    }
});
```
### domainFail
**domainFail**
``` js
/**
 * Fired when the user attempts to access an invalid or unauthorized domain, or when an error occurs establishing a domain
/**
 * Fired when the anonymous session cannot be created
 *    source - the AmeliaChat instance that fired the event
 *    code - a code identifying the type of error
 *    message - the http status text of the failed response
 */
domainFail(source, code, message);
var a = new AmeliaChat({
    listeners: {
        domainFail: function(source, code, message) {
            alert('unable to access domain ' + message + '[' + code + ']');
        }
    }
});
```
### domainFetch
**domainFetch**
``` js
/**
 * Fired during a manual domain selection when the list of domains is fetched
/**
 * Fired when the anonymous session cannot be created
 *    source - the AmeliaChat instance that fired the event
 *    domains - an array of domains the user can access
 */
domainFetch(source, domains);
var a = new AmeliaChat({
    listeners: {
        domainFetch: function(source, domains) {
            createSelectWidget(domains);
        }
    }
});
```
### conversationStart
**conversationStart**
``` js
/**
 * Fired when the anonymous session cannot be created
 *    source - the AmeliaChat instance that fired the event
 *    sessionId - the sessionId of the new conversation
 *    conversationId - the conversationId of the new conversation
 *    domainCode - the attempted domainCode of the new conversation
 */
conversationStart(source, sessionId, conversationId, domainCode)
var a = new AmeliaChat({
    listeners: {
        conversationStart: function(source, sessionId, conversationId, domainCode) {
            console.log('started a conversation on ' + domainCode + ' with sessionId: ' + sessionId + ' and conversationId ' + conversationId);
        }
    }
});
```
### conversationFail
**newConversationFail**
``` js
/**
 * Fired when the conversation cannot be created
 *    source - the AmeliaChat instance that fired the event
 *    status - the http status code of the failed response
 *    statusText - the http status text of the failed response
 *    responseText - the body text of the response
 */
conversationFail(source, status, statusText, responseText)
var a = new AmeliaChat({
    listeners: {
        conversationFail: function(source, status, statusText, responseText) {
            alert('unable to start session ' + statusText + '[' + status + ']');
        }
    }
});
```
### inputDisabled
**inputDisabled**
``` js
/**
 * Fired when user text input should be disabled
 *    source - the AmeliaChat instance that fired the event
 * .  conversation - the input for which the conversation is disabled.  May be an empty object in global cases
 *    messageType - the messageType responsible for causing user input to be disabled
 *    options - a hash of additional options a disabling event might set
 */
inputDisabled(source, conversation, messageType, options);
var a = new AmeliaChat({
    inputDisabled:function(source, conversation, messageType, options) {
        $('textarea.ui-chatbox-input-box').prop("disabled", true);
        $('textarea.ui-chatbox-input-box').addClass('ui-state-disabled');
        if (options && options.uploadRequest) {
             $('textarea.ui-chatbox-input-box').hide();
             $('#fileUpload').show();
       }
    }
});
```
### inputEnabled
**inputEnabled**
``` js
/**
 * Fired when user text input should be enabled
 *    source - the AmeliaChat instance that fired the event
 * .  conversation - the input for which the conversation is enabled.  May be an empty object in global cases
 *    messageType - the messageType responsible for causing user input to be enabled
 *    options - a hash of additional options a disabling event might set
 */
inputEnabled(source, conversation, messageType, options);
var a = new AmeliaChat({
    listeners: {
        inputEnabled:function(source, conversation, messageType, options) {
            $('textarea.ui-chatbox-input-box').prop("disabled", false);
            $('textarea.ui-chatbox-input-box').removeClass('ui-state-disabled');
            if (options && options.uploadRequest) {
                 $('textarea.ui-chatbox-input-box').show();
             $('#fileUpload').hide();
       }
    }
});
```
### ErrorInputBlocked
**ErrorBlockInput**
``` groovy
/**
 * Fired when an user input is attempted when a Amelia will not accept input
 *    source - the AmeliaChat instance that fired the event
 * .  conversation - the input for which the input is blocked
 *    from - the display name of the server user responding that the input is blocked
 *    attemptedText - the text the user attempted to send
 */
ErrorInputBlocked(source, conversation, from, attemptedText);
var a = new AmeliaChat({
    ErrorInputBlocked:function(source, from, attemptedText) {
       $("#chat_div").chatbox("option", "boxManager").ameliaMsg(from,  'Input is not allowed at this time.  If you have an upload or form submission pending, you must finish it');
    }
});
```
### ErrorNoActiveSubscription
**ErrorNoActiveSubscription**
``` groovy
/**
 * Fired when an user input is attempted when there is no active subscription.  Typically, there
 *    is no possible recovery other than the client code starting a new conversation
 *    source - the AmeliaChat instance that fired the event
 * .  conversation - the input for which there is no subscription.
 *    from - the display name of the server user responding that the input is blocked
 *    attemptedText - the text the user attempted to send
 *  @since 1.1
 */
ErrorNoActiveSubscription(source, conversation, from, attemptedText);
var a = new AmeliaChat({
    ErrorNoActiveSubscription(source, from, attemptedText) {
       $("#chat_div").chatbox("option", "boxManager").ameliaMsg(from,  'Error: There is no active conversation subscription');
    }
});
```
### userInit
**userInit**
``` js
/**
 * Prior to 1.4.0, Fired when a non-anonymous user is established in the session
 * After 1.4.0, fired when *any* user is established in the session, anonymous or not
 *    source - the AmeliaChat instance that fired the event
 *    user - the user established
 *      Prior to 1.4.0, user has two properties, name and email
 *      After to 1.4.0, user has four properties properties, name, email, anonymous (true/false) and sso (true/false)
 */
userInit(source, user);
var a = new AmeliaChat({
    listeners: {
        userInit(source, user) {
           $("#loginbtn").val("Logout " + user.name)
        }
    }
});
```
### moodChange
**moodChange**
``` js
/**
 * Fired when the emotional state of Amelia has changed
 *    source - the AmeliaChat instance that fired the event
 * .  conversation - the input for which the mood has changed.
 *    newMood - the new mood
 *    oldMood - the old mood
 */
moodChange(source, conversation, newMood, oldMood);
var a = new AmeliaChat({
    moodChange(source, newMood, oldMood) {
       $("#mood_div").addClass(newMood);
       $("#mood_div").removeClass(oldMood);
    }
});
```
The moods will always be one of theEmoticontypes, as of the time of this writing: **AMUSED,  ANGRY, BEMUSED, CONFUSION, CONTEMPT,  DISGUSTED, EXCITED, FEAR, HAPPY, HAPPY_SINCERE, JOY, NEUTRAL, POUT, SAD, SIMPLE_SMILE, SINCERE_SMILE, SMIRK_LEFT, SMIRK_RIGHT, SURPRISED**
# Integration Points
Amelia has two main integration points for client code that wishes to assemble more custom features.  They relate to the two Amelia messages above, [OutboundFormInputMessage](#AmeliaV3JavascriptSDK-V3.7+-outboundforminputmessage) and [OutboundIntegrationMessage](/pages/createpage.action?spaceKey=AmeliaDocsV37&title=outboundintegrationmessage&linkCreation=true&fromPageId=11940105).  They leverage the special components of those messages, and are used for submitting back to the server, and for contacting external points, respectively.  You can find more information on the server side components, and how to generate these attributes, in the [Custom UI Overview page](Overview)s.
## Handling Forms
Forms allow the creation of custom widgets and the submission of structured data back to Amelia.  The appearance of a form will usually suspend chat, as Amelia will be waiting for the structured form submission before proceeding further in the BPN.  Design your flows, introductory text, and widgets accordingly.
### Sample formInputData
Messages can will come with a JSON description of the form to assemble in an attribute called **formInputData**. 
**Sample formInputMessageData**
``` js
{
    //a name for the form; useful for identifiers
    "name":"carSelectionForm",
    //a display name for the form section, e.g. a header
    "nameForDisplay":"Car Selection Form",
    //the type of the form, can be used to make decisions on placement or layout
    "formType":"inlineform",
    //the fields in this form
    "fields":[{
        //the name of this form field
        "name":"carSelectionField",
        //the type of this form field; note that this is an arbitrary string set in the BPN; the client code is responsible for handlig
        //all possible tyeps
        "fieldType":"singleSelection",
        //the options available, e.g. for widgets that demand it, such as <select/> or banks of checkboxes or radio buttons
        "options":[{
            //the displayable name
            "name":"Lamborghini Aventador 2016",
            //the value of the submission when selected
            "value":"la2016",
            // if it should be selected by default
            "selected":false,
            //if it should be disabled by default
            "disabled":false,
                //if it should be hidden by default
            "hidden":false
        },{
            "name":"VW Beetle 1971",
            "value":"vb1971",
            "selected":false,
            "disabled":false,
            "hidden":false
        },{
            "name":"VW Brasilia 1977",
            "value":"vr1977",
            "selected":true,
            "disabled":false,
            "hidden":false
        }],
        // a struct indicating how to formulate the message in the chat window after submission
        // if present, the appropriate 
        "selectionUtteranceMetadata":{
                // the prefix
            "prefixSingle":"I select the vehicle",
            "prefixMultiple":"I select the vehicles",
            "conjunction":"and"
        }
    }],
    // not currently used
    "selectionUtteranceMetadata":{
        "staticUtterance":"",
        "conjunction":"and"
    },
    //what manner of input Amelia will accept, must be FORM_ONLY, CHAT_ONLY, or BOTH - if FORM_ONLY, the inputDisabled event will be fired
    "allowedUserInputs":"FORM_ONLY"
}
```
### Building a Form
The above attributes have the necessary components to build a form, but the client code must still build it.   To illustrate, The following example will build a form using jquery.
**Building a form with jquery**
``` js
 OutboundTextMessage(source, conversation, messageType, msgBody, headers) {
    var atts = msgBody.attributes.formInputData;
    /**
     * A helper function to create a radio or checkbox from an option
     *    name - the name of the form field
     *    option - the options object as described in OutboundFormInputMessage
     *    id - the id to set on this HTML element
     *    type - the type of the element to create  
     *    parent - the HTML element in which to place the new input
     */ 
    var createCb = function(name, option, id, type, parent) {
        var l = $('<label></label>')
            .attr('for', id)
            .text(option.name)
            .addClass('myLabel')
            .appendTo(parent)
        var f = $('<input></input>')
            .attr('type', type)
            .attr('name', name )
            .attr('value', option.value)
            .attr('checked', option.selected)
            .attr('disabled', option.disabled)
            .attr('id', id)
            .appendTo(parent);
    }
    // if we have attributes, create a <form/> inside #chat_div
    if (atts) {
        var section = $('<form></form>')
            .appendTo($('#chat_div'));
        //add a header block above our form elements
        $('<h3></h3>').text(atts.nameForDisplay).appendTo(section);
        //loop through all the fields in our formInputData
        for (var i = 0;i< atts.fields.length;i++) {
            var field = atts.fields[i];
            switch (field.fieldType) {
                case "multipleSelection":
                    // multipleSelection will result in a checkbox
                    for (var c = 0;c<field.options.length;c++) {
                        createCb(field.name, field.options[c], field.name +'_'+c, 'checkbox', section)
                    }
                    break;
                case "singleSelection":
                    //single selection will result in a radio button
                    for (var c = 0;c<field.options.length;c++) {
                        createCb(field.name, field.options[c], field.name +'_'+c, 'radio', section)
                    }
                    break;
                default:
                    console.error("unknown type " + field.fieldType);
            }
        }
        // create a submit button
        var btn = $('<input></input>')
            .attr('type', 'submit')
            .attr('value', 'Submit')
            .appendTo(section);
        //attach a handler to the button that will submit to Amelia but suppress the normal form action
        btn.on('click', function() {
            a.submit(this.form, atts);
            event.preventDefault();
            return false;
        })
}
```
Note that the construction of an HTML form is not strictly necessary; any widget or component that can eventually submit in the proper format back to Amelia will suffice.
### Submitting the Form
Submitting the form is handled by the [submit](#AmeliaV3JavascriptSDK-V3.7+-submit) method of AmeliaChat.  To repeat here, there are two forms:
#### a.submit(form, formInputData)
form - an HTML \<form/\> element containing all inputs to be submitted.  (image, button, and select will not be included)
formInputMessageData - the formInputMessageData that created the form
#### a.submit(json, formInputData)
json - the JSON to be submitted.  Allows for more flexibility, but the client code is responsible for assembling the submission properly
formInputMessageData - the formInputMessageData that created the form
## Handling Integrations
Whereas form integrations are intended to help the creation of forms to submit data back to Amelia, Integrations are by nature more flexible.  There is still a structure to allow the BPN author to define the data semantically in terms of sections, subsections, and section fields, but this structure is more generic and less focused around submissions back to Amelia.  Unlike Forms, Integration data will **not** cause Amelia to stop and wait for structured data.  Rather, they are used to start a named BPN, along with optional arguments.  This allows for more freedom in terms of design, but a closer coordination between the UI and BPN designers, as BPNs of the proper name must be available in an accessible domain, and be able to utilize the arguments provided.
### Beginning an Integration: OutboundIntegrationMessage
Integrations typically begin with a response to an **OutboundIntegrationMessage**.  This special message type contains an attribute **integrationMessageData**.  integrationMessageData contains definitions for sections, fields, and message constructors that can be defined on the BPN side in order to construct more complex widgets on the client side.  See the [Custom UI Overview page](Overview) for the most up to date documentation on the structure and creation of these messages in the BPN designer.  Once generated in the BPN, it will arrive as an attribute that your OutboundIntegrationMessage can handle, somewhat like this:
``` js
{
  "name": "myTestSection",
  "sectionType": "default",
  "title": "My Test Section",
  "children": [
    {
      "name": "mailingAddress",
      "sectionType": "default",
      "title": "Mailing Address",
      "children": [],
      "sectionFields": [
        {
          "name": "line1",
          "label": "Street",
          "value": "40 Wall Street",
          "actionProcess": {
            "processName": "change_street_address",
            "processArgs": {
              "line1": "40 Wall Street"
            }
          },
                selectionUtteranceMetadata: {
                    staticUtterance:"I would like to change my email address"
                }
        },
        {
          "name": "line2",
          "label": "Apartment, Floor, etc.",
          "value": "13 Floor"
        }
      ]
    }
  ],
  "sectionFields": []
}
```
The crucial element to note is the **actionProcess** item attached to the "line1" street field.  **actionProcess** defines the BPN and the arguments to invoke when an interaction is selected for a particular object.  While an actionProcess here is attached to a field, it can be attached to a subsection or section as well.  selectionUtteranceMetadata can also be involved; if you include it, that message will be emitted in the chat window when the action is invoked.  You can also provide your own completely custom message, but as the selectionUtteranceMetadata is defined in the BPN, using it can help keep your administration centralized.
### Handling the message and submitting the action
Using this actionProcess is slightly more complicated that using a form, but it reduces down to invoking the chat.action method with the proper arguments.  By example, again using jquery:
**setting up an action response**
``` js
/** your handler **/
OutboundIntegrationMessage:function(source, conversation, messageType, msgBody, headers) {
    var mid = msgBody.id;
    var atts = msgBody.attributes.integrationMessageData;
    //helper method to create a field with a label
    var createField = function(field, id, parent) {
        var l = $('<label></label>')
                .attr('for', id)
                .text(field.label)
                .addClass('myLabel')
                .appendTo(parent)
        var f = $('<input></input>')
                .attr('name', field.name )
                .attr('value', field.value)
                .attr('id', id)
                .appendTo(parent);
    }
    //helper method to create a button that can be clicked to invoke a process
    var createActionClicky = function(ap, selectionUtterance, message, parent) {
        $('<input/>')
            .attr('type', 'button')
            .attr('value', 'Clicky')
            .click(function() {
                a.action(ap.processName, ap.processArgs, selectionUtterance, message)
            }).appendTo(parent)
    }
    if (atts) {
        var section = $('<div></div>')
                .text(atts.instructions || atts.nameForDisplay)
                .appendTo($('.lane2'))
                .css({ backgroundColor: 'white'});
        for (var i=0;i<atts.children.length;i++) {
            var child = atts.children[i];
            var sub;
            if (child.sectionFields.length > 0) {
                $('<h3></h3>')
                        .text(child.title)
                        .appendTo(section);
                sub = $('<form style="border:1px black solid"></form>')
                        .appendTo(section);
                var fieldset = $('<fieldset style="border:2px red solid"></fieldset>')
                        .appendTo(sub);
                for (var j=0;j<child.sectionFields.length;j++) {
                    if (child.sectionFields[j].extendedDescription) {
                        sub.append(child.sectionFields[j].extendedDescription);
                    } else {
                        createField(child.sectionFields[j], mid + '_' + i +'_'+j, fieldset);
                    }
                    if (child.sectionFields[j].actionProcess) {
                        createActionClicky(child.sectionFields[j].actionProcess, child.sectionFields[j].selectionUtteranceMetadata, fieldset);
                    }
                }
            }
        }
    }
}
```
Visually, the end result of this is a box with a fieldset and an HTML form field and a button next to it.  The important function is createActionClicky and the line that calls it.  As we process the integrationMessageData, we look through the sections, subsections, and fields.  If we come across one with an actionProcess, we know the BPN designer intended for this to have additional interaction.  We create a button, and, since we are processing the message currently, we can immediately attach to it a click handler that simply passes the name and the arguments defined in the BPN, and the user will emit int he chat the text outlined int he BPN:
**createActionClicky**
``` js
    //helper method to create a button that can be clicked to invoke a process
    var createActionClicky = function(ap, selectionUtterance, message, parent) {
        $('<input/>')
            .attr('type', 'button')
            .attr('value', 'Clicky')
            .click(function() {
                a.action(ap.processName, ap.processArgs, selectionUtterance, message)
            }).appendTo(parent)
    }
```
-   ap.processName, as defined in the BPN, is **change_street_address**.  There must be a BPN of this name in a domain visible to that user.
-   ap.processArgs, as defined in the BPN, is equivalent to the initial value of the field.  Each key/value will be passed to the BPN as initial arguments.  Note that these arguments **DO NOT UPDATE AUTOMATICALLY IN RESPONSE TO CHANGES IN ANY USER INTERACTIONS YOU DESIGN.**  If you would like to pass in a different set of arguments, you may supply your own JSON object in key-value form; however, it becomes your responsibility to ensure the submission is in a format the BPN expects.
-   selectionUtterance is a simple struct defined on the BPN.  Only one attribute is supported, staticUtterance, and, if present, the user will say this in the chat upon conducting the interaction.
-   message - a custom message you can generate yourself.  It will override anything in selectionUtterance.
If neither message nor selectionUtterance is provided, a neutral default statement will be emitted into chat.
# Recipes and Snippets
## Integrating with an avatar
If you need to integrate the unity amelia avatar into a UI based on the javascript SDK, the trickiest issue is that many different types of messages can send commands for an avatar.  While you can handle it with different listeners for each message type, you can take care if it all in one by using the messageReceived listener:
**queueing bml for an avatar**
``` js
messageReceived:function(chat, message) {
    var body = JSON.parse(message.body);
    var atts = body.attributes;
    //console.error(body);
    //console.error(atts);
    if (atts.bml && me.pendingUserConversation !== true) {
        var bml = JSON.parse(atts.bml);
        if (bml instanceof Array) {
            for (var i = 0; i < bml.length; i++) {
                var currentBml = bml[i].toString();
                me.bmlQueue.enqueue(currentBml);
            }
        } else {
            me.bmlQueue.enqueue(bml);
        }
        me.tryDequeue();
    }
}
```
 The above handler will look at all messages, and, if there is bml present, pass it to the queue where it can be deQueued immediately or in an interval function.
### Relevant Avatar commands exposed as top level functions by Unity
``` js
# most commands to an avatar send a message to a CommsManager
#send bml to an avatar for speaking/moving
SendMessage("CommsManager", "LoadBMLStringRemotely",bml);
#execute a command, needs to be called after SceneLoaded (see below)
#SendMessage("CommsManager", commandName, params);
SendMessage("CommsManager", "SetDomain", "test"); //will change Amelia's badge to an appropriate image which must already exist
SendMessage("CommsManager", "ChangeVoice", 'VW Julie'); //most appropriately called from an OutboundAvatarChangeVoiceMessage
# Avatar events
# The avatar does not expose events to listen to; it invokes methods that you must place as top level functions
function SceneLoaded(){ } //called when the avatar has fully loaded as is ready for input
                          //you do not want to send commands to the avatar until this has been called
function SetInUse(busy) // busy is 'True' or 'False' indicating whether the avatar is currently busy
                        // called when speech begins and ends
function SetInMotion(moving) // moving is 'True' or 'False" indicating whether the avatar is currently moving
                             // called when motion begins and ends
```
# Live Debugging Minimized Javascript
Production builds have amelia-chat.js and all dependencies minimized and obfuscated, which can make troubleshooting and debugging difficult.  In many browsers, however, you can unpack the javascript and add breakpoints and logging to the live page.  (Note: this technique is not unique to the SDK, but it is useful when dealing with any minimized javascript.)
First, open your browser's dev tools, and navigate to the source you would like.  For this example, we will use amelia-chat-with-deps.min.js and Chrome as our browser.
1.  Look for the three vertical dots in the upper right corner of Chrome.  That opens up a menu.  In that menu, you will see **More Tools**, and inside that submenu will be **Developer Tools**.  Open developer tools, and you will see something like this screenshot:  
    ![](attachments/11940105/11940109.png)  
2.  Select "Sources" in the top bar of the dev tools, and, in the left pane, you will see all the resources used on the pane.  Navigate to the script you want to debug, in our case **/AmeliaCust/webjars/amelia-js-client/1.2.1/amelia-chat-with-deps.min.js**, and select it.  This will show the minimized javascript in the right pane.
3.  At the bottom left of the right pane, look for the two braces – **{ }**.  That is the "pretty print" option, and Chrome will do its best to unminimize the javascript, resulting in something like this next screenshot:  
    ![](attachments/11940105/11940108.png)  
    Which, while not the exact same source representation, is functionally equivalent and, more importantly for debugging, what is running currently on the site.  
4.  From there, you need to find the code you wish to debug.  (Note: in amelia-chat-with-deps.min.js, the amelia-chat portion does not even begin until towards the end of the file, as most of this file will be the dependencies.)  
5.  Place breakpoints.  Find the line or lines that you wish to debug, and right click on the line number. The menu will bring up an option to place a breakpoint.  Once placed, you will see a marker on the line number, and the code will stop at that point, allowing you to inspect the state and step through the function as it goes, all the way through the stack.
6.  Add conditions.  Sometimes, breakpoints are cumbersome, and you just want to watch the flow.  You can do this in Chrome with **conditional breakpoints**.  Right click on the marker you created, and enter whatever javascript  you wish to proceed, as in this example:  
    ![](attachments/11940105/11940107.png)  
7.  You can put whatever javascript statements you wish in this box; as long as they are valid, they will be executed.  The last statement is crucial.  If the last statement returns true, the breakpoint will stop.  If the last statement returns false, the code will not stop at this point.  In this example, the code will not stop, but instead print this to the browser's console:  
    ![](attachments/11940105/11940106.png)
A combination of these techniques should provide some insight into any running javascript, be it dependency, SDK, UX code, or something else, and help track down problems
{% /version %}
