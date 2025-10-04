{% version "3.x" %}
There are several checks that require restarts of the different Amelia components. The following alerts require a restart.
# [R](https://paas.ipcenter.com/IPmon/NY1-IPmon24/cgi-bin/extinfo.cgi?type=2&host=amelia-engine.metlife-amelia-prod.ipsoft.com.ipsoft&service=Amelia+Response+Time)esponse Time Alert
The Amelia response time alert will go critical immediately if the response time is \> 20 seconds. This means that its taking more than 20 seconds for the Amelia engine to respond to the customer interacting with her.
If this happens after an Amelia engine restart, the first step is to log into Amelia's production URL and start a conversation with her.  This causes the Mbean to register upon instantiation of the conversation.
If starting a conversation does not work, restart amelia-engine and amelia-web services then check their status to verify the run properly.
``` text
systemctl restart amelia-engine.service@p001 (where 001 is the pod number)
systemctl restart amelia-admin-web
systemctl restart amelia-user-web
systemctl restart amelia-admin-service
systemctl status amelia-engine.service@p001 (where 001 is the pod number)
systemctl status amelia-admin-web
systemctl status amelia-user-web
systemctl status amelia-admin-service
```
# Garbage Collector Q1 Old Generation Alert
If this alert appears, restart the amelia-engine and amelia-web services with these commands then check status to confirm they run properly:
``` text
systemctl restart amelia-engine.service@p001 (where 001 is the pod number)
systemctl restart amelia-admin-web
systemctl restart amelia-user-web
systemctl restart amelia-admin-service
systemctl status amelia-engine.service@p001 (where 001 is the pod number)
systemctl status amelia-admin-web
systemctl status amelia-user-web
systemctl status amelia-admin-service
```
# Amelia V3 Webcheck Alert
This alert indicates Amelia's web interface front end is down.
1.  Log into Amelia's production URL to check the web interface is visible and functions.
2.  Check the IPmon for related issues. If the disk is full, for example, restarting the web service is ineffective.
3.  Verify all other possible issues are explored before restarting the amelia-web services. 
``` text
systemctl restart amelia-user-web.service
systemctl restart amelia-admin-web.service
```
> [!info]  
>
> If you cannot access the web interface with the named URL BUT you are able to access via IP address, the alert likely is caused by an DNS/Load balancer issue.

# Chrony Offset Alert
This alert is received for any Amelia based alerts unable to be resolved by automation.
1.  SSH into the host using the hostname and switch to root using the sudoscript ss command.
2.  Run the following command:
    ``` text
    chronyc -a 'burst 4/4'
    ```
