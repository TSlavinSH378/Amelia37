A chat overlay is a popup window that appears over a web page. Conversing with Amelia with a chat overlay can lead her to display web pages in the main browser window, as needed. This example shows how to install and demonstrate a basic chat overlay.
![](attachments/11939945/25460822.png)
Figure. Custom Chat Overlay in an Example Website
Your browser does not support the HTML5 video element
Figure. Video Demonstration of Custom Chat Overlay
# Requirements
-   Amelia 3.4.12+
-   Custom UI 5.5.0+
# Setup UI Bundles
In Amelia's System Settings admin pages, the UI Bundles link opens a workspace to add, edit, and manage custom user interfaces (UIs). For a new bundle or to edit a bundle, the Config Json text area includes the UI bundle JSON. The [Customize UI with config.json](Customize%20UI%20with%20config_json) page has details about each parameter setting in the file.
These parameters need to be set:
-   `headerDisabled` set to `true`
-   `rejoin` set to `true` if chat overlay will reload pages
-   `browserTabTitle` sets header title if `headerDisabled` set to `true` (Custom UI version 5.8.0+)
![](attachments/11939945/11939946.png)
Figure. UI Bundles New/Edit Workspace with headerDisabled Parameter Highlighted
# Configure Response Headers
Embedding an Amelia overlay into a website is restricted by web browser X-FRAME-OPTIONS response headers. There are two work arounds.
## Chrome and Firefox Browsers
For these browsers, add the frame-ancestors CSP header to the UI Bundle configuration, as described above.
``` groovy
"frame-ancestors":"https://MYDOMAIN.com"
```
> [!warning]  
>
> This method is not supported by Safari, IE11, or browsers using the iOS operating system.

