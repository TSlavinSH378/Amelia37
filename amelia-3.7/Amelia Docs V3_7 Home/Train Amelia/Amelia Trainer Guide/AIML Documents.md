Amelia uses Artificial Intelligence Markup Language (AIML) files to chit chat with people, for example, if someone asks Amelia about her favorite movie. The chit chat sub system module responds when no higher priority module is triggered by an utterance.
The chit chat module primarily uses AIML to respond but in rare cases also uses a Semantic Role Labelling (SRL) module. When chit chat is triggered, Amelia's Debug mode displays *AIML* in the Sub Systems tab of the Subsystem Responses page for a given utterance.
![](attachments/11939692/11939693.jpg)
Figure. Chit Chat Subsystem Module Output
The modified AIML standard Amelia uses contains approximately 100,000 categories with patterns and templates. These are organized into roughly 75 files visible in the AIML Documents page. Some files are structured and contain categories related to the file name while others are unstructured. Amelia uses a regular expression to find a pattern closest to an utterance then returns the template for the category as her response.
The AIML Documents page also includes a set of text files used by Amelia. The SET files, for example, contains lists of food, movies, and other named entities. The utterance "I like Shrek" could be matched to the "I like \<set name="movies"\>" pattern with Amelia responding, "I like Interstellar." MAP files map contractions to their full form, for example, *you're* maps to *you are*.
Files visible in the AIML Documents page are stored in the amelia-kdb master database and retrieved from the amelia-kdb slave database. Changes are saved first to the master database then replicated to the slave database. Amelia's engine service starts with a basic set of AIML documents optimized to load quickly then loads files from the amelia-kdb slave database after the Amelia instance starts.
In rare cases, Amelia uses Semantic Role Labelling (SRL) to identify the agents of the central verb in the user utterance then uses that information to ask the user a question. Templates shape Amelia's responses. For example, if the person says, "I play soccer most nights" Amelia will use SRL to respond with a question, "Where do you play?" or "Who do you play with?"
# Modifying AIML Files
AIML files are modified by Cognitive engineers working with clients.
![](attachments/11939692/11939695.jpg)
Figure. AIML Documents Workspace
![](attachments/11939692/11939694.png)
Figure. AIML Document Edit Page
# AIML File Structure
The modified AIML standard Amelia uses contains approximately 100,000 categories with patterns and templates. These are organized into roughly 75 files visible in the AIML Documents page. Some files are structured and contain categories related to the file name while others are unstructured. Amelia uses a regular expression to find a pattern closest to an utterance then returns the template for the category as her response.
The AIML Documents page also includes a set of text files used by Amelia. The SET files, for example, contains lists of food, movies, and other named entities. The utterance "I like Shrek" could be matched to the "I like \<set name="movies"\>" pattern with Amelia responding, "I like Interstellar." MAP files map contractions to their full form, for example, *you're* maps to *you are*.
## Category
An AIML file is made of categories, for example:
``` groovy
<category>
    <pattern>HAVE YOU SEEN MY BOTTLE *</pattern>
    <template>I think you've had enough.</template>
</category>
```
Each category has a pattern followed by a template field. User utterances are matched with the pattern and the corresponding response is stored in the template tags. 
## Pattern
The Pattern definition can be atomic, an exact string to be matched with the user utterance. Or a pattern can have a wild card ( underscore \_ or asterisk \*) as in the code example above. Underscore has the highest priority, followed by atomic pattern and lastly, patterns with asterisk.  
For example, if the user utterance is, "Have you seen my bottle of water?", and AIML definitions have the following three categories:
**First Category**
``` groovy
<category>
    <pattern>HAVE YOU SEEN _</pattern>
    <template>I think you've had enough.</template>
</category>
```
**Second Category**
``` groovy
<category>
    <pattern>HAVE YOU SEEN MY BOTTLE OF WATER</pattern>
    <template>... </template>
</category>
```
**Third Category**
``` groovy
<category>
    <pattern>HAVE YOU SEEN MY BOTTLE *</pattern>
    <template>I think you've had enough.</template>
</category>
```
The first category pattern would be matched to "Have you seen my bottle of water?" because it has an underscore as a wild card. If the first pattern did not exist, the second category pattern would've been matched. Amelia searches for a pattern across categories in a Depth First search. At each level of attempted matching of AIML files to user utterance, patterns are ordered according to the precedence order described above.
## Template
Templates can have a certain XML tags present, they could be used for setting or retrieving variables or calling another category, etc.
``` groovy
<category>
    <pattern>IS SOMEONE *</pattern>
    <template><bot name="master"/> is always working behind the scenes.</template>
</category>
```
In this case, the variable *master* is retrieved. Variables related to Amelia's personality could be set in a text file present along with the AIML files, further variables related to the user are usually set during the conversation. Some of the user variables are defined in the AIML files and are often set to unknown.
# Editing AIML Files
> [!info]  
>
> In most cases, IPsoft Cognitive Engineers work with clients to modify AIML files based on their project requirements. Modifying or removing AIML files can break other files that reference data within existing AIML files.

In this example, from the TutorialsPoint online course linked below, demonstrates how AIML tags can be used to set and get variables based on parts of a user utterance.
-   The first category pattern matches the user utterance, "I am Jane" or "I am Fred."
-   The first category template response captures the name value in the user utterance with \<star/\> and sets the variable username equal to the value of \<star/\>.
-   The second category pattern matches the user utterance, "Good night."
-   The second category template gets the variable username, set in the first category template, and responds using the username inline with response.
``` groovy
<?xml version = "1.0" encoding = "UTF-8"?>
<aiml version = "1.0.1" encoding = "UTF-8"?>
   <category>
      <pattern>I am *</pattern>
      <template>
         Hello <set name = "username"> <star/>! </set>
      </template>  
   </category>  
   <category>
      <pattern>Good Night</pattern>
      <template>
         Hi <get name = "username"/> Thanks for the conversation!
      </template>  
   </category>  
</aiml>
```
In cases where a category that is not already present, either create a new AIML file or add new categories to an existing file. Be careful to preserve the correct XML format when editing files.
Because of the large number of AIML files, use a text editor to do a text based search for patterns and templates within the AIML files before creating more AIML files.
# More Resources about AIML
<http://www.alicebot.org/documentation/aiml-primer.html>
<https://www.tutorialspoint.com/aiml/>
<http://alicebot.blogspot.in/2013/01/aiml-20-draft-specification-released.html>
## Attachments:
![](images/icons/bullet_blue.gif) [amelia-v3-aiml-debug-subsystems-3.4.9.jpg](attachments/11939692/11939693.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-5-14_14-42-12.png](attachments/11939692/11939694.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia-v3-aiml-workspace-3.4.9.jpg](attachments/11939692/11939695.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2018-5-14_12-21-43.png](attachments/11939692/11939696.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-5-14_12-21-24.png](attachments/11939692/11939697.png) (image/png)  
