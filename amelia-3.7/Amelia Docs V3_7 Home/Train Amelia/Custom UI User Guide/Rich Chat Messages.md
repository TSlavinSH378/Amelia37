-   [Video](#RichChatMessages-Video)
-   [Image](#RichChatMessages-Image)
-   [Link](#RichChatMessages-Link)
-   [Document](#RichChatMessages-Document)
-   [Table Data](#RichChatMessages-TableData)
Multimedia content – video, images, documents, links, and data in table format – can be displayed in Amelia's conversation in the custom user interface. Data is sent with an integration message from a BPN Script task to the interface.
Messages can be presented in different sizes based on media type.
Table. Media Type and Message Sizes

| Size | Media Type |
| ----|----|
| Small | Links without preview, documents |
| Medium | Images |
| Large | Links with thumbnails, documents with thumbnails, video |

The code examples below can be dropped into a Script task in a simple BPN to demonstrate how they work. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/20809332/20809336.png)
Figure. Simple BPN to Display Video in Conversation Area
# Video
> [!warning]  
>
> To display video will require the CSP headers to be updated with the UI Bundles workspace in the System Settings section of Amelia's administration pages. Below is an example CSP header that allows display of videos from Vimeo and YouTube.
>
> ``` groovy
> default-src 'self' maps.googleapis.com data: blob: fonts.googleapis.com *.youtube.com *.vimeo.com *.archive.org fonts.gstatic.com ws: media.giphy.com 'unsafe-eval' 'unsafe-inline'; frame-ancestors https://alexandra-co.squarespace.com;
> ```
>
>   

A BPN Script task will display a video with this example code. Properties are described below the code.
``` groovy
def jsonString = '''
    {
        "action":"addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "Media",
            "subComponent": "VideoEmbed",
            "src": "https://player.vimeo.com/video/1846726",
            "title": "Amelia, Ipsoft\'s Virtual Assistant",
            "descr": "ipsoft.com"
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
Table. Video Properties

| Property | Description |
| ----|----|
| subComponent | Video or VideoEmbed. Video is for files stored in Amelia's Content Manager. VideoEmbed is used for YouTube and Vimeo videos.; |
| src | Location of the video file, either the path in Content Manager or a URL. |
| title | Optional. Title to display underneath the video. |
| descr | Optional. Description to display underneath the video. |

# Image
A BPN Script task will display an image with this example code. The `subComponent` value is `Image`. Properties are described below the code.
``` groovy
def jsonString = '''
    {
        "action":"addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "Media",
            "subComponent": "Image",
            "src": "https://static.pexels.com/photos/37403/bora-bora-french-polynesia-sunset-ocean.jpg"
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
Table. Image Properties

| Property | Description |
| ----|----|
| src | Location of the image file, either the path in Content Manager or a URL. |

# Link
A BPN Script task will display a link with this example code. The `subComponent` value is `Link`. Properties are described below the code.
``` groovy
def jsonString = '''
    {
        "action":"addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "Media",
            "subComponent": "Link",
            "linkUrl": "https://www.ipsoft.com/amelia/",
            "title": "Amelia, Ipsoft\'s Virtual Assistant",
            "descr": "ipsoft.amelia.com",
            "thumb": "https://static.pexels.com/photos/37403/bora-bora-french-polynesia-sunset-ocean.jpg"
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
Table. Link Properties

| Property | Description |
| ----|----|
| linkUrl | The destination URL |
| title | Optional.;Title to display underneath the link. |
| descr | Optional. Description to display underneath the link. |
| thumb | Optional. Thumbnail image to display underneath the link. |

# Document
A BPN Script task will display a document with this example code. The `subComponent` value is `Document`. Properties are described below the code.
``` groovy
def jsonString = '''
    {
        "action":"addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "Media",
            "subComponent": "Document",
            "href": "http://www.pdf995.com/samples/pdf.pdf",
            "title": "Amelia, Ipsoft\'s Virtual Assistant",
            "descr": "ipsoft.amelia.com",
            "thumb": "https://static.pexels.com/photos/37403/bora-bora-french-polynesia-sunset-ocean.jpg",
            "download": true
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
Table. Document Properties

| Property | Description |
| ----|----|
| href | Link to the document |
| title | Optional.;Title to display underneath the document. |
| descr | Optional. Description to display underneath the;document. |
| thumb | Optional. Thumbnail image to display underneath the document. |
| download | Optional. True allows the document to be downloaded. |

# Table Data
A BPN Script task will display data in a table format with this example code. The `subComponent` value is `TableData`. Properties are described below the code.
``` groovy
def jsonString = '''
    {
        "action": "addChatMessage",
        "payload": {
            "componentType": "MessageIntegration",
            "subComponentType": "TableData",
            "title": "Account Balance",
            "descr": "Access all awards in this handy table with links.",
            "rows": [
                [
                    "Above & Beyond",
                    "Recognizes co-workers for demonstrating clinic values"
                ],
                [
                    "Anniversary List",
                    "Years of service at 5-year increments<br/><a href='Monthly'>https://www.wikipedia.org/'>Monthly List</a>"
                ],
                [
                    "Argent Society",
                    "Recognition of allied health status service<br/><a href='#'>Argent Society - RST</a><br/><a href='#'>Argent Society - ARZ, FLA</a>"
                ],
                [
                    "Associate Appointment",
                    "Recognizes individuals , not consulting or adminstrative staff who contribute on a continuing basis in unusually important ways to the practice, research and educational activities<br/><a href='#'>Info/Nominate</a>"
                ],
                [
                    "E-cards",
                    "Recognizes co-workers with an electronic greeting card<br/><a href='#'>E-cards</a>"
                ],
                [
                    "Excellence Awards",
                    "Mayo clinic fosters recognition of its staff through the Awards for Excellence program. Award recipients are dedicated individuals who exemplify the values of excellence for which Mayo is known<br/><a href='#'>Info/Nominate</a><br/><a href='#'>Recipients 2017</a><br/><a href='#'>Recipients 2016</a>"
                ],
                [
                    "Manager Recognition Tools",
                    "Manager guide to employee recognition<br/><a href='#'>Giving Employee Recognition</a>"
                ],
                [
                    "Recognition Events",
                    "Special events held throughout the year to show appreciation to Mayo employees, volunteers, students and retirees<br/><a href='#'>Event Info</a>"
                ],
                [
                    "Recognition / Hospitality Funds",
                    "Institutional funds for each department to be used for expenses associated with recognition of individual or team performance, group hospitality and social activities<br/><a href='#'>Funds Info</a>"
                ],
                [
                    "Retirements",
                    "Recognizes retiring employees meeting Mayo Clinic’s criteria of age and continuous years of service in a benefit eligible position<br/><a href='#'>Reception Planning List</a><br/><a href='#'>Monthly YTD List</a>"
                ],
                [
                    "Years of Service Recognition - Allied Health Staff",
                    "Recognizes employees for years of service at 5 year intervals, beginning with completion of 5 years of service.<br/><a href='#'>Info</a><br/><a href='#'>Award Redemption</a>"
                ]
            ]
        }
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
Table. Table Data Properties

| Property | Description |
| ----|----|
| title | Title to display underneath the table |
| descr | Description to display underneath the;table |
| rows | An array with each row of data a nested comma-delimited array. HTML tags allowed: , , , , , , , , , , 
, 
, 
, 
 |

## Attachments:
![](images/icons/bullet_blue.gif) [image2019-7-17_16-19-28.png](attachments/20809332/20809336.png) (image/png)  
