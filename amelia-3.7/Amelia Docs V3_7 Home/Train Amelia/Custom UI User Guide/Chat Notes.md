{% version "3.x" %}
In Amelia's custom user interface, chat notes can contain text, images, buttons, maps, and other content. They appear in the chat not panel on the right side of the interface. Chat notes can be used to display data shared in a conversation with Amelia with the ability to edit some or all of the data.
![](attachments/11939936/11939937.jpg)
Figure. Basic Chat Note Example
> [!warning]  
>
> Chat notes also can display banners, as described on the [Banners](Banners) page. Chat notes also can be edited, deleted, opened, and closed as described on the [Edit a Chat Note](Edit%20a%20Chat%20Note) page.

# Create a Chat Note
This demonstration creates a basic chat note to appear in the chat note panel.
![](attachments/11939936/20809259.png)
Figure. doChatNote BPN
## Create the BPN
In the Amelia administration pages, use the Process Memory and Process Knowledge links to create a new BPN model and name it doChatNote. Save the new model then build each of the BPN tasks as described below.
Table. BPN Specifications to Create a Chat Note

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | define chat note | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 3 | say integration message sent | Exit the BPN |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save tab
-   Click the Deploy tab
These steps load the BPN model into Amelia’s memory.
## A Script to Create a Chat Note
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above. The elements used to build the chat note are described in the next section.
Note the use of basic HTML tags in the value field of the Text markupType. In addition, in Amelia version 3.6.0, the Send task has been replaced with a call in the Script task to send the integration message directly to the user interface to display the chat note.
``` bash
def jsonString = '''
    {
        "action": "addChatNotesIntegration",
        "componentType": "ChatNote",
        "payload": [{
            "component": "Banner",
            "title": "My Banner",
            "styles": {
                "height": "100%",
                "color": "#fff",
                "backgroundColor": "#4d5aff"
            },
            "subcomponents": [{
                    "subcomponent": "Markup",
                    "markupType": "Text",
                    "value": "Welcome to SSMC Chat Support",
                    "fontSize": "headline",
                    "fontWeight": "bold"
                },
                {
                    "subcomponent": "Markup",
                    "markupType": "Text",
                    "value": "Chat with Amelia, our Virtual SSMC Desk Representative, to help you:",
                    "fontSize": "title",
                    "fontWeight": "regular"
                },
                {
                    "subcomponent": "Markup",
                    "markupType": "Text",
                    "value": "<br/><br/><b>Create a ticket</b><br/><br/>Update a ticket<br/>Check ticket status<br/><br/>",
                    "fontSize": "subhead",
                    "fontWeight": "normal"
                }
            ]
        }]
    }
    '''
messageService.sendIntegrationMessage(jsonString)
```
## Interact with Amelia
When the BPN model is built and approved, as described in the section above, open Amelia’s custom UI chat interface.
1.  Click the web browser reload button to refresh the chat interface page and clear any earlier interactions.
2.  Ask Amelia to run the doChatNote workflow by typing this command in the chat interface:
    
    |  |
    | ----|
    | run the workflow doChatNote |
    
3.  Amelia displays a chat notes panel on the right side with a chat note. Click the chat note header to toggle display of its contents.
# Chat Note Properties
Chat notes have specific properties, settings, and values to display content on the right side of a custom user interface.
## Common Properties
Table. Common Properties

