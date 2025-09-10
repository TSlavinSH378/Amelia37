# Platform Restart
The example below refers to p001 for one conversation pod.  If multiple pods are used, add stop/start for those pods, for example, p002, p003, p004, and so on.
## Bring Services Down Serially
Run these commands to bring services down serially.
``` groovy
systemctl stop amelia-account-service
systemctl stop amelia-admin-service
systemctl stop amelia-admin-web
systemctl stop amelia-batch-service
systemctl stop amelia-engine-service@p001
systemctl stop amelia-escalation-service
systemctl stop amelia-integration-service
systemctl stop amelia-model-server@p001
systemctl stop amelia-user-web
systemctl stop amelia-syntaxnet
systemctl stop amelia-duckling-service
# stop whatever other locally installed amelia- rpms you have installed
systemctl stop clam-freshclam.service
systemctl stop clamd@av-gateway.service
systemctl stop ipsoft-av-gateway.service
systemctl stop mysql@amelia-adb
systemctl stop mysql@amelia-cdb-p001
systemctl stop mysql@amelia-kdb-master
systemctl stop mysql@amelia-kdb-slave
systemctl stop haproxy
systemctl stop rabbitmq-server
systemctl stop redis
systemctl stop redis-sentinel
```
## Start Services
In a cluster, bring up all adb, kdb-master, cdb pods, kdb slaves, rabbitmq, redis-sentinel up first, for example, run these commands.
``` groovy
systemctl start mysql@amelia-adb
systemctl start mysql@amelia-cdb-p001
systemctl start mysql@amelia-kdb-master
systemctl start mysql@amelia-kdb-slave
systemctl start redis-sentinel
systemctl start redis
```
If a single node Amelia, simply run the above commands.
In a cluster, the last node to have shutdown the database should be the first one to start. There is no need to bootstrap a node.
### RabbitMQ
In a cluster, run this command on all rabbitmq nodes within 15-30 seconds of each other:
``` groovy
systemctl start rabbitmq-server
```
If a single node Amelia, simply run this command:
``` groovy
systemctl start rabbitmq-server
```
### Other Services
Then on each node, run these commands to start the other services serially:
``` groovy
systemctl start haproxy
systemctl start redis
systemctl start clam-freshclam.service
systemctl start clamd@av-gateway.service
systemctl start ipsoft-av-gateway.service
systemctl start amelia-syntaxnet
systemctl start amelia-duckling-service
systemctl start amelia-admin-service (wait for it to finish)
systemctl start amelia-account-service (wait for it to finish)
systemctl start amelia-engine-service@p001 (wait for it to finish before moving on)
systemctl start amelia-model-server@p001
systemctl start amelia-batch-service
systemctl start amelia-escalation-service
systemctl start amelia-integration-service
systemctl start amelia-admin-web
systemctl start amelia-user-web
```
# List Services
To list services, run the amelia-host-status command to provide an overview of service status and generate output similar to this example.
``` text
amelia-host-status
domain                    : <amelia_instance_domain>
fqdn                      : <amelia_instance_fqdn>
hostname                  : app01
ipaddress                 : <amelia_instance_ip>
kernelrelease             : 3.10.0-693.11.1.el7.x86_64
memorysize                : 85.26 GB
operatingsystem           : Scientific
operatingsystemrelease    : 7.3
processor0                : Intel(R) Xeon(R) CPU E7-8891 v2 @ 3.20GHz
processorcount            : 12
productname               : VMware Virtual Platform
selinux                   : true
selinux_config_mode       : permissive
selinux_current_mode      : permissive
/etc/hosts information
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
<amelia_instance_ip>     <amelia_instance_fqdn> app01
Filesystem            Size  Used Avail Use% Mounted on
/dev/mapper/vg0-root   20G   13G  7.9G  61% /
devtmpfs               16G     0   16G   0% /dev
tmpfs                  16G     0   16G   0% /dev/shm
tmpfs                  16G  2.6M   16G   1% /run
tmpfs                  16G     0   16G   0% /sys/fs/cgroup
tmpfs                  16G   19M   16G   1% /tmp
/dev/sda1             497M  137M  361M  28% /boot
/dev/mapper/vg1-apps  300G  250G   50G  84% /apps
tmpfs                 3.2G     0  3.2G   0% /run/user/0
tmpfs                 3.2G     0  3.2G   0% /run/user/65600
tmpfs                 3.2G     0  3.2G   0% /run/user/65761
tmpfs                 3.2G     0  3.2G   0% /run/user/41491
tmpfs                 3.2G     0  3.2G   0% /run/user/41106
tmpfs                 3.2G     0  3.2G   0% /run/user/41559
tmpfs                 3.2G     0  3.2G   0% /run/user/41325
tmpfs                 3.2G     0  3.2G   0% /run/user/68372
tmpfs                 3.2G     0  3.2G   0% /run/user/68298
tmpfs                 3.2G     0  3.2G   0% /run/user/68722
tmpfs                 3.2G     0  3.2G   0% /run/user/68422
tmpfs                 3.2G     0  3.2G   0% /run/user/40366
tmpfs                 3.2G     0  3.2G   0% /run/user/65908
tmpfs                 3.2G     0  3.2G   0% /run/user/40282
tmpfs                 3.2G     0  3.2G   0% /run/user/41562
tmpfs                 3.2G     0  3.2G   0% /run/user/42679
tmpfs                 3.2G     0  3.2G   0% /run/user/68936
tmpfs                 3.2G     0  3.2G   0% /run/user/42610
tmpfs                 3.2G     0  3.2G   0% /run/user/67292
tmpfs                 3.2G     0  3.2G   0% /run/user/40890
/apps permissions
64         0  drwxr-xr-x  11  root    root    174  Feb  12  08:42  /apps/
67         0  drwxr-xr-x  17  root    root    277  Dec  30  17:51  /apps/IPsoft
100663360  0  drwxr-xr-x  4   root    root    28   Dec  9   2015   /apps/var
100663361  0  drwxr-xr-x  2   root    root    6    Dec  9   2015   /apps/yumlocal
16373327   0  drwx------  2   root    root    118  Mar  13  14:17  /apps/tmp
103363665  0  drwx------  2   root    root    6    Jan  24  01:01  /apps/rpms
436381693  0  drwxr-xr-x  2   root    root    85   Mar  19  2018   /apps/artifacts
134310980  0  drwx------  3   root    root    24   Dec  19  2018   /apps/backup
436293557  0  drwx------  2   root    root    6    Jun  5   2019   /apps/src
7013       0  drwx------  3   icinga  icinga  21   Nov  5   06:42  /apps/icinga
Users
uid=496(mysql) gid=496(mysql) groups=496(mysql),1002(amelia)
uid=494(redis) gid=494(redis) groups=494(redis),1002(amelia)
uid=495(rabbitmq) gid=495(rabbitmq) groups=495(rabbitmq)
uid=188(haproxy) gid=188(haproxy) groups=188(haproxy)
uid=498(amelia) gid=1002(amelia) groups=1002(amelia)
uid=497(netdata) gid=497(netdata) groups=497(netdata),492(docker)
UNIT                                       LOAD   ACTIVE   SUB     DESCRIPTION
amelia-account-service.service             loaded active   running IPsoft Amelia Account Service
amelia-admin-service.service               loaded active   running IPsoft Admin Service
amelia-admin-web.service                   loaded active   running IPsoft Amelia Admin Web
amelia-batch-service.service               loaded active   running IPsoft Amelia Batch Service
amelia-duckling-service.service            loaded active   running IPsoft Amelia Duckling Service
amelia-engine-service@p001.service         loaded active   running IPsoft Amelia Engine Service - p001
amelia-escalation-service.service          loaded active   running IPsoft Amelia Escalation Service
amelia-gateway-liveengagemessaging.service loaded active   running IPsoft Amelia Gateway LiveEngageMessaging
amelia-gateway-msteams.service             loaded active   running IPsoft Amelia Gateway MSTeams
amelia-gateway-slack.service               loaded active   running IPsoft Amelia Gateway Slack
amelia-gateway-twilio.service              loaded active   running IPsoft Amelia Gateway Twilio
amelia-integration-service.service         loaded active   running IPsoft Amelia Integration Service
amelia-model-server@p001.service           loaded active   running IPsoft Amelia Model Server - p001
amelia-rest-gateway.service                loaded active   running IPsoft Amelia Rest Gateway
amelia-syntaxnet.service                   loaded active   running IPsoft Amelia SyntaxNet
amelia-user-web.service                    loaded active   running IPsoft Amelia User Web
clamd@av-gateway.service                   loaded active   running clamd scanner (av-gateway) daemon
haproxy.service                            loaded active   running HAProxy Load Balancer
ipsoft-av-gateway.service                  loaded active   running IPsoft Antivirus Gateway
ipsoft-firstboot.service                   loaded inactive dead    IPsoft-Firstboot
mysql@amelia-adb.service                   loaded active   running Percona XtraDB Cluster with config /etc/sysconfig/mysql.amelia-adb
mysql@amelia-cdb-p001.service              loaded active   running Percona XtraDB Cluster with config /etc/sysconfig/mysql.amelia-cdb-p001
mysql@amelia-kdb-master.service            loaded active   running Percona XtraDB Cluster with config /etc/sysconfig/mysql.amelia-kdb-master
mysql@amelia-kdb-slave.service             loaded active   running Percona XtraDB Cluster with config /etc/sysconfig/mysql.amelia-kdb-slave
netdata.service                            loaded active   running Real time performance monitoring
onebank-openbank-api.service               loaded active   running OneBank OpenBank Api
rabbitmq-server.service                    loaded active   running RabbitMQ broker
redis-p001.service                         loaded active   running Redis persistent key-value database
redis-sentinel.service                     loaded active   running Redis Sentinel
redis.service                              loaded active   running Redis persistent key-value database
sshd.service                               loaded active   running OpenSSH server daemon
Amelia User Web Self-check
{"status":"UP"}
Amelia Admin Web Self-check
{"status":"UP"}
Amelia Account Service Self-check
{"status":"UP"}
Amelia Admin Service Self-check
{"status":"UP"}
Amelia Engine Service Self-check
{"status":"UP"}
Amelia Model Service Self-check
{"status":"UP"}
Amelia Integration Service Self-check
{"status":"UP"}
Amelia Batch Service Self-check
{"status":"UP"}
Amelia Escalation Service Self-check
{"status":"UP"}
Amelia Duckling Service Self-check
quack!
```
