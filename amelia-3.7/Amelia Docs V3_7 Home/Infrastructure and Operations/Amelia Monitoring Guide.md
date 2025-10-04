{% version "3.x" %}
# Overview
This document will cover each part of Amelia and how IPsoft monitors its systems. This document covers the checks, how they work, and their default values.
Depending on what each customer uses as their monitoring tool, adjustments will need to be made by their monitoring team. IPsoft monitors each core component as a separate host. This approach logically separates the component into groups that can be easily understood. In most deployments, all the components are installed on a single host. In some of the newer deployments some components may be split onto their own hosts.
This document covers the monolith style of deployment. To add monitoring for separate hosts, the client would simple need to deploy core operating system checks to each physical and virtual machine host.
# Component: ipsoft-av-gateway
This service scans for viruses any files uploaded with the Amelia interface. It was introduced with the Amelia 3.5 release and included in 3.6 and 3.7 releases.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – ipsoft-av-gateway
    -   Checks if a named process is running with a matching name of “amelia-account-service”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-account-service
The amelia-account-service handles users, user groups, roles, and authentication systems.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-account-service
    -   Checks if a named process is running with a matching name of “amelia-account-service”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-admin-service
The amelia-admin-service initializes the knowledge database (KDB) with default resources and runs scheduled jobs for classifiers and other resources.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-admin-service
    -   Checks if a named process is running with a matching name of “amelia-admin-service”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-admin-web
The amelia-admin-web component is the web interface for Amelia's administration pages.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-admin-web
    -   Checks if a named process is running with a matching name of “amelia-admin-web”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-batch-service
The amelia-batch-service generates periodic batch processing jobs for metrics and summary computations, as well as maintenance and cleaning.
Checks:
-   Log file age V3
    -   Checks if a file path has been modified within X seconds.
    -   Critical 300s, no warning.
    -   File: /apps/IPsoft/amelia/amelia-batch/var/log/amelia-batch.log
    -   This is polled via a shell command on the running host.
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-batch-service
    -   Checks if a named process is running with a matching name of “amelia-batch-service”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-duckling
