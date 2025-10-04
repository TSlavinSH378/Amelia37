{% version "3.x" %}
The Amelia Camel HTTP4 Component is a drop-in replacement for the standard [Camel HTTP4 component](http://camel.apache.org/http4.html), providing conveniences for making HTTP requests from Amelia via Camel in a standardized manner in an effort to significantly reduce boilerplate code both within Amelia as well as within Camel.
Using this component for making requests to any HTTP server through Camel is straightforward. The general steps for doing so are as follows, and are described in detail farther below:
1.  Add this component as an asset in the Amelia Integration Framework.
2.  Create a Camel flow, attaching the asset from the previous step.
3.  From a BPN:
    1.  Describe an HTTP request by constructing an `httpRequest` object.
    2.  Make the HTTP request by running the integration flow from above.
    3.  Examine the response described by the resulting `httpResponse` object.
This component may be used exactly like the standard Camel HTTP4 component, but the primary benefit is that your Camel Spring DSL (XML) file can be much simpler because this component takes care of mapping your `httpRequest` object onto the various Camel message headers used by the HTTP4 component. It also takes care of bundling up the response into an `httpResponse` object to be sent back to Amelia.
# Adding this Component as an Asset
As mentioned above, the first step to using this component from your Camel flows is to add this component as an asset to the Amelia Integration Framework. If the desired version of this component is not already an asset in your desired Amelia instance, you need to add it.
You can find all published versions of this component in our internal Artifactory binary repository. To download a particular version, do the following:
1.  Open a browser to <https://artifactory.ipsoft.com/artifactory/libs-release-local/net/ipsoft/ameliav3x/camel/ameliav3x-camel-http/1.0.3/ameliav3x-camel-http-1.0.3-all.jar>
2.  Click the link for the version you want to use (hopefully the latest)
3.  Click the link for the `ameliav3x-camel-http-VERSION-all.jar` file to download it. (**IMPORTANT**: choose the `all` file).
    > [!warning]  
    >
    > Although the JAR file has an `all` classifier, the only classes it contains from outside of this project are the classes from the `ameliav3x-camel-core` module, which are shadowed, so you don't have to explicitly add the `ameliav3x-camel-core` module as an asset, unless you plan to directly use classes from that module.
Once you have downloaded the component, go to the Integration Framework in the Amelia Admin UI of the instance in which you want to add it as an asset. Start creating a new asset, and when you reach the **New Assets** dialog box, fill in the fields as follows:
-   **Name:** Use the full name of the JAR file you downloaded above (e.g., `ameliav3x-camel-http-1.0-all.jar`). While this is not required, it is a **very strongly** recommended convention for convenient asset management.
-   **Domain:** Choose the `global` domain. Since this component is not domain-specific, it is recommended that you add it as an asset in the `global` domain so that it is available to flows in all domains.
-   **Attach Files**: Drag and drop the JAR file you downloaded above, or click to navigate to it and select it.
> [!warning]  
>
> Adding a version of this component as an asset is a one-time step. The only time you would need to perform this step again is when you want to upload a newer version of this component. By naming the asset the same as the JAR file name, you may have multiple versions of this component as assets, allowing existing flows to continue using an earlier version, while new flows use a newer version. The existing flows may then be upgraded as and when desired.
> [!warning]  
>
> If you want to use the `UriOptions` bean as shown in the examples in the rest of this document, repeat the same steps above for the `ameliav3x-camel-core` module by first going to <https://artifactory.ipsoft.com/artifactory/libs-release-local/net/ipsoft/ameliav3x/camel/ameliav3x-camel-core/1.0.1/ameliav3x-camel-core-1.0.1.jar> to find the version of the `ameliav3x-camel-core-VERSION.jar` file you want to use and adding it as an asset to the `global` domain (if you have permission).

# Creating a Camel Flow using this Component
Using this component in a Camel flow involves the following steps:
1.  Create a Camel flow in Amelia
2.  Fill in the required fields as desired (Name, Domain, etc.).
    > [!warning]  
    >
    > It is recommended that you name your Camel flow after the API it will be used for (e.g., "SNOW" or "Service Now" for the Service Now REST API), not any specific operation since the flow is intended to support all API operations.
3.  Attach the assets you added in the previous section (this component and the core component)
4.  Add a property named `baseURL` (case-sensitive) and set its value to the base URL of the HTTP server to which you want to send requests.
5.  Switch to **Source View** and use the following source as a starting point:
    ``` groovy
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://camel.apache.org/schema/spring
           http://camel.apache.org/schema/spring/camel-spring.xsd">
      <bean id="http4" class="net.ipsoft.ameliav3x.camel.component.http4.AmeliaHttpComponent"/>
      <bean id="http4Options" class="net.ipsoft.ameliav3x.camel.UriOptions"/>
      <camelContext id="httpContext" xmlns="http://camel.apache.org/schema/spring">
        <route id="httpRoute">
          <from uri="direct:start"/>
          <setHeader headerName="Exchange.HTTP_URI" id="setHttpBaseUrl">
            <simple>{{baseURL}}</simple>
          </setHeader>
          <bean ref="http4Options" method="set(throwExceptionOnFailure, false)"/>
          <toD uri="http4:host?${bean:http4Options}"/>
          <bean ref="varpop" method="moveToOutboundVariables(httpResponse)" id="setOutboundVariables"/>
        </route>
      </camelContext>
    </beans>
    ```
    ```
    ```
6.  Save the flow
7.  Deploy the flow
This starting point does not include any advanced configuration, such as using a proxy, setting up SSL, or any type of authentication, but all of that can be added in the same way you would add these things with the standard [Camel HTTP4 component](http://camel.apache.org/http4.html). In addition, see the **Reference Guide** section farther below.
# Making HTTP Requests using this Component
## General Steps
Once this component is added as an asset to the Amelia Integration Framework, and you have create a Camel flow with the asset attached, as described in the previous sections, making HTTP requests from a BPN is straightforward:
1.  Create a script task to construct an `httpRequest` map to send to Camel
2.  Run the integration flow
3.  Create a script task to examine the `httpResponse` map returned from Camel
The `httpRequest` object must be a `Map` and may contain the following entries:
-   **method**: the HTTP method (e.g., `GET`)
-   **path**: request path relative to the base URL defined on the Camel flow (see above)
-   **queryParams**: Map of name-value pairs to set as URL query parameters
-   **headers**: Map of name-value pairs to set as request headers
-   **body**: String or Object to send as the request body
The `httpResponse` object is a `Map` and may contain the following entries:
-   **statusCode**: integer HTTP status code (e.g., 200)
-   **reason**: HTTP status text associated with the status code (e.g. OK)
-   **headers**: Map of name-value pairs of response headers
-   **text**: response body as a String, if there is one
-   **json**: parsed response body as a Map or List, if body is a JSON string
-   **errorMessage**: parsing error message if JSON parsing failed
See the **Reference Guide** below for full details regarding the `httpRequest` and `httpResponse` objects.
## Example: Telling Chuck Norris Jokes
To illustrate the general steps described in the previous section, this section aims to get you up and running as quickly as possible, using the infamous [Internet Chuck Norris Database](http://www.icndb.com/) (ICNDb) API.
### Add this Component as an Asset
Add this component as an asset to the Amelia Integration Framework as described earlier, if the asset does not already exist.
### Create a Camel Flow using this Component to Get a Joke
To create a Camel flow that uses the asset you added in the previous section, do the following:
1.  In Amelia's Integration Framework, create a new flow and fill in the required fields as follows:
    -   **Name:** ICNDB
    -   **Code:** icndb
    -   **Domain:** (choose the desired domain)
    -   **Assets:** (choose the assets you uploaded in the previous section: this component as well as the core component)
    -   **Description:** Internet Chuck Norris Database API
    -   **Properties**:
    -   **baseURL **(case-sensitive) = [https://api.icndb.com](https://api.icndb.com/)
2.  Choose the flow's **Source View**, delete the contents, then copy and paste the following contents:  
    ``` groovy
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://camel.apache.org/schema/spring
           http://camel.apache.org/schema/spring/camel-spring.xsd">
      <bean id="http4" class="net.ipsoft.ameliav3x.camel.component.http4.AmeliaHttpComponent"/>
      <bean id="http4Options" class="net.ipsoft.ameliav3x.camel.UriOptions"/>
      <camelContext id="httpContext" xmlns="http://camel.apache.org/schema/spring">
        <route id="httpRoute">
          <from uri="direct:start"/>
          <setHeader headerName="Exchange.HTTP_URI" id="setHttpBaseUrl">
            <simple>{{baseURL}}</simple>
          </setHeader>
          <bean ref="http4Options" method="set(throwExceptionOnFailure, false)"/>
          <toD uri="http4:host?${bean:http4Options}"/>
          <bean ref="varpop" method="moveToOutboundVariables(httpResponse)" id="setOutboundVariables"/>
        </route>
      </camelContext>
    </beans>
    ```
    ```
    ```
3.  Save the flow.
4.  Deploy the flow. **NOTE:** If deployment fails, it might be because the `baseURL` property was not saved on the flow. Re-open the flow and make sure the property is there. If not, re-add the property. Then save and deploy again.
### Create a BPN to Request a Joke and Tell It
In the same domain in which you deployed the flow in the previous section, create a new BPN named `TellJoke` with the following elements connected in the following order:
1.  **Start Event**
2.  **Script Task** labeled `prepare joke request` and containing the following script:
    ``` groovy
    execution.setVariable 'httpRequest', [
        path       : '/jokes/random',
        queryParams: [
            limitTo  : ['nerdy'],
            firstName: userService.user.firstName(),
            lastName : userService.user.lastName(),
        ]
    ]
    ```
    ```
    ```
3.  **User Task** labeled `run the integration flow icndb`
4.  **Script Task** labeled `extract joke from response` and containing the following script:
    ``` groovy
    def httpResponse = execution.getVariable 'httpResponse'
     def joke = httpResponse?.json?.value?.joke ?: 'No joke!'
     execution.setVariable 'joke', joke
    ```
    ```
    ```
5.  **User Task** labeled `say ${joke}`
6.  **End Event**
Now save, deploy, and run the BPN to have Amelia tell you a joke, starring *you*!
# Reference Guide
## HTTP Request Structure
In order to define the HTTP request that you want to make, this component expects an **Amelia execution variable** of type `Map` named `httpRequest` (which appears on the Camel side as an exchange property of the same name) with the following entries (all of which are *optional*):

| Name | Type | Value |
| ----|----|----|
| method | String | HTTP method (default:;GET if no body; else POST) |
| path | String | URL path (relative to a base URL, see below) |
| queryParams | Map | Query parameters (a Map of name-value pairs) |
| headers | Map | HTTP headers (a Map of name-value pairs) |
| body | Object;or String | Message body (see details below) |

Here are more details about each entry:
-   **method**: The message header Exchange.HTTP_METHOD is set to this value. If not specified, defaults to POST if a body (see below) is specified, otherwise defaults to GET.
-   **path**: Path relative to the value of the input message header Exchange.HTTP_URI, which is generally set to the value of a Camel flow property. The input message header Exchange.HTTP_PATHis set to this value.
-   **queryParams**: Name-value pairs of query parameters. The component automatically constructs a query string from this map and sets the input message header Exchange.HTTP_QUERY to the result.
-   **headers**: Name-value pairs of request headers. These headers will be added as input message headers. As a convenience, header names may use underscores (\_) in place of dashes (-), which simply allows surrounding quotes to be dropped in Groovy code. Before setting such a header, the component will replace underscores with dashes. For example, rather than having to specify a header name as 'Content-Type', it may be specified without quotes as Content_Type, which will have the same result.
-   **body**: The request body. If the body is a String, it will be left unchanged. Otherwise, if the Content-Type header is specified and the MIME subtype ends with json, the body will be converted to a JSON string. If the Content-Type header contains the MIME type application/x-www-form-urlencoded and the body is a Map, it will be converted to a string formatted identically to a query string, as defined by [HTML 4.01 Specification](https://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1). In any other case, the body remains unchanged. The result is set as the body of the input message on the exchange.
    > [!warning]  
    >
    > Prior to any such processing of the `body`, if there is initially no value associated with the key `'body'` in the `httpRequest` map, it will be set to the body of the inbound message in the exchange, but only if that body is not an instance of `net.ipsoft.ameliav3.integration.client.IntegrationRequest` (because it is simply an internal object sent from Amelia).
> [!warning]  
>
> Prior to any other processing of the `httpRequest` exchange property as described above, all values within the map that are instances of `CharSequence` (i.e., `String`, `GString`, etc.) have property placeholders resolved. This means that any property placeholders appearing anywhere within the `path`, `queryParams` values, `headers` values, or the `body` (if the body is a `Map` or `Collection`) are resolved before anything else occurs.

The note above is significant because it allows you to write environment-independent requests on the Amelia side (in BPNs) and have environment-specific properties resolved on the Camel end. For example, the following shows a request for obtaining an OAuth2 access token:
``` groovy
execution.setVariable 'httpRequest', [
    path   : '/rest/pub.mediator.oauth2.getOAuth2AccessToken',
    headers: [
        Content_Type: 'application/x-www-form-urlencoded',
    ],
    body   : [
        client_id    : '{{clientId}}',
        client_secret: '{{clientSecret}}',
        grant_type   : 'client_credentials',
    ],
]
```
Notice that the values of `client_id` and `client_secret` contain property placeholders because they are not only sensitive values, but also because they are potentially environment-specific. Therefore, the code above remains environment-independent, and when the variable above is sent to Camel, this component will resolve the property placeholders with the property values defined in the environment before making the HTTP request.
## HTTP Response Structure
Upon execution of an HTTP request, this component sets the exchange property named `httpResponse` to a `Map` with the following entries:

| Name | Type | Description |
| ----|----|----|
| statusCode | int | HTTP status code (e.g.,;200) |
| reason | String | HTTP status reason (e.g.,;OK) |
| headers | Map | HTTP response headers (e.g.,;{Content-Type=application/json, ...}) |
| text | String | Raw response body (absent if there is no response body, or body was successfully parsed as a JSON string) |
| json | Object | Result of parsing response body as a JSON string (absent if there is no response body, the;Content-Type header does not contain a MIME subtype ending with json, or parsing failed) |
| errorMessage | String | Message from;JsonException thrown while parsing response body as a JSON string (absent if no parsing occurred, or parsing succeeded) |

Continuing with the example at the end of the previous section, here is what the `httpResponse` exchange property might look like after executing the request:
``` groovy
[
    statusCode: 200,
    reason    : 'OK',
    headers   : [
        'Content-Type': 'application/json',
        ...
    ],
    json      : [
        access_token: '301fed9149...',
        token_type  : 'Bearer',
        expires_in  : 3600
    ]
]
```
## Camel Context
Since this Amelia HTTP4 component is an extension of the standard Camel HTTP4 component, your Camel context file will differ very little from what it would look like when using the standard Camel HTTP4 component. Again, the file `src/test/resources/META-INF/spring/camel-context.xml` in this project shows the recommended starting point. In that file, the primary addition is the declaration of the following bean, which is an instance of the Amelia HTTP4 component:
``` groovy
<bean id="http4" class="net.ipsoft.ameliav3x.camel.component.http4.AmeliaHttpComponent"/>
```
Since the bean `id` is `http4`, it overrides the default association of `http4` with the standard HTTP4 component, but since the bean is an extension of the standard component, it acts as a drop-in replacement, meaning that it can be used exactly as the standard component in *every* way.
However, the Amelia HTTP4 component allows you to specify an `httpRequest` exchange property (populated from a BPN execution variable of the same name) rather than having to explicitly set the various message headers that the standard component uses (such as `Exchange.HTTP_METHOD`, `Exchange.HTTP_PATH`, etc.). Instead, the Amelia component uses the `httpRequest` exchange property to set such message headers (and the message body, if supplied) for you.
Further, the Amelia HTTP4 component then constructs an `httpResponse` exchange property after making the request, gathering all of the relevant message headers and message body (if there is one) for you, so it can be sent back to Amelia.
The benefit is that your context file can be much simpler since the Amelia HTTP4 component handles the vast majority of the boilerplate code. When you pass in an appropriate `httpRequest` object from Amelia, your context file can be as simple as the following:
``` groovy
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring
       http://camel.apache.org/schema/spring/camel-spring.xsd">
    <bean id="http4" class="net.ipsoft.ameliav3x.camel.component.http4.AmeliaHttpComponent"/>
    <camelContext id="httpContext" xmlns="http://camel.apache.org/schema/spring">
      <route id="httpRoute">
        <from uri="direct:start"/>
        <setHeader headerName="Exchange.HTTP_URI" id="setHttpBaseUrl">
          <simple>{{baseURL}}</simple>
        </setHeader>
        <toD uri="http4:host"/>
        <bean ref="varpop" method="moveToOutboundVariables(httpResponse)" id="setOutboundVariables"/>
      </route>
    </camelContext>
</beans>
```
Of course, this simple context file does not include any type of authentication that might be required, nor any other options that you may need to set on the HTTP4 component, but again, you can set those options exactly as you would for the standard HTTP4 component.
{% /version %}
