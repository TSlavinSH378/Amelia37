# Check SElinux Status
``` groovy
getenforce
```
# Look at Service Status
``` groovy
systemctl list-units --all amelia-\* redis\* rabbitmq\* mysql@\* haproxy\* netdata\* sshd.service ipsoft-av-gateway check-amelia-\*.socket clam\* | awk '/UNIT/,/^$/'
```
# Look at HAproxy Status
``` groovy
echo "show stat" | socat /var/run/haproxy.sock stdio | cut -d "," -f 1,2,18,57,74 | column -s, -t
```
# Check Log Files
If everything seems up, look for stack traces in the following logs:
/apps/IPsoft/amelia/amelia-model-server/var/p001/log/amelia-model-server.log  
/apps/IPsoft/amelia/amelia-admin-service/var/log/amelia-admin-service.log  
/apps/IPsoft/amelia/amelia-escalation-service/var/log/amelia-escalation-service.log  
/apps/IPsoft/amelia/amelia-batch-service/var/log/amelia-batch-service.log  
/apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log  
/apps/IPsoft/amelia/amelia-account-service/var/log/amelia-account-service.log  
/apps/IPsoft/amelia/amelia-integration-service/var/log/amelia-integration-service.log
**  
**
Then look for any issues in these database log files:
/apps/IPsoft/amelia/amelia-kdb-master/mysqld.log  
/apps/IPsoft/amelia/amelia-kdb-slave/mysqld.log  
/apps/IPsoft/amelia/amelia-cdb-p001/mysqld.log  
/apps/IPsoft/amelia/amelia-adb/mysqld.log
Then look for any issues in the RabbitMQ log files:
/var/log/rabbitmq/rabbit@\*.log
Finally look at the yum log file with this command:
``` groovy
tail -40 /var/log/yum.log
```
