{% version "3.x" %}
When troubleshooting, there could be log files to check and preserve, for example, escalation logs for escalated chats. The table below lists the location of log files used by the Amelia system.
> [!warning]  
>
> For log folder paths, the p001 folder file name is for pod numbered 001. Update the pod number folder name if needed.


| Service | File Location |
| ----|----|
| amelia-account-service | /apps/IPsoft/amelia/amelia-account-service/var/log |
| amelia-admin-service | /apps/IPsoft/amelia/amelia-admin-service/var/log/amelia-admin-service.log |
| amelia-admin-web | /apps/IPsoft/amelia/amelia-admin-web/var/log/amelia-admin-web.log |
| amelia-batch-service | /apps/IPsoft/amelia/amelia-batch-service/var/log/amelia-batch-service.log |
| amelia-duckling | /apps/IPsoft/amelia/amelia-duckling-service/log/error.log |
| amelia-engine-service | /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log |
| amelia-escalation-service | /apps/IPsoft/amelia/amelia-escalation-service/var/log/amelia-escalation-service.log |
| amelia-integration | /apps/IPsoft/amelia/amelia-integration-service/var/log/amelia-integration-service.log |
| amelia-model-server | /apps/IPsoft/amelia/amelia-model-server/var/p001/log/amelia-model-server.log |
| amelia-syntaxnet | /apps/IPsoft/amelia/syntaxnet/log |
| amelia-user-web | /apps/IPsoft/amelia/amelia-user-web/var/log/amelia-user-web.log |
| h20 | /apps/IPsoft/amelia/amelia-h2o/var/log/h2o_10.55.6.21_54321-5-error.log |
| HAProxy | /apps/IPsoft/log/haproxy.log |
| RabbitMQ | /var/log/rabbitmq/var/log/rabbitmq/rabbit@app01.log |
| MySQL | /apps/mysql/data/<fqdn>.err |
| adb | /apps/IPsoft/amelia/amelia-adb/mysqld.log/apps/IPsoft/backups/amelia-adb/amelia_mysql_backup.log |
| cdb | /apps/IPsoft/backups/amelia-cdb-p001/amelia_mysql_backup.log |
| kdb-master | /apps/IPsoft/amelia/amelia-kdb-master/mysqld.log |
| kdb-slave | /apps/IPsoft/amelia/amelia-kdb-slave/mysqld.log/apps/IPsoft/backups/amelia-kdb-slave/amelia_mysql_backup.log |
| Redis | /var/log/redis/redis-p001.log/var/log/redis/redis.log/var/log/redis/sentinel.log |
| REST Gateway | /apps/IPsoft/amelia/amelia-rest-gateway/var/log/amelia-rest-gateway.log |

{% /version %}