| Element | Description |
| ----|----|
| action | addChatNotesIntegration;– Creates a new chat note if no other chat note with the same title exists. If another chat note with the same title exists, content will be replaced with the latest data provided.deleteChatNoteIntegration – Deletes a chat note based on the title. If no chat note exists with the same title, the action does not execute. |
| componentType | ChatNote is only possible value |
| header | Title header for the entire chat note. To preserve the header throughout a process workflow, the header should be passed along whenever a new integration message is passed to Amelia's interface.If no header is provided, the previous header will persist if it was defined before. To remove a header, pass an empty string for header property, "header" : "", |
| payload | Contains chat note components and subcomponents. Each element of the array represents a single chat note. |
| component | ChatNote, Banner, or Divider |
| title | Unique because titles identify chat notes when adding and deleting chat notes |
| styles | Style labels, text, and description elements. Applies to all labels and text in a chat note.; Properties can be defined with nested JSON, for example, as a string of key:value pairs separated by commas, "styles":{ "labelSize":"subhead", "labelWeight":"regular", "bodySize":"caption" }labelSize – Options are micro (<h8>), caption (<h7>), body (<h6>), subhead (<h5>), header (<h4>), title (<h3>), headline (<h2>), and display (<h1>)
labelWeight – Options are regular and bold
bodySize – Options are small, caption, and body |
| forceOpenState | Closed or Open. Closed collapses the chat note. Open expands the chat note. Can draw user attention to an open chat note. |
| actionProcess | For chat notes, defines what data to pass to a specific BPN when editing with the Edit button. Has additional settings and values. If actionProcess is not present in the code, the Edit button will not appear.actionName – The name of the BPN to call when the Edit link is clickedactionArguments – Additional data to pass to the BPN when the Edit link is clicked. Values are passed as keys and values in a single object.
actionMessage – Custom message output as the user's utterance in the conversation area, for example, "I want to edit my address." If value is empty, the default utterance is, "I have invoked an action."Only be triggered on click of the edit button. Only one edit button per chat note. If no actionProcess info is provided in the integration message, the edit button will be hidden. In order for the action (BPN) to be triggered with the UI, the parent BPN should stay open. Having ask lemma at the end of the parent BPN is one way to keep the BPN open. Parent BPN is the BPN from which the integration message with actionProcess data is passed. |
| subcomponent | Current value is Markup |
| markupType | Options are Text, ImageLarge, ImageSmall, Video, Table, Default. The HTML string is only allowed in the Text subcomponent. |
| label | Text for heading for a subcomponent of a chat note. Appears as a title for each subcomponent. |

## Subcomponent markupType Properties
### Text
Table. Text Properties

| Property | Description |
| ----|----|
| value | Used for Text subcomponents only. Inline HTML is allowed only in Text subcomponents. Tags allowed: , , , , , , , , , , 
, 
, 
, 
Use of non-allowed tags will generate the message, "Illegal HTML found. Please check your JSON." |

``` groovy
{
    "subcomponent": "Markup",
    "markupType": "Text",
    "label": "Text Label",
    "value": "<b>Lorem Ipsum</b> is simply dummy text of the <i>printing and typesetting</i> industry. Lorem Ipsum has been the industry\'s standard dummy text ever since the 1500s,   <u>when an unknown printer took a galley of type and scrambled it to make a type specimen book</u>."
}
```
### ImageLarge
Table. ImageLarge Properties

| Property | Description |
| ----|----|
| imageBase64 | Image data passed with an image URL or base64 data |
| description | Text snippet |

``` groovy
{
    "subcomponent": "Markup",
    "markupType": "ImageLarge",
    "label": "Large Image",
    "imageBase64": "data:image/gif;base64...",
    "description": "Description for Large Image"
}
```
### ImageSmall
Table. ImageSmall Properties

| Property | Description |
| ----|----|
| imageBase64 | Image data passed with an image URL or base64 data |
| description | Text snippet. Description is aligned left with image aligned right. If no description, image is aligned left. |

``` groovy
{
    "subcomponent": "Markup",
    "markupType": "ImageSmall",
    "imageBase64": "http://vignette3.wikia.nocookie.net/hotwheels/images/a/ab/Vw-brasilia-1977.jpg/revision/latest?cb=20160812013532",
    "label": "Small Image",
    "description": "It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal distribution of letters, as opposed to using \'Content here, content here\', making it look like readable English."
}
```
### Video
Table. Video Properties

| Property | Description |
| ----|----|
| url | Video data passed with a video URL |
| description | Text snippet |

``` groovy
{
    "subcomponent": "Markup",
    "markupType": "Video",
    "label": "Video",
    "description": "This is some crazy video about something really, really crazy",
    "url": "https://ia600202.us.archive.org/34/items/bookupload/bookupload.m4v"
}
```
### Table
Table. Basic Table Properties

| Property | Description |
| ----|----|
| headers | Single array with comma-delimited values for each table column heading |
| rows | Single array with one array for each row. The row array has comma-delimited values for each table column. |

