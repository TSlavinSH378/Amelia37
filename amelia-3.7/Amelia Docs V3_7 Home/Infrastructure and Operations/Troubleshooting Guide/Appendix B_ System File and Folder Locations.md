{% version "3.x" %}
When debugging, there could be system files to check and preserve. The table below lists the file locations used by the Amelia system. If a folder or file does not exist, in most cases, it is for a service not installed, for example, a LivePerson integration.
# Configuration Files
The Amelia system includes configuration files for the system, service units, and properties.
## System Configuration Files

| File Location | Description | Notes |
| ----|----|----|
| /etc/sysconfig/amelia | Amelia Boot secret | Do not lose this file |
| /etc/sysconfig/amelia-engine | Set java memory options for Amelia engine | Optional file, may not exist |
| /apps/IPsoft/amelia/amelia-engine@p001/amelia-engine.conf | amelia-engine configuration file | p001 is the pod number |
| /etc/sysconfig/amelia-escalation | Set java memory options for Amelia escalation | Optional file, may not exist |
| /etc/sysconfig/amelia-web | Set java memory options for Amelia web | Optional file, may not exist |
| /etc/rsyslog.d/amelia.conf | rsyslog config for Amelia logging |  |
| /etc/chrony.conf | Time configuration | Back up if modified from default IPsoft install. May not be installed if ntp is used. |

## Service Unit Configuration Files

| File Location | Description | Notes |
| ----|----|----|
| /etc/systemd/system/multi-user.target.wants/amelia-batch.service | Service unit configuration for amelia-batch |  |
| /etc/systemd/system/multi-user.target.wants/amelia-engine.service | Service unit configuration for amelia-engine |  |
| /etc/systemd/system/multi-user.target.wants/amelia-escalation.service | Service unit configuration for amelia-escalation |  |
| /etc/systemd/system/multi-user.target.wants/amelia-web.service | Service unit configuration for amelia-web |  |

## Property Configuration Files

| File Location | Description | Notes |
| ----|----|----|
| /apps/IPsoft/amelia/amelia-batch/application.properties | Property configuration |  |
| /apps/IPsoft/amelia/amelia-engine@p001/application.properties | Property configuration | p001 is the pod number |
| /apps/IPsoft/amelia/amelia-escalation/application.properties | Property configuration |  |
| /apps/IPsoft/amelia/amelia-web/application.properties | Property configuration |  |

# Backup Files

| File Location | Description | Notes |
| ----|----|----|
| /apps/IPsoft/backups | Default backup directory for MySQL backups | Check contents of /etc/cron.d/amelia_mysql_backup for configured location. Back up directory. |

#  HAProxy

| File Location | Description | Notes |
| ----|----|----|
| /etc/haproxy/haproxy.cfg | HAProxy configuration | Back up if modified from default IPsoft install |
| /etc/haproxy/ | HAProxy directory | For pem and other certificate files; back up directory |

# MySQL Files

| File Location | Description | Notes |
| ----|----|----|
| /etc/my.cnf | MySQL configuration |  |
| /root/.my.cnf | root MySQL config | Back up if exists |
| /etc/cron.d/amelia_mysql_backup | Schedules Amelia MySQL backups |  |

# RabbitMQ

| File Location | Description | Notes |
| ----|----|----|
| /etc/rabbitmq/ | Rabbitmq server configuration files | Back up directory |
| /var/lib/rabbitmq/ | Run-time rabbitmq server directory | Back up directory |
| /var/lib/rabbitmq/ | Run-time rabbitmq server directory | Back up directory |

# Redis

| File Location | Description | Notes |
| ----|----|----|
| /etc/redis.conf | Redis configuration | Back up if exists |
| /etc/redis-sentinel.conf | Redis configuration for cluster | Back up if it exists |
| /apps/redis/ | Redis data | Back up directory |

# System Files

| File Location | Description | Notes |
| ----|----|----|
| /etc/passwd | System password file | If any sysadmin / post-install changes |
| /etc/shadow | System shadow password file | If any sysadmin / post-install changes |
| /etc/group | System group file | If any sysadmin / post-install changes |
| /etc/hosts | Local hosts file |  |
| /var/log/yum.log* | Yum installation log | Nice to have, for post-installation RPMs installed |
| /var/lib/rabbitmq/ | Run-time rabbitmq server directory | Back up directory |
| /root/.ssh/ | Root ssh keys / directory | May have additional keys & original id* files |
| /apps/IPsoft/amelia/amelia_ks.jceks | Amelia keystore |  |

{% /version %}
