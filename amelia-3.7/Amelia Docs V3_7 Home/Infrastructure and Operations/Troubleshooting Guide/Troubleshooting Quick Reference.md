{% version "3.x" %}
The table below includes links to the most common issues encountered by the Amelia software system and possible solutions.
-   System-related solutions are in [System Troubleshooting](System%20Troubleshooting).
-   Standard Operating Procedures for Amelia-related problems are in [Standard Operating Procedures](Standard%20Operating%20Procedures).
-   The Amelia monitoring process is described in [Monitoring Overview](Monitoring%20Overview).
-   The appendices have information about [log file locations](https://docs.amelia.com/display/AmeliaDocsV2/Appendix+A%3A+Log+File+Locations) and [system file and folder locations](Appendix%20B_%20System%20File%20and%20Folder%20Locations).
Table: Common Issues, Causes, and Possible Solutions

| Issue | Cause(s) | Solution(s) |
| ----|----|----|
| Disk /app folder error | Insufficient Disk space | Disk - /appsManaging Log Files |
| RAM error | Insufficient RAM | Managing Swap Memory |
| MySQL stops | Cluster-related crash when cluster reports a node is available when it is not available. | Percona/MySQLmysqld/mysql_safe |
| Mulesoft fails | Too many queued messages | RabbitMQ |
| RabbitMQ fails | Messages don’t clear | RabbitMQ |

In addition, these resources might be useful to troubleshooting problems:
-   [Commands to Monitor Service Status](https://docs.ipsoft.com/display/AmeliaDocsV3/Monitoring+Overview#MonitoringOverview-CommandstoMonitorServiceStatus)
-   [Using grep to Find Problems](https://docs.ipsoft.com/pages/viewpage.action?pageId=11929473#AmeliaStandardOperatingProcedures(SOPs)-UsinggreptoFindProblems)
-   [Log File Locations](Appendix%20A_%20Log%20File%20Locations)
-   [System File Locations](Appendix%20B_%20System%20File%20and%20Folder%20Locations)
{% /version %}
