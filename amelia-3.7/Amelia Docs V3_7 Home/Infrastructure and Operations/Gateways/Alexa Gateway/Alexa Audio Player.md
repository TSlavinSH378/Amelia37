The Alexa audio player, in a sense, can be considered a separate component outside the Amelia skill.  When invoked, the original conversation is closed within Amelia and the Alexa Audio player takes over.
# Audio Controls and Features
When the audio player is being used the user is able to control the playback simply by invoking Alexa's name without the skill. Alexa is able to recall which skills are associated with the queued audio and will perform call backs to the gateway as necessary.
## Sample flow

| User | Amelia/Alexa |
| ----|----|
| Hey Alexa, open Amelia | Hello there (New conversation) |
| Play podcast A | (BPN with present task → Conversation closes)*(Alexa audio player begins) |
| Hey Alexa, Pause | (Audio pauses) |
| Hey Alexa, Resume | (Audio resume) |
| Hey Alexa, open Amelia | Hello there (New conversation;→ Audio queue cleared) |

> [!warning]  
> Alexa will also say any prior buffered message in a Say task before the Present task.


| Supported Actions | Unsupported Actions |
| ----|----|
| Pause | Loop on |
| Resume | Loop off |
| Start Over | Shuffle on |
| Next | Shuffle off |
| Previous |  |

# Present URL "Playlist"
Because of separation between Amelia and the AudioPlayer we need to ensure that any relevant audio urls are passed all at once before the audio player begins.  
This is achieved through a present lemma and a html file.   
Based on the described use case, the URLs will be listed in tabular data with two columns (id, url)  
We are currently using the FreeMarker feature of [Presenting Dynamic Content](http://dtools.ipsoft.com/confluence/display/RND/Presenting+Dynamic+Content) in order to format the data in an html file.   
The expected format that the gateway is looking for looks as follows:  
{TrackNumber}, {URL1}, {URL2}, ...  
1, https://example.com/file1.mp3, https://example.com/file2.mp3,
> [!warning]  
>
> Count in the regular fashion (1,2,3) rather than the programmer (0,1,2)

The reason for the playlist is to simply allow the user to move to the next track should they so desire.
> [!warning]  
>
> The term "playlist" is used loosely. **Alexa will only play the first track selected and end the playback once the track is finished**. 

## Script Task
The formatting of the tabular data and variable setting can be done within a script task.
![](attachments/23397231/23397235.png)
Should you want to play only one audio file, this can be done by manually defining the track number and querying the track url from the table.![](attachments/23397231/23397236.png)
## HTML file
![](attachments/23397231/23397238.png)
## BPN
Within the Present task, the following options need to be selected: 
Preview: Inline Only  
Download: No
![](attachments/23397231/23397239.png)
This list will act as a "playlist" for the Alexa Audio Player. This means that if I begin at track 2, I can go back and forth to track 1, or 3.  
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-9-5_13-56-6.png](attachments/23397231/23397235.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-5_13-56-58.png](attachments/23397231/23397236.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-5_13-59-55.png](attachments/23397231/23397237.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-5_14-0-24.png](attachments/23397231/23397238.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-5_14-2-30.png](attachments/23397231/23397239.png) (image/png)  
