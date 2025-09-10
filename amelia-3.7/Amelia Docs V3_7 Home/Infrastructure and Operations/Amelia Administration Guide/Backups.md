# Amelia Backups
The Amelia system data and configuration details and conversations can be backed up. The system data and configuration details also can be restored.
## Amelia System Backups
#CLI backups are covered here in Confluence: [Artifact Promotion](#) [Backup tools for BPN artifacts](#)
Backups of Amelia’s system and configuration details are found in the Artifact Promotion control panel and workspace within the administration pages.
### The Artifact Promotion Interface
To access the Artifact Promotion control panel and workspaces, click the dropdown link from the top left of Amelia's chat interface. The administration page appears with tabs on the left. Click the Artifact Promotion tab once to open the Artifact Promotion control panel. The panel lists existing backups and a Create Archive button to create new archive backups and a Restore Archive button to use a backup archive to rebuild the Amelia instance.
![](attachments/11940296/11940298.png)
Figure Artifact Promotion Control Panel
### Create Archive Backups
The Artifact Promotion control panel and workspace are available through Amelia's dropdown list at the top left of her chat interface.
1.  Click the dropdown list at the top left of Amelia's chat interface. Select Admin. The administration pages display.
2.  Click the Artifact Promotion tab on the left side of the administration page to display the Artifact Promotion control panel.  
    To edit an existing backup, click twice on a backup name listed in the control panel.  
    To add a new backup, click the Create Archive button at the top of the Artifact Promotion control panel.
3.  On the Artifact Promotion form that appears on the right side of the interface, select one, some, or all domains to back up. Click the Next button at the bottom of the workspace.
4.  Select which artifacts to backup, for example, BPN Models, Variable Resolvers, Grammars, and FAQs.
5.  For each artifacts selected for backup, select which entries to include, for example, one, some, or all BPN Models. Click the Next button at the bottom of the workspace to continue.
6.  When artifacts have been selected, the Selected Artifacts page appears with a list of archives to back up. Click the Finish button at the bottom of the workspace to start the backup. Click the Back button at the bottom of the workspace to change archives to back up.
### Restore a Backup
The Artifact Promotion control panel and workspace are available through Amelia's dropdown list at the top left of her chat interface.
1.  Click the dropdown list at the top left of Amelia's chat interface. Select Admin. The administration pages display.
2.  Click the Artifact Promotion tab on the left side of the administration page to display the Artifact Promotion control panel.
3.  Click twice on a backup name listed in the control panel. The Artifact Promotion form appears in right side workspace.
4.  Click the Browse button to find an archive file to restore. Enter a password if needed. Click the Next button at the bottom of the workspace.
## Amelia Conversation Backups
The Metrics interface includes the ability to export conversations by user specified day, hour. and minute time periods. The export can include up to 2000 conversations in each exported file.
1.  Click the dropdown list at the top left of Amelia's chat interface. Select Metrics. The Metrics page displays.
2.  Click the Export tab at the top right of the Metrics page.
3.  Click the All Domains check box then deselect any domains not needed.
4.  Click the From dropdown list and select a start date. The At time dropdown list appears when a date is selected.  
    ![](attachments/11940296/11940297.png)  
    Figure 23. Metrics Workspace with Hour/Minute Dropdown List  
5.  Click the At dropdown list to select an hour. When the hour displays, click on the zero values after the hour and type in any minutes, for example, changing 01:00 to 01:15.
6.  Click the To dropdown list and select an end date.
7.  When the At time dropdown list appears, click the At dropdown list to select an end hour and minute, as needed.
8.  Click whether or not to include a full transcript, escalation log, and/or not started data in the export.
9.  Click the Export button to export data.
10. Click Yes or No on the confirmation popup to export conversation data.
The export confirmation popup details how many conversations meet the date/time range selected and how many will be exported, as shown below.
![](attachments/11940296/11940299.png)
Figure 24. Conversation Export Confirmation Popup Displaying Number of Records to Export
# Files to Backup
For completeness and disaster recovery best practices, the following files and directories are candidates for backup.  The target use-case is standing up a new, fresh install of an Amelia host to replace an unrecoverable one, restoring the original's configuration and data.  
It is up to partners to implement backing up of these files and directories when Amelia is installed on your premises.  This includes the database dumps mentioned below.
## Files and Directories
Table: Backup Files and Directories

