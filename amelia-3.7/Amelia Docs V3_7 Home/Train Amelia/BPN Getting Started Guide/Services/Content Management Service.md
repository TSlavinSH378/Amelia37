-   [Methods](#ContentManagementService-Methods)
    -   [addFile](#ContentManagementService-addFile)
    -   [addFileBase64](#ContentManagementService-addFileBase64)
    -   [getResourceUrl](#ContentManagementService-getResourceUrl)
    -   [getResourceUrl](#ContentManagementService-getResourceUrl.1)
    -   [findResourceById](#ContentManagementService-findResourceById)
    -   [getResourceBytes](#ContentManagementService-getResourceBytes)
    -   [getResourceBase64](#ContentManagementService-getResourceBase64)
    -   [getBucketResources](#ContentManagementService-getBucketResources)
-   [cmObjectMetadata Properties](#ContentManagementService-cmObjectMetadataProperties)
-   [Retrieve File Metadata with cmService](#ContentManagementService-RetrieveFileMetadatawithcmService)
    -   [Create a BPN](#ContentManagementService-CreateaBPN)
    -   [A Script to Access Multimedia Services](#ContentManagementService-AScripttoAccessMultimediaServices)
    -   [Interact with Amelia](#ContentManagementService-InteractwithAmelia)
This service includes methods to add, find, encode, and retrieve multimedia assets from the content management system used by BPN tasks and scripts.
# Methods
## addFile
    String addFile(String bucketName, String fileName, byte[] fileBytes)
Adds a resource (file) to BPN's content manager. If a resource with the same name already exists under the specified bucket, it will be overwritten. Returns the *cmObjectMetadataId* of the newly added/updated file.
Table. cmService addFile Parameters/Definitions

| Parameter | Definition |
| ----|----|
| bucketName | Name of the target bucket |
| fileName | File name |
| fileBytes | File bytes |

## addFileBase64
    String addFileBase64(String bucketName, String fileName, String base64EncodedFile)
Adds a resource (file) as Base64-encoded to BPN's content manager. If a resource with the same name already exists under the specified bucket, it will be overwritten. Returns the *cmObjectMetadataId* of the newly added/updated file.
Table. cmService addFileBase64 Parameters/Definitions

| Parameter | Definition |
| ----|----|
| bucketName | Name of the target bucket |
| fileName | File name |
| base64EncodedFile | A file encoded as a base64-encoded string |

## getResourceUrl
    String getResourceUrl(String cmObjectMetadataId)
Obtains the URL to get direct access to the specified resource. The content disposition is determined by the value of *net.ipsoft.ameliav3.model.cm.AbstractCmObjectMetadata#contentDisposition*. Returns a URL pointing to the resource, for example, /Amelia/**view**/K6TKAE3PIAIAA-1/1f0be744-9896-11e7-87d8-685b35c6ba87 or /Amelia/**download**/K6TKAE3PIAIAA-1/1f0be744-9896-11e7-87d8-685b35c6ba87
Table. cmService getResourceUrl Parameters/Definitions

| Parameter | Definition |
| ----|----|
| cmObjectMetadataId | CM object metadata ID |

## getResourceUrl
    String getResourceUrl(String cmObjectMetadataId, String contentDisposition)
Obtains the URL to get direct access to the specified resource. Returns a URL pointing to the resource, for example, /Amelia/**view**/K6TKAE3PIAIAA-1/1f0be744-9896-11e7-87d8-685b35c6ba87 or /Amelia/**download**/K6TKAE3PIAIAA-1/1f0be744-9896-11e7-87d8-685b35c6ba87
Table. cmService getResourceUrl Parameters/Definitions

| Parameter | Definition |
| ----|----|
| cmObjectMetadataId | CM object metadata ID |
| contentDisposition | Defines the content disposition type requested by the controller method |

## findResourceById
    CmObjectMetadata findResourceById(String cmObjectMetadataId)
Finds the multimedia resource by its CM object metadata ID. Returns the resource metadata, or null if the object does not exist.
Table. cmService findResourceById Parameters/Definitions (Process)

| Parameter | Definition |
| ----|----|
| cmObjectMetadataId | CM object metadata ID |

## getResourceBytes
    byte[] getResourceBytes(String cmObjectMetadataId)
Gets the bytes of the specified multimedia resource. Returns a byte array, or null if the resource does not exist.
Table. cmService getResourceBytes Parameters/Definitions (Conversation)

| Parameter | Definition |
| ----|----|
| cmObjectMetadataId | CM object metadata ID |

## getResourceBase64
    String getResourceBase64(String cmObjectMetadataId)
Gets the resource as a base64 encoded string. Returns a base64-string representation of the resource file bytes, or null if the resource does not exist.
Table. cmService getResourceBase64 Parameters/Definitions (Conversation)

| Parameter | Definition |
| ----|----|
| cmObjectMetadataId | CM object metadata ID |

## getBucketResources
    List<CmObjectMetadata> getBucketResources(String bucketName)
Obtains the metadata of all resources associated with a given bucket. Returns a list containing all the resource metadata visible from the current conversation. Also, include the resources found under eventual system buckets with a matching name.
Table. cmService getBucketResources Parameters/Definitions (Conversation)

| Parameter | Definition |
| ----|----|
| bucketName | Name of the bucket whose resources should be obtained |

# cmObjectMetadata Properties
The cmObjectMetadata variable has the same properties as uploaded file metadata in a Request task.
Table. cmObjectMetadata Properties

| Property | Description |
| ----|----|
| bucketId | Bucket ID |
| bucketName | Bucket name |
| objectId | Resource metadata ID |
| objectName | Resource name |
| contentType | Resource content type |
| contentLength | Resource length |
| contentDisposition | Resource content disposition |
| httpContentDisposition | Content disposition mappable to;RFC 2616 ("INLINE" or "ATTACHMENT") |
| contentMd5 | resource MD5 |
| scope | Scope to which an object is associated ("CONVERSATION" or "SYSTEM") |
| url | URL to get direct access to the resource |

# Retrieve File Metadata with cmService
This example uses the cmService in a BPN Script task to retrieve the internal path to an image uploaded with a Request task.
![](attachments/11939523/11939524.png)
Figure. BPN Script Task Uses cmService to Retrieve Internal URL
## Create a BPN
In the Amelia administration pages, use the Process Knowledge tab to create a new BPN model and name it testCmService. Save the new model then build each of the BPN tasks as described below.
Create these Tasks in a BPN, as described and ordered in the table below.
Table 45. BPN Specifications to Upload a Multimedia File with cmService

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let’s get started! | Let the user know the BPN workflow has started and initialize Amelia |
| 2 | request an image identified by test_var and store into images | A Request task also assigned the variable test_var to metadata about the uploaded image file, including the internal file path to the image.Click the flow line from the Request task edge to select the flow that leads to the Script task. Click the Properties Panel at the right edge of the workspace. In the Name field, type success for the Name property and upload:succeeded() for the Expression property.Click the Properties Panel and set the Cancellable property to Yes. |
| 3 | parse test_var with cmService | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 4 | say URL is ${url} and full URL is ${full_url} | Displays the content variables defined in the script below |
| 5 | say cancelled | Create a second path with a single BPNCreate a flow line from the Request task edge to the Say task (Task 4) and a second flow from the new Say task (Task 5) to the End task.Click the flow line from the Request task edge to select the flow that leads to the Say task (Task 4). Click the Properties Panel at the right edge of the workspace. In the Name field, type cancel for the Name property and upload:canceled() for the Expression property. Click the flow line and select the wrench icon and Default flow. |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save button
-   Click the Deploy button
These steps load the BPN model into Amelia’s memory.
## A Script to Access Multimedia Services
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 2 in the table above.
``` groovy
//replace domain-path-to-amelia-instance with base URL
def baseURL = "domain-path-to-amelia-instance";
resources = execution.getVariable('test_var');
cmObjectMetadataId = resources[0].objectId;
url = cmService.getResourceUrl(cmObjectMetadataId);
fullURL = baseURL + url;
execution.setVariable('url', url);
execution.setVariable('full_url', fullURL);
```
## Interact with Amelia
When the BPN models are built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the right edge of the Mind panel..
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the testCmService workflow by typing this command in the chat interface:
    ``` bash
    run the workflow testCmService
    ```
3.  Amelia displays the image file internal file path and full URL – environment URL plus the internal file path – within her conversation.
> [!info]  
>
> While copy/pasting the full URL in a web browser will display the uploaded image, the image will not appear in the Buckets workspace. Amelia V3 has two scopes for multimedia files, system and conversation. System scope includes files uploaded and created in the Buckets workspace. Conversation scope includes files uploaded and managed as part of a conversation controlled by a BPN process. BPNs look for multimedia files first in the conversation scope and, if not found, search the system Buckets.

## Attachments:
![](images/icons/bullet_blue.gif) [image2018-1-5_11-4-7.png](attachments/11939523/11939524.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2018-1-5_11-3-28.png](attachments/11939523/11939525.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-19_13-2-38.png](attachments/11939523/11939526.png) (image/png)  
