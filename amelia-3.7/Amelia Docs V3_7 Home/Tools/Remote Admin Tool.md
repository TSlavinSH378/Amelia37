{% version "3.x" %}
> [!info]  
>
> [Conductor Engine CLI](Conductor) is the next generation of this tool. Consider using Conductor instead unless there is a legacy reason to use this tool.

# Overview
This tool can be used to make Amelia application configuration changes. This includes changes to users, domains, escalations queues, auth systems, integration hosts, and anything else found under the System Settings section of the admin UI.
# Intended Audience
This tool and its documentation are meant to be used by users with Administrator access to their Amelia instances. This tool will allow users to programmatically and autonomously retrieve and update system configuration settings in an Amelia instance.
# Required Authorities

| Sections | Required Authorities |
| ----|----|
| Authentication PolicyAuthentication System | AUTHORITY_ADMIN_VIEW

    AUTHORITY_ADMIN_RBAC
\| \| Domain \|
    AUTHORITY_ADMIN_DOMAIN_VIEW
    AUTHORITY_ADMIN_DOMAIN_EDIT
\| \| Escalation Queue \|
    AUTHORITY_ADMIN_ESCALATION_QUEUE_VIEW
    AUTHORITY_ADMIN_ESCALATION_QUEUE_EDIT
\| \| Escalation Team \|
    AUTHORITY_ADMIN_ESCALATION_TEAM_VIEW
    AUTHORITY_ADMIN_ESCALATION_TEAM_EDIT
\| \|
Integration Host
Integration Cluster
\|
    AUTHORITY_ADMIN_INTEGRATION_VIEW
    AUTHORITY_ADMIN_INTEGRATION_EDIT
\| \| 1Desk Instance \|
    AUTHORITY_ADMIN_ONE_DESK_INSTANCE_VIEW
    AUTHORITY_ADMIN_ONE_DESK_INSTANCE_EDIT
    AUTHORITY_ADMIN_DOMAIN_VIEW
\| \| Role \|
    AUTHORITY_ADMIN_VIEW
    AUTHORITY_ADMIN_RBAC
\| \| UI Bundle \|
    AUTHORITY_ADMIN_VIEW
    AUTHORITY_ADMIN_UI_BUNDLE_EDIT
    AUTHORITY_ADMIN_UI_BUNDLE_DEPLOY
\| \| User \|
    AUTHORITY_ADMIN_USER_VIEW
    AUTHORITY_ADMIN_USER_EDIT
\| \| User Group \|
    AUTHORITY_ADMIN_VIEW
    AUTHORITY_ADMIN_RBAC