## All Web Browsers and HAproxy
If using SSO and HAproxy, a comprehensive solution that works for all web browsers uses the HAproxy configuration file to set response headers. Add the following to the amelia-user-web portion of the HAproxy configuration file.
``` groovy
rspdel ^X-Frame-Options:.*
rspadd X-Frame-Options:\ ALLOWALL
rspadd Access-Control-Allow-Origin:\ *
```
# Setup Custom Chat Overlay iframe
The chat overlay iframe requires a URL be configured and two images be hosted and referenced.
## Configure the iframe URL
The chat overlay URL includes two querystring parameters passed with the iframe `src` parameter, `embed` and `domainCode`.
``` groovy
PROTOCOL://DOMAIN/Amelia/ui/YOUR_BUNDLE_NAME/?embed=iframe&domainCode=YOUR_AMELIA_DOMAIN_CODE
```
The iframe `src` URL value defines the iframe tag, as shown in this example. The `img` elements with `close.png` and `open.png` are described immediately below.
``` groovy
<div class="chat-overlay">
  <div class="chat-overlay-wrapper">
        <div class="chat-overlay-header-mobile">
        <img class="close" src="./close.png" alt="toggle chat overlay" />
      </div>
      <iframe id="receiver" src="https://MyAmelia.ipsoft.com/Amelia/ui/MyAmeliaUIBundle/?embed=iframe&domainCode=MyAmeliaDomainCode" frameborder="0" width="100%" height="100%" allow="geolocation; microphone; camera">
        <p>Your browser does not support iframes.</p>
      </iframe>
      <div class="chat-overlay-header">
        <img class="chat-overlay-header-img close" src="./close.png" alt="toggle chat overlay" />
        <img class="chat-overlay-header-img open" src="./icon.png" alt="toggle chat overlay" />
      </div>
  </div>
</div>
```
## Add Open and Close Images
The open.png and close.png image files need to be hosted somewhere then referenced in the `img` parameter of the iframe `chat-overlay-header-img` class, as shown above when creating the iframe.
![](attachments/11939945/23396875.png)
Figure. open.png File
![](attachments/11939945/23396876.png)
Figure. close.png File
# Update Parent Page
The HTML parent page needs listener code added to the bottom of the page, as well as CSS styles and two images.
## Add Listener Code
Add code to the bottom of the parent web page to listen for chat overlay messages. The receiveMessage function receives messages from the Custom UI sent to the parent page. The sendMessage function sends messages from the parent page to the Custom UI.
``` groovy
<script>
function receiveMessage(e, data) {
    /**
     * Receive message from child frame and update the DOM
     * @param {Object} data - data used to update the DOM
     * @returns - no return
     */
    // Check to make sure that this message came from the correct domain.
    var url = e.data.url;
    if (e.origin !== 'https://MyAmelia.ipsoft.com')
      return;
     if (e.data.action === "checkout" && e.data.additionalData) {
        window.location.href = "/checkout/?additionalData="+ e.data.additionalData;
    }
  }
  function sendMessage(data) {
    /**
     * Use data object and postMessage to URL provided (postMessage to child frame)
     * @param {Object} data - data to be sent to url provided of child frame
     * @returns - no return
     */
    var receiverElem = document.getElementById('receiver').contentWindow;
    receiverElem.postMessage(data, "https://MyAmelia.ipsoft.com/Amelia/ui/MyAmeliaUIBundle/?embed=iframe&domainCode=MyAmeliaDomainCode");
  }
window.addEventListener('message', receiveMessage);
</script>
```
## Add Chat Overlay Code
To render messages sent by Amelia's custom user interface, add this code to the bottom of the parent web page.
``` groovy
<script>
  function openChatOverlay (receiverElem, imgElemOpen, imgElemClose) {
    document.getElementById('receiver').classList.add("open");
    document.getElementById('receiver').classList.remove("close");
    document.getElementsByClassName('chat-overlay')[0].classList.add("chat-overlay-open");
    document.getElementsByClassName('chat-overlay')[0].classList.remove("chat-overlay-closed");
    document.getElementsByClassName('chat-overlay-header-mobile')[0].classList.remove('close');
    imgElemClose.style.opacity = 1;
    imgElemOpen.style.opacity = 0;
    localStorage.setItem('chatOverlayOpen', true);
  }
  function closeChatOverlay (receiverElem, imgElemOpen, imgElemClose) {
    document.getElementById('receiver').classList.add("close");
    document.getElementById('receiver').classList.remove("open");
    document.getElementsByClassName('chat-overlay')[0].classList.add("chat-overlay-closed");
    document.getElementsByClassName('chat-overlay')[0].classList.remove("chat-overlay-open");
    document.getElementsByClassName('chat-overlay-header-mobile')[0].classList.add('close');
    imgElemOpen.style.opacity = 1;
    imgElemClose.style.opacity = 0;
    localStorage.setItem('chatOverlayOpen', false);
  }
  function toggleChatOverlay () {
    /**
     * Toggles opening and closing of the chatOverlay
     * @returns - no return
     */
    var chatOverlayHeaderImgElemOpen = document.getElementsByClassName('chat-overlay-header-img open')[0];
    var chatOverlayHeaderImgElemClose = document.getElementsByClassName('chat-overlay-header-img close')[0];
    var receiverElem = document.getElementById('receiver');
    if (receiverElem.classList.contains('close')) {
      openChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    } else {
      closeChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    }
  }
  var chatOverlayHeaderElem = document.getElementsByClassName('chat-overlay-header')[0];
  chatOverlayHeaderElem.addEventListener('click', toggleChatOverlay);
  var chatOverlayHeaderElemMobile = document.getElementsByClassName('chat-overlay-header-mobile')[0];
  chatOverlayHeaderElemMobile.addEventListener('click', toggleChatOverlay);
  if (typeof(Storage) !== "undefined") {
    var chatOverlayOpen = localStorage.getItem('chatOverlayOpen');
    var chatOverlayHeaderImgElemOpen = document.getElementsByClassName('chat-overlay-header-img open')[0];
    var chatOverlayHeaderImgElemClose = document.getElementsByClassName('chat-overlay-header-img close')[0];
    var receiverElem = document.getElementById('receiver');
    if (chatOverlayOpen && localStorage.getItem('chatOverlayOpen') !== "true") {
      closeChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    } else {
      openChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
    }
  } else {
      // Sorry! No Web Storage support..
    console.log('No localStorage support')
  }
</script>
```
## Add CSS Styles
These styles should be added anywhere in the body or head section of the web page HTML file.
``` groovy
<style>
.chat-overlay {
  position: fixed;
  width: 376px;
  height: 500px;
  bottom: 24px;
  right: 24px;
  z-index: 90;
}
.chat-overlay-open {
    height: 512px;
}
.chat-overlay-closed {
    height: 78px;
}
.chat-overlay-wrapper {
  width: 376px;
  height: 448px;
}
.chat-overlay-header-mobile {
    display: none;
}
.chat-overlay-header {
  position: relative;
  height: 56px;
  width: 56px;
  border: 1px solid black;
  background: #000;
  margin-left: auto;
  border-radius: 50%;
  box-shadow: 1rem 1rem 5rem rgba(0, 0, 0, 0.5);
}
#receiver {
  transition: opacity 1s ease-in-out;
  opacity: 1;
  background: rgba(0, 0, 0, 0.5);
  box-shadow: 1rem 1rem 5rem rgba(0, 0, 0, 0.5);
  border-radius: 0.5rem;
}
#receiver.close {
  height: 0;
  opacity: 0;
  overflow: hidden;
}
#receiver.open {
  height: 100%;
  opacity: 1;
  overflow: hidden;
}
.chat-overlay-header-img {
  position: absolute;
  max-width: 14px;
  max-height: 14px;
  transition: opacity 1s ease-in-out;
  opacity: 1;
  right: 0px;
  left: 0px;
  top: 0px;
  bottom: 0px;
  margin: auto;
}
.chat-overlay-header-img.open {
  opacity: 0;
}
.absolute-cart-box {
  display: none;
}
@media only screen and (max-width: 768px) {
  .chat-overlay {
    width: 100%;
    position: fixed;
    height: 100%;
  }
  .chat-overlay-header-mobile {
    display: flex;
    width: inherit;
    height: 9%;
    background: #4d5aff;
  }
  .chat-overlay-header-mobile img {
    height: 30%;
    padding: 1rem;
    margin-left: auto;
  }
  .chat-overlay-header-mobile.close {
    display: none;
  }
  #receiver {
    border-radius: 0;
  }
  #receiver.close {
    height: 0;
    opacity: 0;
    overflow: hidden;
  }
  #receiver.open {
    height: 91%;
    opacity: 1;
    overflow: hidden;
  }
  .chat-overlay-open {
    height: 100%;
    bottom: 0px;
    right: 0px;
    }
  .chat-overlay-closed {
        height: 70px;
    bottom: 24px;
    right: 24px;
    }
  .chat-overlay-wrapper {
    width: 100%;
    height: 100%;
  }
}
</style>
```
# Create a BPN
A simple BPN can be created to pass a JSON data object to Amelia's custom user interface which sends data as a message to the parent page.
![](attachments/11939945/25460821.png)
Table. BPN Specifications to Create a Custom Chat Overlay

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say Let’s get started | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | create and send JSON object | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Custom Chat Overlay
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
> [!warning]  
>
> The `destinationURL` value below is the iframe src parameter value used to create the chat overlay above. The `action` property also connects to the `e.data.action` code block in the listener code above.

``` groovy
def jsonString = '''
{
    "action": "sendChatOverlayEvent",
    "payload": {
        "componentType": "MessageIntegration",
        "subComponentType": "ChatOverlay",
        "formMessageType": "chatOverlay",
        "destinationUrl": "YOUR_PARENT_FRAME_URL",
        "data": {
            "action": "checkout",
            "additionalData": "MyAdditionalData"
        }
    }
}
'''
messageService.sendIntegrationMessage(jsonString)
```
## Talk with Amelia
Call up the web page with the chat overlay then in the overlay type run the workflow BPN_NAME to display the message. BPN_NAME is the name of the BPN created above.  
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-9-4_10-47-56.png](attachments/11939945/11939946.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-4_10-44-58.png](attachments/11939945/11939947.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-9-4_8-51-45.png](attachments/11939945/11939948.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_9-0-48.png](attachments/11939945/23396875.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-8-19_9-1-26.png](attachments/11939945/23396876.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-11_12-21-15.png](attachments/11939945/25460821.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-11_12-22-48.png](attachments/11939945/25460822.png) (image/png)  
![](images/icons/bullet_blue.gif) [TShirtDemoVideo.mp4](attachments/11939945/25460823.mp4) (video/mp4)  
