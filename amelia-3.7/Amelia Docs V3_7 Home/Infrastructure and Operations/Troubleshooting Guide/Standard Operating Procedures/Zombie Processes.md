{% version "3.x" %}
Zombie processes are processes that exist but do nothing. They’re neither active or disappeared from a system.
To find zombie processes, log in with the sudoscript ss command and enter this command:
``` bash
ss
ps auxwww | grep -w Z | grep defunct | grep -v grep
```
Then check the parent process IDs of these zombies. If IpmonX processes, then bounce IpmonX.
To kill zombie processes:
``` bash
ps aux
kill -HUP $(ps -A -ostat,ppid | grep -e '[zZ]'| awk '{ print $2 }')
```
> [!warning]  
>
> Confirm services are up and running. Look at the log file to determine what caused failure. Then escalate to IPsoft. If zombie processes cannot be removed, escalate to IPsoft.
{% /version %}