This component uses the open source duckling service to handle multi-lingual date normalization tasks.
Checks:
-   Process – amelia-duckling
-   Checks if a named process is running with a matching name of “amelia-duckling”.
-   Critical: 1, no warning
-   This is polled via a shell command \`ps\` specific to the installed OS.
# Component: amelia-engine-service
amelia-engine-service is a core component responsible for powering Amelia.
Checks:
-   Amelia Engine Log File Age v3
    -   Checks if a file path has been modified within X seconds.
    -   Critical 300s, no warning.
    -   File: /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log
    -   This is polled via a shell command on the running host.
-   Amelia Mbean Perf - amelia.metrics:name counter.status.200.health
-   Amelia Mbean Perf - amelia.metrics:name gauge.response.health
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-engine-service
    -   Checks if a named process is running with a matching name of “amelia-engine-service”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-escalation-service
The amelia-escalation component escalates to a human operator chat conversations Amelia is unable to complete.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-escalation-service
    -   Checks if a named process is running with a matching name of “amelia-escalation-service”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-integration
This component creates, deploys, and uses flows that integrate third-party data synchronously with BPNs.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-integration-service
    -   Checks if a named process is running with a matching name of “amelia-integration-service”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-model-server
This component serves trained classifier models.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-model-server
    -   Checks if a named process is running with a matching name of “amelia-model-server”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
# Component: amelia-syntaxnet
This component provides linguistic analysis of sentences and syntactic dependency relations among words, as well as computes parts of speech tags.
Checks:
-   Java Process – amelia-syntaxnet
-   Checks if a named process is running with a matching name of “amelia-syntaxnet”.
-   Critical: 1, no warning
-   This is polled via a shell command \`ps\` specific to the installed OS.
# Component: amelia-user-web
The amelia-user-web component is the web interface for Amelia, including the custom user interface functionality formerly in the amelia-clientname-web service.
Checks:
-   File Descriptor Utilization
    -   Monitors the number open files the process currently has.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: OpenFileDescriptorCount of the mbean: java.lang:type=OperatingSystem
-   Garbage Collection - G1 Old Generation
    -   Automatically detects type and deploys proper mbean/attribute. CMS, G1, etc
    -   Monitors the length of time in seconds’ garbage collection ran.
    -   Critical 10s, Warning 5s
    -   This is polled via a JMX query for the mbean: java.lang:type=GarbageCollector
-   Heap Utilization
    -   Monitoring the java heap memory utilization.
    -   Critical and warning are dynamically calculated to be 95% and 90% of the system max.
    -   This is polled via a JMX query for the attribute: HeapMemoryUsage.used of the mbean: java.lang:type=Memory
-   Java Process – amelia-user-web
    -   Checks if a named process is running with a matching name of “amelia-user-web”.
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Nonheap Utilization
    -   Same as Heap utilization only with the attribute being NonHeapMemoryUsage.used
-   Amelia Web Log Scrubber
    -   Monitors a log file every X seconds and parses each line over a set of regex patterns
    -   Critical if any events match
    -   File: /apps/IPsoft/amelia/amelia-user-web/var/log/amelia-user-web.log
    -   This is polled via a script that runs on the shell of the running host.
    -   Rules: See “Amelia_web_logger” at the end of this document.
-   Amelia User Web Error
# Component: Host OS
This is the physical or virtual host system all the various components run on. The majority of the generic OS-level checks will exist here.
Checks:
-   Amelia Backup Log – {filepath}
    -   Monitors the backup tool for failures via a log scrubber. This is currently being phased out for remote offsite backups.
    -   Critical if any events match.
    -   File: dynamic, generally /apps/backup/amelia_mysql_backup.log
    -   This is polled via a script that runs on the shell of the running host.
    -   Rules: See “IPsoft-amelia_mysql_backup” at the end of this document.
-   Amelia SSL Expiry
    -   Monitors status of the SSL certification for expiration.
    -   Critical: 30d, Warning: 60d
    -   This is polled by using openssl and looking at the certificate chain.
-   Amelia Webcheck
    -   Monitors basic availability of Amelia but ensuring the basic web interface is online.
    -   Critical: non http 200 response.
    -   This is polled by hitting a dynamic URL and looking for a HTTP 200 return code.
-   Chrony Offset
    -   Monitors time sync drift between the local host and a defined time server.
    -   Critical: 5000ms, Warning: 2500ms
    -   This is polled interfacing with the chronyd shell
-   Disk – {partition_name}
    -   Monitors disk space usage per partition
    -   Critical: 95%, Warning: 90%
    -   This is polled reading the disk information from “df” and other sources.
-   HAProxy BackEnd
    -   Monitors the status of all HAproxy defined backends
    -   Critical: Status down or connection utilization above 80%
    -   This is polled by interfacing with the HAproxy “stats” socket.
-   HAProxy Frontend
    -   Same as backend only for Frontend
-   Host Memory
    -   Monitors the amount of free system memory
    -   Critical: 98%, Warning: 95%
    -   This is polled by looking at the /proc/meminfo data
-   Inodes - {partition_name}
    -   Monitors the inode usage per disk partition
    -   Critical: 90%, Warning 80%
    -   This is polled by reading the disk information from /proc
-   Linux Message Log
-   Monitors a log file every X seconds and parses each line over a set of regex patterns
    -   Critical if any events match
    -   File: /var/log/messages
    -   This is polled via a script that runs on the shell of the running host.
    -   Rules: See “Linux_Messages_Scrubber” at the end of this document.
-   Load Average
    -   Monitors the numbering of waiting threads in the system.
    -   This is only used for performance data so there are no warning/critical thresholds.
    -   This is polled by looking at the /proc data and using “ps”
-   Proc – {Process_name}
    -   Monitors the status of specific processes
    -   Critical: 1, no warning
    -   This is polled via a shell command \`ps\` specific to the installed OS.
    -   Process List:
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
-   Swap Usage
    -   Monitors the amount of swap being used.
    -   Critical: 90%, Warning: 80%
    -   This is polled by reading /proc/meminfo
-   TCP – {port_number}
    -   Monitors if the specific open is open for connections
    -   Critical is port is not open
    -   This is polled by attempting to open a socket to the port.
    -   Port List:
        -   80
        -   443
        -   23
-   Uninterruptable Processes
    -   Monitors for any processes which may be stuck for any reason.
    -   Critical if any processes are found
    -   This is polled via a shell command \`ps\` specific to the installed OS.
-   Zombies Processes
    -   Monitors for any zombie processes which did not exit when killed.
    -   Critical if any processes are found.
    -   This is polled via a shell command \`ps\` specific to the installed OS.
# app0\[1\].\[env\]-v3-\[client\].amelia.ipcenter.com
Internal naming convention for the application host level checks.
Checks:
-   Amelia Backup Log - /apps/backup
-   Amelia SSL Expiry
-   Amelia Webcheck
-   Amelia YUM Audit Log
-   Audit Size Test
-   Chrony Offset
-   Disk - /
-   Disk - /apps
-   Disk - /boot
-   Disk - /dev/shm
-   Disk - /run
-   Disk - /sys/fs/cgroup
-   Disk Latency
-   File Handle Usage
-   HAProxy Back End
-   HAProxy Front End
-   Host Memory
-   IPremoted Unix
-   Inodes - /
-   Inodes - /apps
-   Inodes - /boot
-   Inodes - /dev/shm
-   Inodes - /run
-   Inodes - /sys/fs/cgroup
-   Linux Messages Log
-   Load Average
-   Performance Data
-   Proc - chronyd
-   Proc - crond
-   Proc - haproxy
-   Proc - haproxy-systemd
-   Proc - mysqld
-   Proc - mysqld_safe
-   Proc - sshd
-   Proc - syslog
-   Proc - xinetd
-   SSH
-   Swap Usage
-   TCP - 443
-   TCP - 80
-   Total Procs
-   Touch - Monitoring Tracer
-   Uninterruptable Processes
-   Zombies
-   Amelia Backup Log - adb
-   Amelia Backup Log - cdb-p001
-   Amelia Backup Log - kdb_slave
# Component: MySQL Database
The relational database stores conversationd and other information in Amelia.
Checks:
-   Alert Log
    -   Monitors a log file every X seconds and parses each line over a set of regex patterns
    -   Critical if any events match
    -   File: /var/log/messages
    -   This is polled via a script that runs on the shell of the running host.
    -   Rules: See “IPsoft-ipcenter_mysql_alert_log” at the end of this document.
-   File Size – {file_name}
    -   Monitors the size of a specific database file
    -   Critical: 30gb, No warning
    -   Files:
        -   /apps/mysql/data/amelia/ACT_HI_ACTINST.ibd
        -   /apps/mysql/data/amelia/ACT_HI_PROCINST.ibd
        -   /apps/mysql/data/amelia/ACT_HI_VARINST.ibd
        -   /apps/mysql/data/amelia/ACT_RU_EXECUTION.ibd
        -   /apps/mysql/data/amelia/ACT_RU_METER_LOG.ibd
        -   /apps/mysql/data/amelia/ACT_RU_VARIABLE.ibd
    -   This is polled via looking at the size of a file path.
-   Max Sessions
    -   Monitors the number of active sessions/connects to the database server.
    -   Critical: 900, Warning 750
    -   This is polled by querying the database for the number of active connections.
        -   Query: show status like 'Threads_connected'
-   Open Tables
    -   Monitors the number of table tables.
    -   Critical: 18000, Warning: 13000
    -   This is polled by querying the database for the number of open tables.
        -   Query: show global status like 'Open_tables'
-   Questions per Second
    -   Monitors the number of queries per second.
    -   Critical: 10000, Warning: 9000
    -   This is polled by querying the database for the number of queries in the past second.
        -   Query: show global status like 'Questions'
-   Slow Queries
    -   Monitors the number of queries that exceed the warning/critical thresholds.
    -   Critical: 20s, Warning: 10s
    -   This is polled by querying the database for the number of active queries exceeding the thresholds.
        -   Query: show global status like 'Slow_queries'
-   Table Opening Rate
    -   Monitors the number of tables that open between polling cycles.
    -   Critical: 5000, Warning: 3000
    -   This is polled by looking at the number of open tables between two polling cycles.
        -   Query: show global status like 'Opened_tables'
# apps-IPsoft-amelia-amelia-adb-data - Port 13345
Authentication SQL database.
Checks:
-   MySQL Alert Log
-   MySQL Max Sessions
-   MySQL Open Tables
-   MySQL PerfData
-   MySQL Questions Per Second
-   MySQL Slow Queries
-   MySQL Uptime
# apps-IPsoft-amelia-amelia-cdb-p001-data - Port 13325
Conversation database POD.
Checks:
-   MySQL Alert Log
-   MySQL Max Sessions
-   MySQL Open Tables
-   MySQL PerfData
-   MySQL Questions Per Second
-   MySQL Slow Queries
-   MySQL Uptime
# apps-IPsoft-amelia-amelia-kdb-master-data - Port 13305
Knowledge database master.
Checks:
-   MySQL Alert Log
-   MySQL Max Sessions
-   MySQL Open Tables
-   MySQL PerfData
-   MySQL Questions Per Second
-   MySQL Slow Queries
-   MySQL Uptime
# apps-IPsoft-amelia-amelia-kdb-slave-data - Port 13315
Knowledge database slave.
Checks:
-   MySQL Alert Log
-   MySQL Max Sessions
-   MySQL Open Tables
-   MySQL PerfData
-   MySQL Questions Per Second
-   MySQL Slow Queries
-   MySQL Uptime
-   MySQL Slave Replication Status V3
-   MySQL Long Running Query
# Component: RabbitMQ - Port 13351
RabbitMQ provides a messaging service between other components.
Checks:
-   Aliveness
    -   Sends and receives a test message to confirm RabbitMQ is functional.
    -   No thresholds
    -   This is polled by interfacing with the RabbitMQ API and sending a test message to a test queue. If the message is received back the check returns ok.
-   Connections
    -   Monitors the number of active connections.
    -   Critical: 750, Warning: 500
    -   This is polled by interfacing with the RabbitMQ API and polling the number of active connections API endpoint.
-   Nodes
    -   Monitors the number and state of nodes in a RabbitMQ cluster.
    -   This check has 4 thresholds, each uses critical: 90 and warning: 80
        -   Msg_count: total number of messages in the message bus.
        -   Msg_ready_count: total ready to be received messages.
        -   Msg_unack_count: total message sent but not acknowledged by the recipient.
        -   Consumer_count: total number of consumers attached to the bus.
    -   This is polled by interfacing with the RabbitMQ API and polling the node status and connection status endpoints.
-   Objects
    -   Number of vhosts, exchanges, bindings, queues, and channels
    -   vhosts: 1, exchanges: 15, bindings: 38, queues: 20, channels: 71
-   Overview
    -   Monitors the overall health of RabbitMQ as reported by it’s internal API.
    -   No thresholds
    -   This is polled by interfacing with the RabbitMQ API and polling the status endpoint.
-   Partitions
    -   Monitors for any network partitions between RabbitMQ cluster nodes.
    -   No threshold
    -   This is polled by interfacing with the RabbitMQ API and polling the node status endpoint.
-   Queues
    -   Monitors the status and size of all defined queues on the RabbitMQ cluster.
    -   This check has 4 thesholds, Critical: 100,100,100,-1 and Warning: 50,50,50,-1
    -   “-1” tells the check to not enforce the threshold.
        -   Msg_count: total number of messages in the message bus.
        -   Msg_ready_count: total ready to be received messages.
        -   Msg_unack_count: total message sent but not acknowledged by the recipient.
        -   Consumer_count: total number of consumers attached to the bus.
    -   This is polled by interfacing with the RabbitMQ API and polling the queue status endpoint.
-   Watermark
    -   Monitors the internal health checks performed by RabbitMQ for cpu/disk/memory levels.
    -   No thresholds, these are defined inside of RabbitMQ.
    -   This is polled by interfacing with the RabbitMQ API and polling the node status endpoint.
# Component: Redis - Port 13341
Purpose: Temporary in-memory storage for Amelia data.
Checks:  All of these checks are polled by a custom shell script that interfaces with the redis-cli.
-   Clients Blocked
    -   Monitors the number of connected clients which are blocked for any reason.
    -   Critical: 10, Warning: 5
-   Clients Connected
    -   Monitors the number of connected clients in any state.
    -   No thresholds, performance data only.
-   HitRatio
    -   Monitors the performance of the SET vs GET actions for cache efficiency
    -   No thresholds, performance data only.
-   Log Scrubber
-   Monitors a log file every X seconds and parses each line over a set of regex patterns.
    -   Critical if any events match
    -   File: /var/log/redis/redis.log
    -   This is polled via a script that runs on the shell of the running host.
    -   Rules: See “amelia_redis_log” at the end of this document.
-   Memory Fragmentation Ratio
    -   Monitors the ratio of memory fragmentation.
    -   No threshold, performance data only.
-   Memory Used
    -   Monitors the amount of total memory consumed by Redis
    -   No threshold, performance data only.
-   Memory Used LUA
    -   Monitors the amount of LUA memory consumed by Redis
    -   No threshold, performance data only.
-   Memory Used RSS
    -   Monitors the amount of RSS memory consumed by Redis
    -   No threshold, performance data only.
-   PerfData: AOF Current Size
-   PerfData: Evicted Keys
-   PerfData: Expired Keys
-   PerfData: Keyspace
-   PerfData: Keyspace Hits
-   PerfData: Keyspace Misses
-   PerfData: Operations per Second
-   Persistence
    -   Monitors the data of the disk backup for the in-memory objects.
    -   No threshold, performance data only.
-   Uptime
    -   Monitors the uptime of redis
    -   No threshold, performance data only.
# Log Scrubber Config Files
All config use this format: unique_name;state;min matches;max matches;regular expression to match
## Amelia_engine_logger
``` bash
FAILED TO LEARN PROCESS OK;OK;1;;.*Failed to learn process.*
LEARNED MODELS OK;OK;1;;.*Error obtaining learned models for conversation.*
IGNORE;OK;1;;.*Exception while executing runnable.*
IGNORE1;OK;1;;.*No such property: difference for class.*
IGNORE2;OK;1;;.*Duplicate entry.*
NETWORK UNAVAILABLE;CRITICAL;1;;.*io.grpc.StatusRuntimeException: UNAVAILABLE: Network closed for unknown reason.*
ERROR;CRITICAL;1;;^\d{4}-[0-1]\d-[0-3]\d\s[0-2]\d:[0-5]\d:[0-5]\d\.\d{3}\sERROR(?!.*AMELIA_ENGINE_SIMPLE_REPEATING)(?!.*n\.i\.a\.engine\.quartz\.SessionStateMachine)(?!.*INFO\s\d+\s\-\-\-\s\[MessageBroker\-\d+\]\so\.s\.w\.s\.c\.WebSocketMessageBrokerStats)(?!.*Failed\sto\sack\sor\sclose\ssession)(?!.*while\sclosing\scommand\scontext)(?!.*script-logger.*)
Huge Grammar;CRITICAL;3;;.*Storing regular expression.*huge.*
```
## Amelia_liveperson_logger
``` bash
ignore1;OK;1;;.*WebSocketClientSockJsSession.*
Authorization failure;CRITICAL;3;;.*DEBUG.*Authorization.*
ERROR;CRITICAL;1;;^\d{4}-[0-1]\d-[0-3]\d\s[0-2]\d:[0-5]\d:[0-5]\d\.\d{3}\sERROR(?!.*Ignoring\sreceived\smessage\sdue\sto\sstate=CLOSED).*
Error Polling;CRITICAL;10;;.*Error while polling for incoming chat request in listener.*
Authorization failure;CRITICAL;3;;.*DEBUG.*Authorization.*
ERROR;CRITICAL;1;;.*AgentStatus-0.*
```
## Amelia_redis_log
``` bash
RDB Error;CRITICAL;1;;.*Background saving error.*
Disk Full;CRITICAL;1;;.*No space left.*
RDB Write Error;CRITICAL;1;;.*Write error saving DB.*
Master connection lost;CRITICAL;1;;.*Connection with master lost.*
Read Only ERROR;CRITICAL;1;;.*RedisCommandExecutionException: READONLY.*
```
## Amelia_web_logger
``` bash
Error calling method;OK;1;;.*Error calling method: load.*
SQLErrorCodesFactory;CRITICAL;1;;.*Error while extracting database.*
MultimediaFileObjectService;CRITICAL;1;;.*Failed to check file metadata.*
AmeliaProviderManagerImpl;CRITICAL;12;;.*Failed to refresh Authentication.*
LynxEngine Huge Grammar;CRITICAL;1;;.*Huge regular expression.*
SqlExceptionHelper;CRITICAL;1;;.*SQL Error.*
Lost connection to Redis Sentinel;CRITICAL;1;;.*Lost connection to Sentinel.*
Connection timeout;CRITICAL;1;;.*Closing XhrStreamingSockJsSession[id=snmtkkx4].*
```
## Generic-JVM-Log
``` bash
Failed to login to JabberBot;CRITICAL;1;;Failed to login to JabberBot
OutOfMemoryError;CRITICAL;1;;java.lang.OutOfMemoryError
DB Connection Error;CRITICAL;1;;.*marked as broken because of.*
DB Not Prepared;CRITICAL;1;;.*WSREP has not yet prepared node for application use.*
REST GW Dropped webhook messages;CRITICAL;50;;.*WARN.*n.i.a.c.m.h.WebhookPostingMessageHandler.*Dropping stale message.*
ERROR JournalPersistenceAdapter;CRITICAL;4;;Failed to checkpoint a message store
Eliza Illegal State Exception;CRITICAL;1;;java.lang.IllegalStateException: Unexpected event after connect: \[null\]
Dispatch was rejected.  Queue probably full;CRITICAL;50;;Dispatch was rejected.  Queue probably full
IPim posts failing in automata;CRITICAL;5;;UpdateTicketAction WARN - Failed to get an IPim ticket in
Exhausted JDBC pool;CRITICAL;1;;org.springframework.jdbc.UncategorizedSQLException: Hibernate operation: Cannot open connection.*uncategorized SQLException for SQL
Cannot Acquire DB Connections;CRITICAL;3;;Caused by: java.sql.SQLException: Connections could not be acquired from the underlying database!
Communications Link Failure;CRITICAL;3;;Caused by: com.mysql.jdbc.exceptions.jdbc4.MySQLNonTransientConnectionException: Communications link failure
Last Packet Sent;CRITICAL;3;;Last packet sent to the server was.*ago
Increase MaxThreads;CRITICAL;3;;SEVERE: All threads (\d+) are currently busy, waiting. Increase maxThreads (\d+) or check the servlet status
Bean;CRITICAL;1;;Error creating bean with name
Link to OCS IM Disconnected;CRITICAL;1;;JBuddyBot WARN – lost connection.*NETWORK ERROR
Too many Open Files;CRITICAL;1;;java.io.IOException: Too many open files
ConcurrentModeFailure;CRITICAL;3;;.*concurrent mode failure.*
ConcurrentModeFailure;WARNING;2;;.*concurrent mode failure.*
LDAP Connection Failed;CRITICAL;12;;.*com.sun.jndi.ldap.LdapClientFactory.createPooledConnection.*
RoutingService;Critical;1;;.*RoutingService WARN - Pending 15001, skipping.*
Javax SSLException;Critical;1;;javax.net.ssl.SSLException: hostname in certificate didn't match
Read Only Redis;Critical;1;;.*READONLY You can’t write against a read only slave.*
saw deaths of mirrors;CRITICAL;1;;saw deaths of mirrors
REST gateway dropping message;CRITICAL;1;;.*Dropping stale message.*
```
## IPsoft-amelia_mysql_backup
``` bash
Ignore metric;OK;1;;.*metric_job_error.frm.*
Ignore metric2;OK;1;;.*metric_job_error.ibd.*
Ignore statements;OK;1;;.*statements_with_errors_or_warnings.frm.*
Insufficient disk space;CRITICAL;1;;.*No space left on device.*
Backup Failed;CRITICAL;1;;.*Error.*
```
## IPsoft-amelia_rabbitmq_splitbrain
Also see the rabbitmq log at the bottom of this page.
``` bash
RabbitMQ Splitbrain1;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Cancel received for.*
RabbitMQ Splitbrain2;CRITICAL;1;;.*Exception summary: org.springframework.amqp.rabbit.support.ConsumerCancelledException.*
RabbitMQ Splitbrain3;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Failed to declare queue.*
RabbitMQ Splitbrain4;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Queue declaration failed; retries left=.*
RabbitMQ Splitbrain5;CRITICAL;1;;.*o.s.a.r.l.SimpleMessageListenerContainer : Consumer received fatal exception on startup.*
RabbitMQ Splitbrain6;CRITICAL;1;;.*SimpleMessageListenerContainer : Failed to check/redeclare auto-delete.*
RabbitMQ Splitbrain7;CRITICAL;1;;.*no binding.*
RabbitMQ Splitbrain8;CRITICAL;1;;.*starting_partitioned_network.*
RabbitMQ Splitbrain9;CRITICAL;1;;.*inconsistent_database.*
RabbitMQ Splitbrain10;CRITICAL;1;;.*running_partitioned_network.*
RabbitMQ Splitbrain11;CRITICAL;1;;.*Partial partition detected.*
RabbitMQ Splitbrain12;CRITICAL;10;;.*STOMP error frame sent.*
RabbitMQ Splitbrain13;CRITICAL;1;;.*Processing error.*
RabbitMQ Splitbrain14;CRITICAL;1;;.*timed out flushing while connection closing.*
```
## IPsoft-amelia_user_web_log
``` bash
Health check failed;CRITICAL;10;;.*Health check failed.*
```
## IPsoft-amelia-yum_log
``` bash
RPM Updated via YUM;CRITICAL;1;;.*Updated.* (?!.*amelia.*)
RPM Erased via YUM;CRITICAL;1;;.*Erased.* (?!.*amelia.*)
RPM Installed via YUM;CRITICAL;1;;.*Installed.* (?!.*amelia.*)
```
## IPsoft-haproxy_logger
``` bash
ERROR;CRITICAL;1;;.*ERROR.*
BOGUS VRRP;CRITICAL;1;;.*bogus\sVRRP\spacket\sreceived.*
INVALID IP COUNT;CRITICAL;1;;.*received/san\sinvalid\sip\snumber\scount.*
```
## IPsoft-ipcenter_mysql_alert_log
``` bash
Failing assertion;CRITICAL;1;;.*InnoDB: Failing assertion: btr_page_get_prev.*
CRIT_delete_markwas;CRITICAL;1;;.*InnoDB: Unable to find a record to delete-markwas not found on update.*
CRIT_page_corruption;CRITICAL;1;;.*InnoDB: Database page corruption on disk or a failed file read of page.*
CRIT_corrupt_database;CRITICAL;1;;.*InnoDB: Aborting because of a corrupt database page in the system tablespace.*
WARNING IP;OK;1;;.*[Warning].*IP.*address.*
FATAL ERROR DETECTED;CRITICAL;1;;.*FATAL.*
POSSIBLE SQL CRASH;CRITICAL;1;;.*This could be because you hit a bug.*
ASSERTION FAILURE;CRITICAL;1;;.*Assertion failure in thread.*
OK1;OK;1;;Aborted connection .* to db: .* user: .* host: .* \(Got (an error|timeout) (reading|writing) communication packets\)
OK2;OK;1;;Start binlog_dump to slave_server
IGNORE_slave_SQL_thread_was_killed;OK;100;;slave SQL thread was killed
IGNORE_Slave_SQL_thread_initialized;OK;100;;Slave SQL thread initialized
IGNORE_Incorrect_key_file_for_table;OK;100;;Incorrect key file for table
IGNORE_statement_is_not_safe_to_log_in_statement_format;OK;1;;Statement is not safe to log in statement format
IGNORE_Unsafe_statement_written_to_the_binary_log_using_statement_format;OK;1;;Unsafe statement written to the binary log using statement format
IGNORE_Start_binlog_dump_to_slave_server;OK;1;;Start binlog_dump to slave_server
IGNORE_Slave_SQL_thread_exiting;OK;1;;Slave SQL thread exiting
IGNORE_Got_an_error_from_unknown_thread;OK;1;;Got an error from unknown thread
IGNORE_Sort_aborted;OK;1;;Sort aborted
IGNORE_Query_execution_was_interrupted;OK;1;;Query execution was interrupted
IGNORE_Access_denied_for_user;OK;1;;Access denied for user
IGNORE_Created_page;OK;1;;Created page
IGNORE_turning_message_relay_requesting:on;OK;1;;turning message relay requesting on
IGNORE_referenced_FK_check_fail;OK;1;;referenced FK check fail
IGNORE_WSREP_could_not_find_key;OK;;WSREP: could not find key
CRITICAL;CRITICAL;1;;.*ERROR.*
```
## LDAP_failure
``` bash
LDAP_FAILURE3;CRITICAL;1;;^(?!.*\[sssd\[be\[LDAP\]\]\]).*LDAP_FAILURE.*
LDAP_FAILURE;CRITICAL;1;;.*ldap_result\serror.*
LDAP_FAILURE2;CRITICAL;1;;.*Failed.to.retrieve.users.*
```
## Linux_Messages_Scrubber
``` bash
Ignore vmc memory alerts;OK;1;;vmc0.*$domain Unknown: out of memory
SAN ERROR;CRITICAL;1;;RSCN database changed
NETWORK_ISSUE;CRITICAL;1;;link is not ready
FRAME_ERROR;CRITICAL;1;;frame dropped
SAN ERROR2;CRITICAL;1;;LOOP DOWN
Out of Memory;CRITICAL;1;;Out of Memory
SCSI error;CRITICAL;1;;SCSI error
Disk Failure;CRITICAL;1;;Disk failure
POSSIBLE_HARDWARE_ISSUE;CRITICAL;1;;Hardware Error
OVPN_PACKET_ERROR;CRITICAL;1;;openvpn .*: Authenticate/Decrypt packet error: packet HMAC authentication failed
OVPN_FATAL_DECRYPTION_ERROR;CRITICAL;1;;openvpn .*\: Fatal decryption error \(process_incoming_link\), restarting
OVPN_SIGUSR1;CRITICAL;1;;openvpn .*\: SIGUSR1\[soft,decryption-error\] received, process restarting
PowerDNS Security Update Mandatory;CRITICAL;1;;PowerDNS Security Update Mandatory
BLAS_INSTALLED;CRITICAL;1;;undefined symbol
```
## rabbitmq
Also see the IPsoft-amelia_rabbitmq_splitbrain log above.
``` bash
RabbitMQ Splitbrain1;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Cancel received for.*
RabbitMQ Splitbrain2;CRITICAL;1;;.*Exception summary: org.springframework.amqp.rabbit.support.ConsumerCancelledException.*
RabbitMQ Splitbrain3;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Failed to declare queue.*
RabbitMQ Splitbrain4;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Queue declaration failed; retries left=.*
RabbitMQ Splitbrain5;CRITICAL;1;;.*o.s.a.r.l.SimpleMessageListenerContainer : Consumer received fatal exception on startup.*
RabbitMQ Splitbrain6;CRITICAL;1;;.*SimpleMessageListenerContainer : Failed to check/redeclare auto-delete.*
RabbitMQ Splitbrain7;CRITICAL;1;;.*no binding.*
RabbitMQ Splitbrain8;CRITICAL;1;;.*starting_partitioned_network.*
RabbitMQ Splitbrain9;CRITICAL;1;;.*inconsistent_database.*
RabbitMQ Splitbrain10;CRITICAL;1;;.*running_partitioned_network.*
RabbitMQ Splitbrain11;CRITICAL;1;;.*Partial partition detected.*
RabbitMQ Splitbrain1;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Cancel received for.*
RabbitMQ Splitbrain2;CRITICAL;1;;.*Exception summary: org.springframework.amqp.rabbit.support.ConsumerCancelledException.*
RabbitMQ Splitbrain3;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Failed to declare queue.*
RabbitMQ Splitbrain4;CRITICAL;1;;.*o.s.a.r.listener.BlockingQueueConsumer   : Queue declaration failed; retries left=.*
RabbitMQ Splitbrain5;CRITICAL;1;;.*o.s.a.r.l.SimpleMessageListenerContainer : Consumer received fatal exception on startup.*
RabbitMQ Splitbrain6;CRITICAL;1;;.*SimpleMessageListenerContainer : Failed to check/redeclare auto-delete.*
RabbitMQ Splitbrain7;CRITICAL;1;;.*no binding.*
RabbitMQ Splitbrain8;CRITICAL;1;;.*starting_partitioned_network.*
RabbitMQ Splitbrain9;CRITICAL;1;;.*inconsistent_database.*
RabbitMQ Splitbrain10;CRITICAL;1;;.*running_partitioned_network.*
RabbitMQ Splitbrain11;CRITICAL;1;;.*Partial partition detected.*
```
## Percona/MySQL
Marked as broken because of SQLSTATE. WSREP has not yet prepared node for application use to trigger an alarm
``` groovy
** ERROR ** mnesia_event got {inconsistent_database, running_partitioned_network, rabbit@app01}
```
{% /version %}