\|
# Example Usage
**Export Domain Configuration File**
``` groovy
java -jar ameliav3x-remote-admin-<version>-all.jar [arguments] [options]
```
# Typical Usage
In most use cases, this tool will be used to export a configuration item as its JSON representation, this JSON file can then be used to import into another instance which will create or update the appropriate configuration there. Additional convenience actions will continue to be added to accomplish tasks like setting greeting BPNs, adding integration hosts to clusters, assigning permissions, and more.
Many of the JSON files will contain UUIDs that reference other configuration items in the instance. Such as a domain referencing an authentication policy or a 1Desk instance. Be mindful when importing JSON files that if a given UUID does not exist in the target instance, the field may be left blank or the item will fail to be updated or created. To create something like a domain from scratch, the other dependencies must be created or identified first, and their UUIDs copied into the import file used to create the domain.
# Options
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Name</th>
<th class="confluenceTh">Argument</th>
<th class="confluenceTh">Description</th>
<th class="confluenceTh">Details</th>
</tr>
<tr class="odd">
<th colspan="4" class="confluenceTh" style="text-align: center;">Required Arguments</th>
</tr>
&#10;<tr class="odd">
<th class="confluenceTd">--type</th>
<td class="confluenceTd">--type VAL</td>
<td class="confluenceTd">The section to perform the action on</td>
<td class="confluenceTd"><p>AUTH_POLICY, AUTH_SYSTEM, DOMAIN, ESCALATION_QUEUE, ESCALATION_TEAM, INTEGRATION_HOST, INTEGRATION_CLUSTER, ROLE, UI_BUNDLE, USER, USER_GROUP</p></td>
</tr>
<tr class="even">
<th class="confluenceTd">--url</th>
<td class="confluenceTd">--url VAL</td>
<td class="confluenceTd">The Amelia instance URL</td>
<td class="confluenceTd"><pre><code>https://ipsoft-amelia-qa-currentstable.ipsoft.com/Amelia</code></pre></td>
</tr>
<tr class="odd">
<th class="confluenceTd">--user</th>
<td class="confluenceTd">--user VAL</td>
<td class="confluenceTd">The Amelia instance username</td>
<td class="confluenceTd"><a href="mailto:somebody@ipsoft.com">somebody@ipsoft.com</a></td>
</tr>
<tr class="even">
<th class="confluenceTd">--pass</th>
<td class="confluenceTd">--pass VAL</td>
<td class="confluenceTd">The Amelia instance password</td>
<td class="confluenceTd"><p>supersecretpassword</p></td>
</tr>
<tr class="odd">
<th class="confluenceTh" style="text-align: center;">Optional Arguments</th>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<th class="confluenceTd">--action</th>
<td class="confluenceTd">--action VAL</td>
<td class="confluenceTd">The action to perform</td>
<td class="confluenceTd"><p>IMPORT, EXPORT, DELETE, SET_GREETING, SET_PRE_ESCALATE, SET_PRE_CLOSE, HOST_TO_CLUSTER (default: EXPORT)</p></td>
</tr>
<tr class="odd">
<th class="confluenceTd">--ignore-cert</th>
<td class="confluenceTd">--ignore-cert</td>
<td class="confluenceTd">Ignores certificate errors when connecting to a host. Please only use this with hostnames you trust.</td>
<td class="confluenceTd">(default: false)</td>
</tr>
<tr class="even">
<th class="confluenceTd">--log</th>
<td class="confluenceTd">--log VAL</td>
<td class="confluenceTd">Sets the log level for the application</td>
<td class="confluenceTd">[TRACE | DEBUG | INFO | WARN | ERROR] (default: INFO)</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--auth-policy-name</th>
<td class="confluenceTd">--auth-policy-name VAL</td>
<td class="confluenceTd">The name of an authentication policy in the Amelia instance</td>
<td class="confluenceTd">Used to export</td>
</tr>
<tr class="even">
<th class="confluenceTd">--auth-system-code</th>
<td class="confluenceTd">--auth-system-code VAL</td>
<td class="confluenceTd">The code of an authentication system in the Amelia instance</td>
<td class="confluenceTd">Used to export</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--bpn-name</th>
<td class="confluenceTd">--bpn-name VAL</td>
<td class="confluenceTd">The name of a BPN in the Amelia instance</td>
<td class="confluenceTd">Used for setting greeting BPNs, BPN must be in the same domain it is being set to and must be deployed</td>
</tr>
<tr class="even">
<th class="confluenceTd">--domain-code</th>
<td class="confluenceTd">--domain-code VAL</td>
<td class="confluenceTd">The domain code of a domain in the Amelia instance</td>
<td class="confluenceTd">Used to export and for setting greeting BPNs. Not the domain name!</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--export-file</th>
<td class="confluenceTd">--export-file FILE </td>
<td class="confluenceTd">File on your local file system to export configuration files too</td>
<td class="confluenceTd">Path to a file to write exported data to. For UI Bundles this should be a directory, the configuration and ZIP files will be exported there</td>
</tr>
<tr class="even">
<th class="confluenceTd">--import-file</th>
<td class="confluenceTd">--import-file FILE </td>
<td class="confluenceTd">File on your local file system to read configuration from</td>
<td class="confluenceTd">Path to a file that contains data exported with this tool</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--integration-cluster-name</th>
<td class="confluenceTd">--integration-cluster-name VAL </td>
<td class="confluenceTd">The name of an integration cluster in the Amelia instance</td>
<td class="confluenceTd">Used to export or to add hosts to clusters</td>
</tr>
<tr class="even">
<th class="confluenceTd">--integration-host-name</th>
<td class="confluenceTd">--integration-host-name VAL </td>
<td class="confluenceTd">The name of an integration host in the Amelia instance</td>
<td class="confluenceTd">Used to export or to add hosts to clusters</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--onedesk-instance-name</th>
<td class="confluenceTd"><p>--onedesk-instance-name VAL </p></td>
<td class="confluenceTd">The name of a 1Desk instance in the Amelia instance</td>
<td class="confluenceTd">Used to export a 1Desk instance</td>
</tr>
<tr class="even">
<th class="confluenceTd">--queue-name</th>
<td class="confluenceTd">--queue-name VAL</td>
<td class="confluenceTd">The name of an escalation queue in the Amelia instance</td>
<td class="confluenceTd">Used to export an escalation queue</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--role-name</th>
<td class="confluenceTd">--role-name VAL </td>
<td class="confluenceTd">The name of a role in the Amelia instance</td>
<td class="confluenceTd">Used to export a user role</td>
</tr>
<tr class="even">
<th class="confluenceTd">--team-name</th>
<td class="confluenceTd">--team-name VAL </td>
<td class="confluenceTd">The name of an escalation team in an Amelia instance</td>
<td class="confluenceTd">Used to export an escalation team</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--ui-bundle-code</th>
<td class="confluenceTd">--ui-bundle-code VAL </td>
<td class="confluenceTd">The code of a UI bundle in the Amelia instance</td>
<td class="confluenceTd">Used to export a UI bundle</td>
</tr>
<tr class="even">
<th class="confluenceTd">--ui-bundle-zip</th>
<td class="confluenceTd">--ui-bundle-zip FILE </td>
<td class="confluenceTd">A ZIP file on your local file system that can be imported to an Amelia instance</td>
<td class="confluenceTd">Used to import a UI bundle</td>
</tr>
<tr class="odd">
<th class="confluenceTd">--user-email</th>
<td class="confluenceTd">--user-email VAL  </td>
<td class="confluenceTd">The email address of a user in the Amelia instance</td>
<td class="confluenceTd">Used to export a user</td>
</tr>
<tr class="even">
<th class="confluenceTd">--user-group-name</th>
<td class="confluenceTd">--user-group-name VAL </td>
<td class="confluenceTd">The name of a user group in the Amelia instance</td>
<td class="confluenceTd">Used to export a user group</td>
</tr>
</tbody>
</table>
# Download
External Releases: https://artifactory.ipsoft.com/artifactory/libs-release-local/net/ipsoft/ameliav3x/ameliav3x-remote-admin
{% /version %}
