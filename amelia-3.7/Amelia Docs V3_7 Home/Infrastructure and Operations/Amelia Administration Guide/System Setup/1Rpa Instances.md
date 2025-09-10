Robotic Process Automation (RPA) enables software bots to mimic human interaction with a user interface. 1RPA hosts can be registered with Amelia then called with the run the rpa bot BPN task. Bots called from within a BPN must exist on the 1RPA host.
To view registered 1RPA instances, click the System Settings link on the left side of Amelia's administration pages then click the Audit Log link to display a searchable list of events.
To edit a 1RPA instance click the ![](attachments/28476193/28476205.png) pencil icon to the left of a name listed in the 1Rpa Instances workspace.
![](attachments/28476193/28476206.png)
Figure. 1Rpa Instances Workspace
The edit instance workspace appears when an existing instance is opened or a new instance is created. Access to any instance is global.
![](attachments/28476193/28476207.png)
Figure. New 1Rpa Instance Workspace
Table. New 1Rpa Instance Workspace Elements

| Element | Description |
| ----|----|
| Name | A Unique name for the instance, usually <client code>-1rpa |
| API URL Base | The base URL for all 1Desk APIs.; Normally just the FQDN plus /ap  (External hostname). |
| Public URL | The public URL of the instance (API URL Base without /api).; Currently this is only used by individual BPNs and may be removed in the future. |
| API User Email | The email address of a user in Rpa that Amelia will use to invoke 1Desk APIs.; This user should have global permissions. (A new user should be created with a System Password Policy, meaning it doesn't expire) |
| Change API Password | Uncheck to force a change in the API password |
| API User Password | Password of user |
| MQ URI | The RabbitMQ connect string to the 1RPA broker (internal hostname) |
| MQ User | Username of MQ user.; The default is ipsoft |
| Change MQ Password | Uncheck to force a change in the MQ password |
| MQ Password | Password of MQ user. ;rabbitmqctl authenticate_user <username> <password>rabbitmqctl authenticate_user guest guest # verifies the user guest with password guest; make sure the user/pass works |

