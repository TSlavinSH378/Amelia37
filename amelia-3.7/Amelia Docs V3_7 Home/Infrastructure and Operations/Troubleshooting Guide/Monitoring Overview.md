-   [Amelia Systems](#MonitoringOverview-AmeliaSystems)
    -   [amelia-account-service](#MonitoringOverview-amelia-account-service)
    -   [amelia-admin-service](#MonitoringOverview-amelia-admin-service)
    -   [amelia-admin-web](#MonitoringOverview-amelia-admin-web)
    -   [amelia-batch-service](#MonitoringOverview-amelia-batch-service)
    -   [amelia-duckling](#MonitoringOverview-amelia-duckling)
    -   [amelia-engine-service](#MonitoringOverview-amelia-engine-service)
    -   [amelia-escalation-service](#MonitoringOverview-amelia-escalation-service)
    -   [amelia-integration](#MonitoringOverview-amelia-integration)
    -   [amelia-model-server](#MonitoringOverview-amelia-model-server)
    -   [amelia-syntaxnet](#MonitoringOverview-amelia-syntaxnet)
    -   [amelia-user-web](#MonitoringOverview-amelia-user-web)
    -   [Host OS](#MonitoringOverview-HostOS)
    -   [MySQL](#MonitoringOverview-MySQL)
-   [RabbitMQ](#MonitoringOverview-RabbitMQ)
-   [Redis](#MonitoringOverview-Redis)
-   [Linux Server](#MonitoringOverview-LinuxServer)
-   [Commands to Monitor Service Status](#MonitoringOverview-CommandstoMonitorServiceStatus)
Amelia is monitored as a collection of multiple services broken up into relevant technology groups. Each technology group is a separate service with a unique name, for example, amelia-batch-service or amelia-escalation-service. In the case of a cluster, each node is a service with a different app name, for example, app01, app02, app03. Each of these systems are monitored in different ways.
When troubleshooting, begin with the alert or other indication of a problem. If the system is slow or down with no alerts, however, begin with the basic environment and systems then the Amelia systems, as described in this document. Collect as much information as possible before contacting IPsoft.
Troubleshooting Amelia systems and environment uses the monitoring and other output of technology groups to identify and resolve problems. Each Amelia host is monitored in the following ways.
## Amelia Systems
The Amelia software system is organized into services, for example, amelia-user-web manages Amelia's different user-facing interfaces while amelia-admin-web manages Amelia's administration pages used to configure her functionality.
### amelia-account-service
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-account-service. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-admin-service
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-admin-service. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-admin-web
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-admin-web. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-batch-service
The routine monitoring checks include:
-   Log file age V3 - checks if file path has been modified within X seconds. Critical 300s, no warning.
-   File Descriptor Utilization - monitors number open files to 95-90% of system max
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-batch-service. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-duckling
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-duckling. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-engine-service
The routine monitoring checks include:
-   Amelia Engine Log File Age V3 - checks if file path has been modified within X seconds. Critical 300s, no warning.
-   Amelia Mbean Perf - amelia.metrics:name counter.status.200.health
-   Amelia Mbean Perf - amelia.metrics:name gauge.response.health
-   File Descriptor Utilization - monitors number open files to 95-90% of system max
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-engine-service. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-escalation-service
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-engine-service. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-integration
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-integration. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-model-server
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-model-server. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-syntaxnet
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-syntaxnet. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
### amelia-user-web
The routine monitoring checks include:
-   File Descriptor Utilization - monitors number open files. Critical: 95%, Warning: 90%.
-   Garbage Collection – G1 Old Generation checks the amount of time GC takes and alerts if it is in excess of 5 seconds.
-   Heap Utilization checks the amount of Heap memory usage and alerts if above 85%.
-   Java Process checks if named process is running with amelia-user-web. Critical is 1, no warning.
-   Nonheap Utilization same as Heap Utilization only with the attribute being NonHeapMemoryUsage.used.
-   Amelia Log Scrubber/Monitoring watches logs in real time for specific regex patterns for common issues and exceptions.
-   Amelia User Web Error.
### Host OS
The routine monitoring checks include:
-   Amelia Backup Log – {filepath} where default is /apps/IPsoft/backups. Monitors the backup tool for failures via a log scrubber. This is currently being phased out for remote offsite backups. Critical if any events match.
-   Amelia SSL Expiry - Monitors status of the SSL certification for expiration. Critical: 30d, Warning: 60d.
-   Amelia Webcheck - Monitors basic availability of Amelia but ensuring the basic web interface is online. Critical: non http 200 response.
-   Chrony Offset - Monitors time sync drift between the local host and a defined time server. Critical: 5000ms, Warning: 2500ms.
-   Disk – {partition_name} Monitors disk space usage per partition. Critical: 95%, Warning: 90%.
-   HAProxy BackEnd - Monitors the status of all HAproxy defined backends. Critical: Status down or connection utilization above 80%.
-   HAProxy Frontend - Same as backend only for Frontend
-   Host Memory - Monitors the amount of free system memory. Critical: 98%, Warning: 95%.
-   Inodes - {partition_name} Monitors the inode usage per disk partition. Critical: 90%, Warning 80%.
-   Linux Message Log - Monitors a log file every X seconds and parses each line over a set of regex patterns. Critical if any events match.
-   Load Average - Monitors the numbering of waiting threads in the system. This is only used for performance data so there are no warning/critical thresholds.
-   Proc – {Process_name} Monitors the status of specific processes. Critical: 1, no warning
    -   Chronyd
    -   Crond
    -   Exim
    -   Firewalld
    -   Haproxy
    -   Mysqld
    -   Sshd
    -   Syslog
    -   Xinetd
    -   Redis
    -   Redis-sentinel
-   Swap Usage - Monitors the amount of swap being used. Critical: 90%, Warning: 80%.
-   TCP – {port_number} - Monitors if the specific open is open for connections. Critical is port is not open
    -   80
    -   443
    -   23
-   Uninterruptable Processes - Monitors for any processes which may be stuck for any reason. Critical if any processes are found.
-   Zombies Processes - Monitors for any zombie processes which did not exit when killed. Critical if any processes are found.
### MySQL
The routine monitoring checks include:
-   Alert Log - Monitors a log file every X seconds and parses each line over a set of regex patterns. Critical if any events match.
-   File Size - {file_name} Monitors the size of a specific database file. Critical: 30gb, No warning.
    -   /apps/IPsoft/amelia/amelia-kdb-master/data/ACT_HI_ACTINST.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-master/data/ACT_HI_PROCINST.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-master/data/ACT_HI_VARINST.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-master/data/ACT_RU_EXECUTION.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-master/data/ACT_RU_METER_LOG.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-master/data/ACT_RU_VARIABLE.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-slave/data/ACT_HI_ACTINST.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-slave/data/ACT_HI_PROCINST.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-slave/data/ACT_HI_VARINST.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-slave/data/ACT_RU_EXECUTION.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-slave/data/ACT_RU_METER_LOG.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-slave/data/ACT_RU_VARIABLE.ibd
    -   /apps/IPsoft/amelia/amelia-kdb-master/mysqld.log
    -   /apps/IPsoft/amelia/amelia-kdb-slave/mysqld.log
-   Max Sessions
-   Open Tables
-   Questions Per Second
-   Slow Queries
-   Table Opening Rate
## RabbitMQ
The routine monitoring checks include:
-   Aliveness checks if rabbitmq is open to accept connections and data.
-   Connections checks the number of active connections.
-   Nodes checks the status of nodes.
-   Objects checks the number of objects in the cluster.
-   Overview checks the status of rabbitmq as defined by the software itself.
-   Partitions checks inner-cluster data partitions.
-   Queues checks the status and size of the queues.
-   Watermark checks disk space usage.
## Redis
The routine monitoring checks include:
-   Clients Blocked checks the number of clients where data is blocked.
-   Clients Connected checks the number of connected clients.
-   HitRatio checks the ratio of cache hits, for Perfdata Only.
-   Log Scrubber
-   Memory Frag Ratio checks the fragmentation ratio.
-   Memory Used
-   Memory Used LUA
-   Memory Used RSS
-   PerfData: AOF Current Size
-   PerfData: Evicted Keys
-   PerfData: Expired Keys
-   PerfData: Keyspace
-   PerfData: Keyspace Hits
-   PerfData: Keyspace Misses
-   PerfData: Operations per Second
-   Persistence
-   Uptime
## Linux Server
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
## Commands to Monitor Service Status
These commands report on the status of Amelia’s systems.
Table. Monitoring CLI Commands

| Service | Command |
| ----|----|
| Amelia (all) | systemctl status amelia-\* |
| amelia-account-service | systemctl status amelia-account.service |
| amelia-admin-service | systemctl status amelia-admin.service |
| amelia-admin-web | systemctl status amelia-admin-web.service |
| amelia-batch-service | systemctl status amelia-batch.service |
| amelia-duckling | systemctl status amelia-duckling.service |
| amelia-engine-service | systemctl status amelia-engine.service@p001 (where 001 is the pod number) |
| amelia-escalation-service | systemctl status amelia-escalation.service |
| amelia-integration | systemctl status amelia-integration.service |
| amelia-model-server | systemctl status amelia-model-server.service@p001 (where 001 is the pod number) |
| amelia-syntaxnet | systemctl status amelia-syntaxnet.service |
| amelia-user-web | systemctl status amelia-user-web.service |
| All services | systemctl status all-services |
| RabbitMQ | rabbitmqctl status |
| MySQL | service mysql status OR ps aux | grep mysql |

