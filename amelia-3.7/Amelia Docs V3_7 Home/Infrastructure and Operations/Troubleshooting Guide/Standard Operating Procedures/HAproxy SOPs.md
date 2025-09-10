# Check HAProxy Status
Run this command:
``` text
echo "show stat" | socat /var/run/haproxy.sock stdio | cut -d "," -f 1,2,18,57 | column -s, -t
pxname svname status last_chk
```
which generates this output:
``` text
stats FRONTEND OPEN 
stats BACKEND UP 
ft_amelia-web-http FRONTEND OPEN 
ft_amelia-web-https FRONTEND OPEN 
bk_amelia-user-web localhost UP 
bk_amelia-user-web BACKEND UP 
bk_amelia-admin-web localhost UP 
bk_amelia-admin-web BACKEND UP 
bk_amelia-h2o-web app01.prod2-cognitive.amelia.ipcenter.com UP 
bk_amelia-h2o-web app02.prod2-cognitive.amelia.ipcenter.com UP 
bk_amelia-h2o-web app03.prod2-cognitive.amelia.ipcenter.com UP 
bk_amelia-h2o-web BACKEND UP 
ft_rabbit-amqp FRONTEND OPEN 
bk_rabbit-amqp app01.prod2-cognitive.amelia.ipcenter.com UP 
bk_rabbit-amqp app02.prod2-cognitive.amelia.ipcenter.com UP 
bk_rabbit-amqp app03.prod2-cognitive.amelia.ipcenter.com UP 
bk_rabbit-amqp BACKEND UP 
ft_rabbit-stomp FRONTEND OPEN 
bk_rabbit-stomp app01.prod2-cognitive.amelia.ipcenter.com UP 
bk_rabbit-stomp app02.prod2-cognitive.amelia.ipcenter.com UP 
bk_rabbit-stomp app03.prod2-cognitive.amelia.ipcenter.com UP 
bk_rabbit-stomp BACKEND UP 
ft_mysql-kdb-master FRONTEND OPEN 
bk_mysql-kdb-master app01.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-kdb-master app02.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-kdb-master app03.prod2-cognitive.amelia.ipcenter.com DOWN Service Unavailable
bk_mysql-kdb-master BACKEND UP 
ft_mysql-kdb-slave FRONTEND OPEN 
bk_mysql-kdb-slave app01.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-kdb-slave app02.prod2-cognitive.amelia.ipcenter.com DOWN Connection reset by peer
bk_mysql-kdb-slave app03.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-kdb-slave BACKEND UP 
ft_mysql-adb FRONTEND OPEN 
bk_mysql-adb app01.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-adb app02.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-adb app03.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-adb BACKEND UP 
ft_account-service FRONTEND OPEN 
bk_account-service app01.prod2-cognitive.amelia.ipcenter.com UP HTTP content check matched
bk_account-service app02.prod2-cognitive.amelia.ipcenter.com DOWN HTTP content check did not match
bk_account-service app03.prod2-cognitive.amelia.ipcenter.com DOWN HTTP content check did not match
bk_account-service BACKEND UP 
ft_engine-service-all FRONTEND OPEN 
bk_engine-service-all app01.prod2-cognitive.amelia.ipcenter.com UP HTTP content check matched
bk_engine-service-all app02.prod2-cognitive.amelia.ipcenter.com DOWN HTTP content check did not match
bk_engine-service-all app03.prod2-cognitive.amelia.ipcenter.com DOWN HTTP content check did not match
bk_engine-service-all BACKEND UP 
ft_engine-service-p001 FRONTEND OPEN 
bk_engine-service-p001 app01.prod2-cognitive.amelia.ipcenter.com UP HTTP content check matched
bk_engine-service-p001 app02.prod2-cognitive.amelia.ipcenter.com DOWN HTTP content check did not match
bk_engine-service-p001 app03.prod2-cognitive.amelia.ipcenter.com DOWN HTTP content check did not match
bk_engine-service-p001 BACKEND UP 
ft_mysql-cdb-p001 FRONTEND OPEN 
bk_mysql-cdb-p001 app01.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-cdb-p001 app02.prod2-cognitive.amelia.ipcenter.com UP OK
bk_mysql-cdb-p001 app03.prod2-cognitive.amelia.ipcenter.com DOWN 1/2 Service Unavailable
bk_mysql-cdb-p001 BACKEND UP 
ft_redis-sentinel FRONTEND OPEN 
bk_redis-sentinel app01.prod2-cognitive.amelia.ipcenter.com UP (tcp-check)
bk_redis-sentinel app02.prod2-cognitive.amelia.ipcenter.com UP (tcp-check)
bk_redis-sentinel app03.prod2-cognitive.amelia.ipcenter.com UP (tcp-check)
bk_redis-sentinel BACKEND UP 
ft_model-server-p001 FRONTEND OPEN 
bk_model-server-p001 app01.prod2-cognitive.amelia.ipcenter.com UP HTTP content check matched
bk_model-server-p001 app02.prod2-cognitive.amelia.ipcenter.com DOWN Connection error during SSL handshake (Connection refused)
bk_model-server-p001 app03.prod2-cognitive.amelia.ipcenter.com DOWN HTTP content check did not match
bk_model-server-p001 BACKEND UP 
ft_tf_syntaxnet FRONTEND OPEN 
bk_tf_syntaxnet app01.prod2-cognitive.amelia.ipcenter.com no check 
bk_tf_syntaxnet app02.prod2-cognitive.amelia.ipcenter.com no check 
bk_tf_syntaxnet app03.prod2-cognitive.amelia.ipcenter.com no check 
bk_tf_syntaxnet BACKEND UP 
ft_duckling-service FRONTEND OPEN 
bk_duckling-service app01.prod2-cognitive.amelia.ipcenter.com UP HTTP content check matched
bk_duckling-service app02.prod2-cognitive.amelia.ipcenter.com UP HTTP content check matched
bk_duckling-service app03.prod2-cognitive.amelia.ipcenter.com UP HTTP content check matched
bk_duckling-service BACKEND UP
```
Or to keep watching refresh, run this command:
``` text
watch 'echo "show stat" | socat /var/run/haproxy.sock stdio | cut -d "," -f 1,2,18,57 | column -s, -t '
```
Or run this command:
``` text
/apps/IPsoft/bin/amelia-haproxy-status
```
# HAProxy Back or Front End is Down
If haproxy back or front end is down, type these commands to restart haproxy followed by restarts of amelia-engine@p001 and amelia-user-web@p001. The p001 suffix refers to the specific pod number.
``` text
systemctl restart haproxy
systemctl restart amelia-engine@p001 (where 001 is the pod number)
systemctl restart amelia-user-web
```