| Location | Use | Notes |
| ----|----|----|
| /etc/sysconfig/amelia | Amelia Boot secret | Do not lose this file |
| /etc/sysconfig/amelia-engine | Set java memory options for Amelia engine | Optional file, may not exist |
| /etc/sysconfig/amelia-escalation | Set java memory options for Amelia escalation | Optional file, may not exist |
| /etc/sysconfig/amelia-web | Set java memory options for Amelia web | Optional file, may not exist |
| /etc/sysconfig/mule-esb | Mule ESB secret | Do not lose this file |
| /etc/sysconfig/mule-mmc | Mule MMC secret | Do not lose this file |
| /etc/cron.d/amelia_mysql_backup | Schedules Amelia MySQL backups |  |
| /apps/backup/ | Default backup directory for MySQL backups | Check contents of /etc/cron.d/amelia_mysql_backup for configured location. Back up directory. |
| /etc/rsyslog.d/amelia.conf | rsyslog config for Amelia logging |  |
| /etc/systemd/system/multi-user.target.wants/amelia-batch.service | Service unit configuration for amelia-batch |  |
| /etc/systemd/system/multi-user.target.wants/amelia-engine.service | Service unit configuration for amelia-engine |  |
| /etc/systemd/system/multi-user.target.wants/amelia-escalation.service | Service unit configuration for amelia-escalation |  |
| /etc/systemd/system/multi-user.target.wants/amelia-web.service | Service unit configuration for amelia-web |  |
| /etc/systemd/system/multi-user.target.wants/amelia-<client>-web.service | Service unit configuration for amelia-jsclient-web | Back up if exists |
| /etc/systemd/system/multi-user.target.wants/amelia-liveperson.service | Service unit configuration for amelia-liveperson | Back up if exists |
| /etc/systemd/system/multi-user.target.wants/amelia-solidus.service | Service unit configuration for amelia-solidus | Back up if exists |
| /apps/IPsoft/amelia/amelia-batch/application.properties | Property configuration | [Back up all application.properties files] |
| /apps/IPsoft/amelia/amelia-engine/application.properties | Property configuration |  |
| /apps/IPsoft/amelia/amelia-escalation/application.properties | Property configuration |  |
| /apps/IPsoft/amelia/amelia-web/application.properties | Property configuration |  |
| /apps/IPsoft/amelia/amelia-<client>-web/application.properties | Property configuration | Back up if exists |
| /apps/IPsoft/amelia/amelia-liveperson/application.properties | Property configuration | Back up if exists |
| /apps/IPsoft/amelia/amelia-solidus/application.properties | Property configuration | Back up if exists |
| /etc/haproxy/haproxy.cfg | HAProxy configuration | Back up if modified from default IPsoft install |
| /etc/haproxy/ | HAProxy directory | For pem and other certificate files; back up directory |
| /etc/chrony.conf | Time configuration | Back up if modified from default IPsoft install. May not be installed if ntp is used. |
| /etc/my.cnf | MySQL configuration |  |
| /root/.my.cnf | root MySQL config | Back up if exists |
| /etc/rabbitmq/ | Rabbitmq server configuration files | Back up directory |
| /etc/redis.conf | Redis configuration | Back up if exists |
| /etc/redis-sentinel.conf | Redis configuration for cluster | Back up if it exists |
| /apps/redis/ | Redis data | Back up directory |
| /apps/IPsoft/mule/esb/apps/ | Directory containing MuleSoft flows | Back up if exists |
| /etc/passwd | System password file | If any sysadmin / post-install changes |
| /etc/shadow | System shadow password file | If any sysadmin / post-install changes |
| /etc/group | System group file | If any sysadmin / post-install changes |
| /etc/hosts | Local hosts file |  |
| /var/log/yum.log* | Yum installation log | Nice to have, for post-installation RPMs installed |
| /var/lib/rabbitmq/ | Run-time rabbitmq server directory | Back up directory |
| /root/.ssh/ | Root ssh keys / directory | May have additional keys & original id* files |
| /apps/IPsoft/amelia/amelia_ks.jceks | Amelia keystore |  |
| /apps/IPsoft/mule/mmc/webapps/mmc/WEB-INF/classes/META-INF/databases/mmc-mysql.properties | MuleSoft MMC properties file |  |
| /apps/IPsoft/mule/mmc/webapps/mmc/WEB-INF/classes/META-INF/databases/tracking-persistence-mysql.properties | MuleSoft MMC properties file |  |
| /apps/IPsoft/mule/mmc/conf/keystore.jks | MuleSoft keystore |  |
| /apps/IPsoft/mule/esb/domains/ | MuleSoft Domains Configuration | Back up directory |
| /apps/IPsoft/mule/esb/conf/ | MuleSoft Configuration | Back up directory |
| /apps/IPsoft/mule/esb/conf-flows/ | MuleSoft Configuration Flows | Back up directory |

## Database Backups
As part of every Amelia host installation, whether single node or cluster, a cron job is automatically configured to back up the Amelia databases.
### cron Database Script
The cron job is in /etc/cron.d/amelia_mysql_backup
``` bash
/etc/cron.d/amelia_mysql_backup
# cat /etc/cron.d/amelia_mysql_backup
#Ansible: Amelia MySQL backup
30 4 * * * root /apps/mysql/scripts/amelia_mysql_backup.pl --dir /apps/backup
```
/apps/backup is the default directory where backups are stored.  If you wish to change this to another partner-supplied on-premise directory, you can do so.
To manually kick-off a backup, run nohup /apps/mysql/scripts/[amelia_mysql_backup.pl](http://amelia_mysql_backup.pl) --dir /apps/backup \# change /apps/backup if required
Results of the backup operation are written to /apps/backup/amelia_mysql_backup.log.  If successful the last line will be similar to 170105 04:30:20 completed OK!
### Adding Other Databases
If other databases are created locally in an instance, these need to be added to the backup schedule.
Edit /apps/mysql/scripts/[amelia_mysql_backup.pl](http://amelia_mysql_backup.pl) on the respective host(s)
``` bash
Modify line ~24
Change my @individual_dbs = ('amelia', 'data');
to
my @individual_dbs = ('amelia', 'data', 'OTHER DATABASE NAME 1', 'OTHER DATABASE NAME 2');
etc.
```
## Attachments:
![](images/icons/bullet_blue.gif) [image2017-4-21 10:0:47.png](attachments/11940296/11940297.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-3-29 13:20:30.png](attachments/11940296/11940298.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-4-21 10:1:57.png](attachments/11940296/11940299.png) (image/png)  
