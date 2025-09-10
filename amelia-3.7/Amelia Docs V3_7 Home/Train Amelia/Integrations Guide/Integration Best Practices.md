# Compliance
Since the introduction of GDPR privacy requirements in the European Union, developers need to be mindful of how client data is used within their work.
## How can you be sure to be compliant?
When it comes to pulling consumer data, be sure to follow the “[Principles relating to processing of personal data](http://www.privacy-regulation.eu/en/5.htm)” EU GDPR article that basically states that personal data shall be:
-   Processed lawfully, fairly and in a transparent manner
-   Collected only for specified, explicit and legitimate purposes
-   Adequate, relevant and limited to what is necessary
-   Accurate and kept up to date
-   Held only for the absolute time necessary and no longer
-   Processed in a manner that ensures appropriate security of the personal data
## What is considered personal data?
Any information related to a natural person/data subject that can directly or indirectly identify that person. Some examples are:
-   Name, email, address & phone number
-   Persona Info (Sexual orientation, gender preference, racial identity)
-   Bank details
-   Medical info
When retrieving data from client system endpoints, make sure only the minimum amount of data required is returned. Extreme care should also be taken when logging any payloads or specific data that could be considered under compliance regulations. When any of this data is required to pass through Amelia or her integrations, explicit client sign off should be obtained.
# Development Environment
Integrations can be built with either the Integration visual editor or with an IDE working with source code.
![](attachments/11945252/11945253.png)
Figure. Amelia Integration Visual Editor
![](attachments/11945252/11945254.png)
Figure. Source Code Editor
## Enable Visual Designer to Work with Source Code
The camel namespace prefix allows the visual designer to render different components. For example, here is how to declare and use the namespace to allow the visual designer to work. The key declaration is on lines 4 and 10: camel-context.xml syntax for enabling the visual designer

|  |  |
| ----|----|
| 12
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18 | <?xml;version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:camel="http://camel.apache.org/schema/spring"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring
       http://camel.apache.org/schema/spring/camel-spring.xsd">
  <camel:camelContext id="...">
    <camel:route id="...">
      <camel:from uri="direct:start">
        <camel:description layoutX="20" layoutY="20" layoutWidth="120" layoutHeight="120"/>
      </camel:from>
      <!-- ... -->
    </camel:route>
  </camel:camelContext>
</beans> |

## Prevent Visual Designer from Adding XML Visual Elements
Alternatively, to prevent the visual designer from inserting all sorts of visual elements within your XML file, *exclude* the declaration shown in line 4 above, and instead, include the `xmlns` attribute of the `camelContext` element shown on line 9 below:
**camel-context.xml for disabling the visual designer**

|  |  |
| ----|----|
| 12
3
4
5
6
7
8
9
10
11
12
13
14
15 | <?xml;version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring
       http://camel.apache.org/schema/spring/camel-spring.xsd">
  <camelContext xmlns="http://camel.apache.org/schema/spring">
    <route id="...">
      <from uri="direct:start"/>
      <!-- ... -->
    </route>
  </camelContext>
</beans> |

The decision should be made based on who will be supported the project in the future, will the visual designer be used and is it important, or is code quality and readability?
The remainder of this document uses the more compact notation so that the examples are more readable here. In addition, for brevity, the surrounding `beans` element is excluded from the examples.
# Element IDs
If you don't explicitly add `id` attributes to your elements, the Integration Framework will auto-generate them. In some cases, this is fine. However, adding meaningful `id` attributes to elements aids debugging. Most importantly, `camelContext` and `route` elements should have meaningful `id` attribute values.
For example, in a Camel flow that's making HTTP requests to a ServiceNow API, `id` values might be set like so:

|  |
| ----|
| <camelContext;xmlns="http://camel.apache.org/schema/spring" id="serviceNowApiContext">
  <route id="serviceNowApiRoute">
    <from uri="direct:start"/>
    <!-- ... -->
  </route>
</camelContext> |

Notice the `camelContext` and `route` elements have `id` values of `serviceNowApiContext` and `serviceNowApiRoute`, respectively. These values will be used in log entries, making it obvious as to which Camel flow is executing, thus making debugging easier.
# Reusable Connectors
The core of an integration strategy is the concept of building connectors that can be used for any use case. An integration flow should not contain any business or process specific logic, it should just be a mechanism to pass data back and forth between Amelia and an external service/endpoint. The IPsoft Cognitive team maintains a library of Camel templates for common use cases.
# Properties and Property Sets
Make the flows environment independent by using properties and property sets. Properties and Property Sets should be used to store any environment specific information needed for an integration. This could include hosts, ports, authentication credentials, API paths, and other details. This feature also allows encryption of values of passwords and other sensitive data. 
To create a Property Set, go to the Property Set tab in the Integrations workspace.
![](attachments/11945252/11945255.png)
Figure. Property Set Interface in Integrations Workspace
In this example, properties for a MySQL database are use to connect to the database with an integration flow. Actual values are retrieved from environment variables set on the server. However, these values also could be defined in the property set.
![](attachments/11945252/11945256.png)
Figure. Property Set Example for MySQL Connection
Notice there are properties in the flow itself. Use the up and down arrows to choose which properties take priority. Keeping properties in a Property Set allow use of the same properties across multiple integration flows if they need to use the same shared resource.
# Using a Proxy
When connecting to resources in a client environment, or hosted by a service provider, from an IPsoft hosted Amelia instance, it is highly recommended to use the IPsoft proxy. IPsoft firewalls need to whitelist all IP addresses to allow outgoing connections. If these IP addresses change without IPsoft knowing, integrations will start to fail (and ideally you have Exception Handling to account for connection failure). For an HTTP connection, can use the proxy by including these properties in your flow:

|  |
| ----|
| <properties>   <property key="http.proxyHost" value="proxy.ipsoft.com"/>
   <property key="http.proxyPort" value="80"/>
   <property key="http.proxyScheme" value="http"/>
</properties> |

