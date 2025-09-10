-   [Greeting](#AlexaOverview-Greeting)
-   [Utterance Recognition](#AlexaOverview-UtteranceRecognition)
-   [Conversation](#AlexaOverview-Conversation)
-   [Installation](#AlexaOverview-Installation)
-   [Distribution](#AlexaOverview-Distribution)
The Alexa Gateway allows Amazon Alexa users to speak to Amelia by invoking her name (or a customized name) as a skill. Invoking the skills name automatically launches a new conversation with Amelia.
## Greeting
As with any Amelia conversation, Amelia begins by greeting the user. Using the greeting BPN feature from Amelia, she introduces the user to all the functionalities of the skill as well as conveys any relevant information.
## Utterance Recognition
Once a conversation starts, Alexa will attempt to recognize and transcribe the user's utterance and match it with one of the skill's intents, filling any appropriate slots with the parsed information.
Amazon deprecated an older slot type known as AMAZON.LITERAL (which passes the entire transcription) in favor of it's new feature, custom slots. As a result of this change, a custom slot was made with a set of sample utterances designed to catch most, if not all, utterances spoken by the user. Given that there is only one custom intent with the aforementioned custom slot, Amazon will match with this intent a majority of the time. The other intents are mandatory built-in intents.
With the entire utterance converted into a transcription, this information can be passed into Amelia as if a user typed within a chat.
## Conversation
As with any conversation, Alexa and the user alternate speaking and listening to one another. Should the user stop speaking or trigger the close intent, the skill will close in Alexa and therefore also close the conversation with Amelia.
## Installation
Installation of the skill on the Amazon Alexa Developer Console requires a JSON file from IPsoft then configuring an endpoint.
1.  IPsoft will provide a .json file that can be drag-and-dropped into the skill builder to create all the necessary intents and slots needed.
2.  The skill's endpoint will need to be configured to point at an Alexa Gateway enabled instance of Amelia.
For more information please refer to our skill installation guide.
## Distribution
The Amelia skill can be used either privately or publicly depending on the use case.
Private skills will need to be deployed via an Alexa for Business account. (For more information - <https://aws.amazon.com/alexaforbusiness/>) 
Public skills will need to be certified by Amazon to be placed into their store (For more information - <https://developer.amazon.com/docs/custom-skills/certification-requirements-for-custom-skills.html>)
