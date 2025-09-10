As of Custom UI version 5.15.0, it is possible to send customized text to speech (TTS) to the chat window. JavaScript code is passed with the **customJS** parameter in the config.json file.
Refer to [Custom UI Bundles](https://docs.ipsoft.com/display/AmeliaDocsV37/Custom+UI+Bundles) page for details about configuring a custom user interface and [Customize UI with config.json](https://docs.ipsoft.com/display/AmeliaDocsV37/Customize+UI+with+config.json) for details about the config.json file.
# Set Value for customJS Parameter
To set up text to speech, add a third-party library script to a document head then prettify and minify JavaScript code and pass it to the customJS parameter in the config.json file.
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
3.  Minify the pretty printed JavaScript and add the customJS parameter to the config.json file, as in this example.
    ``` groovy
    {
      "customJS": "(() => {var s = document.createElement('script');s.type = 'text/javascript';s.src = 'http://somedomain.com/somescript'; document.head.appendChild(s); var audio = document.createElement('audio'); document.body.appendChild(audio);})();"
    }
    ```
# Example TTS Configuration
This example uses Amazon Polly with documentation here. In this example, JavaScript code is created then pretty printed and minified then passed to the customJS parameter in the config.json file.
1.  Create a script with fetchCustomSpeech and playCustomSpeech to pass as a value to the customJS parameter.The fetchCustomSpeech function must call chat.addFetchedAudio and pass the parameters for tts and {audio:url}, as in this example.
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
2.  Pretty print then minify the JavaScript and pass it to the customJS parameter, as shown in this example.
    ``` groovy
    {
      "customJS": "(() => {var s = document.createElement('script'); s.type = 'text/javascript'; s.src = 'https://sdk.amazonaws.com/js/aws-sdk-2.283.1.min.js'; document.head.appendChild(s); var audio = document.createElement('audio'); document.body.appendChild(audio);})(); window.fetchCustomSpeech=function(e,t){AWS.config.region='YOUR_REGION',AWS.config.credentials=new AWS.CognitoIdentityCredentials({IdentityPoolId:'YOUR_IDENTITY_POOL_ID'});const o={OutputFormat:'mp3',SampleRate:'16000',Text:'',TextType:'text',VoiceId:'Matthew'};o.Text=e.text.replace(/<(?:.|\\n)*?>/gm,''),new AWS.Polly({apiVersion:'2016-06-10'}).synthesizeSpeech(o,(o,n)=>{if(o)console.log('error',o);else{const o=document.getElementsByTagName('audio'),a=new Uint8Array(n.AudioStream).buffer,c=new Blob([a]),d=URL.createObjectURL(c);o[0].src=d,t.addFetchedAudio(e,{audio:d})}})},window.playCustomSpeech=function(e,t){const o=document.getElementsByTagName('audio');o[0].onended=(()=>{t.onFetchedAudioPlayEnd()}),o[0].src=e.audio,o[0].play()};"
    }
    ```
