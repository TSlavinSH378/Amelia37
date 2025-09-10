-   [Purging Binary Database Log Files](#PerconaMySQLSOPs-PurgingBinaryDatabaseLogFiles)
-   [Purge Database gcache.page Files](#PerconaMySQLSOPs-PurgeDatabasegcache.pageFiles)
    -   [Single Node Environment](#PerconaMySQLSOPs-SingleNodeEnvironment)
    -   [Clustered Environments](#PerconaMySQLSOPs-ClusteredEnvironments)
-   [Percona/VMware-VMotion](#PerconaMySQLSOPs-Percona/VMware-VMotion)
These operating procedures help debug possible issues the Percona/MySQL database.
# Purging Binary Database Log Files
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
# Purge Database gcache.page Files
Sometimes an Amelia cluster running Percona/MySQL does not delete gcache.page files. This is a known Percona software bug. The gcache.page files not deleted can use significant hard drive space.
## Single Node Environment
You will need client approval to do this, as there is downtime involved with this process.
> [!warning]  
> If there are multiple pods, stop then restart each pod by updating the @p00x suffix where x is the pod number.

1.  First, bring down all services, in order:  
    ``` text
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
    ``` text
    ls -l | grep gcache.page
    ```
3.  Remove all of these files with this command:  
    ``` text
    rm -f gcache.page*
    ```
4.  Once these files are removed, start the services in order:  
    ``` text
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
## Clustered Environments
On Clustered Environments, there is no need to shutdown all services; All the database servers including slave, are load balanced across all the nodes using haproxy.
Due to this, you can just stop the database in question, clear the cache files, and start the database back up; make sure it syncs up.
> [!warning]  
>
> When a database is gcaching, please check the whole environment, the other nodes are more than likely to have the same issue.

# Percona/VMware-VMotion
Troubleshooting where 2019-07-2 is the date in which you are looking for in the log, run these commands
``` text
grep '2019-07-2' mysqld.log | grep 'New cluster view' | wc -l
grep '2019-07-2' mysqld.log | grep 'New cluster view' | tail -5
```
``` text
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
