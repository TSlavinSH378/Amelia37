-   [Overview](#ImportExportandDeployAmeliaTool-Overview)
-   [Intended Audience](#ImportExportandDeployAmeliaTool-IntendedAudience)
-   [Required Authorities](#ImportExportandDeployAmeliaTool-RequiredAuthorities)
-   [Command Usage](#ImportExportandDeployAmeliaTool-CommandUsage)
-   [Command Option Flags (changed in 3.6.4 and 3.7.4)](#ImportExportandDeployAmeliaTool-CommandOptionFlags(changedin3.6.4and3.7.4))
-   [Supported Content](#ImportExportandDeployAmeliaTool-SupportedContent)
-   [Directory Structure (changed in 3.7.9)](#ImportExportandDeployAmeliaTool-DirectoryStructure(changedin3.7.9))
-   [Content Container Types](#ImportExportandDeployAmeliaTool-ContentContainerTypes)
    -   [Amelia](#ImportExportandDeployAmeliaTool-Amelia)
    -   [File System](#ImportExportandDeployAmeliaTool-FileSystem)
    -   [Git](#ImportExportandDeployAmeliaTool-Git)
    -   [Zip](#ImportExportandDeployAmeliaTool-Zip)
-   [Release Notes](#ImportExportandDeployAmeliaTool-ReleaseNotes)
-   [Download](#ImportExportandDeployAmeliaTool-Download)
-   [FAQs](#ImportExportandDeployAmeliaTool-FAQs)
> [!info]  
>
> [Conductor Engine CLI](Conductor) is the next generation of this tool. Consider using Conductor instead unless there is a legacy reason to use this tool.

# Overview
The Amelia V3 ImpExDep (**Imp**ort/**Ex**port/**Dep**loy) Tool can be used to move Amelia knowledge content between instances, file systems, and Git repositories. The tool can also be used to delete or deploy content in an Amelia instance.
# Intended Audience
This import/export and deploy tool is intended for use by Amelia administrators and engineers who regularly move and deploy content between environments.
# Required Authorities
> [!warning]  
>
> The authorities detailed here are specific to each content type. To access any content, the authority AUTHORITY_ADMIN_VIEW must be added as well.

The user account used to authenticate the tool will need to have the appropriate authorities to modify content within an Amelia instance. They are as follows:

| Content Type | Required Authorities |
| ----|----|
| BPNSCRIPT | /** * Allows user to create and edit a BPN. */AUTHORITY_ADMIN_BPN_EDIT/** * Allows a user to deploy a BPN. */AUTHORITY_ADMIN_BPN_DEPLOY/** * Allows a user to view a BPN. */AUTHORITY_ADMIN_BPN_VIEW

\| \|
TABULAR
\|
    /** * Allows admin to add new files to tabular data. */AUTHORITY_TABULAR_ADD/** * Allows admin to edit the tabular data metadata and content. */AUTHORITY_TABULAR_EDIT/** * Allows admin to view tabular data. */AUTHORITY_TABULAR_VIEW
\| \|
MULTIMEDIA
\|
    /** * Allows users to view Content Manager. */AUTHORITY_ADMIN_CONTENT_MANAGEMENT_VIEW/** * Allows users to create and edit documents/buckets in Content Manager. */AUTHORITY_ADMIN_CONTENT_MANAGEMENT_EDIT/** * Allows users to delete documents/buckets in Content Manager. */AUTHORITY_ADMIN_CONTENT_MANAGEMENT_DELETE
\| \|
GRAMMARINTENTENTITYCLASSIFIERTRAININGNLU (3.7 only)
\|
    /** * Allows knowledge designers to see the training system related panel like intent, entity, training dashboard. */AUTHORITY_TRAINING_VIEW/** * Allows knowledge designers to edit the train entities like intent, entity. */AUTHORITY_TRAINING_EDIT
\| \|
SEMNET
\|
    /** * Allows users to view Semnet documents. */AUTHORITY_ADMIN_SEMNET_DOCUMENT_VIEW/** * Allows users to create and edit Semnet documents. */AUTHORITY_ADMIN_SEMNET_DOCUMENT_EDIT/** * Allows users to delete Semnet documents. */AUTHORITY_ADMIN_SEMNET_DOCUMENT_DELETE
\| \|
INTEGRATION_ASSET, INTEGRATION_FLOW,INTEGRATION_PROPERTY_SET
\|
    /** * Allows user to create and edit an Integration Flow or Asset. */AUTHORITY_ADMIN_INTEGRATION_EDIT/** * Allows a user to deploy an Integration Flow. */AUTHORITY_ADMIN_INTEGRATION_DEPLOY/** * Allows a user to view an Integration Flow or Asset. */AUTHORITY_ADMIN_INTEGRATION_VIEW
\| \|
RESPONSE_POOL
\|
    /** * Allows user to see the response pool. */AUTHORITY_RESPONSE_POOL_VIEW/** * Allows user to edit the response pool. */AUTHORITY_RESPONSE_POOL_EDIT
\| \|
AIML
\|
    /** * Allows users to view AIML documents. */AUTHORITY_ADMIN_AIML_DOCUMENT_VIEW/** * Allows users to create and edit AIML documents. */AUTHORITY_ADMIN_AIML_DOCUMENT_EDIT/** * Allows users to delete AIML documents. */AUTHORITY_ADMIN_AIML_DOCUMENT_DELETE
\|
# Command Usage
**Usage**
``` groovy
java -jar ameliav3x-impex-<version>-all.jar [arguments] [options] [flags]
```
See the table below for detailed information on the available arguments, options, and flags.
# Command Option Flags (changed in 3.6.4 and 3.7.4)
<table class="wrapped confluenceTable" style="width: 1160.0px;">
<tbody>
<tr class="header">
<th class="confluenceTh" style="width: 128.0px">Name</th>
<th class="confluenceTh" style="width: 572.0px">Description</th>
<th class="confluenceTh" style="width: 460.0px">Argument Details</th>
</tr>
<tr class="odd">
<th colspan="3" class="confluenceTh" style="text-align: center; width: 1160.0px;">Arguments</th>
</tr>
&#10;<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--sourceUrl VAL</th>
<td class="confluenceTd" style="width: 572.0px">The URL of the source content. Always required unless using --targetUrl and --clean.</td>
<td class="confluenceTd" style="width: 460.0px"><p>Example URLs:</p>
<p>Amelia <strong>(must end in /Amelia WITHOUT a trailing slash</strong>):</p>
<p>https://&lt;your-hostname&gt;/Amelia</p>
<p>Git (<strong>must start with ssh or http and end with .git</strong>):</p>
<p>ssh://&lt;username&gt;@&lt;hostname&gt;/&lt;repository-name&gt;.git</p>
<p>https://&lt;username&gt;@&lt;hostname&gt;/&lt;repository-name&gt;.git</p>
<p>ZIP Files (<strong>must end with .zip</strong>):</p>
<p>/tmp/backup/backup.zip</p>
<p>https://&lt;hostname&gt;/OneITSM.zip</p>
<p>File System (<strong>if none of the above conditions are met, the URL is assumed to be a file system directory</strong>):</p>
<p>/tmp/backup</p>
<p>C:\Users\user\workspace</p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--targetUrl VAL</th>
<td class="confluenceTd" style="width: 572.0px">The URL of the target content. (required)</td>
<td class="confluenceTd" style="width: 460.0px">See valid URLs above.</td>
</tr>
<tr class="odd">
<th class="confluenceTh" style="text-align: center; width: 1160.0px;">Options</th>
<td></td>
<td></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--sourceUser VAL</th>
<td class="confluenceTd" style="width: 572.0px">Username of the account used to login to the system identified by --sourceUrl</td>
<td class="confluenceTd" style="width: 460.0px"><p>If this option is not provided but --sourceUrl is it will be prompted for.</p>
<p><strong>Applies to: Amelia, Git</strong></p></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--sourcePass VAL</th>
<td class="confluenceTd" style="width: 572.0px">The password of the account used to login to the system identified by --sourceUrl</td>
<td class="confluenceTd" style="width: 460.0px"><p>If this option is not provided but --sourceUrl is it will be prompted for.</p>
<p>If you have special characters in your passwords such as '@' and '&amp;' surround it with single quotes if providing in the command.</p>
<p><strong>Applies to: Amelia, Git</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--sourceDomain VAL</th>
<td class="confluenceTd" style="width: 572.0px">Domain <strong>CODE</strong> in the Amelia instance (required if sourceUrl is an Amelia instance, will be prompted if not given)</td>
<td class="confluenceTd" style="width: 460.0px"><p>If this option is not provided but --sourceUrl is it will be prompted for.</p>
<p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--targetUser VAL</th>
<td class="confluenceTd" style="width: 572.0px">Username of the account used to login to the system identified by --targetUrl</td>
<td class="confluenceTd" style="width: 460.0px"><p>If this option is not provided but --targetUrl is it will be prompted for.</p>
<p><strong>Applies to: Amelia, Git</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--targetPass VAL</th>
<td class="confluenceTd" style="width: 572.0px">The password of the account used to login to the system identified by --targetUrl</td>
<td class="confluenceTd" style="width: 460.0px"><p>If this option is not provided but --targetUrl is it will be prompted for</p>
<p>If you have special characters in your passwords such as '@' and '&amp;' surround it with single quotes if providing in the command.</p>
<p><strong>Applies to: Amelia, Git</strong></p></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--targetDomain VAL</th>
<td class="confluenceTd" style="width: 572.0px">Domain CODE in the Amelia instance</td>
<td class="confluenceTd" style="width: 460.0px"><p>If this option is not provided but --targetUrl is it will be prompted for.</p>
<p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--gitBranch VAL</th>
<td class="confluenceTd" style="width: 572.0px">Git branch for changes to be pushed to or pulled from</td>
<td class="confluenceTd" style="width: 460.0px"><p>Required if --sourceUrl or --targetUrl is a Git repository, will be prompted if not given.</p>
<p>Probably shouldn't be master. <img src="images/icons/emoticons/wink.svg" /></p>
<p><strong>Applies to: Git</strong></p></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--commitMessage VAL</th>
<td class="confluenceTd" style="width: 572.0px">Message to be supplied on commit when using Git as a target (required if skipPrompts flag is used, will be prompted if not given)</td>
<td class="confluenceTd" style="width: 460.0px"><strong>Applies to: Git</strong></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--sshKeyPath VAL</th>
<td class="confluenceTd" style="width: 572.0px">Local file system path of the SSH private key to be used to authenticate with a Git repository (required if URL begins with ssh)</td>
<td class="confluenceTd" style="width: 460.0px"><p>Default is usually ~/.ssh/id_rsa</p>
<p><strong>Applies to: Git</strong></p></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--sshPassphrase VAL</th>
<td class="confluenceTd" style="width: 572.0px">Passphrase for the SSH key specified by sshKeyPath (required if URL begins with ssh)</td>
<td class="confluenceTd" style="width: 460.0px"><strong>Applies to: Git</strong></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--search VAL</th>
<td class="confluenceTd" style="width: 572.0px">If specified, value is used to search through each applicable content type before exporting. This would provide the same result as typing in the value in one of the search boxes in the Admin UI. (optional, default: null)</td>
<td class="confluenceTd" style="width: 460.0px"><div class="content-wrapper">
<p>Currently, does not affect <strong>SEMNET</strong> or <strong>GRAMMAR</strong>.</p>
<p><strong>Applies to: Amelia</strong></p>
</div></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--include VAL</th>
<td class="confluenceTd" style="width: 572.0px">Content types to be included in all actions, anything not included is excluded. Cannot be combined with --exclude. (optional, default: ALL)</td>
<td class="confluenceTd" style="width: 460.0px"><div class="content-wrapper">
<p>To explicitly include multiple content types, specify this option multiple times such as:</p>
<p>--include <strong>BPN</strong> --include <strong>INTENT</strong> --include <strong>ENTITY</strong></p>
<p><strong>Applies to: Amelia, File System, Git, Zip<br />
</strong></p>
</div></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--exclude VAL</th>
<td class="confluenceTd" style="width: 572.0px">Content types to be excluded from all actions, anything not excluded is included. Cannot be combined with --include. (optional, default: NONE)</td>
<td class="confluenceTd" style="width: 460.0px"><div class="content-wrapper">
<p>To explicitly exclude multiple content types, specify this option multiple times such as:</p>
<p>--exclude <strong>BPN</strong> --exclude <strong>INTENT</strong> --exclude <strong>ENTITY</strong></p>
<p><strong><strong>Applies to: Amelia, File System, Git, Zip</strong></strong></p>
</div></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--importStrategy VAL</th>
<td class="confluenceTd" style="width: 572.0px">How to import the content into the target (optional, default: MERGE)</td>
<td class="confluenceTd" style="width: 460.0px"><p><strong>OVERWRITE</strong>: make the content in the target match the source, will delete any content that would be overwritten and creates everything new. Anything that existed in the target and not the source will be deleted.</p>
<p><strong>MERGE</strong>: combine the source and target content, will update any existing content and create anything new.</p>
<p><strong>ADD</strong>: adds source content to the target, will not overwrite or delete anything (target wins all conflicts).</p>
<p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--revisions, – revisionTarget VAL</th>
<td class="confluenceTd" style="width: 572.0px">The choice to export revisions up to the latest or deployed revision (optional, default: DEPLOTYED)</td>
<td class="confluenceTd" style="width: 460.0px"><p><strong>LATEST</strong>: export all revisions up to the latest minor revision.</p>
<p><strong>DEPLOYED</strong>: export all revisions up to the latest deployed revision.</p>
<p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--deployTimeout VAL</th>
<td class="confluenceTd" style="width: 572.0px">Time to wait for deploying integration flows (optional, default: 30 seconds)</td>
<td class="confluenceTd" style="width: 460.0px"><p>VAL is a whole number of seconds.</p>
<p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--log VAL</th>
<td class="confluenceTd" style="width: 572.0px">Set the log level for Impex and other related classes (optional, default: INFO)</td>
<td class="confluenceTd" style="width: 460.0px"><div class="content-wrapper">
<p>VAL is standard log levels, <strong>DEBUG</strong>, <strong>INFO</strong>, <strong>WARN</strong>, etc.</p>
</div></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--tabularColumn VAL</th>
<td class="confluenceTd" style="text-align: left; width: 572.0px;">Specify any number of column names and data types to be used across tabular data files. (optional)</td>
<td class="confluenceTd" style="text-align: left; width: 460.0px;"><p>VAL is a key-value pair of a column name and a data type such as "name"="String" Valid data types are: String, Integer, Double, Date, Time, Date-Time</p>
<p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTh" style="text-align: center; width: 1160.0px;">Flags</th>
<td></td>
<td></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--shallow</th>
<td class="confluenceTd" style="width: 572.0px">Deprecated as of 3.7.9. Only exports a single revision, respecting whether LATEST or DEPLOYED is also given for the --revisions option. Use this if you don't care about maintaining version numbers between environments and just want to quickly move content (optional, default: false)</td>
<td class="confluenceTd" style="width: 460.0px"><strong>Applies to: Amelia</strong></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="text-align: left; width: 128.0px;">--revisionless</th>
<td class="confluenceTd" style="text-align: left; width: 572.0px;">Deprecated as of 3.7.9. The same as above, however, the revision number will not be included in file names written to the file system.</td>
<td class="confluenceTd" style="text-align: left; width: 460.0px;"><strong>Applies to: Amelia</strong></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--clean</th>
<td class="confluenceTd" style="width: 572.0px">If specified, all content in the target will be deleted respecting the include and exclude options (optional, default: false)</td>
<td class="confluenceTd" style="width: 460.0px"><p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--deploy</th>
<td class="confluenceTd" style="width: 572.0px"><strong>Deprecated as of 3.7.5.</strong>  Requires --sourceUrl and --targetUrl to be supplied. If specified, applicable content will be deployed according to what was deployed in the source. The same revisions will attempt to be deployed if they don't exist nothing will be deployed. (optional, default: false)</td>
<td class="confluenceTd" style="width: 460.0px"><p>Only applicable to <strong>BPN</strong> and <strong>CLASSIFIER.</strong></p>
<p><strong>Applies to: Amelia<br />
</strong></p></td>
</tr>
<tr class="odd">
<th class="confluenceTd" style="width: 128.0px">--ignore-cert</th>
<td class="confluenceTd" style="width: 572.0px">Ignores certificate errors in the source or target Amelia instance (optional, default: false)</td>
<td class="confluenceTd" style="width: 460.0px"><p>Please only use this with hostnames that you trust!</p>
<p><strong>Applies to: Amelia</strong></p></td>
</tr>
<tr class="even">
<th class="confluenceTd" style="width: 128.0px">--skipPrompts</th>
<td class="confluenceTd" style="width: 572.0px">Skips prompt that appears in Git actions by accepting them or making any choice to attempt to move forward (optional, default: false)</td>
<td class="confluenceTd" style="width: 460.0px"><p>Currently used for accepting Git changes to be pushed <strong>(Caution: this will commit and push EVERY change found in the local repository, make sure you know what you are doing).</strong></p>
<p><strong>Applies to: Git<br />
</strong></p></td>
</tr>
</tbody>
</table>
# Supported Content
The following table describes the content types that are supported across the version series.

| 
 | 0.5 | 3.6 | 3.7 | Notes |
| ----|----|----|----|----|
| BPN |  |  |  |  |
| SCRIPT |  |  |  |  |
| TABULAR |  |  |  | Requires Core 3.6.17+ |
| MULTIMEDIA |  |  |  |  |
| INTENT |  |  |  |  |
| ENTITY |  |  |  |  |
| GRAMMAR |  |  |  |  |
| TRAINING |  |  |  |  |
| CLASSIFIER |  |  |  |  |
| INTEGRATION_ASSET |  |  |  | Encrypted properties must be manually updated after importing! |
| INTEGRATION_FLOW |  |  |  |  |
| RESPONSE_POOL |  |  |  |  |
| NLU |  |  |  | NLU configuration only exists in Amelia Core 3.7+ |

# Directory Structure (changed in 3.7.9)
The directory structure that will be used to read/write content outside of Amelia will look like this:
> [!note]  
>
>     /tmp/test/impex/ncp_source (the file system path specified by sourceUrl or targetUrl)
>     ├── aiml
>     │   ├── ai.aiml (a AIML XML file, can be uploaded/downloaded in the Amelia admin application)
>     │   └── aiml_list.json (a JSON collection of all AIML files)
>     ├── bpn
>     │   ├── Deployment (a regular directory folder)
>     │   │   ├── LearnKnowledge.bpmn (a BPN XML file, can be uploaded/downloaded in the Amelia admin application)
>     │   │   └── LearnKnowledge.json (a JSON file representing a BPN model and its metadata)
>     │   ├── Greeting
>     │   │   ├── Greeting.bpmn
>     │   │   └── Greeting.json
>     │   ├── Integrations
>     │   │   ├── ConfigureMySqlIntegration.bpmn
>     │   │   └── ConfigureMySqlIntegration.json
>     │   └── bpn_list.json (a JSON collection of all BPN models and folders, also known as the BPN tree)
>     ├── classifier
>     │   ├── amelia_module_spanless_model.zip (a classifier model ZIP file, can be uploaded/downloaded in the Amelia admin application)
>     │   ├── auto.intents.zip
>     │   ├── brain_learn_intent_model.zip
>     │   ├── checkInCheckOut.zip
>     │   ├── classifier_list.json (a JSON collection of all classifier models)
>     │   ├── faqIntents.zip
>     │   ├── garbage.zip
>     │   ├── more_garbage.zip
>     │   ├── testIntent.zip
>     │   └── weather_intent_model.zip
>     ├── entity
>     │   ├── entities.json (a entity JSON file, can be uploaded/downloaded in the Amelia admin application)
>     │   └── entity_list.json (a JSON collection of all entities)
>     ├── grammar
>     │   ├── grammar_list.json (a JSON collection of all grammars)
>     │   └── grammars.xml (a grammar XML file, can be uploaded/downloaded in the Amelia admin application)
>     ├── integration_asset
>     │   ├── ameliav3x-camel-http-3.7-SNAPSHOT-all.jar.json (a JSON file representing an integratoion asset and its metadata)
>     │   └── asset_list.json (a JSON collection of all integration assets)
>     ├── integration_flow
>     │   ├── flow_list.json (a JSON collection of all integration flows)
>     │   └── impex_test.json (a JSON file representing an integration flow and its metadata)
>     ├── integration_property_set
>     │   ├── impex.properties.json (a JSON file representing and integration property set)
>     │   └── set_list.json (a JSON collection file of all integration property sets)
>     ├── intent
>     │   ├── intent_list.json (a JSON collection of all intents)
>     │   └── intents.tsv (a intent TSV file, can be uploaded/downloaded in the Amelia admin application)
>     ├── multimedia
>     │   ├── bucket_list.json (a JSON collection of all multimedia content buckets)
>     │   ├── hajsfhjoahsf (a regular directory folder)
>     │   │   └── resource_list.json (a JSON collection of all resources within the parent bucket)
>     │   └── images
>     │       ├── ballin.jpg (an arbitrary resource stored in a bucket)
>     │       ├── banking-wealth-management-16-9_570.jpg
>     │       ├── c4jt321.png
>     │       ├── engine_log.PNG
>     │       ├── insurance-policy-information-16-9_570.jpg
>     │       ├── resource_list.json
>     │       ├── wicket.PNG
>     │       └── zenyatta_with__roundfill.png
>     ├── nlu
>     │   └── nlu_settings.json (a JSON file representing the NLU settings for a domain)
>     ├── response_pool
>     │   ├── NCP_GROUP (a regular directory folder)
>     │   │   └── NCP_POOL
>     │   │       ├── en-GB_5.json (a JSON file representing a response pool entry in the parent group + pool)
>     │   │       ├── en-US_1.json
>     │   │       ├── en-US_2.json
>     │   │       ├── es-ES_4.json
>     │   │       └── es-MX_3.json
>     │   └── pool_list.json (a JSON collection of all response pools)
>     ├── script
>     │   ├── script_list.json (a JSON collection of all scripts and folders, also known as the script tree)
>     │   └── test (a regular directory folder)
>     │       └── test1.json (a JSON file representing a script library)
>     ├── semnet
>     │   ├── semantic-memory-kobayashi-maru.pdf.json (a JSON file representing a SemNet docuement)
>     │   └── semnet_list.json (a JSON collection file of all SemNet documents)
>     ├── tabular
>     │   ├── ingredients.json (a JSON file representing a tabular data file)
>     │   └── tabular_list.json (a JSON collection of all tabular data)
>     └── training
>         ├── testing.json (a JSON file representing a training document)
>         └── training_list.json (a JSON collection of all training documents)

# Content Container Types
The content container type of a source or target is determined by the **--sourceUrl** or **--targetUrl** arguments (see example URLs in the table above).
## Amelia
When the source/target URL is an Amelia instance (identified by ending with '/Amelia'), the application will send requests to the Amelia APIs to export/import all content based on the given command. This is all handled in memory and does not write anything to the local file system.
A note on content with revisions that can be controlled, BPNs and classifier models. As of version 3.7.9, the default behavior will be to export only deployed revisions. This is a change from previous default behavior which attempted to export ALL revisions up to the latest. Exporting more than one revision is no longer supported and only the latest or deployed revision will be considered based on the given arguments. See the file structure above for exactly what this looks like.
## File System
When the source/target URL is a file system path, the tool will read/write files on the local file system in the directory structure described above. Most content types are stored using JSON files that contain their metadata and main content.
## Git
When the source URL is a Git repository, the tool will clone the specified branch (**--gitBranch**) of the repository to a temporary directory on the local file system and treat it as a file system source from there. When the target URL is a Git repository, the tool will clone the repository to a temporary directory on the local file system, then copy all of the content from the source into that local directory. The tool will then prompt the user (unless **--skipPrompts** is used) to review the changes in the repository and confirm 3 times (stage, commit, push). If **--commitMessage** is not provided it will be prompted for. 
When using a Git source/target there are two authentication options. Either typical username/password using an HTTP URL, or using an SSH private key and passphrase with an SSH URL. The tool will determine which is needed based on the URL and prompt for any required options not supplied in the command.
## Zip
When the source URL is a .zip file, the tool will extract the file into the same directory as the zip and treat it as a file system source from there. The zip file can either be local or remote, however, the tool does not currently handle any authentication needed for a remote zip file. If the URL to the file begins with 'http' it is assumed to be a remote file and the tool will attempt to download it before extracting its contents.
# Release Notes
[Impex Release Notes](Import%20Export%20Tool%20Releases)
# Download
> [!info]  
>
> Using this tool requires Java 8 Update 152 or above on the executing machine (your laptop, server, or otherwise).

External Releases: <https://artifactory.ipsoft.com/artifactory/libs-release-local/net/ipsoft/ameliav3x/ameliav3x-impex/>
Use the same login used to access the docs.ipsoft.com website.
# FAQs
Q: Why are there multiple versions of the tool?
A: Each minor version of Amelia Core (3.5, 3.6, 3.7, etc.) has a corresponding Java SDK release to accommodate any breaking changes in the APIs. Impex and other tools will follow the same release pattern where there will be a corresponding release for each Core/SDK version.
Q: Which version should I use?
A: You should use the impex version that corresponds to your source and target Amelia Core version, for Amelia 3.5 use impex-0.5, for Amelia 3.6 use impex-3.6, and so on.
Q: What if I need to move content between instances on different minor version?
A: TL;DR you're gonna have a bad time. It's doable, however not all content will be transferable between versions, the best solution would be exporting to a file system with the appropriate version for the source, and then importing from the file system with the appropriate version for the target.
Q: What's with all these JSON files?
A: The JSON files that you see side by side with the actual content contains the metadata for that content that Amelia Core needs to maintain various functionality and relationships between dependencies. The tool will not work properly if you delete or modify these files in any way.
Q: Why am I getting an SSLHandshakeException?
Click here to expand...
01-22-19 17:07:45 ERROR (AmeliaContentContainer.java:454) - java.util.concurrent.ExecutionException: org.springframework.web.client.ResourceAccessException: I/O error on GET request for "<https://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/Amelia/api/init>": java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.; nested exception is [javax.net](http://javax.net/).ssl.SSLHandshakeException: java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.  
net.ipsoft.ameliav3.sdk.common.AmeliaApiException: java.util.concurrent.ExecutionException: org.springframework.web.client.ResourceAccessException: I/O error on GET request for "<https://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/Amelia/api/init>": java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.; nested exception is [javax.net](http://javax.net/).ssl.SSLHandshakeException: java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.  
at net.ipsoft.ameliav3.sdk.impl.common.BaseApiCommand.execute(BaseApiCommand.java:67)  
at net.ipsoft.ameliav3x.impex.impl.container.AmeliaContentContainer.login(AmeliaContentContainer.java:451)  
at net.ipsoft.ameliav3x.impex.impl.container.AmeliaContentContainer.init(AmeliaContentContainer.java:62)  
at net.ipsoft.ameliav3x.impex.AmeliaV3Impex.main(AmeliaV3Impex.java:149)  
Caused by: java.util.concurrent.ExecutionException: org.springframework.web.client.ResourceAccessException: I/O error on GET request for "<https://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/Amelia/api/init>": java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.; nested exception is [javax.net](http://javax.net/).ssl.SSLHandshakeException: java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.  
at java.util.concurrent.FutureTask.report(FutureTask.java:122)  
at java.util.concurrent.FutureTask.get(FutureTask.java:192)  
at net.ipsoft.ameliav3.sdk.impl.common.BaseApiCommand.execute(BaseApiCommand.java:57)  
... 3 more  
Caused by: org.springframework.web.client.ResourceAccessException: I/O error on GET request for "<https://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/Amelia/api/init>": java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.; nested exception is [javax.net](http://javax.net/).ssl.SSLHandshakeException: java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.  
at org.springframework.web.client.RestTemplate.doExecute(RestTemplate.java:674)  
at org.springframework.web.client.RestTemplate.execute(RestTemplate.java:621)  
at org.springframework.web.client.RestTemplate.getForEntity(RestTemplate.java:320)  
at net.ipsoft.ameliav3.sdk.impl.auth.BaseLoginCommandImpl.doInit(BaseLoginCommandImpl.java:40)  
at net.ipsoft.ameliav3.sdk.impl.auth.LoginCommandImpl.doExecute(LoginCommandImpl.java:41)  
at net.ipsoft.ameliav3.sdk.impl.auth.LoginCommandImpl.doExecute(LoginCommandImpl.java:23)  
at java.util.concurrent.FutureTask.run(FutureTask.java:266)  
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)  
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)  
at java.lang.Thread.run(Thread.java:748)  
Caused by: [javax.net](http://javax.net/).ssl.SSLHandshakeException: java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.  
at sun.security.ssl.Alerts.getSSLException(Alerts.java:192)  
at sun.security.ssl.SSLSocketImpl.fatal(SSLSocketImpl.java:1959)  
at sun.security.ssl.Handshaker.fatalSE(Handshaker.java:302)  
at sun.security.ssl.Handshaker.fatalSE(Handshaker.java:296)  
at sun.security.ssl.ClientHandshaker.serverCertificate(ClientHandshaker.java:1514)  
at sun.security.ssl.ClientHandshaker.processMessage(ClientHandshaker.java:216)  
at sun.security.ssl.Handshaker.processLoop(Handshaker.java:1026)  
at sun.security.ssl.Handshaker.process_record(Handshaker.java:961)  
at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:1072)  
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1385)  
at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1413)  
at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1397)  
at [sun.net](http://sun.net/).www.protocol.https.HttpsClient.afterConnect(HttpsClient.java:559)  
at [sun.net](http://sun.net/).www.protocol.https.AbstractDelegateHttpsURLConnection.connect(AbstractDelegateHttpsURLConnection.java:185)  
at [sun.net](http://sun.net/).www.protocol.https.HttpsURLConnectionImpl.connect(HttpsURLConnectionImpl.java:162)  
at org.springframework.http.client.SimpleBufferingClientHttpRequest.executeInternal(SimpleBufferingClientHttpRequest.java:78)  
at org.springframework.http.client.AbstractBufferingClientHttpRequest.executeInternal(AbstractBufferingClientHttpRequest.java:48)  
at org.springframework.http.client.AbstractClientHttpRequest.execute(AbstractClientHttpRequest.java:53)  
at org.springframework.web.client.RestTemplate.doExecute(RestTemplate.java:660)  
... 9 more  
Caused by: java.security.cert.CertificateException: No subject alternative DNS name matching [app01.nickcp-v3-ipsoft.amelia.ipcenter.com](http://app01.nickcp-v3-ipsoft.amelia.ipcenter.com/) found.  
at sun.security.util.HostnameChecker.matchDNS(HostnameChecker.java:214)  
at sun.security.util.HostnameChecker.match(HostnameChecker.java:96)  
at sun.security.ssl.X509TrustManagerImpl.checkIdentity(X509TrustManagerImpl.java:455)  
at sun.security.ssl.X509TrustManagerImpl.checkIdentity(X509TrustManagerImpl.java:436)  
at sun.security.ssl.X509TrustManagerImpl.checkTrusted(X509TrustManagerImpl.java:200)  
at sun.security.ssl.X509TrustManagerImpl.checkServerTrusted(X509TrustManagerImpl.java:124)  
at sun.security.ssl.ClientHandshaker.serverCertificate(ClientHandshaker.java:1496)  
... 23 more
A: You are trying to use the tool with a URL that does not have a valid certificate. You can get around this by using the \`--ignore-cert\` option, however you should only do this if you are sure the server is one that you trust.
