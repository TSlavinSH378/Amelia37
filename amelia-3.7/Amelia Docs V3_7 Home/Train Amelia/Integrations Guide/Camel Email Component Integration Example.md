{% version "3.x" %}
The Amelia Camel Mail Component is a drop-in replacement for the standard [Camel Mail component](http://camel.apache.org/mail.html), providing conveniences for sending mail from Amelia via Camel in a standardized manner in an effort to significantly reduce boilerplate code both within Amelia as well as within Camel.
Using this component for sending mail through Camel is straightforward. The general steps for doing so are as follows, and are described in detail farther below:
1.  Add this component as an asset in the Amelia Integration Framework.
2.  Create a Camel flow, attaching the asset from the previous step.
3.  From a BPN:
    1.  Describe a mail request by constructing a `mailRequest` object.
    2.  Make the mail request by running the integration flow from above.
    3.  Examine the response described by the resulting `mailResponse` object.
This component may be used exactly like the standard Camel Mail component, but the primary benefit is that your Camel Spring DSL (XML) file can be much simpler because this component takes care of mapping your `mailRequest` object onto the various Camel message headers used by the Mail component. It also takes care of bundling up the response into a `mailResponse` object to be sent back to Amelia.
# Adding the Email Component as an Asset
As mentioned above, the first step to using this component from your Camel flows is to add this component as an asset to the Amelia Integration Framework. If the desired version of this component is not already an asset in your desired Amelia instance, you need to add it.
You can find all published versions of this component in our external Artifactory binary repository. To download a particular version, do the following:
1.  Open a browser to <https://artifactory.ipsoft.com/artifactory/libs-release-local/net/ipsoft/ameliav3x/camel/ameliav3x-camel-mail/1.1.1/ameliav3x-camel-mail-1.1.1-all.jar> and login.
> [!warning]  
>
> Although the JAR file has an `all` classifier, the only classes it contains from outside of this project are the classes from the `ameliav3x-camel-core` module, which are shadowed, so you don't have to explicitly add the `ameliav3x-camel-core` module as an asset, unless you plan to directly use classes from that module.

Once you have downloaded the component, go to the Integration Framework in the Amelia Admin UI of the instance in which you want to add it as an asset. Start creating a new asset, and when you reach the **New Assets** dialog box, fill in the fields as follows:
-   **Attach Files**: In the area at the bottom of the dialog window, drag and drop the JAR file you downloaded above, or click to navigate to it and select it. Once attached, the filename should appear near the bottom of the dialog window (e.g., `ameliav3x-camel-mail-1.0-all.jar`).
-   **Name:** Copy the name of the file from the bottom of the dialog window and paste it into the **Name** field. While this is not required, it is a **very strongly** recommended convention for convenient asset management.
-   **Domain:** Choose the `global` domain, if you have permissions to do so. Since this component is not domain-specific, it is recommended that you add it as an asset in the `global` domain so that it is available to flows in all domains.
> [!warning]  
>
> Adding a version of this component as an asset is a one-time step. The only time you would need to perform this step again is when you want to upload a newer version of this component. By naming the asset the same as the JAR file name, you may have multiple versions of this component as assets, allowing existing flows to continue using an earlier version, while new flows use a newer version. The existing flows may then be upgraded as and when desired.

# Creating a Camel Flow using this Component
Using this component in a Camel flow involves the following steps:
1.  Create a Camel flow in Amelia
2.  Fill in the required fields as desired (Name, Domain, etc.)
3.  Attach the asset you added in the previous section (this component)
4.  Add a **property** named `smtp.host` (case-sensitive) and set its value to the hostname of the mail server, including the port, if not using the default port for the protocol (e.g., `mymailhost:465`).
5.  Switch to **Source View** and use the following source as a starting point (where we're using the `smtp` protocol):
    ``` groovy
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://camel.apache.org/schema/spring
           http://camel.apache.org/schema/spring/camel-spring.xsd">
      <!--
        Set this bean's ID to any desired protocol supported by the mail
        component, making sure it matches the protocol in the URI used
        farther below.
      -->
      <bean id="smtp" class="net.ipsoft.ameliav3x.camel.component.mail.AmeliaMailComponent"/>
      <camelContext xmlns="http://camel.apache.org/schema/spring">
        <route id="sendMail">
          <from uri="direct:start"/>
          <!-- finally -->
          <onCompletion>
            <bean ref="varpop" method="moveToOutboundVariables('mailResponse')"/>
          </onCompletion>
          <!-- catch -->
          <onException>
            <exception>java.lang.Exception</exception>
            <redeliveryPolicy maximumRedeliveries="1"/>
            <handled>
              <constant>true</constant>
            </handled>
            <setProperty propertyName="mailResponse">
              <groovy>
                [success: false, errorMessage: exchange.properties.CamelExceptionCaught.message]
              </groovy>
            </setProperty>
          </onException>
          <!-- try -->
          <!--
            The ID of the bean declared above must match the protocol in the
            following URI. Also, the prefix of the property (smtp.host) must
            match the protocol as well (e.g., if using smtps instead of smtp,
            specify the property smtps.host instead of smtp.host, and set a
            Camel flow property by the same name).
            If you do not define the smtp.host property on the Camel flow, it
            defaults to the value following the colon (127.0.0.1 in this case).
          -->
          <toD uri="smtp:{{smtp.host:127.0.0.1}}"/>
        </route>
      </camelContext>
    </beans>
    ```
    ```
    ```
6.  Save the flow
7.  Deploy the flow
This starting point does not include any advanced configuration, including setting a username and password, but such configuration can be added in the same way you would add these things with the standard [Camel Mail component](http://camel.apache.org/mail.html). Alternatively, this extension of the Mail component supports configuration via Camel flow properties (see below). In addition, see the **Example** section below.
# Sending Mail using this Component
## General Steps
Once this component is added as an asset to the Amelia Integration Framework, and you have created a Camel flow with the asset attached, as described in the previous sections, sending mail from a BPN is straightforward:
1.  Create a script task to construct a `mailRequest` map to send to Camel
2.  Run the integration flow
3.  Create a script task to examine the `mailResponse` map returned from Camel
The `mailRequest` object must be a `Map` and may contain any of the options available for the [Camel Mail component](http://camel.apache.org/mail.html), as well as a `body` and a list of zero or more `attachments` (see below).
The `mailResponse` object is a `Map` and may contain the following entries:
-   `success`: a Boolean value indicating whether or not the mail was sent (i.e., no exception was thrown when attempting to send the mail)
-   `errorMessage`: if not successful (i.e., an exception was thrown), the error message from the exception
## Example: Sending an HTML Mail Message
To illustrate the general steps described in the previous section, this section steps you through the process of sending a simple HTML mail message.
### Add this Component as an Asset
Add this component as an asset to the Amelia Integration Framework as described earlier, if the asset does not already exist.
### Create a Camel Flow using this Component to Send Mail
To create a Camel flow that uses the asset you added in the previous section, do the following:
1.  In Amelia's Integration Framework, create a new flow and fill in the required fields as follows:
    -   **Name:** SendMail
    -   **Code:** sendmail
    -   **Domain:** (choose the desired domain)
    -   **Assets:** (choose the asset you uploaded in the previous section)
    -   **Description:** Send Mail
2.  Choose the flow's **Source View**, delete the contents, then copy and paste the XML document shown in the previous section.
3.  Save the flow.
4.  Deploy the flow.
### Create a BPN to Send Mail
In the same domain in which you deployed the flow in the previous section, create a new BPN named `SendMail` with the following elements connected in the following order:
1.  **Start Event**
2.  **Script Task** labeled `prepare mail request`, containing the following script:
    ``` groovy
    def user = userService.user
    execution.setVariable 'mailRequest', [
        subject    : 'Greetings!',
        from       : "${user.firstName()} ${user.lastName()} <${user.email()}>",
        to         : user.email(),
        contentType: 'text/html',
        body       : "<h1>Hello ${user.firstName()}!</h1>",
    ]
    ```
    ```
    ```
3.  **User Task** labeled `run the integration flow sendmail`
4.  **Script Task** labeled `check result`, containing the following script:
    ``` groovy
    def mailResponse = execution.getVariable 'mailResponse'
    def success = mailResponse?.success ?: false
    def error = mailResponse?.errorMessage ?: 'Unknown error sending mail'
    execution.setVariable 'result', success ? 'Check your inbox' : error
    ```
    ```
    ```
5.  **User Task** labeled `say ${result}`
6.  **End Event**
Now save, deploy, and run the BPN to have Amelia send mail to you. If there is no SMTP server running on the server where Camel is running, then Amelia should say the following error message:
``` groovy
Couldn't connect to host, port: 127.0.0.1, 25; timeout 30000.
```
That's a partially successful test because it means the BPN ran the integration flow and received a response back. It was simply unable to send the mail since there was no SMTP server running there.
> [!warning]  
>
> Although we set the `from` value directly in the BPN example above, this may be configured as a Camel flow property instead, in which case, the `from` would be left out of the `mailRequest`payload above. To set the `from` value as a property, the property name would be prefixed with the ID of the bean plus a period, which would yield a property name of `smtp.from` in this case.

## Mail Component Configuration via Properties
In addition to being able to set options on the Mail component via entries in the `mailRequest` map (again, see [Camel Mail component](http://camel.apache.org/mail.html) for all available options), options may also be set via properties on the Camel flow. To identify which properties should be used to configure the component, the property names must be prefixed with the protocol plus a period (`.`). For example, when using the `smpts` protocol, properties intended to configure options must start with `smtps.` (e.g., `smtps.from`). Using this convention allows you to avoid explicitly specifying the corresponding options on the URI. They will be set implicitly.
The only exceptions to this convention are `username` and `password`. Even when setting properties named `smtps.username` and `smtps.password`, the mail component will not allow them to be set implicitly. These two options must be set *explicitly* on the URI, like so:
``` groovy
<toD uri="smtps:{{smtps.host:localhost}}?username={{smtps.username}}&amp;password={{smtps.password}}"/>
```
You would then set the `smtps.username` and `smtps.password` properties on the Camel flow, as appropriate for the SMTP server, and the password property should be encrypted.
> [!warning]  
>
> Options specified as flow properties take precedence over options sent via the `mailRequest` object. For example, when using `smtps`, the property named `smtps.from` would override a `from` value sent via the `mailRequest`. This allows environment-specific values set as flow properties to override environment-independent values sent via the `mailRequest`, should it be necessary.

## Using a Mail Template
As an alternative to sending the mail body via the `body` entry in the `mailRequest` execution variable, you may instead associate the key `bodyResource` with the location on the classpath of a [Velocity](http://velocity.apache.org/)template to evaluate in order to produce the mail body. In addition, you may provide a Velocity context via a `Map` value associated with the key `bodyContext`.
You may add the Velocity template to the classpath either by adding it directly as an asset or packaging into a JAR file (possibly with other templates as well) that you add as an asset.
For example, assume you have a Velocity template named `greeting.html.vm` with the following contents:
``` groovy
<html>
<body>
Hello, <em>${firstName}</em>!
</body>
</html>
```
In order to use this template to generate mail, you must do the following:
1.  Add the following dependencies as assets to your Camel flow:
    -   The mail template file
    -   `camel-velocity-2.20.2.jar`
    -   `velocity-engine-core-2.0.jar`
2.  Reference the mail template from the `mailRequest` (see below)
3.  Supply Velocity context values via the `mailRequest` (see below)
To reference the mail template via the `mailRequest` object, you might have something like the following in a BPN script, where `bodyResource` references the classpath location of the mail template:
``` groovy
execution.setVariable 'mailRequest', [
    from        : ...,
    to          : ...,
    subject     : ...,
    contentType : 'text/html',
    bodyResource: 'greeting.html.vm',
    bodyContext : [
        firstName: userService.user.firstName(),
    ],
]
```
In addition, your `camel-context.xml` file would need to set headers and reference the [Velocity component](http://camel.apache.org/velocity.html) prior to the Mail (SMTP) component, like so:
``` groovy
<setHeader headerName="CamelVelocityTemplate">
  <simple>${exchangeProperty.mailRequest['body']}</simple>
</setHeader>
<setHeader headerName="CamelVelocityResourceUri">
  <simple>${exchangeProperty.mailRequest['bodyResource']}</simple>
</setHeader>
<setHeader headerName="CamelVelocitySupplementalContext">
  <simple>${exchangeProperty.mailRequest['bodyContext']}</simple>
</setHeader>
<toD uri="velocity:template"/>
<toD uri="smtp:{{smtp.host:127.0.0.1}}"/>
```
Notice the headers, which are used by the `velocity` component, and the associated values from the `mailRequest` exchange property:
-   `CamelVelocityTemplate`: The `body` in `mailRequest` may be literal Velocity template text. The `body` and `bodyResource` values are mutually exclusive. You must specify Velocity template text via one or the other, not both. Note that you can either literally set the `body` text within a BPN script, or you could retrieve the text of a template that is stored in **Amelia's Content Manager**.
-   `CamelVelocityResourceUri`: The `bodyResource` in `mailRequest` may refer to a Velocity template resource from the classpath, which you would attach as an asset. For example, if you add `greeting.html.vm` as an asset, then you would set `bodyResource` to `greeting.html.vm`. This approach is an alternative to storing template files in Amelia's Content Manager as mentioned in the previous point.
-   `CamelVelocitySupplementalContext`: The `bodyContext` within `mailRequest` must be a `Map` of name-value pairs for value substitution within the Velocity template (whether the template is specified via `body` or `bodyResource`).
    For example, if your Velocity template contains the expression `${firstName}` and `bodyContext` contains the key `firstName`, then the value associated with that key would be substituted for the expression. In addition to the context supplied via `bodyContext`, other values are placed into the Velocity context as listed in the **Velocity Context** section of the [Camel Velocity Component documentation](http://camel.apache.org/velocity.html).
The Velocity component sets the input message body to the result of evaluating the template against the context.
# Adding Attachments
In order to add one or more attachments to a mail message, supply a list of `attachments` within the `mailRequest` execution variable, like so:
``` groovy
execution.setVariable 'mailRequest', [
    from        : ...,
    to          : ...,
    subject     : ...,
    ...,
    attachments : [
        // First attachment
        [
            name           : ...,
            content        : ...,  // mutually exclusive with contentResource
            contentResource: ...,  // mutually exclusive with content
            contentType    : ...,
            headers: [             // optional
                name: value,
                ...,
            ]
        ],
        // Second attachment
        [
            name           : ...,
            ...,
        ],
        ...
    ],
]
```
Each element of the `attachments` list must be a `Map` describing an attachment, where the following entries are supported for each attachment:
-   `name`: the name of the attachment as it will appear in the recipient's mail client
-   `content`: the content of the attachment, which can be a `String`, `byte[]`, `InputStream`, or `Object`, each handled as follows:
    -   `String`: the content is assumed to be a Base64 encoded string, and the component attempts to decode it as such. If decoding fails, the content is left unchanged. Otherwise, the content is the byte array resulting from successful decoding.
    -   `byte[]`: the content is left as-is
    -   `InputStream`: the content is the array of bytes read from the input stream
    -   `Object`: if the subtype of the attachment's `contentType` contains `json` (ignoring case), the object is converted to a JSON string, serving as the content. Otherwise, the content is the result of converting the object to a `String`.
-   `contentResource`: used in lieu of `content`, specifying a resource on the classpath (supplied via an asset attached to the flow). The array of bytes read from the classpath resource becomes the content. If the resource could not be found, the content is empty.
-   `contentType`: the MIME type of the content (e.g., `image/jpg`)
-   `headers`: a `Map` of name-value pairs to set as headers on the attachment. This is typically required when the attachment is intended to be embedded within the mail body, such as images and icons.
There are likely 2 primary means for supplying attachment content: (1) as a Camel flow asset, or (2) as a Content Manager item. These approaches are covered in the next sections.
## Supplying an Attachment via an Asset
To supply an attachment via a Camel flow asset, you can either upload the file to be attached directly as an asset, or you could package it into a JAR file (perhaps with other attachments) and upload the JAR file as an asset.
In the case of directly uploading the file to attach as an asset, you would then add the asset to your Camel flow and set the value of `contentResource` to the name of the asset. For example, if adding the file `foo.jpg` as an attachment, you could upload it directly as an asset. When attaching the asset to a Camel flow, it will be placed at the root of the classpath, so you would reference it as follows:
``` groovy
execution.setVariable 'mailRequest', [
    ...,
    attachments : [
        [
            name           : 'foo.jpg',
            contentResource: 'foo.jpg',
            contentType    : 'image/jpeg',
            ...,
        ],
    ],
    ...,
]
```
If packaging multiple attachments in a JAR file, you might want to organize them into folders. For example, you might have various types of attachments, such as images and videos, so you might package them up in a JAR file like so:
```
images/foo.jpg
images/bar.png
videos/demo.mp4
```
If you were to upload such a JAR file as an asset and add the asset to your Camel flow, you would refer to each attachment by it's path within the JAR file, like so:
``` groovy
execution.setVariable 'mailRequest', [
    ...,
    attachments : [
        [
            name           : 'foo.jpg'
            contentResource: 'images/foo.jpg',
            contentType    : 'image/jpeg',
            ...,
        ],
    ],
    ...,
]
```
The advantage of this approach is that the attachments are deployed along with the Camel flows. However, the downside is that if you need to update a file, you must not only upload the new version of the file, but must also redeploy the Camel flows that use it.
As alternative, you may want to supply an attachment from the Content Manager, as described in the next section.
## Supplying an Attachment via the Content Manager
Supplying an attachment from the Content Manager may be preferable to providing it via a Camel asset because it does not require you to redeploy Camel flows that use the asset when you upload a new version of the asset. The downside, however, is that you must transfer the attachment from Amelia to Camel, which might cause a performance hit for large attachments.
To use a Content Manager item as an attachment, you must retrieve either the `byte` array of the item or its Base64-encoded string value, and pass it as the value of `content` in the `mailRequest` object. For example, if you have a Content Manager bucket named `images` containing an image file named `foo.jpg`, you would do the following to send it as an attachment:
``` groovy
def images = cmService.getBucketResources 'images'
def fooImageId = images.find { it.objectName() == 'foo.jpg' }.objectId()
def fooImageBytes = cmService.getResourceBytes fooImageId
execution.setVariable 'mailRequest', [
    ...,
    attachments : [
        [
            name       : 'foo.jpg'
            content    : fooImageBytes,
            contentType: 'image/jpeg',
            ...,
        ],
    ],
    ...,
]
```
Note that sending the Base64-encoded string will have the same effect as sending the byte array. Both will end up as a Base64-encoded string on the Camel side because the object serialization that occurs will automatically convert the byte array to a Base64-encoded string. However, particularly for larger files, it may be beneficial to use the byte array from the BPN side because it will be smaller than the Base64-encoded string, and thus may help reduce the impact on the performance of managing execution variables.
## Embedding an Image Attachment
In order to embed an attached image within the mail body, there are a couple of additional steps required. The first step is to specify a Content ID in the `src` attribute of the `img` element. For example, if you want to embed the Amelia logo in a mail body, you might do something like so within the mail body:
``` groovy
<img src="cid:amelia-logo" border="0" height="36" width="174">
```
To associate an image with this image element, you would need to specify an attachment in your `mailRequest`, like so:
``` groovy
[
    name           : 'amelia-logo.png',
    contentType    : 'image/png',
    content        : ...,  // or contentResource
    contentResource: ...,  // or content
    headers        : [
        'Content-ID': '<amelia-logo>',
    ],
]
```
Note that the value of the `Content-ID` header must match the value following the `cid:` prefix in the `src` attribute of the `img` tag (`amelia-logo` in this example), surrounded by `<` and `>` (`<amelia-logo>` in this example).
{% /version %}
