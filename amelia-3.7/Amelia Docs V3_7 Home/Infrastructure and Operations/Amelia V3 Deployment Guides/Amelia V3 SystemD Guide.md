-   [Override Files](#AmeliaV3SystemDGuide-OverrideFiles)
-   [Validating if a Service Is Overridden](#AmeliaV3SystemDGuide-ValidatingifaServiceIsOverridden)
-   [Current Amelia V3 Override Settings](#AmeliaV3SystemDGuide-CurrentAmeliaV3OverrideSettings)
When rebooting an Amelia V3 host or restarting individual processes, all underlying components they depend on must be started first.
To start underlying components first, Amelia V3 includes systemd drop-in files for Amelia daemons and Percona / MySQL databases.  These files are independent of unit files provided by IPsoft for the amelia-\* RPMs or from third party vendors such as Percona, rabbitmq-server, redis, and haproxy. While these native package systemd unit files can be changed at any time, they should not be edited. Changes should only be made to Amelia V3 drop-in unit files applied on top of the original unit files which override values from the original files.
Amelia V3 override files are stored on disk at /etc/systemd/system/\<service\>.service.d/override.conf
## Override Files
Each Amelia daemon has its own drop-in file, specifying the list of services it **Requires** to be running before itself starts.  For example, the override for amelia-account-service is at /etc/systemd/system/amelia-account-service.service.d/override.conf with this After= and Requires= syntax.
**/etc/systemd/system/amelia-account-service.service.d/override.conf**
``` groovy
[Unit]
After=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service mysql@amelia-adb.service
Requires=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service mysql@amelia-adb.service
```
If any of haproxy.service, rabbitmq-server.service, mysql@amelia-kdb-slave.service, mysql@amelia-adb.service are not loaded and active when amelia-account-service is requested to start, they are requested to start first.

| Setting | Definition |
| ----|----|
| After | Specifies all the services that should be running before this service is started. Entries are separated by a single space. |
| Requires | Mandates these services MUST be running before this service is started. If any of these required services are not already running or fail to start, this service will not be started. Entries are separated by a single space. |

## Validating if a Service Is Overridden
To validate if a service is overridden, open a command line console and type this systemctl command where \<daemon\> is an Amelia V3 or other service:
``` bash
systemctl status -l <daemon>
```
This systemctl command should output status similar to this example:
``` bash
# systemctl status -l amelia-user-web
- amelia-user-web.service - IPsoft Amelia User Web
Loaded: loaded (/usr/lib/systemd/system/amelia-user-web.service; enabled; vendor preset: disabled)
Drop-In: /etc/systemd/system/amelia-user-web.service.d
-override.conf
Active: active (running) since Fri 2018-01-05 04:23:57 GMT; 19h ago
```
## Current Amelia V3 Override Settings
> [!warning]  
>
> These override settings are subject to change at any time.

**Overrides**
``` groovy
amelia-account-service-override
[Unit]
After=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service mysql@amelia-adb.service
Requires=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service mysql@amelia-adb.service
amelia-adb-override
[Unit]
After=haproxy.service
Requires=haproxy.service
amelia-admin-service-override
[Unit]
After=haproxy.service rabbitmq-server.service mysql@amelia-kdb-master.service
Requires=haproxy.service rabbitmq-server.service mysql@amelia-kdb-master.service
amelia-admin-web-override
[Unit]
After=haproxy.service redis.service rabbitmq-server.service mysql@amelia-kdb-master.service
Requires=haproxy.service redis.service rabbitmq-server.service mysql@amelia-kdb-master.service
amelia-batch-service-override
[Unit]
After=haproxy.service rabbitmq-server.service mysql@amelia-kdb-master.service
Requires=haproxy.service rabbitmq-server.service mysql@amelia-kdb-master.service
amelia-cdb-p001-override
[Unit]
After=haproxy.service
Requires=haproxy.service
amelia-conceptnet-api-override
[Unit]
After=haproxy.service rabbitmq-server.service postgresql-9.5.service
Requires=haproxy.service rabbitmq-server.service postgresql-9.5.service
amelia-engine-p001-service-override
[Unit]
After=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service mysql@amelia-cdb-p001.service
Requires=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service mysql@amelia-cdb-p001.service
amelia-escalation-service-override
[Unit]
After=haproxy.service rabbitmq-server.service mysql@amelia-kdb-master.service
Requires=haproxy.service rabbitmq-server.service mysql@amelia-kdb-master.service
amelia-kdb-master-override
[Unit]
After=haproxy.service
Requires=haproxy.service
amelia-kdb-slave-override
[Unit]
After=haproxy.service
Requires=haproxy.service
amelia-model-server-override
[Unit]
After=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service
Requires=haproxy.service rabbitmq-server.service mysql@amelia-kdb-slave.service
amelia-user-web-override
[Unit]
After=haproxy.service redis.service rabbitmq-server.service mysql@amelia-kdb-slave.service
Requires=haproxy.service redis.service rabbitmq-server.service mysql@amelia-kdb-slave.service
```
