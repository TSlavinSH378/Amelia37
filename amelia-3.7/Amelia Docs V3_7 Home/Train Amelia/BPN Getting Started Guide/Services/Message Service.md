The Message Service allows an integration message to be sent directly from a script task, which eliminates the need for a Send the Integration Message task after the Script task that prepares the message payload.
# Methods
## sendIntegrationMessage
`public void sendIntegrationMessage(@NonNull String payload)`
messageService.sendIntegrationMessage(payload.toJsonString())
Creates a payload using *sectionBuilder*, and sends it on an integration message right away.
``` groovy
def buildIntegrationMessage() {
    return sectionBuilder.create()
      .title("Address #1")
      .name("address_1")
      .addSubSection()
        .title("Mailing Address")
        .name("mailingAddress")
        .newSectionField()
          .name("line1")
          .value("40 Wall Street")
          .label("Street")
          .backToSection()
      .backToParentSection()
      .build()  
}
def payload = buildIntegrationMessage()
messageService.sendIntegrationMessage(payload.toJsonString())
```
