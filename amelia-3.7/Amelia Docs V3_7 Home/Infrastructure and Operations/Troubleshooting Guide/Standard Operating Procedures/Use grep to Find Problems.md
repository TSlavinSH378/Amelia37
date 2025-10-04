{% version "3.x" %}
Use the grep command to try and find specific errors. For example, these commands can help locate an authentication error or activity from a specific date:
``` bash
tail -n 1000 /apps/IPsoft/amelia/amelia-admin-web/var/log/amelia-admin-web.log | grep AUTHENTICATION_SUCCESS
tail -n 1000 /apps/IPsoft/amelia/amelia-user-web/var/log/amelia-user-web.log | grep AUTHENTICATION_SUCCESS
tail -n 2000 /apps/IPsoft/amelia/amelia-engine-service/var/p001/log/amelia-engine-service.log | grep 2016-12-22
```
> [!warning]  
>
> For the engine log folder, the p001 folder file name is for pod numbered 001. Update the pod number folder name if needed.

The following terms can be used with the grep command to find possible issues in log files:

| Search Term | Log File to Search | Description |
| ----|----|----|
| not avail | amelia-engine.log | Find errors caused by lack of availability. |
| conversation ID | amelia-engine.log | If you have an ID, use it to isolate any errors in a conversation. |
| Unable to evaluate script | amelia-engine.log | Find script-related errors |
| in huge cache | amelia-engine.log | Find grammar files that generate excessively large cache storage. |
| Too large | amelia-engine.log | Find errors caused by large data size. |
| error | any log file |  |
| invalid | any log file |  |
| oom | any log file | Out of memory errors |
| 404, 501, etc | web log files | Common web server errors |
| <file path> | any log file | Search for mention of a specific <file path> |
| <service name> | any log file | Search for mention of a specific <service name> |

See [Appendix A](https://docs.amelia.com/display/AmeliaDocsV2/Appendix+A%3A+Log+File+Locations) for the location of log files used by the Amelia system.
{% /version %}