3.  To see the peers, run the following chronyc command:
    ``` text
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
    ``` text
    systemctl restart chronyd
    ```
    You may see a 'no peer found' type message.  If so, very possibly the service is healing itself.  Give the system several more minutes or a half hour before continuing to step 3.
# Upload File 503 Errors
When files do not upload and an unknown or 503 error displays, the problem could be anti-virus software included with Amelia that checks files before they upload. If the anti-virus software is not running or otherwise not functioning, files will not upload.
The ipsoft-av-gateway service sometimes does not restart properly because the systemd unit file, <clamd@av-gateway.servic>e, is static. This can be confirmed with this command:
``` text
systemctl list-unit-files | grep -e clamd -e av-gateway
```
which generates this output:
``` text
clamd@.service                                static
clamd@scan.service                            disabled
ipsoft-av-gateway.service                     enabled
```
For hosts with ipsoft-av-gateway.service installed, run this command in a root shell:
``` text
echo -e "[Unit]\nRequires=clamd@av-gateway.service" | SYSTEMD_EDITOR=/usr/bin/tee systemctl edit ipsoft-av-gateway.service
```
To start the ipsoft-av-gateway service one time in the root shell, run these commands:
``` text
systemctl restart ipsoft-av-gateway.service
sleep 30
systemctl status ipsoft-av-gateway.service
```
This one line command combines both steps:
``` text
echo -e "[Unit]\nRequires=clamd@av-gateway.service" | SYSTEMD_EDITOR=/usr/bin/tee systemctl edit ipsoft-av-gateway.service; systemctl restart ipsoft-av-gateway; sleep 30; systemctl status ipsoft-av-gateway
```
## Scenario 1: Restarted in Incorrect Order
Run the clam-freshclam command first. Then restart the clamd@av-gateway.service and test to upload a file using the Amelia front-end.
## Scenario 2: Can't Stop Anti-Virus Service
Possible need to Kill that PID and then restart the service with this command in a root shell:
``` text
# systemctl restart clam-freshclam.service clamd@av-gateway.service ipsoft-av-gateway.service
```
## Scenario 3: On-Premise, Unable to To Run
Edit the /apps/IPsoft/amelia/amelia-common-config/application.properties file, add this line with this command in a root shell:
``` text
# echo amelia.file.virus-scan.enabled=false >> /apps/IPsoft/amelia/amelia-common-config/application.properties
```
then restart user-web and admin-web with this command in a root shell:
``` text
# systemctl restart amelia-user-web amelia-admin-web
```
## Scenario 4: On-Premise, Port Blocked
If Amelia is installed at the client's location, check definition updates over port 80 are not blocked. 
A firewall rule is probably in place, as its unable to connect to (104.16.186.138) database.clamav.net on port 80 and generates this error:
``` text
ClamAV health check failed for 127.0.0.1:3310
```
Check the /etc/haproxy/haproxy.cfg file is correct.
## Scenario 5: Multiple Issues with File Uploads/Downloads
Check the anti-virus gateway files in the /apps/IPsoft/ipsoft-av-gateway/config/jmx/ folder.
If there are no files in this directory, run these commands in a root shell:
``` text
# cp /apps/IPsoft/amelia/amelia-engine-service/config-p001/jmx/* /apps/IPsoft/ipsoft-av-gateway/config/jmx/
# chown ipsoft:ipsoft /apps/IPsoft/ipsoft-av-gateway/config/jmx/*
# chmod 600 /apps/IPsoft/ipsoft-av-gateway/config/jmx/*
```
Once the jmx files appear in the folder, restart the services in the following order:
``` text
# systemctl restart clam-freshclam.service clamd@av-gateway.service ipsoft-av-gateway.service
```
# Resolving ipsoft-av-gateway Not Restarting
## ceiceIssue
Some instances have been found where ipsoft-av-gateway does not restart properly.  This is due to the systemd unit file, clamd@av-gateway.service, being *static*.
Static units are those which cannot be enabled/disabled; however it doesn't mean they are always executed.  They will only execute if another unit depends on them, or if they are manually started.  Run this command to view status.
``` text
# systemctl list-unit-files | grep -e clamd -e av-gateway
clamd@.service                                static
clamd@scan.service                            disabled
ipsoft-av-gateway.service                     enabled
```
## Solution
On the hosts with ipsoft-av-gateway.service installed, run the following one-liner in a *root* shell:
**Edit unit file**
``` text
echo -e "[Unit]\nRequires=clamd@av-gateway.service" | SYSTEMD_EDITOR=/usr/bin/tee systemctl edit ipsoft-av-gateway.service
```
To start up the ipsoft-av-gateway service (one-time) in the root shell, run this command:
**Restart ipsoft-av-gateway.service**
``` groovy
systemctl restart ipsoft-av-gateway.service
sleep 30
systemctl status ipsoft-av-gateway.service
```
## Shortcut
For those who like a one-liner, run this command:
**One-liner**
``` text
echo -e "[Unit]\nRequires=clamd@av-gateway.service" | SYSTEMD_EDITOR=/usr/bin/tee systemctl edit ipsoft-av-gateway.service; systemctl restart ipsoft-av-gateway; sleep 30; systemctl status ipsoft-av-gateway
```
{% /version %}