A basic table uses header, row, and cell structures with no custom formatting.
``` groovy
{
    "subcomponent": "Markup",
    "markupType": "Table",
    "label": "Table",
    "headers": ["Header 1", "Header 2", "Header 3", "Header 4", "Header 5"],
    "rows": [
        ["cell 1", "cell 2", "cell 3", "cell 4", "cell 5"],
        ["cell 1", "cell 2", "cell 3", "cell 4", "cell 5"],
        ["cell 1", "cell 2", "cell 3", "cell 4", "cell 5"],
        ["cell 1", "cell 2", "cell 3", "cell 4", "cell 5"],
        ["cell 1", "cell 2", "cell 3", "cell 4", "cell 5"]
    ]
}
```
A table with custom formatting uses additional properties. The row definition also changes the row structure, as shown below in the code example.
Table. Custom Table Properties

| Property | Description |
| ----|----|
| headerAlign | Aligns header cell text. Options are left, right, or center. Default is center. |
| headerSize | Size of the header. Options are display (), headline (), title (), header (), body (), caption (), micro (), and subhead ().;Default is subhead (). |
| headerBackgroundColor | Background color of header cells, either HEX (e.g. "#00000") or rgba (e.g. "rgba(0,0,0)").;Default is primary color defined in config.json file. |
| headerTextColor | Font color of header text, either;HEX (e.g. "#00000") or rgba (e.g. "rgba(0,0,0)"). Default is primaryTextColor defined in config.json file. |
| bodyAlign | Aligns non header cell contents. Options are left, right, center.;Default is center. |
| verticalHeader | Position of the header, on left column edge or across top row of the table. Set to true, the header will be on the left column edge of the table. Set to false, or not provided, the header will be positioned across the top row of the table. |
| columns | Array of column width percentage for each table column. Controls width of each column.;Default behavior is self-adjusting based on the longest string within a column. |
| highlight | For each row,;background color of a cell, either be HEX (e.g. "#00000") or rgba (e.g. "rgba(0,0,0)"). Default is no background. |
| value | For each row, content for a cell. HTML tags allowed;<b>, </b>, <strong>, </strong>, <i>, </i>, <u>, </u>, <a>, </a>, </br>, </ br>, <br />, <br/> |
| actionProcess | Same functionality as actionProcess used to define a payload.For chat notes, defines what data to pass to a specific BPN when editing with the Edit button. Has additional settings and values. If actionProcess is not present in the code, the Edit button will not appear.actionName – The name of the BPN to call when the Edit link is clickedactionArguments – Additional data to pass to the BPN when the Edit link is clicked. Values are passed as keys and values in a single object.
actionMessage – Custom message output as the user's utterance in the conversation area, for example, "I want to edit my address." If value is empty, the default utterance is, "I have invoked an action."Only be triggered on click of the edit button. Only one edit button per chat note. If no actionProcess info is provided in the integration message, the edit button will be hidden. In order for the action (BPN) to be triggered with the UI, the parent BPN should stay open. Having ask lemma at the end of the parent BPN is one way to keep the BPN open. Parent BPN is the BPN from which the integration message with actionProcess data is passed. |

