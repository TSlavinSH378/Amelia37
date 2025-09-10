> [!info]  
>
> Please note this page is a work in progress. Content is likely to change as Amelia V3 evolves and more in-depth documentation becomes available.

Amelia interacts with people with a chat interface, as shown below. The mobile SDK and web interface allow Amelia also to be integrated into mobile applications and Skype, LivePerson, and other social channels.
# Website-Based Channels
The primary delivery channel for Amelia is a website. There are four primary website-based channels:
-   The basic website interface allows users to converse with Amelia with few visual distractions.
-   The administration website pages include a Mind view to provide a view into how Amelia develops her responses.
-   A Custom User Interface (UI) allows conversations that also include data extracted from the conversation.
## The Basic Website Interface
![](attachments/11940373/11940382.jpg)
Figure 4. Amelia Basic Website Interface
Table 1. Amelia Basic Website Interface Elements

| Interface Element | Description |
| ----|----|
| Top Navigation | Links to the MIND view of Amelia's interaction in 2D and 3D. |
| Amelia Avatar | Amelia appears in the top left of the screen |
| Conversation Area | The conversation transcript appears on the right side of the screen |
| Text Input | A single line text box directly below Amelia and the Conversation Area |

The navigation links at the top right allow access to interact with Amelia, define her behaviors, and evaluate her performance. User roles determine which links appear in the top navigation.
Table 2. Amelia Dropdown List Elements

| Top Navigation Link | Description |
| ----|----|
| User | The basic interface to interact with Amelia |
| Mind | Adds a diagnostic view to the basic Amelia interface to see how Amelia makes decisions and responds |
| 3D | View a conversation with Amelia in a dark theme. In 3D view, click plus sign at top right to display top navigation links and return to User view. |
| Conversations | For agents and supervisors, view and interact with conversations. |
| Admin | Forms to add BPNs, Intents, Entities, and other data used by Amelia, as well as system administration tasks. |
| Logout | Ends the user session |

##  The Mind Interface
Selecting Mind from the dropdown list displays the dialog systems Amelia uses to evaluate responses on the right side of the screen. The basic chat interface moves to the left side.
![](attachments/11940373/11940381.jpg)
Each primary and secondary tab in the Mind interface are described in more detail later in this document.
Table 3. Amelia Mind Interface Elements

| MIND View Links | Description |
| ----|----|
| Semantic Memory | Displays results of Amelia parsing utterances with subsystems |
| Episodic Memory | Displays semantic similarity comparisons and context matching of a conversation against a repository of conversations. |
| Process Memory | Displays any Business Process Network (BPN) triggered by user utterances |
| Emotional Memory | Displays Amelia's positive and/or negative humanization responses over course of an interaction |
| Analytic Memory | Displays comparison of utterances with prior predictive analysis results |

## Custom Interface
Amelia also includes a custom interface. For example, Amelia can build a car insurance quote on the right side of the screen as she leads the user through questions used to calculate risk and set rates.
This interface also includes the ability for Amelia to present users with a range of interaction options, for example, Yes/No and multiple choice questions.
![](attachments/11940373/11940384.png)
# Mobile Applications
The Amelia mobile app is built for iOS 9.0+ and Android platforms. The mobile version is under development. With the mobile interface, clicking the red button at the top right displays the chat notes and clicking the X at the top right of the notes returns to the conversation area.
![](attachments/11940373/11940383.png)
# Social Channels
In addition to website-based delivery channels, Amelia also works with a variety of social and other channels:
-   Skype for Business
-   LivePerson chat
-   Facebook Messenger
-   Slack
-   Text and SMS
-   Amazon's Alexa/Echo and Google's Home/Assistant
-   Voice conversations
These interactions are through a REST API exposed within an Amelia instance. Amelia also integrates with Solidus help systems.
![](attachments/11940373/11940377.png)
# Links
[](attachments/11940373/11940379.pdf)
[Amelia Web Core UI Design Guide (v1.2)](attachments/11940373/11940379.pdf) (PDF \| 109pp \| 15.2MB \| 04/30/2018)
The UI elements listed are meant to work on v2 and v3 moving forward. 
## Attachments:
![](images/icons/bullet_blue.gif) [image2017-9-15_15-9-31.png](attachments/11940373/11940374.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-15_15-9-0.png](attachments/11940373/11940375.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-15_15-8-24.png](attachments/11940373/11940376.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-9-15_15-7-48.png](attachments/11940373/11940377.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-custom-ui-style-guide-v1.2.jpg](attachments/11940373/11940378.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [AmeliaStyleGuideV1.2_20180430_RO.pdf](attachments/11940373/11940379.pdf) (application/pdf)  
![](images/icons/bullet_blue.gif) [AmeliaStyleGuideV1.1_20171109.pdf](attachments/11940373/11940380.pdf) (application/pdf)  
![](images/icons/bullet_blue.gif) [amelia_v3_home_mind_view-2.jpg](attachments/11940373/11940381.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia_v3_home_basic_view-2.jpg](attachments/11940373/11940382.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [amelia-v3-mobile-ui-2017-1023.png](attachments/11940373/11940383.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-desktop-ui-2017-1023.png](attachments/11940373/11940384.png) (image/png)  
![](images/icons/bullet_blue.gif) [AmeliaStyleGuideV1.0_20171016-cover.jpg](attachments/11940373/11940385.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [AmeliaStyleGuideV1.0_20171016.pdf](attachments/11940373/11940386.pdf) (application/pdf)  
