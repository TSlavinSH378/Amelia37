{% version "3.x" %}
If an alert identifies an Amelia system, or the basic system troubleshooting has not resolved a problem, these procedures describe how to identify and resolve issues within the Amelia system.
# Amelia Restart SOPs
There are several checks that require restarts of the different Amelia components. The following alerts require a restart.
## [R](https://paas.ipcenter.com/IPmon/NY1-IPmon24/cgi-bin/extinfo.cgi?type=2&host=amelia-engine.metlife-amelia-prod.ipsoft.com.ipsoft&service=Amelia+Response+Time)esponse Time Alert
The Amelia response time alert will go critical immediately if the response time is \> 20 seconds. This means that its taking more than 20 seconds for the Amelia engine to respond to the customer interacting with her.
If this happens after an Amelia engine restart, the first step is to log into Amelia's production URL and start a conversation with her.  This causes the Mbean to register upon instantiation of the conversation.
If starting a conversation does not work, restart amelia-engine and amelia-web services then check their status to verify the run properly.
``` bash
systemctl restart amelia-engine.service@p001 (where 001 is the pod number)
systemctl restart amelia-admin-web
systemctl restart amelia-user-web
systemctl restart amelia-admin-service
systemctl status amelia-engine.service@p001 (where 001 is the pod number)
systemctl status amelia-admin-web
systemctl status amelia-user-web
systemctl status amelia-admin-service
```
## Garbage Collector Q1 Old Generation Alert
If this alert appears, restart the amelia-engine and amelia-web services with these commands then check status to confirm they run properly:
``` bash
systemctl restart amelia-engine.service@p001 (where 001 is the pod number)
systemctl restart amelia-admin-web
systemctl restart amelia-user-web
systemctl restart amelia-admin-service
systemctl status amelia-engine.service@p001 (where 001 is the pod number)
systemctl status amelia-admin-web
systemctl status amelia-user-web
systemctl status amelia-admin-service
```
## Amelia V3 Webcheck Alert
This alert indicates Amelia's web interface front end is down.
1.  Log into Amelia's production URL to check the web interface is visible and functions.
2.  Check the IPmon for related issues. If the disk is full, for example, restarting the web service is ineffective.
3.  Verify all other possible issues are explored before restarting the amelia-web services. 
``` bash
systemctl restart amelia-user-web.service
systemctl restart amelia-admin-web.service
```
> [!info]  
>
> If you cannot access the web interface with the named URL BUT you are able to access via IP address, the alert likely is caused by an DNS/Load balancer issue.

## Chrony Offset Alert
This alert is received for any Amelia based alerts unable to be resolved by automation.
1.  SSH into the host using the hostname and switch to root using the sudoscript ss command.
2.  Run the following command:
    ``` bash
    chronyc -a 'burst 4/4'
    ```
3.  To see the peers, run the following chronyc command:
    ``` bash
    [root@app01.dev-ihg.amelia.ipcenter.com:2 alandry]# chronyc sources
    210 Number of sources = 5
    MS Name/IP address         Stratum Poll Reach LastRx Last sample
    ===============================================================================
    ^- ntp1.svc.ipsoft.com           3   6    17     1   -244us[ -244us] +/-  114ms
    ^- 4.144.155.104.bc.googleus     3   6    17     1  +1635us[+1276us] +/-  100ms
    ^- paladin.latt.net              2   6    17     1  +6443us[+6084us] +/-   99ms
    ^- clocka.ntpjs.org              2   6    17     1   +639us[ +280us] +/-   26ms
    ^* pool-173-71-69-90.cmdnnj.     1   6    17     1  -1007us[-1366us] +/- 5491us
    ```
4.  This will output the peers, their status, stratum, and delay (noted as Last sample in the final column).  us=microseconds ms=milliseconds s=seconds
5.  If that doesn't recover your alert after 5 minutes, then try the following:
    ``` bash
    systemctl restart chronyd
    ```
    You may see a 'no peer found' type message.  If so, very possibly the service is healing itself.  Give the system several more minutes or a half hour before continuing to step 3.
