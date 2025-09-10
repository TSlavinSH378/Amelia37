-   [Creating a New Skill](#AlexaSkillCreation-CreatingaNewSkill)
-   [Interaction Model](#AlexaSkillCreation-InteractionModel)
-   [EndPoint](#AlexaSkillCreation-EndPoint)
-   [Skill ID](#AlexaSkillCreation-SkillID)
-   [Audio Player (Optional)](#AlexaSkillCreation-AudioPlayer(Optional))
> [!warning]  
>
> This guide does not cover certification and distribution of the skill.

# Creating a New Skill
1.  Log into Amazon's developer account at [https://developer.amazon.com](https://developer.amazon.com/) 
2.  Navigate to the Alexa Skills Kit Developer Console
3.  Click the button on the right labeled **Create Skill**
4.  Create a new **Skill Name** (This is not the same as the invocation name)
5.  When choosing a model to add to your skill, select **Custom  
    **![](attachments/23397229/23397244.png)  
6.  Choose a template → **Start from scratch**
# Interaction Model
1.  Navigate to JSON Editor on the left hand menu
2.  Use the IPsoft provided JSON file and copy and paste (or drag and drop) into the editor.
3.  Correct the invocation name to a new unique name.   
    > [!warning]  
    >
    > There are invocation name requirements. For more information refer to the invocation menu option on the left.
    ![](attachments/23397229/23397245.png)  
4.  Click Save and Build Model
# EndPoint
1.  Navigate to endpoint and enter the URL of your Amelia instance. It should look something like this:  
    https://{HOST}/Amelia/alexa/api/messages  
    ![](attachments/23397229/23397246.png)  
2.  Click Save Endpoints
# Skill ID
-   Navigate to the skill and View the Skill Id by clicking the words "View Skill ID"
-   This value will be needed in the Alexa Gateway application.properties file.  
    **"amzn1.ask.skill.abcdefgh-1234-4321-1234-abcdefgh1234"**  
    ![](attachments/23397229/25461630.png)  
# Audio Player (Optional)
1.  Navigate to Interfaces on the left hand panel.
2.  Toggle the Audio Player switch to enable the feature.  
    ![](attachments/23397229/25461653.png)  
3.  Click Save Interfaces
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-9-5_15-6-1.png](attachments/23397229/23397244.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-5_15-8-9.png](attachments/23397229/23397245.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-5_15-10-46.png](attachments/23397229/23397246.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-7_10-46-46.png](attachments/23397229/25461630.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-10-8_9-33-2.png](attachments/23397229/25461653.png) (image/png)  
