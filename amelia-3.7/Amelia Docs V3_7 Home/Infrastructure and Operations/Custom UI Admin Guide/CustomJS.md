> [!warning]  
>
> Use of CustomJS is the responsibility of our clients to implement, test, and maintain. IPsoft is happy to help guide our clients, provide examples, and so on. But clients assume responsibility for use of CustomJS features.

The config.json file has a property, **customJS**, which can be used to implement small targeted feature workarounds, for example, to add analytics or text to speech (TTS). However, please confirm first with IPsoft staff before implementing features with this property. The feature may be available as built in functionality. Significant changes to the custom user interface should be requested through IPsoft staff. Use of the customJS property should be a last resort.
Only one instance of the customJS property can be used in a custom user interface. Multiple features need to be concatenated intp a single minimized bit of code passed with the config.json file.
Refer to [Custom UI Bundles](https://docs.ipsoft.com/display/AmeliaDocsV37/Custom+UI+Bundles) for details about configuring a custom user interface and [Customize UI with config.json](https://docs.ipsoft.com/display/AmeliaDocsV37/Customize+UI+with+config.json) for details about the config.json file.
# Capture Analytics Data
As of Custom UI version 5.5.1, it is possible to capture analytics data for the custom user interface. JavaScript code is passed with the **customJS** property in the config.json file.
Analytics data can be sent with an external script to receive data or without an external script.
## External Script to Process Data
Data can be processed with an external script adapted to receive data in a structured format. Code used to collect data is pretty printed then minified before being added to the **customJS** property in the config.json file.
1.  Create a script file to receive analytics data. The script includes a **sendAnalytics** function and receives values for **eventType**, **conversationId**, **sessionId**, **agentName**, and **domainCode** wrapped in a **data** value. These values are sent when **resetConversation** or **closedConversation** events happen in the custom user interface.  
    For example, this JavaScript code creates a **sendAnalytics** function and writes to Amelia's **console.log** function.
    ``` groovy
    function sendAnalytics (data) {
        // My analytics code below to process s, type, src values ...
        console.log('data', data);
    }
    ```
2.  Pretty print the JavaScript code used to collect data.
    ``` groovy
    var s = document.createElement('script');
    s.type = 'text/javascript';
    s.src = 'http://somedomain.com/somescript';
    document.head.appendChild(s);
    ```
3.  Minify the pretty print JavaScript code. Then add it to the **customJS** property in the config.json file.
    ``` groovy
    {
      "customJS": "(() => {var s = document.createElement('script');s.type = 'text/javascript';s.src = 'http://somedomain.com/somescript';document.head.appendChild(s);})();"
    }
    ```
## No External Script to Process Data
If there is no external analytics file to process data, the **customJS** property is set to receive data using Amelia's **console.log** functionality.
``` groovy
{
  "customJS": "window.sendAnalytics = function (data) {console.log('data', data);};"
}
```
## Example to Collect Clicked Links
This code collects any custom user interface links clicked by the user. JavaScript is used to capture URLs with data collected and sent with the **customJS** property in the config.json file.
1.  Create a JavaScript function **getClick** to create a list to capture data about links clicked.
    ``` groovy
    <script type="text/javascript">
    var list = []; 
    function getClick(url) {
        console.log(url);
        list.push(url);
        console.log(list);
    }
    </script>
    ```
2.  Pretty print the JavaScript function.
    ``` groovy
    var s = document.createElement('script');
    s.type = 'text/javascript';
    s.text = 'var list = []; function getClick(url) {console.log(url); list.push(url); console.log(list);}';
    document.head.appendChild(s);
    ```
3.  Minify the pretty print JavaScript code. Then add it to the **customJS** property in the config.json file.
    ``` groovy
    {
    "customJS": "(() => {var s = document.createElement('script');s.type = 'text/javascript';s.text = 'var list = []; function getClick(url) {console.log(url);list.push(url);console.log(list);}';document.head.appendChild(s);})();"
    }
    ```
# Add Text to Speech (TTS)
As of Custom UI version 5.15.0, it is possible to send customized text to speech (TTS) to the chat window. JavaScript code is passed with the **customJS** property in the config.json file.
## Set Value for customJS property
To set up text to speech, add a third-party library script to the document head then prettify and minify JavaScript code and pass it to the customJS property in the config.json file.
1.  Add the TTS third-party library script to the head of the custom user interface document. Then create an element where the audio will play from.
2.  Pretty print code for the TTS third-party library and audio element, as in this example.
    ``` groovy
    var s = document.createElement('script');
    s.type = 'text/javascript';
    s.src = 'http://somedomain.com/somescript';
    document.head.appendChild(s);
    var audio = document.createElement('audio');
    document.body.appendChild(audio);
    ```
3.  Minify the pretty printed JavaScript and add the customJS property to the config.json file, as in this example.
    ``` groovy
    {
      "customJS": "(() => {var s = document.createElement('script');s.type = 'text/javascript';s.src = 'http://somedomain.com/somescript'; document.head.appendChild(s); var audio = document.createElement('audio'); document.body.appendChild(audio);})();"
    }
    ```
## Example TTS Configuration
This example uses Amazon Polly with documentation here. In this example, JavaScript code is created then pretty printed and minified then passed to the customJS property in the config.json file.
1.  Create a script with fetchCustomSpeech and playCustomSpeech to pass as a value to the customJS property.The fetchCustomSpeech function must call chat.addFetchedAudio and pass the propertys for tts and {audio:url}, as in this example.
    ``` groovy
    const fetchCustomSpeech = (tts, chat) => {
       AWS.config.region = 'YOUR_REGION';
       AWS.config.credentials = new AWS.CognitoIdentityCredentials({ IdentityPoolId: 'YOUR_IDENTITY_POOL_ID' });
       // Create synthesizeSpeech params JSON
       const speechParams = {
         OutputFormat: 'mp3',
         SampleRate: '16000',
         Text: '',
         TextType: 'text',
         VoiceId: 'Matthew'
       };
       speechParams.Text = tts.text.replace(/<(?:.|\\n)*?>/gm, '');
       // Create the Polly service object and presigner object
       const polly = new AWS.Polly({ apiVersion: '2016-06-10' });
       polly.synthesizeSpeech(speechParams, (error, data) => {
         if (error) {
           console.log('error', error);
         } else {
           const audio = document.getElementsByTagName('audio');
           const uInt8Array = new Uint8Array(data.AudioStream);
           const arrayBuffer = uInt8Array.buffer;
           const blob = new Blob([arrayBuffer]);
           const url = URL.createObjectURL(blob);
           audio[0].src = url;
           chat.addFetchedAudio(tts, { audio: url });
         }
       });
     };
    ```
    The playCustomSpeech function must call chat.onFetchedAudioPlayStart at the start of playing and chat.onFetchedAudioPlayEnd method after the speech has ended, as in this example.
    ``` groovy
    const playCustomSpeech = (toPlay, chat) => {
        chat.onFetchedAudioPlayStart();
        const audio = document.getElementsByTagName('audio');
        audio[0].onended = () => {
            chat.onFetchedAudioPlayEnd();
        };
        audio[0].src = toPlay.audio;
        audio[0].play();
    };
    ```
2.  Pretty print then minify the JavaScript and pass it to the customJS property, as shown in this example.
    ``` groovy
    {
      "customJS": "(() => {var s = document.createElement('script'); s.type = 'text/javascript'; s.src = 'https://sdk.amazonaws.com/js/aws-sdk-2.283.1.min.js'; document.head.appendChild(s); var audio = document.createElement('audio'); document.body.appendChild(audio);})(); window.fetchCustomSpeech=function(e,t){AWS.config.region='YOUR_REGION',AWS.config.credentials=new AWS.CognitoIdentityCredentials({IdentityPoolId:'YOUR_IDENTITY_POOL_ID'});const o={OutputFormat:'mp3',SampleRate:'16000',Text:'',TextType:'text',VoiceId:'Matthew'};o.Text=e.text.replace(/<(?:.|\\n)*?>/gm,''),new AWS.Polly({apiVersion:'2016-06-10'}).synthesizeSpeech(o,(o,n)=>{if(o)console.log('error',o);else{const o=document.getElementsByTagName('audio'),a=new Uint8Array(n.AudioStream).buffer,c=new Blob([a]),d=URL.createObjectURL(c);o[0].src=d,t.addFetchedAudio(e,{audio:d})}})},window.playCustomSpeech=function(e,t){const o=document.getElementsByTagName('audio');o[0].onended=(()=>{t.onFetchedAudioPlayEnd()}),o[0].src=e.audio,o[0].play()};"
    }
    ```
# Change Chat Log Background Image
First, minify a script. The image must be a Base64 string value.
``` groovy
var styles = document.createElement('style'); styles.innerHTML = '.main--wrapper { background: url(data:image/png;base64,iREST_OF_BASE64_STRING) left top no-repeat; background-size: 24px;}'; document.body.appendChild(styles);
```
Then add the script to the config.json file as a value for the **customJS** property.
``` groovy
{
"customJS": "(() => { var styles = document.createElement('style'); styles.innerHTML = '.main--wrapper { background: url(data:image/png;base64,iREST_OF_BASE64_STRING) left top no-repeat; background-size: 24px;}'; document.body.appendChild(styles); })()"
}
```
# Change Chat Notes Button Colors
First, minify a script.
``` groovy
var chatNotesStyles = document.createElement('style'); chatNotesStyles.innerHTML = '.ChatNote__edit-button {background-color: #FFF; color: #0000FF;}'; document.body.appendChild(chatNotesStyles);
```
Then add the script to the config.json file as a value for the **customJS** property.
``` groovy
{
"customJS": "(() => { var styles = document.createElement('style'); styles.innerHTML = '.main--wrapper { background: url(data:image/png;base64,iREST_OF_BASE64_STRING) left top no-repeat; background-size: 24px;}'; document.body.appendChild(styles); var chatNotesStyles = document.createElement('style'); chatNotesStyles.innerHTML = '.ChatNote__edit-button {background-color: #FFF; color: #0000FF;}'; document.body.appendChild(chatNotesStyles); })()"
}
```
# Combine Chat Log Background and Button Colors
To combine a chat log background image with button colors, both scripts can be added as a single minified script value for the **customJS** property in the config.json file.
``` groovy
{
"customJS": "(() => { var styles = document.createElement('style'); styles.innerHTML = '.main--wrapper { background: url(data:image/png;base64,iREST_OF_BASE64_STRING) left top no-repeat; background-size: 24px;} .ChatNote__edit-button {background-color: #FFF; color: #0000FF;}'; document.body.appendChild(styles);})()"
}
```