## Upload File 503 Errors
When files do not upload and an unknown or 503 error displays, the problem could be anti-virus software included with Amelia that checks files before they upload. If the anti-virus software is not running or otherwise not functioning, files will not upload.
The ipsoft-av-gateway service sometimes does not restart properly because the systemd unit file, <clamd@av-gateway.servic>e, is static. This can be confirmed with this command:
``` groovy
systemctl list-unit-files | grep -e clamd -e av-gateway
```
which generates this output:
``` groovy
clamd@.service                                static
clamd@scan.service                            disabled
ipsoft-av-gateway.service                     enabled
```
For hosts with ipsoft-av-gateway.service installed, run this command in a root shell:
``` groovy
echo -e "[Unit]\nRequires=clamd@av-gateway.service" | SYSTEMD_EDITOR=/usr/bin/tee systemctl edit ipsoft-av-gateway.service
```
To start the ipsoft-av-gateway service one time in the root shell, run these commands:
``` groovy
systemctl restart ipsoft-av-gateway.service
sleep 30
systemctl status ipsoft-av-gateway.service
```
This one line command combines both steps:
``` groovy
echo -e "[Unit]\nRequires=clamd@av-gateway.service" | SYSTEMD_EDITOR=/usr/bin/tee systemctl edit ipsoft-av-gateway.service; systemctl restart ipsoft-av-gateway; sleep 30; systemctl status ipsoft-av-gateway
```
### Scenario 1: Restarted in Incorrect Order
Run clam-freshclam first. Then restart the <clamd@av-gateway.servic>e and test to upload a file within the front-end.
### Scenario 2: Can't Stop Anti-Virus Service
Possible need to Kill that PID and then restart the service with this command in a root shell:
``` groovy
# systemctl restart clam-freshclam.service clamd@av-gateway.service ipsoft-av-gateway.service
```
### Scenario 3: On-Premise, Unable to To Run
Edit the /apps/IPsoft/amelia/amelia-common-config/application.properties file, add this line with this command in a root shell:
``` groovy
# echo amelia.file.virus-scan.enabled=false >> /apps/IPsoft/amelia/amelia-common-config/application.properties
```
then restart user-web and admin-web with this command in a root shell:
``` groovy
# systemctl restart amelia-user-web amelia-admin-web
```
### Scenario 4: On-Premise, Port Blocked
If Amelia is installed at the client's location, check definition updates over port 80 are not blocked. 
A firewall rule is probably in place, as its unable to connect to (104.16.186.138) [database.clamav.net](http://database.clamav.net) on port 80 and generates this error:
`ClamAV health check failed for 127.0.0.1:3310`
Check the /etc/haproxy/haproxy.cfg file is correct.
### Scenario 5: Multiple Issues with File Uploads/Downloads
Check the anti-virus gateway files in the /apps/IPsoft/ipsoft-av-gateway/config/jmx/ folder.
If there are no files in this directory, run these commands in a root shell:
``` groovy
# cp /apps/IPsoft/amelia/amelia-engine-service/config-p001/jmx/* /apps/IPsoft/ipsoft-av-gateway/config/jmx/
# chown ipsoft:ipsoft /apps/IPsoft/ipsoft-av-gateway/config/jmx/*
# chmod 600 /apps/IPsoft/ipsoft-av-gateway/config/jmx/*
```
Once the jmx files appear in the folder, restart the services in the following order:
``` groovy
# systemctl restart clam-freshclam.service clamd@av-gateway.service ipsoft-av-gateway.service
```
## Restart Amelia Core
Should you need to restart Amelia Core, please use the following procedure:
1.  Log into Amelia, become root using the sudoscript ss command, then issue this command:
    ``` bash
    systemctl restart amelia-engine.service@p001 (where 001 is the pod number)
    ```
2.  Please wait patiently, this process may take a few minutes.
3.  Next, issue this command to restart Amelia core:
    ``` bash
    systemctl restart amelia-user-web.service
    systemctl restart amelia-admin-web.service
    systemctl restart amelia-admin-service
    ```
4.  Then verify the Amelia Services are up and running with these commands:
    ``` bash
    systemctl status amelia-engine.service@p001 (where 001 is the pod number)
    systemctl status amelia-user-web.service
    systemctl status amelia-admin-web.service
    systemctl status amelia-admin-service
    ```
5.  Once you have confirmed the process completes, verify Amelia's integrity by logging into your Amelia web portal.
## Restart All Amelia Components
In the highly unlikely event a complete restart of all Amelia components is needed, a system reboot is the best option. However, there is a component-by-component restart process that can be used for troubleshooting.
> [!warning]  
>
> This process should never be used because a reboot is the best way to fully restart all components of Amelia. We are placing this process here so that users may become familiar with the general dependencies required for each service. These steps are the same flow that systemd uses to start Amelia upon system boot.

Table. Start/Restart Dependencies

| Service | Description |
| ----|----|
| amelia-admin-service | Creates a kdb the first time it is run |
| amelia-account-service | Needed for amelia-admin-web and amelia-user-webCreates an adb the first time it is run |
| admin-web | Requires a kdb to be created first |
| amelia-user-web | Creates a cdb the first time it is run |
| amelia-model | Requires a kdb to be created first |
| amelia-engine-service | Requires kdb-slave and cdb to be created first |

Shutdown all components of Amelia in this order, one by one:
``` bash
systemctl stop amelia-syntaxnet
systemctl stop amelia-user-web
systemctl stop amelia-model-server@p001 (where 001 is the pod number)
systemctl stop amelia-integration-service
systemctl stop amelia-batch.service
systemctl stop amelia-escalation.service
systemctl stop amelia-web.service
systemctl stop amelia-engine.service@p001 (where 001 is the pod number)
systemctl stop amelia-account-service
systemctl stop amelia-admin-service
systemctl stop amelia-h20
systemctl stop redis-sentinel.service
systemctl stop redis.service
systemctl stop rabbitmq-server.service
systemctl stop haproxy.service
systemctl stop mysql.service
```
You will then reverse this process, one by one, to start each component process:
``` bash
systemctl start mysql.service
systemctl start haproxy.service
systemctl start rabbitmq-server.service
systemctl start redis.service
systemctl start redis-sentinel.service
systemctl start amelia-h20
systemctl start amelia-admin-service
systemctl start amelia-account-service
systemctl start amelia-engine.service@p001 (where 001 is the pod number)
systemctl start amelia-web.service
systemctl start amelia-escalation.service
systemctl start amelia-batch.service
systemctl start amelia-integration-service
systemctl start amelia-model-server@p001 (where 001 is the pod number)
systemctl start amelia-user-web
systemctl start amelia-syntaxnet
```
In addition, Amelia instance that include a custom user interface need to stop then start the custom UI service. The service name varies and uses the file name format amelia-company_name-web where company_name is the full or shortened customer name.
## Managing Log Files
Common log files and and log files for amelia-engine, amelia-admin-web, and amelia-user-web can be used to extract data.
## Location of Common Log Files
The most common log files are at these locations on the server:
-   /apps/IPsoft/amelia/amelia-admin-web/var/log/amelia-admin-web.log
-   /apps/IPsoft/amelia/amelia-user-web/var/log/amelia-user-web.log
-   /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log (where 001 is the pod number)
There could be other log and system files to check and preserve, for example, escalation logs for escalated chats. These are described in Appendix A.
## Files for amelia-engine, amelia-admin-web, and amelia-user-web
To to tail the amelia-engine-service log file after login as root:
``` bash
sudo -i
tail -f -n 500 /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log (where 001 is the pod number)
```
To tail the amelia-admin-web log file after login as root:
``` bash
sudo -i
tail -f -n 500 /apps/IPsoft/amelia/amelia-admin-web/var/log/amelia-admin-web.log
```
To tail the amelia-user-web log file after login as root:
``` bash
sudo -i
tail -f -n 500 /apps/IPsoft/amelia/amelia-user-web/var/log/amelia-user-web.log
```
## BPN Script Errors
Errors from BPN script tasks appear in Amelia's error log files and include a stack trace. Refer to the Amelia User Guide for information on how to add error message reporting from BPN script tasks to appear in Amelia's Mind interface.
## Using grep to Find Problems
Use the grep command to try and find specific errors. For example, these commands can help locate an authentication error or activity from a specific date:
``` bash
tail -n 1000 /apps/IPsoft/amelia/amelia-admin-web/var/log/amelia-admin-web.log | grep AUTHENTICATION_SUCCESS
tail -n 1000 /apps/IPsoft/amelia/amelia-user-web/var/log/amelia-user-web.log | grep AUTHENTICATION_SUCCESS
tail -n 2000 /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log | grep 2016-12-22
```
> [!warning]  
>
> For the engine log folder, the p001 folder file name is for pod numbered 001. Update the pod number folder name if needed.

The following terms can be used with the grep command to find possible issues in log files:

| Search Term | Log File to Search | Description |
| ----|----|----|
| not avail | amelia-engine.log | Find errors caused by lack of availability. |
| conversation ID | amelia-engine.log | If you have an ID, use it to isolate any errors in a conversation. |
| Unable to evaluate script | amelia-engine.log | Find script-related errors |
| in huge cache | amelia-engine.log | Find grammar files that generate excessively large cache storage. |
| Too large | amelia-engine.log | Find errors caused by large data size. |
| error | any log file |  |
| invalid | any log file |  |
| oom | any log file | Out of memory errors |
| 404, 501, etc | web log files | Common web server errors |
| <file path> | any log file | Search for mention of a specific <file path> |
| <service name> | any log file | Search for mention of a specific <service name> |

See [Appendix A](https://docs.amelia.com/display/AmeliaDocsV2/Appendix+A%3A+Log+File+Locations) for the location of log files used by the Amelia system.
# HAProxy Back or Front End
If haproxy back or front end is down, type these commands to restart haproxy followed by restarts of amelia-engine@p001 and amelia-user-web@p001. The p001 suffix refers to the specific pod number.
``` bash
systemctl restart haproxy
systemctl restart amelia-engine@p001 (where 001 is the pod number)
systemctl restart amelia-user-web
```
# RabbitMQ
These operating procedures help debug possible RabbitMQ issues.
## RabbitMQ Users
An Amelia RabbitMQ instance requires 4 users to be present:
-   amelia
-   ipsoft
-   monitoring
The monitoring and ipsoft accounts belong to a group. If not sure, compare their account details to a working environment.
## **List active users**
Run this command to list active users:
``` bash
# rabbitmqctl list_users
Listing users ...
ipsoft  [administrator]
monitoring  [monitoring]
amelia  []
```
## **Add a User**
Run this command to add a user:
``` bash
# rabbitmqctl add_user monitoring <password>
```
> [!warning]  
>
> Do NOT assign random passwords. See below for instructions.  All passwords are unique for each user in every single environment, only monitoring uses the same password.

## **Add User to Group**
Run this command to add a user to a group:
``` bash
# rabbitmqctl set_user_tags monitoring monitoring
```
## List/Set Permissions
Run this command to list and set permissions:
``` bash
# rabbitmqctl list_permissions
Listing permissions in vhost "/" ...
monitoring  .*  .*  .*
ipsoft  .*  .*  .*
amelia  .*  .*  .*
# rabbitmqctl set_permissions -p / monitoring ".*" ".*" ".*"
```
## RabbitMQ Overview Alert
> [!info]  
>
> **Do not restart RabbitMQ unless you intend to restart ALL components of Amelia.**

This alert indicates several possible problems.
1.  List queues that are not empty.
    ``` bash
    # rabbitmqctl list_queues|grep queue.amelia.cache|grep -v 0$
    ```
2.  Check if there are any consumers for those queues.
    ``` bash
    # rabbitmqctl list_consumers|grep <queue name>
    ```
    > [!info]  
    >
    > **If the queue name does NOT begin with queue.amelia.cache DO NOT continue.**
3.  If the command returns nothing, then purge the queue.
    ``` bash
    # rabbitmqctl purge_queue <queue name>
    ```
# Percona/MySQL
These operating procedures help debug possible issues the Percona/MySQL database.
## Purging Binary Database Log Files
In cases where disk space is limited, purging binary database log files can reclaim space. These files can be located with this command:
``` bash
ps aux | grep mysqld | grep -v mysqld_safe | grep -v grep | grep datadir
```
If the binary log files are sizeable and older than 24 hours, and disk space needs to be reclaimed, purge the log files.
1.  For master or slave MySQL instances, connect with the mysql command prompt.
2.  For each MySQL slave instance, type then execute this command at the mysql prompt and check the Relay_Master_Log_File information for date, name, and size:
    ``` bash
    SHOW SLAVE STATUS \G
    ```
3.  For each non-master/slave instance, type then execute this command at the mysql prompt to list all binary log files:
    ``` bash
    ls -la /apps/mysql/data/mysql-bin*
    ```
4.  For each binary log file identified as older than 24 hours and of considerable size, type this command at the mysql prompt to delete log files older than but not including log_file_name:
    ``` bash
    purge binary logs to 'log_file_name'
    ```
    For example, to delete binary log files older than mysql-bin.001186 the command would be purge binary logs to ‘mysql-bin.001186’ and would not purge the mysql-bin.001186 file.
## Purge Database gcache.page Files
Sometimes an Amelia cluster running Percona/MySQL does not delete gcache.page files. This is a known Percona software bug. The gcache.page files not deleted can use significant hard drive space.
### Single Node Environment
You will need client approval to do this, as there is downtime involved with this process.
> [!warning]  
> If there are multiple pods, stop then restart each pod by updating the @p00x suffix where x is the pod number.

1.    
    First, bring down all services, in order:  
    ``` bash
    systemctl stop amelia-account-service
    systemctl stop amelia-admin-service
    systemctl stop amelia-admin-web
    systemctl stop amelia-batch-service
    systemctl stop amelia-engine-service@p001 (where 001 is the pod number)
    systemctl stop amelia-escalation-service
    systemctl stop amelia-integration-service
    systemctl stop amelia-model-server@p001 (where 001 is the pod number)
    systemctl stop amelia-user-web
    systemctl stop amelia-syntaxnet
    systemctl stop amelia-h2o
    systemctl stop mysql@amelia-adb
    systemctl stop mysql@amelia-cdb-p001 (where 001 is the pod number)
    systemctl stop mysql@amelia-kdb-master
    systemctl stop mysql@amelia-kdb-slave
    systemctl stop haproxy
    systemctl stop rabbitmq-server
    systemctl stop redis
    systemctl stop redis-sentinel
    ```
2.  Once all services are verified as down, cd to /apps/IPsoft/amelia/amelia-kdb-master/data/.  
    Before removal, check to remove only gcache files:  
    ``` bash
    ls -l | grep gcache.page
    ```
3.  Remove all of these files with this command:  
    ``` bash
    rm -f gcache.page*
    ```
4.  Once these files are removed, start the services in order:  
    ``` bash
    systemctl start mysql@amelia-adb
    systemctl start mysql@amelia-cdb-p001
    systemctl start mysql@amelia-kdb-master
    systemctl start mysql@amelia-kdb-slave
    systemctl start haproxy
    systemctl start rabbitmq-server
    systemctl start redis
    systemctl start redis-sentinel
    systemctl start amelia-account-service
    systemctl start amelia-admin-service
    systemctl start amelia-admin-web
    systemctl start amelia-batch-service
    systemctl start amelia-engine-service@p001
    systemctl start amelia-escalation-service
    systemctl start amelia-integration-service
    systemctl start amelia-model-server@p001
    systemctl start amelia-user-web
    systemctl start amelia-syntaxnet
    systemctl start amelia-h2o
    ```
5.  Verify all services are online, check the /apps filesystem, and once complete, hand over to client.  
    > [!warning]  
    >
    > When stopping and starting the services, please keep in mind the \`\*@p00X\` version identifier at the end of amelia-{cdb,engine,model}\\.
### Clustered Environments
On Clustered Environments, there is no need to shutdown all services; All the database servers including slave, are load balanced across all the nodes using haproxy.
Due to this, you can just stop the database in question, clear the cache files, and start the database back up; make sure it syncs up.
> [!warning]  
>
> When a database is gcaching, please check the whole environment, the other nodes are more than likely to have the same issue.

## Percona/VMware-VMotion
Troubleshooting where 2019-07-2 is the date in which you are looking for in the log, run these commands
``` groovy
grep '2019-07-2' mysqld.log | grep 'New cluster view' | wc -l
grep '2019-07-2' mysqld.log | grep 'New cluster view' | tail -5
```
``` bash
2019-07-22 14:39:14.612  WARN 14284 — [QuartzScheduler_AmeliaEngineService-Scheduler-app03.prod-v3.amelia.ipcenter.com1563776946271_ClusterManager] com.pool.ProxyConnection   : CDB Pool - Connection com.mysql.jdbc.JDBC4Connection@50ff5b23 marked as broken because of SQLSTATE(08007), ErrorCode(0)
019-07-22 15:19:09.178  WARN 14284 — [grpc-default-executor-77]com.zaxxer.hikari.pool.ProxyConnection   : CDB Pool - Connection com.mysql.jdbc.JDBC4Connection@557c6d3 marked as broken because of SQLSTATE(08S01), ErrorCode(1047)
com.mysql.jdbc.exceptions.jdbc4.MySQLNonTransientConnectionException: WSREP has not yet prepared node for application use
[root@app02.prod-v3.amelia.ipcenter.com:/apps/IPsoft/amelia/amelia-cdb-p001]# grep '2019-07-2' mysqld.log | grep 'New cluster view' | wc -l
46
[root@app02.prod-v3.amelia.ipcenter.com:/apps/IPsoft/amelia/amelia-cdb-p001]# grep '2019-07-2' mysqld.log | grep 'New cluster view' | tail -5
2019-07-24T17:30:42.349074Z 1 [Note] WSREP: New cluster view: global state: dfb376e6-fc4e-11e8-b3d8-4a9f920dc683:96404604, view# -1: non-Primary, number of nodes: 1, my index: 0, protocol version 3
2019-07-24T17:30:42.351468Z 1 [Note] WSREP: New cluster view: global state: dfb376e6-fc4e-11e8-b3d8-4a9f920dc683:96404604, view# -1: non-Primary, number of nodes: 1, my index: 0, protocol version 3
2019-07-24T17:30:47.353457Z 1 [Note] WSREP: New cluster view: global state: dfb376e6-fc4e-11e8-b3d8-4a9f920dc683:96404604, view# -1: non-Primary, number of nodes: 1, my index: 0, protocol version 3
2019-07-24T17:30:47.353692Z 1 [Note] WSREP: New cluster view: global state: dfb376e6-fc4e-11e8-b3d8-4a9f920dc683:96404604, view# -1: non-Primary, number of nodes: 1, my index: 0, protocol version 3
2019-07-24T17:30:47.361204Z 1 [Note] WSREP: New cluster view: global state: dfb376e6-fc4e-11e8-b3d8-4a9f920dc683:96404607, view# 85: Primary, number of nodes: 3, my index: 1, protocol version 3
2019-07-22 07:01:22.155 [info] <0.5741.0> node rabbit@app01 up
2019-07-22 07:01:22.353 [error] <0.5556.0> Mnesia(rabbit@app02): ** ERROR ** mnesia_event got {inconsistent_database, running_partitioned_network, rabbit@app01}
[root@app02.prod-v3.amelia.ipcenter.com:~]# grep 'Started' /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log
2019-05-20 22:41:24.863  INFO 47002 — [main] net.ipsoft.ameliav3.AmeliaEngineService  : Started AmeliaEngineService in 49.963 seconds (JVM running for 51.518)
2019-07-05 16:11:29.456  INFO 23509 — [main] net.ipsoft.ameliav3.AmeliaEngineService  : Started AmeliaEngineService in 44.396 seconds (JVM running for 47.268)
2019-07-05 16:31:17.467  INFO 54483 — [main] net.ipsoft.ameliav3.AmeliaEngineService  : Started AmeliaEngineService in 38.598 seconds (JVM running for 39.628)
2019-07-20 01:27:45.764  INFO 10959 — [main] net.ipsoft.ameliav3.AmeliaEngineService  : Started AmeliaEngineService in 124.532 seconds (JVM running for 131.213)
```
# Zombie Processes
Zombie processes are processes that exist but do nothing. They’re neither active or disappeared from a system.
To find zombie processes, log in with the sudoscript ss command and enter this command:
``` bash
ss
ps auxwww | grep -w Z | grep defunct | grep -v grep
```
Then check the parent process IDs of these zombies. If IpmonX processes, then bounce IpmonX.
To kill zombie processes:
``` bash
ps aux
kill -HUP $(ps -A -ostat,ppid | grep -e '[zZ]'| awk '{ print $2 }')
```
> [!warning]  
>
> Confirm services are up and running. Look at the log file to determine what caused failure. Then escalate to IPsoft. If zombie processes cannot be removed, escalate to IPsoft.
{% /version %}
