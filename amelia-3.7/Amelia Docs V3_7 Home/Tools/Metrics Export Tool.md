> [!info]  
>
> [Conductor Engine CLI](Conductor) is the next generation of this tool. Consider using Conductor instead unless there is a legacy reason to use this tool.

The Amelia MetEx (**Met**rics **Ex**port)Tool can be used to export Amelia conversation metrics and transcripts from a list of domains for a given date range. The tool can also create Eddie replay test files for each conversation exported. The tool is intended to be used with Amelia instances version 3.6 and above to take full advantage of the JSON export format and expanded metrics.
A secondary feature of the tool allows the user to create an Eddie replay file for each conversation exported. To learn more about Eddie conversation tests read the documentation here: <https://eddie-amelia.ipsoft.com/#!/docs/user>.
# Intended Audience
This page and instructions herein are intended for Amelia admins and engineers that regularly need to export conversations from Amelia instances and create test files for those conversations. The export files can also be used in conversation analysis either manually in CSV format or in an automation pipeline in the JSON format.
# Required Authorities
The user account used with the tool must have the following authorities to be able to export metrics from an Amelia instance:
    AUTHORITY_METRICS_VIEW
    AUTHORITY_CONVERSATION_EXPORT
# Usage
Examples:
**Export chats from multiple domains to console**
``` groovy
java -jar ameliav3x-metrics-export-<version>-all.jar [arguments] [options] [flags]
```
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Name</th>
<th class="confluenceTh">Description</th>
<th class="confluenceTh">Argument Details</th>
</tr>
<tr class="odd">
<th colspan="3" class="confluenceTh" style="text-align: center;">Arguments</th>
</tr>
&#10;<tr class="odd">
<th class="confluenceTd">--url VAL</th>
<td class="confluenceTd">The URL of the Amelia instance to export metrics from. Should be a full URL such as <a href="https://ipsoft-v3-amelia-playgroundus.ipsoft.com/Amelia">https://ipsoft-v3-amelia-playgroundus.ipsoft.com/Amelia</a></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<th class="confluenceTd">--properties VAL</th>
<td class="confluenceTd">A JSON file containing values for all arguments and options. If specified the values in the file will be used over anything given on the command line.</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>Example properties file: <a href="http://dtools.ipsoft.com/confluence/download/attachments/93041182/properties.json?version=1&amp;modificationDate=1565295032000&amp;api=v2">properties.json</a></p>
</div></td>
</tr>
<tr class="odd">
<th class="confluenceTh" style="text-align: center;">Options</th>
<td></td>
<td></td>
</tr>
<tr class="even">
<th class="confluenceTd">--user VAL</th>
<td class="confluenceTd">Username of the account used to login to the Amelia instance. If not provided on the command line or properties file it will be prompted for.</td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<th class="confluenceTd">--pass VAL</th>
<td class="confluenceTd">The password of the account used to login to the Amelia instance. If not provided on the command line or properties file it will be prompted for.</td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<th class="confluenceTd">--domains VAL</th>
<td class="confluenceTd">Space-separated list of domain codes to export metrics from.</td>
<td class="confluenceTd"><p>Example: --domains ncp ncp_test ncp2 ncp3</p></td>
</tr>
<tr class="odd">
<th class="confluenceTd">--from VAL</th>
<td class="confluenceTd">Start date to export metrics from.</td>
<td class="confluenceTd">Date format: yyyy-MM-ddThh:mm:ssZ</td>
</tr>
<tr class="even">
<th class="confluenceTd">--to VAL</th>
<td class="confluenceTd">End date to export metrics to.</td>
<td class="confluenceTd">Date format: yyyy-MM-ddThh:mm:ssZ</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--format VAL</th>
<td class="confluenceTd">The choice to export metrics in JSON or CSV format (optional, default: CSV).</td>
<td class="confluenceTd">VAL can be JSON or CSV</td>
</tr>
<tr class="even">
<th class="confluenceTd">--log VAL</th>
<td class="confluenceTd">Set the log level for Impex and other related classes (optional, default: INFO).</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>VAL is standard log levels, <strong>DEBUG</strong>, <strong>INFO</strong>, <strong>WARN</strong>, etc.</p>
</div></td>
</tr>
<tr class="odd">
<th class="confluenceTh" style="text-align: center;">Flags</th>
<td></td>
<td></td>
</tr>
<tr class="even">
<th class="confluenceTd">--create-tests</th>
<td class="confluenceTd">If specified, the tool will create a tests directory in the output directory for an Eddie replay file containing a test for each conversation exported (optional, default: false).</td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="odd">
<th class="confluenceTd">--ignore-cert</th>
<td class="confluenceTd">Ignores certificate errors when connecting to the Amelia instance (optional, default: false).</td>
<td class="confluenceTd"><p>Please only use this with hostnames that you trust!</p></td>
</tr>
<tr class="even">
<th class="confluenceTd">--help</th>
<td class="confluenceTd">Displays the usage message.</td>
<td class="confluenceTd"><br />
</td>
</tr>
</tbody>
</table>
# Output
**Execution Output**
``` groovy
NCPMBP% java -jar build/libs/ameliav3x-metrics-export-3.7-SNAPSHOT-all.jar --properties src/test/resources/properties.json
2019-08-08 16:26:06,460 [main] WARN  -- AmeliaV3Metex.java 55 - using command line specified log levels: INFO
Username: nick.corso-passaro@ipsoft.com
Password: 
2019-08-08 16:26:15,986 [Amelia-API-Exe-0] INFO  -- ApiSessionImpl.java 166 - Logout called on Api Session: ApiSessionImpl(id=d236cdd0-f903-4e23-87d6-a3d462de7dec, created=2019-08-08T20:26:14.751Z)
2019-08-08 16:26:16,620 [main] INFO  -- MetricsExport.java 35 - Exporting metrics for domains [6c64fe50-9432-4482-b206-91bc4cf31adb, b2f83045-3b32-4cf4-ad3c-a3598f495fec]
2019-08-08 16:26:17,933 [Amelia-API-Exe-0] INFO  -- ApiSessionImpl.java 166 - Logout called on Api Session: ApiSessionImpl(id=bbfc875f-a378-4f0b-a69b-d9f2d2187d3d, created=2019-08-08T20:26:15.983Z)
2019-08-08 16:26:18,080 [main] INFO  -- FileIO.java 75 - Export file written to /tmp/metex/chats/chat-export-2019-08-08-16-26-13.json
2019-08-08 16:26:18,091 [main] INFO  -- FileIO.java 75 - Export file written to /tmp/metex/tests/test-export-2019-08-08-16-26-13.replay
```
Output files:
[test-export-2019-08-08-16-26-13.replay](attachments/11940492/32510611.replay)
[chat-export-2019-08-08-16-26-13.json](attachments/11940492/32510612.json)
# Data Dictionary
See the following pages for the appropriate data dictionaries and schemas that are exported by the Metrics Export Tool:
[Data Dictionary - Amelia v3.6](https://docs.ipsoft.com/display/AmeliaDocsV36/Monitoring+with+Administration+Pages#MonitoringwithAdministrationPages-ExportConversations)
[Data Dictionary - Amelia v3.7](https://docs.ipsoft.com/display/AmeliaDocsV37/Monitoring+with+Administration+Pages#MonitoringwithAdministrationPages-DataDictionary)
#  Download
> [!info]  
>
> Using this tool requires Java 8 Update 152 or above on the executing machine (your laptop, server, or otherwise).

External Releases: <https://artifactory.ipsoft.com/artifactory/libs-release-local/net/ipsoft/ameliav3x/ameliav3x-metrics-export/>
