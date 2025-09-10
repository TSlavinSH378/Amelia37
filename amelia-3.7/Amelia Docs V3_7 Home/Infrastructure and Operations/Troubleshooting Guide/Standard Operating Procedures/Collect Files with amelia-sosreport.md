amelia-sosreport is a Bash script that collects various logs, configuration files, and command output into a single easy-to-transfer file.  For environments with limited access, this is helpful to diagnose issues that may arise.
The script is based on shell commands provided by Red Hat (<https://access.redhat.com/solutions/68996>) and has been amended to collect data on specific Amelia software.
To run this script, ensure it is executable then run the script with these commands:
``` text
chmod a+x amelia-sosreport
./amelia-sosreport
```
The script creates these files:
-   /apps/IPsoft/artifacts/sosreport - A directory containing the uncompressed results of the script
-   /apps/IPsoft/artifacts/sosreport/sosreport-$HOSTNAME.tgz - This is the file to transfer to IPsoft for assistance
