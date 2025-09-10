Update the HAproxy configuration file with details about the Amelia Slack configuration.
**Table. HAproxy Changes for Slack**
``` groovy
frontend ft_amelia-web-https
        acl is_slack path_beg -i /Amelia/slack
        use_backend bk_amelia-gateway-slack if is_slack
backend bk_amelia-gateway-slack
        balance leastconn
        server localhost 127.0.0.1:4671 maxconn 2000 check 
```
Update properties in the gateway application.properties file.
**Table. Associated Changes to Gateway Configuration in the Gateway application.properties file**

| Property | Version | Required | Default Value | Description |
| ----|----|----|----|----|
| server.port | 3.5.x | No | 4671 | Port used to handle incoming web requests. Must match the setting in HAproxy. |
| server.servlet-path | 3.5.x/3.6.x/3.7.0 | No | /Amelia/slack | Servlet context path. Must match the setting in HAproxy. |
| server.servlet.context-path | 3.7.1+ | No | /Amelia/slack | Servlet context path. Must match the setting in HAproxy. |

