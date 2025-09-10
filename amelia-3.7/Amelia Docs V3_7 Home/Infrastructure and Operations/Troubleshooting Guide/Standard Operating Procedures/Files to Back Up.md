-   [Files / Directories](#FilestoBackUp-Files/Directories)
-   [Database Backups](#FilestoBackUp-DatabaseBackups)
-   [Adding Other Databases](#FilestoBackUp-AddingOtherDatabases)
For completeness and disaster recovery best practices, the following files / directories are candidates for backup.  The target use-case is standing up a new fresh install of an Amelia host to replace an unrecoverable one, restoring both the original's configuration and data.
> [!info]  
>
> For instances not hosted by IPsoft, clients must implement back up for these files and directories. This includes database dumps described below. This list will change so check back for any updates.
> [!warning]  
>
> As of August 25, 2018, the CDB database will no longer be backed up.

# Files / Directories

| Location | Use | Notes |
| ----|----|----|
| /etc/sysconfig/amelia | Amelia Boot secret1 | Do not lose this file |
| /etc/sysconfig/amelia-integration-service | Amelia Integration Service Boot secret1 | Do not lose this file |
| /etc/sysconfig/mysql.amelia-adb | Set options for Amelia database adb | Back up /etc/sysconfig/mysql* |
| /etc/sysconfig/mysql.amelia-cdb-p0* | Set options for Amelia database cdb-p00* pods | Larger installations may have additional pods p002, p003, p004, etc. |
| /etc/sysconfig/mysql.amelia-kdb-master | Set options for Amelia database kdb-master | Back up /etc/sysconfig/mysql* |
| /etc/sysconfig/mysql.amelia-kdb-slave | Set options for Amelia database kdb-slave | Back up /etc/sysconfig/mysql* |
| /etc/sysconfig/mysql.bootstrap-amelia-adb | Set bootstrap options for Amelia database adb | Back up /etc/sysconfig/mysql* |
| /etc/sysconfig/mysql.bootstrap-amelia-cdb-p001 | Set bootstrap options for Amelia database cdb-p001 | Back up /etc/sysconfig/mysql* |
| /etc/sysconfig/mysql.bootstrap-amelia-kdb-master | Set bootstrap options for Amelia database kdb-master | Back up /etc/sysconfig/mysql* |
| /apps/IPsoft/amelia/amelia-common-config/ | Amelia configuration files | Back up entire directory |
| /apps/IPsoft/amelia/amelia-common-config/amelia_ks.p12 | Amelia java keystore1 | Critical per-instance keystore |
| /apps/IPsoft/amelia/amelia-common-config/application.yml | Amelia configuration & encrypted keys1 | Newer versions will have application.properties instead of application.yml; back up entire directory |
| /apps/IPsoft/amelia/amelia-common-config/application.properties | Amelia configuration & encrypted keys1 | Newer versions will have application.properties instead of application.yml; back up entire directory |
| /apps/IPsoft/amelia/amelia-integration-service/config/ | Amelia integration service configuration files / keystore | Back up entire directory |
| /apps/IPsoft/amelia/amelia-adb/my.cnf | MySQL configuration for Amelia adb |  |
| /apps/IPsoft/amelia/amelia-cdb-p0*/my.cnf | MySQL configuration for Amelia cdb-p0* pods |  |
| /apps/IPsoft/amelia/amelia-kdb-master/my.cnf | MySQL configuration for Amelia kdb-master |  |
| /apps/IPsoft/amelia/amelia-kdb-slave/my.cnf | MySQL configuration for Amelia kdb-slave |  |
| /etc/ansible/ | Amelia instance top-level directory | Easiest to back up everything in this directory |
| /etc/ansible/credentials | Amelia instance passwords and keys | Keep confidential, accessible only by root; created on ADC installation host |
| inventory.fromweb | Default file for the Amelia instance | Keep confidential, accessible only by root. Required for upgrades, changes to instance, restarts, etc. |
| /etc/cron.d/ameliav3_mysql_backup | Schedules Amelia MySQL backups |  |
| /apps/IPsoft/backups | Default backup directory for MySQL backups | Check contents of /etc/cron.d/amelia_mysql_backup for configured location. Back up directory. |
| /etc/systemd/system/*.d/override.conf | SystemD overrides for Amelia | Controls Wants= and After= startup requirements ordering a la systemD |
| /etc/systemd/system/mysql@*.d/override.conf | SystemD overrides for Amelia databases | Controls Wants= and After= startup requirements ordering a la systemD |
| /etc/rsyslog.d/amelia.conf | rsyslog config for Amelia logging |  |
| /etc/systemd/system/multi-user.target.wants/amelia-account-service.service | Service unit configuration for amelia-account-service |  |
| /etc/systemd/system/multi-user.target.wants/amelia-admin-service.service | Service unit configuration for amelia-admin-service |  |
| /etc/systemd/system/multi-user.target.wants/amelia-admin-web.service | Service unit configuration for amelia-admin-web |  |
| /etc/systemd/system/multi-user.target.wants/amelia-batch-service.service | Service unit configuration for amelia-batch-service |  |
| /etc/systemd/system/multi-user.target.wants/amelia-customui*-web.service.service | Service unit configuration for amelia-custom UI | In Amelia >= v3.3.x, customUI RPM is deprecated |
| /etc/systemd/system/multi-user.target.wants/amelia-engine-service@p00*.service | Service unit configuration for amelia-engine service | Back up if exists; larger installations may have additional pods p002, p003, p004, etc. |
| /etc/systemd/system/multi-user.target.wants/amelia-escalation-service.service | Service unit configuration for amelia-escalation-service |  |
| /etc/systemd/system/multi-user.target.wants/amelia-h2o.service | Service unit file for amelia-h2o |  |
| /etc/systemd/system/multi-user.target.wants/amelia-integration-service.service | Service unit configuration for amelia-integration-service |  |
| /etc/systemd/system/multi-user.target.wants/amelia-model-server.service | Service unit configuration for amelia-model-server |  |
| /etc/systemd/system/multi-user.target.wants/amelia-syntaxnet.service | Service unit configuration for amelia-syntaxnet |  |
| /etc/systemd/system/multi-user.target.wants/amelia-user-web.service | Service unit configuration for amelia-user-web |  |
| /etc/systemd/system/multi-user.target.wants/mysql@amelia-adb.service | Service unit configuration for MySQL adb |  |
| /etc/systemd/system/multi-user.target.wants/mysql@amelia-cdb-p00*.service | Service unit configuration for MySQL cdb pods | Larger installations may have additional pods p002, p003, p004, etc. |
| /etc/systemd/system/multi-user.target.wants/mysql@amelia-kdb-master.service | Service unit configuration for MySQL kdb-master |  |
| /etc/systemd/system/multi-user.target.wants/mysql@amelia-kdb-slave.service | Service unit configuration for MySQL kdb-slave |  |
| /apps/IPsoft/amelia/amelia-customuiv3-web/amelia-customuiv3-web.conf | Configuration file for custom UI | In Amelia >= v3.3.x, customUI RPM is deprecated |
| /apps/IPsoft/amelia/amelia-customuiv3-web/application.yml | Application configuration for custom UI | In Amelia >= v3.3.x, customUI RPM is deprecated |
| /apps/IPsoft/amelia/amelia-conceptnet/db/pg_hba.conf | PostgreSQL client authentication configuration file1 | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-account-service/amelia-account-service-exe.conf | Configuration file for amelia-account-service | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-admin-service/amelia-admin-service-exe.conf | Configuration file for amelia-admin-service | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-admin-web/amelia-admin-web-exe.conf | Configuration file for amelia-admin-web | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-batch-service/amelia-batch-service-exe.conf | Configuration file for amelia-batch-service | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-engine-service/amelia-engine-service-exe.conf | Configuration file for amelia-engine-service | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-escalation-service/amelia-escalation-service-exe.conf | Configuration file for amelia-escalation-service | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-integration-service/amelia-integration-service-exe.conf | Configuration file for amelia-integration-service | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-model-server/amelia-model-server-exe.conf | Configuration file for amelia-model-server | Usually not modified from default |
| /apps/IPsoft/amelia/amelia-user-web/amelia-user-web-exe.conf | Configuration file for amelia-user-web | Usually not modified from default |
| /etc/haproxy/haproxy.cfg | HAProxy configuration1 | Back up if modified from default IPsoft install |
| /etc/haproxy/ | HAProxy directory | For pem and other certificate files; back up directory |
| /etc/chrony.conf | Time configuration | Back up if modified from default IPsoft install. May not be installed if ntp is used. |
| /etc/my.cnf | MySQL configuration | Back up if exists |
| /root/.my.cnf | root MySQL config1 | Back up if exists |
| /etc/rabbitmq/ | Rabbitmq server configuration files | Back up directory |
| /etc/redis.conf | Redis configuration | Back up if exists |
| /etc/redis-sentinel.conf | Redis configuration for cluster | Back up if it exists |
| /apps/redis/ | Redis data | Back up directory |
| /etc/passwd | System password file | If any sysadmin / post-install changes |
| /etc/shadow | System shadow password file | If any sysadmin / post-install changes |
| /etc/group | System group file | If any sysadmin / post-install changes |
| /etc/hosts | Local hosts file |  |
| /var/log/yum.log* | Yum installation log | Nice to have, for post-installation RPMs installed |
| /var/lib/rabbitmq/ | Run-time rabbitmq server directory | Back up directory |
| /root/.ssh/ | Root ssh keys / directory | May have additional keys & original id* files |

**Legend**
<sup>1</sup> - If cluster/multi-node, keep in sync if updated since installation. Initial installation ensures the files are created/in-sync across nodes
# Database Backups
Every Amelia host installation, whether single node or cluster, includes a cron job automatically configured to back up the Amelia databases.
The cron job is in /etc/cron.d/ameliav3_mysql_backup
**/etc/cron.d/amelia_mysql_backup**
``` groovy
# cat /etc/cron.d/ameliav3_mysql_backup
#Ansible: Amelia MySQL backup for amelia-kdb-slave
30 3 * * * root /apps/IPsoft/mysql-scripts/ameliav3_mysql_backup.pl --dir /apps/IPsoft/backups/amelia-kdb-slave --socket /apps/IPsoft/amelia/amelia-kdb-slave/mysql.sock
#Ansible: Amelia MySQL backup for amelia-cdb-p001 - no longer backup pods
#30 3 * * * root /apps/IPsoft/mysql-scripts/ameliav3_mysql_backup.pl --dir /apps/IPsoft/backups/amelia-cdb-p001 --socket /apps/IPsoft/amelia/amelia-cdb-p001/mysql.sock
#Ansible: Amelia MySQL backup for amelia-adb
30 3 * * * root /apps/IPsoft/mysql-scripts/ameliav3_mysql_backup.pl --dir /apps/IPsoft/backups/amelia-adb --socket /apps/IPsoft/amelia/amelia-adb/mysql.sock
```
*  
*/apps/IPsoft/backups/is the default directory where backups are stored.* * For Amelia instances not hosted by IPsoft, this directory can be changed.
To manually kick-off a backup, run this command:
``` text
nohup /apps/mysql/scripts/amelia_mysql_backup.pl --dir /apps/backup   # change /apps/backup if required
```
Output results of the backup operation are written to the /apps/backup/amelia_mysql_backup.log file*.* If this command is successful, the last line displays **170105 04:30:20 completed OK!**
# Adding Other Databases
If other databases are created locally in an instance, these need to be added to the backup schedule.
1.  Edit /apps/mysql/scripts/[ameliav3_mysql_backup.pl](http://ameliav3_mysql_backup.pl) on the respective host(s)
2.  Modify line ~24
3.  Change **my @individual_dbs = ('amelia', 'data');***  
    *to  
    **my @individual_dbs = ('amelia', 'data', 'OTHER DATABASE NAME 1', 'OTHER DATABASE NAME 2');**  
    etc.