``` groovy
{
    "subcomponent": "Markup",
        "markupType": "Table",
        "label": "Table",
        "headerAlign": "center",
        "headerSize": "header",
        "headerBackgroundColor": "#05385e",
        "headerTextColor": "#ffffff",
        "verticalHeader": false,
        "bodyAlign": "left",
        "columns":
        [
            "40%", "20%", "13.3%", "13.3%", "13.3%"
        ],
        "headers":
        [
            "Header 1", "Header 2", "Header 3", "Header 4", "Header 5"
        ],
        "rows":
        [
            [
                {
                    "value": "<b>cell 1</b>",
                    "highlight": "#c9e1a7",
                    "actionProcess":
                    {
                        "actionName": "video-from-database",
                        "actionArguments": {},
                        "actionMessage": "I clicked the cell"
                    }
                },
                {
                    "value": "<i>cell 2</i>"
                },
                {
                    "value": "cell 3"
                },
                {
                    "value": "cell 4"
                },
                {
                    "value": "cell 5"
                }
            ],
            [
                {
                    "value": "cell 1"
                },
                {
                    "value": "cell 2"
                },
                {
                    "value": "cell 3"
                },
                {
                    "value": "cell 4"
                },
                {
                    "value": "cell 5"
                }
            ],
            [
                {
                    "value": "cell 1"
                },
                {
                    "value": "<del>cell 2</del>"
                },
                {
                    "value": "cell 3"
                },
                {
                    "value": "cell 4"
                },
                {
                    "value": "cell 5"
                }
            ],
            [
                {
                    "value": "<a href=\'https://www.google.com\' style=\'color: green\' target=\'_blank\'>cell 1</a>"
                },
                {
                    "value": "cell 2"
                },
                {
                    "value": "cell 3"
                },
                {
                    "value": "cell 4"
                },
                {
                    "value": "<s>cell 5</s>"
                }
            ],
            [
                {
                    "value": "cell 1"
                },
                {
                    "value": "cell 2"
                },
                {
                    "value": "cell 3"
                },
                {
                    "value": "<a href=\'https://www.google.com\' target=\'_blank\'>cell 4</a>"
                },
                {
                    "value": "<s>cell 5</s>"
                }
            ]
        ]
}
```
### Map
This subcomponent is a variation of the ImageLarge subcomponent. The map is output as an image wrapped in an HTML anchor tag link. The subcomponent requires use of a map service, for example, Google Maps or Mapquest.
Table. Map Properties

| Property | Description |
| ----|----|
| streetAddress | Street Address or neighborhood name |
| addressCoordinates | If known, the map coordinates for the location. Can be empty. |
| linkUrl | The search URL used for the map service |

``` groovy
{
    "subcomponent": "Markup",
    "markupType": "ImageLarge",
    "label": "Map",
    "streetAddress": "...",
    "addressCoordinates": [...],
    "linkUrl": "https://www.google.com/maps/search/' + URLEncoder.encode(address, 'UTF-8' ) + '/",
    "imageBase64": "..."
}
```
The map subcomponent can be implemented with a BPN Script task using Groovy.
``` groovy
import groovy.json.JsonOutput
import groovy.json.JsonSlurper
def API_KEY = "AIzaSyA9Hpi--2r7oh4W28iPxccZEvHdabC7HPs"
def address = "Park Slope" // here you can use the response variable execution.getVariable("response")
def geoUrl = "https://maps.googleapis.com/maps/api/geocode/json?key=AIzaSyD9g0G3aSn25ljMuvk58Oyg5EzAsiww5ic&address="
def lat = null
def lng = null
def coords = null
def geoConnection = new URL(geoUrl + URLEncoder.encode(address, 'UTF-8' )).openConnection() as HttpURLConnection
// set some headers
geoConnection.setRequestProperty( 'User-Agent', 'groovy-2.4.4' )
geoConnection.setRequestProperty( 'Accept', 'application/json' )
if ( geoConnection.responseCode == 200 ) {
    // get the JSON response
    def json = geoConnection.inputStream.withCloseable { inStream ->
        new JsonSlurper().parse( inStream as InputStream )
    }
    lat = json.results.geometry.location.lat[0]
    lng = json.results.geometry.location.lng[0]
} else {
    println geoConnection.responseCode + ": " + geoConnection.inputStream.text
}
coords = lat + "," + lng
def staticUrl = "https://maps.googleapis.com/maps/api/staticmap?center=" + coords + "&size=400x400&key=AIzaSyBQpMt87SqVJ3c-0bSIaRDnJYEkn6nC7ck&markers=color:blue|label:S|" + coords
def jsonString = '{'+
    '"action":"addChatNotesIntegration",'+
    '"componentType": "ChatNote",'+
    '"payload": [{'+
      '"component": "ChatNote",'+
      '"title": "Map Chat Note",'+
      '"actionProcess": "do_something_to_note",'+
      '"subcomponents": [{'+
        '"subcomponent": "Markup",'+
        '"markupType": "ImageLarge",'+
        '"label": "Map",'+
        '"streetAddress": "' + address + '",'+
        '"addressCoordinates": [ ' + coords + ' ],'+
        '"linkUrl": "https://www.google.com/maps/search/' + URLEncoder.encode(address, 'UTF-8' ) + '/",'+
        '"imageBase64": "' + staticUrl + '"'+
      '}]'+
  '}]}'
jsonString = JsonOutput.toJson(jsonString)
execution.setVariable("jsonString", jsonString)
```
### Default
The default subcomponent is a text block. This subcomponent displays blocks of text in a compressed ergonomic way with lines of text.
Table. Default Properties

