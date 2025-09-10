-   [Managing Log Files](#LogFileSOPs-ManagingLogFiles)
-   [Location of Common Log Files](#LogFileSOPs-LocationofCommonLogFiles)
-   [Files for amelia-engine, amelia-admin-web, and amelia-user-web](#LogFileSOPs-Filesforamelia-engine,amelia-admin-web,andamelia-user-web)
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
``` text
sudo -i
tail -f -n 500 /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log (where 001 is the pod number)
```
To tail the amelia-admin-web log file after login as root:
``` text
sudo -i
tail -f -n 500 /apps/IPsoft/amelia/amelia-admin-web/var/log/amelia-admin-web.log
```
To tail the amelia-user-web log file after login as root:
``` text
sudo -i
tail -f -n 500 /apps/IPsoft/amelia/amelia-user-web/var/log/amelia-user-web.log
```
