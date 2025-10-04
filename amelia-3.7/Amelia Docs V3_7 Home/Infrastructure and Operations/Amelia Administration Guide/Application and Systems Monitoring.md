{% version "3.x" %}
In addition to administration pages that allow monitoring of the software application, Amelia’s systems and software are monitored in different ways externally.
Amelia is monitored as a collection of multiple services and hosts divided into relevant technology groups. Each technology group is a separate host with a unique hostname, for example, amelia-batch. In the case of a cluster, each node is a host with a different app name, for example, app01, app02, app03. Each of these systems are monitored in different ways.
Each Amelia host contains a complete Amelia system, for example, Amelia Batch, Engine, Web, Escalation, MySQL, and so on.
# Amelia Systems
The Amelia software system is organized into services and host groupings, for example, Amelia Batch, Amelia Engine, Amelia Web, and Amelia Escalation.
## Amelia Services
Amelia's operations are organized into a set of application and database services which are monitored.
![](attachments/11940317/11940318.png)
Figure. Amelia's Services
Table. Amelia Services
|                                    |                                                                                                                                                                                                                                                                                                                                           |
|---------------------|---------------------------------------------------|
| Amelia Service                     | Description                                                                                                                                                                                                                                                                                                                               |
| **Application Services**           |                                                                                                                                                                                                                                                                                                                                           |
| amelia-admin-web.service           | The web service for the admin side of Amelia, handles all user actions on the admin side, log will contain errors about invalid scripts or other errors experienced in the admin user interface.                                                                                                                                          |
| amelia-user-web.service            | The end user and agent conversation interface.                                                                                                                                                                                                                                                                                            |
| amelia-engine-service@p001.service | The engine that handles inbound/outbound conversation messages.                                                                                                                                                                                                                                                                           |
| amelia-batch-service.service       | Metrics calculation and other batch jobs.                                                                                                                                                                                                                                                                                                 |
| amelia-escalation-service.service  | Escalation engine.                                                                                                                                                                                                                                                                                                                        |
| amelia-h2o.service                 | Handles analytics engine                                                                                                                                                                                                                                                                                                                  |
| amelia-integration-service.service | Engine for connecting with third parties. Has no access to either database, and interfaces with Amelia only via GRPC calls and RabbitMQ messages. Deploy spring integration contexts to this daemon through admin-web tools. Can be deployed to multiple hosts, though both the contexts and the hosts must be registered in admin tools. |
| amelia-model-server@p001.service   | Handles loading and serving all trained models in an instance                                                                                                                                                                                                                                                                             |
| amelia-syntaxnet.service           | IPsoft Amelia SyntaxNet                                                                                                                                                                                                                                                                                                                   |
| amelia-admin-service.service       | Handles classifier and other model training, for some reason there are also user authentication events and conversation logs in here.                                                                                                                                                                                                     |
| amelia-account-service.service     | Handles requests to users and authentication systems                                                                                                                                                                                                                                                                                      |
| **Database Services**              |                                                                                                                                                                                                                                                                                                                                           |
| amelia-kdb-master                  | The KDB (Knowledge DB) database is used for storing all knowledge configuration, domains, and users. In addition, there is at least one slave of this database which is used at conversation time to query this information.                                                                                                              |
| amelia-cdb-p001                    | The CDB (Conversation Database) is used for storing per-conversation data. There may be multiple instances of the CDB database attached to multiple engines. To support additional conversation throughput, additional instances can be added along with the associated engines.                                                          |
| amelia-adb                         | The ADB (Admin Database) holds users and other authentication data.                                                                                                                                                                                                                                                                       |
The routine application monitoring checks include:
-   File Descriptor Utilization
-   Heap Utilization
-   Java Process - amelia-account-service
-   Nonheap Utilization
Routine database monitoring checks are noted below in the MySQL section.
## Amelia Batch
The routine monitoring checks include:
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Log Scrubber/Monitoring watches logs in real time for specific regex patterns for common issues and exceptions.
-   Process Monitoring checks the status of the /apps/IPsoft/amelia/amelia-batch/amelia-batch.jar process.
-   Amelia Batch Log File Age
-   Amelia Web Log File Age
## Amelia Engine
The routine monitoring checks include:
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Log Scrubber/Monitoring watches logs in real time for specific regex patterns for common issues and exceptions.
-   Process Monitoring checks the status of the /apps/IPsoft/amelia/amelia-engine/amelia-engine.jar process.
-   IMX Mbean Performance Counter checks status of Amelia-specific metrics.
-   Amelia Engine Log File Age
-   Amelia Mbean Perf - amelia.metrics:name counter.status.200.health
## Amelia Web
The routine monitoring checks include:
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Log Scrubber/Monitoring watches logs in real time for specific regex patterns for common issues and exceptions.
-   Process Monitoring checks the status of the /apps/IPsoft/amelia/amelia-web/amelia-web.jar process.
-   Web check monitors the Amelia web UI status.
-   Amelia User Web Log Scrubber
## Amelia Escalation
The routine monitoring checks include:
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Log Scrubber/Monitoring watches logs in real time for specific regex patterns for common issues and exceptions.
-   Process Monitoring checks the status of the /apps/IPsoft/amelia/amelia-excalation/amelia-escalation.jar process.
# MySQL
The routine monitoring checks include:
-   Java Log Scrubber/Monitoring watches logs in real time for specific regex patterns for common issues and exceptions.
-   Max Sessions
-   Open Tables
-   Questions Per Second
-   Slow Queries
-   Table Opening Rate
-   Uptime
The adb, cdb, and kdb (master and slave) database service monitoring checks include:
-   MySQL Alert Log
-   MySQL Long Running Query
-   MySQL Max Sessions
-   MySQL Open Tables
-   MySQL PerfData
-   MySQL Questions Per Second
-   MySQL Slow Queries
-   MySQL Table Opening Rate
-   MySQL Uptime
# RabbitMQ
The routine monitoring checks include:
-   Aliveness checks if rabbitmq is open to accept connections and data.
-   Connections checks the number of active connections.
-   Log Scrubber cleans up the log files.
-   Nodes checks the status of nodes.
-   Objects checks the number of objects in the cluster.
-   Overview checks the status of rabbitmq as defined by the software itself.
-   Partitions checks inner-cluster data partitions.
-   Queues checks the status and size of the queues.
-   Watermark checks disk space usage.
# Redis
The routine monitoring checks include:
-   Process Status
-   Clients Blocked checks the number of clients where data is blocked.
-   Clients Connected checks the number of connected clients.
-   HitRatio checks the ratio of cache hits, for Perfdata Only.
-   Log Scrubber cleans up the log files.
-   Memory Frag Ratio checks the fragmentation ratio.
-   Memory Used.
-   Memory Used LUA.
-   Memory Used RSS.
-   AOF Current Size checks the size of the disk based cache.
-   Perf Data: Evicted Keys checks the number of keys removed due to space.
-   Perf Data: Expired Keys checks the number of keys removed due to TTL.
-   Perf Data: Keyspace checks the size and performance of the database.
-   Perf Data: Keyspace hits
-   Perf Data: Keyspace misses
-   Perf Data: Operations per second
-   Persistence
-   Uptime
# Linux Server
The routine monitoring checks include:
-   Amelia Backup Log checks the log file of the on-box MySQL backups, for a single node, usually app03.
-   Amelia SSL Expiry checks the validity of the SSL certificate.
-   Amelia Webcheck duplicates the amelia-web check of Amelia’s UI.
-   Amelia YUM Audit Log monitors when software is installed or removed with YUM.
-   Chrony Offset checks systemtime against NTP servers.
-   Disk – \[partition name\] monitors the /, /apps, and /boot partitions for size.
-   Disk Latency – checks disk await.
-   HaProxy Back End monitors the backends for Amelia.
-   HaProxy Front End monitors frontends for Amelia.
-   Host Memory checks overall system memory.
-   Inodes – \[partition name\] monitors same partitions as the Disk check.
-   Linux Message Log monitors the /var/log/syslog for general issues.
-   Load Average checks the CPU load.
-   Proc – \[process name\] monitors chronyd, crond, firewalld, haproxy, mysqld, sshd, syslog, xinetd.
-   SSH
-   Swap Usage
-   TCP – 443/80 validates TCP ports 443/80 are open and listened to.
-   Total Procs checks the total number of processes on the system.
-   Uninterruptible Process checks for stuck processes.
-   Zombies checks for processes that are dead but not killed.
# Commands to Monitor Service Status
These commands report on the status of Amelia’s systems.
Table. Monitoring CLI Commands

| System | Command |
| ----|----|
| Amelia (all) | systemctl status amelia-* |
| amelia-engine | systemctl status amelia-engine.service |
| amelia-web | systemctl status amelia-web.service |
| amelia-batch | systemctl status amelia-batch.service |
| amelia-escalation | systemctl status amelia-escalation.service |
| amelia-<client> | systemctl status amelia-<client>-web.service |
| RabbitMQ | rabbitmqctl status |
| MySQL | service mysql status OR ps aux | grep mysql |

{% /version %}
