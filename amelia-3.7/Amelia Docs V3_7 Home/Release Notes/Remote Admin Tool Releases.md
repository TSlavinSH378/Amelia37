{% version "3.x" %}
Release notes for this tool track Amelia releases, for example, 3.6 and 3.7 are backwards compatible within their Amelia releases. A 3.6.1 Remote Admin Tool release both work with Amelia 3.6.0 to the latest 3.6.x Amelia release.
# 3.7.3
Release date: April 16, 2020
## Summary
In the final Remote Admin release we add support for 1RPA instance configuration as well as fix a bug when exporting UI bundles. Across the board dependency handling has been improved.
## Important highlights from this release
1.  1RPA instance configurations can now be imported and exported
2.  Fixed a bug preventing UI bundles from being exported
3.  Improved dependency handling for all configuration types.
## New Feature
AM3-12865 - Add 1RPA instance support
## Bug
AM3-12826 - When exporting UI bundle revisions are not exported properly
## Story
AM3-12866 - exporting/importing a domain should also handle all dependencies
# 3.7.2
Release date: February 7, 2020
## Summary
This is a small release with a few new additions and quality of life features.
## New Feature
AM3-7793 - Maintain conversation event domain settings
## Enhancement (Client Requested)
AM3-11359 - Add the set Pre-Escalation Process functionality to the Escalation Queues Configuration
## Task
AM3-12475 - Replace Gson with Jackson for writing JSON files  
AM3-12474 - Add log message and default value when export or import directory is null  
AM3-11860 - Change import/export file arguments to specify directories  
AM3-11617 - Make remote admin logging the same as impex
## Defect (Client Requested)
AM3-12473 - Fails to import/export the amelia_userId defined in domain configuration settings
# 3.7.1
Release date: June 13, 2019
## Summary
This release adds a few features and fixes an issue that occurred when writing files to the file system.
## New Stuff
AM3-9915 - This change adds support for the other two conversation event processes that can be set on a domain, pre-escalate and pre-close. The actions SET_PRE_ESCALATE and SET_PRE_CLOSE have been added respectively. Use these actions with the --bpnName option to specify which BPN to set for that processes. The BPN must be deployed and must be in the same domain.
AM3-9933 - This change adds a new value to the --action option, DELETE. Currently, this is only implemented for users but may be expanded to other types in the future. To delete a user, specify the DELETE action with a user's email address option.
AM3-9937 - This change allows the --user and --pass options to be omitted from the command line. If they are omitted they will be prompted for when the tool runs.
AM3-9938 - This change will allow setting an initial password for a new user when importing a user file. To do so, the file must have the following properties: changePassword, newPassword, and confirmPassword. Example:
``` groovy
"changePassword": true,
"newPassword":"2Jdef@7Ta*N&",
"confirmPassword":"2Jdef@7Ta*N&"
```
## Bugs Fixed
AM3-9993 - Fixes a bug that caused writing files to non-absolute paths to fail with a NullPointerException.
# 3.6.1
Release date: June 13, 2019
## Summary
This release adds a few features and fixes an issue that occurred when writing files to the file system.
## New Stuff
AM3-9915 - This change adds support for the other two conversation event processes that can be set on a domain, pre-escalate and pre-close. The actions SET_PRE_ESCALATE and SET_PRE_CLOSE have been added respectively. Use these actions with the --bpnName option to specify which BPN to set for that processes. The BPN must be deployed and must be in the same domain.
AM3-9933 - This change adds a new value to the --action option, DELETE. Currently, this is only implemented for users but may be expanded to other types in the future. To delete a user, specify the DELETE action with a user's email address option.
AM3-9937 - This change allows the --user and --pass options to be omitted from the command line. If they are omitted they will be prompted for when the tool runs.
AM3-9938 - This change will allow setting an initial password for a new user when importing a user file. To do so, the file must have the following properties: changePassword, newPassword, and confirmPassword. Example:
``` groovy
"changePassword": true,
"newPassword":"2Jdef@7Ta*N&",
"confirmPassword":"2Jdef@7Ta*N&"
```
## Bugs Fixed
AM3-9993 - Fixes a bug that caused writing files to non-absolute paths to fail with a NullPointerException.
{% /version %}
