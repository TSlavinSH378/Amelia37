-   [A Simple BPN](#CarouselImageOptions-ASimpleBPN)
-   [Example Script Task Code](#CarouselImageOptions-ExampleScriptTaskCode)
Images with text can be presented in the custom user interface as single options as part of a conversation with Amelia. One or more options can be selected from a horizontal carousel.
# A Simple BPN
This simple BPN example displays a carousel with image and text options. The code example below can be dropped into a Script task in a simple BPN to demonstrate how they work. Once the BPN is saved and deployed, type `run the workflow BPNName` in the custom user interface chat box, where `BPNName` is the name of the simple BPN.
![](attachments/28476646/28476647.png)
Figure. Simple BPN to Display Multiple Single Option Images with Text
Running the simple BPN with the code below will display multiple single option images with text in the conversation area.
![](attachments/28476646/28476653.png)
Figure. A Simple BPN Displays Multiple Single Option Images with Text
Navigate the carousel of images with text by clicking the ![](attachments/28476646/28476648.png) and ![](attachments/28476646/28476649.png) buttons that appear on the left and right of the conversation text box. Click the ![](attachments/28476646/28476650.png) button in the conversation text box to submit selected options. Each option selected will display white text against a dark background.
When submitted, each selected option will appear within the conversation area.
![](attachments/28476646/28476654.png)
Figure. Output of a Simple BPN to Display Multiple Single Option Images with Text
# Example Script Task Code
A BPN Script task defines multiple single options with this example code. Click the Expand Source link below to toggle display of the example code. Please note the following details about this code example:
-   Images first must be uploaded to the Content Manager workspace by clicking the Process Memory link in Amelia's administration pages then clicking the Content Manager link.
-   This example code dynamically generates and assigns three images as variables – image1URL, image2URL, image3URL – to manually defined options. Production code most likely would manually define specific images for each option.
-   The formInputData variable contains the definitions for each image and text option and the variable is defined as a string in the last line of the code.
-   The formInputData variable must be added to the Ask task properties panel, specifically, scroll down the panel options and set the Form data variable setting to formInputData. This will collect the one or more options selected and make them available, as needed, for use later in the conversation.
**Multiple Image and Text Carousel Code** Expand source
``` groovy
def bucket = cmService.getBucketResources('images')
def image1Url = '';
def image2Url = '';
def image3Url = '';
for(i = 0; i < bucket.size(); i++){
    if(bucket[i].objectName().matches('car1.png')){
        image1Url = cmService.getResourceUrl(bucket[i].objectId())
    } else if (bucket[i].objectName().matches('car2.png')){
        image2Url = cmService.getResourceUrl(bucket[i].objectId())
    } else if (bucket[i].objectName().matches('car3.png')){
        image3Url = cmService.getResourceUrl(bucket[i].objectId())
    }
}
def formInputData = formInputDataBuilder.create()
                .name("carSelectionForm")
                .nameForDisplay("Car Selection Form")
                .formType("sample")
                .instructions("Please choose one of the following")
                .staticSelectionUtterance("")
                .allowedUserInputs("form_only")
                .addField()
                    .name("carSelectionField")
                    .fieldType("multipleSelectionImageDescr")
                    .postfixedSelectionUtterance("I select the vehicle", "I select the vehicles")
                    .addOption()
                        .name("Grey Volvo Sedan")
                        .imageAltText("This can be a description for the option")
                        .imageBase64(image1Url)
                        .value("la2016")
                        .selected(false)
                        .backToField()
                    .addOption()
                        .name("Blue Volvo Sedan")
                        .imageAltText("This can be a description for the option")
                        .imageBase64(image2Url)
                        .value("vb1971")
                        .selected(false)
                        .backToField()
                    .addOption()
                        .name("Red Range Rover SUV")
                        .imageAltText("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed a nulla aliquam, congue velit vitae, molestie neque.")
                        .imageBase64(image3Url)
                        .value("vr1977")
                        .selected(false)
                        .backToField()
                    .addOption()
                        .name("Blue Volvo Sedan")
                        .imageAltText("This can be a description for the option")
                        .imageBase64(image2Url)
                        .value("vb19ffff")
                        .selected(false)
                        .backToField()
                    .addOption()
                        .name("Red Range Rover SUV")
                        .imageAltText("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed a nulla aliquam, congue velit vitae, molestie neque.")
                        .imageBase64(image3Url)
                        .value("vr19dddd")
                        .selected(false)
                        .backToField()
                    .backToForm()
                .build();
execution.setVariable('formInputData', formInputData.toString())
```
## Attachments:
![](images/icons/bullet_blue.gif) [image2020-1-3_10-20-3.png](attachments/28476646/28476647.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-1-3_10-36-4.png](attachments/28476646/28476648.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-1-3_10-36-29.png](attachments/28476646/28476649.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-1-3_10-38-44.png](attachments/28476646/28476650.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-1-3_10-46-24.png](attachments/28476646/28476653.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-1-3_10-47-30.png](attachments/28476646/28476654.png) (image/png)  