| Property | Description |
| ----|----|
| line | Text line with no decoration |
| lineActive | Text line with green check mark at line end |
| lineDisabled | Greyed out text line |
| lineBreak | Return or next line. Creates space between lines. |

``` groovy
{
    "subcomponent": "Markup",
    "markupType": "TextBlock",
    "label": "Coverages",
    "lines": [{
            "lineActive": "Bodily Injury & Property Damage"
        },
        {
            "lineActive": "Uninsured / Underinsured"
        },
        {
            "lineActive": "Comprehensive"
        },
        {
            "lineBreak": " "
        },
        {
            "lineDisabled": "Collision"
        },
        {
            "lineDisabled": "Glass Damage"
        },
        {
            "line": "100,000 per person"
        },
        {
            "line": "$300,000 per accident"
        }
    ]
}
```
## Divider Component Properties
Dividers can separate components in a payload, for example, to organize chat notes into visually different groups.
Table. Divider Properties

| Property | Description |
| ----|----|
| title | Displays text with the divider. Left blank, no title displays. |

``` groovy
import groovy.json.JsonOutput
import groovy.json.JsonSlurper
def jsonString = '''{
    "action":"addChatNotesIntegration",
    "componentType": "ChatNote",
    "header": "Chat Notes with Dividers",
    "payload": [
    {
      "component": "ChatNote",
        "title": "Chat Note 1",
        "subcomponents": [
        {
            "subcomponent": "Markup",
            "markupType": "Text",
            "label": "Some label",
            "value": "Lorem Ipsum"
        },
        {
            "subcomponent": "Markup",
            "markupType": "Text",
            "value": "Partner Information"
        },
        {
            "subcomponent": "Markup",
            "markupType": "Default",
            "label": "Default Field",
            "value": "Value for display"
        }]
    },
    {
        "component": "Divider",
        "title": "Divider Uno"
    },
    {
        "component": "ChatNote",
        "title": "Chat Note 2",
        "subcomponents": [
        {
            "subcomponent": "Markup",
            "markupType": "Text",
            "label": "Some label",
            "value": "Value"
        }]
    },
    {
        "component": "ChatNote",
        "title": "Chat Note 3",
        "subcomponents": [{
            "subcomponent": "Markup",
            "markupType": "Text",
            "label": "Some label",
            "value": "Value"
        }]
    },
        {
        "component": "Divider",
        "title": "Divider Dos"
    },
    {
        "component": "ChatNote",
        "title": "Chat Note 4",
        "subcomponents": [{
            "subcomponent": "Markup",
            "markupType": "Text",
            "label": "Some label",
            "value": "Value"
        }]
    },
    {
        "component": "Divider",
        "title": "Divider Tres"
    },
    {
        "component": "ChatNote",
        "title": "Chat Note 5",
        "subcomponents": [
        {
            "subcomponent": "Markup",
            "markupType": "Text",
            "label": "Some label",
            "value": "Value"
        }]
    },
    {
        "component": "ChatNote",
        "title": "Chat Note 6",
        "subcomponents": [{
            "subcomponent": "Markup",
            "markupType": "Text",
            "label": "Some label",
            "value": "Value"
        }]
    },
        {
        "component": "Divider",
        "title": "Divider Cuatro"
    },
    {
        "component": "ChatNote",
        "title": "Chat Note 7",
        "subcomponents": [{
            "subcomponent": "Markup",
            "markupType": "Text",
            "label": "Some label",
            "value": "Value"
        }]
    }
]}'''
jsonString = JsonOutput.toJson(jsonString)
execution.setVariable("jsonString", jsonString)
```
{% /version %}
