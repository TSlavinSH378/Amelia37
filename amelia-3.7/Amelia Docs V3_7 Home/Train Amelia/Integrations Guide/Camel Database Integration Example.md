This database example shows how to use Camel in the Source View of the Integration Flow workspace to implement key functionality.
# Camel Code
> [!note]  
>
>     <?xml version="1.0" encoding="UTF-8"?>
>     <beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:camel="http://camel.apache.org/schema/spring" xsi:schemaLocation="http://www.springframework.org/schema/beans
>               http://www.springframework.org/schema/beans/spring-beans-4.2.xsd
>               http://camel.apache.org/schema/spring
>               http://camel.apache.org/schema/spring/camel-spring.xsd
>     ">
>         <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
>             <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
>             <property name="url" value="jdbc:mysql://${dbHost}:${dbPort}/${dbName}"/>
>             <property name="username" value="${dbUser}"/>
>             <property name="password" value="${dbPass}"/>
>         </bean>
>         <camel:camelContext id="mainContext">
>             <camel:route id="route1">
>                 <camel:description layoutX="20" layoutY="20" layoutWidth="970" layoutHeight="640"/>
>                 <camel:from id="mainRouteStart" uri="direct:start">
>                     <camel:description layoutX="20" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:from>
>                 <camel:log message="running $simple{property.sqlStatement}" loggingLevel="INFO" id="c-eb630da6-1b69-49fb-afa1-f1e6eb217523">
>                     <camel:description layoutX="150" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:log>
>                 <camel:setBody id="c-50b78bf5-3733-456b-a349-e45c1aac3972">
>                     <camel:description layoutX="150" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                     <camel:simple id="c-635da76f-8821-4fa4-bbb7-b64e5ad46245">
>                         ${exchangeProperty.sqlStatement}
>                     </camel:simple>
>                 </camel:setBody>
>                 <camel:to uri="jdbc:dataSource" id="c-632e3dd5-9fd8-4c16-ad9d-938857b292ab">
>                     <camel:description layoutX="280" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:to>
>                 <camel:convertBodyTo type="java.lang.String" id="c-7f9d92c9-e573-4b8b-81e5-3f1f9006b1e7">
>                     <camel:description layoutX="670" layoutY="20" layoutWidth="120" layoutHeight="120"/>
>                 </camel:convertBodyTo>
>                 <camel:log message="body is ${body.getClass()} ${body}." loggingLevel="INFO" id="c-7c71ae3b-0e1d-4dcb-bf8e-f5ae1d0c837c">
>                     <camel:description layoutX="810" layoutY="150" layoutWidth="120" layoutHeight="120"/>
>                 </camel:log>
>                 <camel:setProperty propertyName="sqlResponse" id="ee9b7a0d-aa03-11e7-a861-fdebea8f0396">
>                     <camel:description layoutX="740" layoutY="330" layoutWidth="120" layoutHeight="120"/>
>                     <camel:simple id="ee9b7a0e-aa03-11e7-a861-fdebea8f0396"><![CDATA[${body}]]></camel:simple>
>                 </camel:setProperty>
>                 <camel:to uri="bean:varpop?method=moveToOutboundVariables(&apos;sqlResponse&apos;)" id="c-ef1c4903-a2e6-4c65-b9aa-25d602680310">
>                     <camel:description layoutX="20" layoutY="470" layoutWidth="120" layoutHeight="120"/>
>                 </camel:to>
>             </camel:route>
>         </camel:camelContext>
>     </beans>

# Required Flow Properties

| Property | Example Value | Description |
| ----|----|----|
| dbHost

\|
utility01.ams1.amelia.ipcenter.com
\| Hostname of server where database lives \| \|
    dbPort
\| 3306 \| Port to access database instance \| \|
    dbName
\| banking \| Name of the database \| \|
    dbUser
\| amelia \| Username used to access the database \| \|
    dbPassword
\| password \| Password used to access the databse \|
# Required Exchange Properties

| Property | Example Value | Description |
| ----|----|----|
| sqlStatement

\| select \* from Termijnbedrag where CONTRACTREKENINGNUMMER=004000001882; \| SQL query to run against the databse \|
# Returned Variables

| Variable | Value | Description |
| ----|----|----|
| sqlResponse | Array of maps for each table row returned | The result set or result code of the sql statement |

