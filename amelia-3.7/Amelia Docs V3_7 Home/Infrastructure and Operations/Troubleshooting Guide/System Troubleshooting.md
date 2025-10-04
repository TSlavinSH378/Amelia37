{% version "3.x" %}
If there is a problem, but no alerts identify an Amelia system host, start troubleshooting with these steps. These steps look at disk space and other basic environment and system issues that might cause a problem for Amelia.
# Disk - /
Check the current usage with the command: **df -h**. Also, check the usage by directory with **du -h --max-depth=1 /. **The 15 largest files can be found with **find / -xdev -depth -type f -ls \|sort -nr -k 7 \|head -15. **Check which files can be deleted/gzipped/moved. The alert may be due to log files, which can be rotated with **logrotate -vf /etc/logrotate.conf**.
# Disk - /apps
If an alarm for /apps emerges, it must be treated very carefully. This folder holds all files for Amelia and, if it fills up, it will cause an outage.
Check the current usage of the computer with the df –h command. Also, check the usage by directory with du -h --max-depth=1 /apps. The 15 largest files can be found with find / -xdev -depth -type f -ls \|sort -nr -k 7 \|head -15. Check which files can be deleted, gzipped, or moved.
Check the host or any monitoring system to see if the /apps directory is low on disc space. Most likely, Amelia Web also will be down or, if a monitoring system exists, display a disk space warning. Use the cd command to enter the /apps folder. Look for files that can be removed from the /apps/tmp folder.
The alert also may be due to log files, most of which can be rotated with the logrotate -vf /etc/logrotate.conf command.
If the Amelia system still does not recover, go to /apps/backup to see if there are more than 3 files with dates older than yesterday. If so, delete one of the files and await recovery. If it doesn't recover, delete one more until recovery or until there is only 1 backup of the 3 parts in the backup directory. 
If it still does not recover, generate a list of the top 50 files by size and escalate to IPsoft.
IF the /apps folder recovers, type the following and wait between commands:
``` bash
systemctl restart amelia-engine.service@p00x (where x is the pod number)
systemctl restart amelia-admin-service
systemctl restart amelia-admin-web
systemctl restart amelia-user-web
```
Log into Amelia and ensure everything works fine.
# Disk - /boot
If the Disk - /Boot alarm appears, it usually means the machine has been recently updated and a new kernel has been installed.
Check to see if the system has been recently updated with a new kernel with the rpm command:
``` bash
# rpm -q kernel
kernel-2.6.32-279.el6.x86_64
kernel-2.6.32-279.2.1.el6.x86_64
kernel-2.6.32-279.5.2.el6.x86_64
kernel-2.6.32-279.9.1.el6.x86_64
```
If old kernel files are present, get permission to remove some of the older kernels. If approved, purge old kernels safely with these commands:
``` bash
yum install yum-utils
package-cleanup --oldkernels --count=2
```
Check to see that the alarm has recovered. If the alarm has not recovered after purging kernels, please escalate to IPsoft support.
> [!warning]  
>
> If anything is added to this partition that is NOT kernel related, please escalate the ticket IMMEDIATELY to IPsoft support. 

# Disk - /dev/shm
The virtual /dev/shm drive is an implementation of shared memory where the system creates space in memory for cached files to reside. One program will request the memory portion which other processes can then access.
If this alarm spawns, escalate to IPsoft immediately as it means there is something seriously wrong with the operating system.
# GRC Ping Test
Check if the OpenVPN process is running with **ps -ef \| grep openvpn**. Start it if it is not running with **/etc/init.d/openvpn start**. Check /var/log/messages if there are any errors regarding OpenVPN. Restart the process with **/etc/init.d/openvpn restart**. DNSmasq may have to be restarted as well with **/etc/init.d/dnsmasq restart**.
Check if there is any packet loss by running **ifconfig tun0**. After a restart of OpenVPN, RX/TX bytes should be positive values and errors/drops should be zero or very low. Ping the P-t-P IP to check connectivity to the OpenVPN server.
# HTTP - 80
Check if the httpd process is running with **/etc/init.d/httpd status**. Start it if necessary. If the process will not start, kill the old processes manually and restart with the init script. Check logs for errors in /var/log/httpd.
# Inodes - /
Check the inode usage with **df -i /**. Determine the directories with the highest inode usage with **find / -printf "%h\n" \| cut -d/ -f-2 \| sort \| uniq -c \| sort -n**. Investigate the top directories for files that can be safely removed.
# Inodes - /apps
Check the inode usage with **df -i /apps**. Determine the directories with the highest inode usage with **find /apps -printf "%h\n" \| cut -d/ -f-2 \| sort \| uniq -c \| sort -n**. Investigate the top directories for files that can be safely removed. 
# Inodes - /boot
Check the inode usage with **df -i /boot**. Determine the directories with the highest inode usage with **find /boot -printf "%h\n" \| cut -d/ -f-2 \| sort \| uniq -c \| sort -n**. Investigate the top directories for files that can be safely removed.
# Inodes - /dev/shm
Check the inode usage with **df -i /dev/shm**. Determine the directories with the highest inode usage with **find /dev/shm/ -printf "%h\n" \| cut -d/ -f-2 \| sort \| uniq -c \| sort -n**. Investigate the top directories for files that can be safely removed.
# Linux Message Log
This is a log check which reads /var/log/messages log file for errors matching to the defined ones in the config file: **/apps/IPsoft/IPremote/etc/Linux_Messages_Scubber.cfg**
Read the additional info of the ticket, examine message log and see for which error the ticket has occurred. Take appropriate action based upon that.
# Load Average
This alert gets triggered when load on the server is above configured threshold for a given period of time. Sometimes it can be just a sporadic spike, but likely it indicates a process or a few going out of control, causing the CPU to take too much time to process jobs in real time or waiting for disk I/O.
Start with gathering following system diagnostics:
1.  Check current system load:  **cat /proc/loadavg** or **uptime** or **sar -q {1}**
2.  mpstat -P ALL
3.  **iostat** with various options as needed
4.  List the top memory consuming processes:  **ps auxw --sort=-rss \| head**
5.  List of users currently logged in with **w**
6.  Top CPU consuming processes **ps auxw --sort=-%CPU \| head**
7.  Wait for recovery for 30 minutes.
8.  If the load is still above thresholds, the top processes needs to be investigated and appropriate action taken.
# mysqld/mysql_safe
For these issues, do NOT restart the mysql service. Extract relevant data from the mysql log file and include the data with an incident request.
# Managing Swap Memory
When Linux uses all physical RAM on a server, instead of RAM it uses the swap memory, a small slower partition on the hard drive that acts like memory. If the swap fills up and the RAM overflows, the server stops with errors.
> [!info]  
>
> Warning: DO NOT restart any database services for swap related issues.

To recover from this situation, the challenge is to clear out the swap memory. This can be as simple as moving swap memory data to free physical memory, if enough exists. If that is not possible, find any non-database programs and services to restart or kill.
Use the free command to see current memory size and locations and the swapon and swapoff commands to move data in or out of swap memory.
{% /version %}
