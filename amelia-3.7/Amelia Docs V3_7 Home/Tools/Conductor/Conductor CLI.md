-   [Intended Audience](#ConductorCLI-IntendedAudience)
-   [Required Authorities](#ConductorCLI-RequiredAuthorities)
    -   [Knowledge Resources](#ConductorCLI-KnowledgeResources)
    -   [System Configuration](#ConductorCLI-SystemConfiguration)
-   [Usage](#ConductorCLI-Usage)
    -   [Run the application](#ConductorCLI-Runtheapplication)
    -   [Commands](#ConductorCLI-Commands)
        -   [Basic Commands in Amelia 3.x and 4.x](#ConductorCLI-BasicCommandsinAmelia3.xand4.x)
        -   [Additional Commands in Amelia 4.x](#ConductorCLI-AdditionalCommandsinAmelia4.x)
        -   [help Command Example](#ConductorCLI-helpCommandExample)
        -   [BPN import and deployment strategies](#ConductorCLI-BPNimportanddeploymentstrategies)
    -   [Scripts](#ConductorCLI-Scripts)
        -   [Export Amelia Knowledge Content and Domain Configuration](#ConductorCLI-ExportAmeliaKnowledgeContentandDomainConfiguration)
        -   [Import a Domain with Content into an Amelia Instance](#ConductorCLI-ImportaDomainwithContentintoanAmeliaInstance)
        -   [Clean Content from a Target Domain](#ConductorCLI-CleanContentfromaTargetDomain)
        -   [Migrate Authentication Systems and Policies](#ConductorCLI-MigrateAuthenticationSystemsandPolicies)
        -   [Escalation Queues and Teams Commands](#ConductorCLI-EscalationQueuesandTeamsCommands)
        -   [Users and User Groups Commands](#ConductorCLI-UsersandUserGroupsCommands)
        -   [Migrate UI Bundles](#ConductorCLI-MigrateUIBundles)
        -   [Migrate with Dependencies](#ConductorCLI-MigratewithDependencies)
        -   [Metrics Export](#ConductorCLI-MetricsExport)
    -   [Thread Pool Configuration](#ConductorCLI-ThreadPoolConfiguration)
    -   [Logging Configuration](#ConductorCLI-LoggingConfiguration)
-   [File System Output](#ConductorCLI-FileSystemOutput)
-   [FAQs](#ConductorCLI-FAQs)
    -   [What version should I use?](#ConductorCLI-WhatversionshouldIuse?)
    -   [Can I move content between major/minor versions of Amelia?](#ConductorCLI-CanImovecontentbetweenmajor/minorversionsofAmelia?)
-   [Download](#ConductorCLI-Download)
The Conductor Engine CLI application enables users to leverage the functionality of the Conductor engines from their command line. This includes the ability to migrate knowledge and configuration options between Amelia instances, Git repositories, etc. As an added utility function, the ability to export metrics is also included in the application.
# Intended Audience
This page and instructions are intended for Amelia admins and engineers that regularly need to migrate Amelia content and configuration changes or export metrics.
# Required Authorities
> [!warning]  
>
> The authorities detailed here are specific to each content type, to access any content the authority AUTHORITY_ADMIN_VIEW must be added as well.

The user account used to authenticate the tool will need to have the appropriate authorities to modify content within an Amelia instance. They are as follows:
## Knowledge Resources
Each type of content requires specific user authorities to be set in Amelia's Settings/Configuration section in her administration workspaces.

| Content-Type | Required Authorities |
| ----|----|
| BPNSCRIPT

\|
    AUTHORITY_ADMIN_BPN_EDITAUTHORITY_ADMIN_BPN_DEPLOY
    AUTHORITY_ADMIN_BPN_VIEW
\| \|
    TABULAR
\|
    AUTHORITY_TABULAR_ADDAUTHORITY_TABULAR_EDIT
    AUTHORITY_TABULAR_VIEW
\| \|
    MULTIMEDIA
\|
    AUTHORITY_ADMIN_CONTENT_MANAGEMENT_VIEWAUTHORITY_ADMIN_CONTENT_MANAGEMENT_EDIT
    AUTHORITY_ADMIN_CONTENT_MANAGEMENT_DELETE
\| \|
    GRAMMARINTENT
    ENTITY
    CLASSIFIER
    TRAINING
    NLU (3.7+ only)
\|
    AUTHORITY_TRAINING_VIEWAUTHORITY_TRAINING_EDIT
\| \|
    SEMNET
\|
    AUTHORITY_ADMIN_SEMNET_DOCUMENT_VIEWAUTHORITY_ADMIN_SEMNET_DOCUMENT_EDIT
    AUTHORITY_ADMIN_SEMNET_DOCUMENT_DELETE
\| \|
    INTEGRATION_ASSET,INTEGRATION_FLOW,
    INTEGRATION_PROPERTY_SET
\|
    AUTHORITY_ADMIN_INTEGRATION_EDITAUTHORITY_ADMIN_INTEGRATION_DEPLOY
    AUTHORITY_ADMIN_INTEGRATION_VIEW
\| \|
    RESPONSE_POOL
\|
    AUTHORITY_RESPONSE_POOL_VIEWAUTHORITY_RESPONSE_POOL_EDIT
\| \|
    AIML
\|
    AUTHORITY_ADMIN_AIML_DOCUMENT_VIEWAUTHORITY_ADMIN_AIML_DOCUMENT_EDIT
    AUTHORITY_ADMIN_AIML_DOCUMENT_DELETE
\| \|
    Aspect (v4)Aspect Group (v4)
\|
    AUTHORITY_ADMIN_ASPECT_VIEWAUTHORITY_ADMIN_ASPECT_EDIT
\|
## System Configuration
Access to system elements requires specific user authorities to be set in Amelia's Settings/Configuration section in her administration workspaces.

| System Element | Required Authorities |
| ----|----|
| Authentication PolicyAuthentication System | AUTHORITY_ADMIN_VIEWAUTHORITY_ADMIN_RBAC

\| \| Domain \|
    AUTHORITY_ADMIN_DOMAIN_VIEWAUTHORITY_ADMIN_DOMAIN_EDIT
\| \| Escalation Queue \|
    AUTHORITY_ADMIN_ESCALATION_QUEUE_VIEWAUTHORITY_ADMIN_ESCALATION_QUEUE_EDIT
\| \| Escalation Team \|
    AUTHORITY_ADMIN_ESCALATION_TEAM_VIEWAUTHORITY_ADMIN_ESCALATION_TEAM_EDIT
\| \|
Integration Host
Integration Cluster
\|
    AUTHORITY_ADMIN_INTEGRATION_VIEWAUTHORITY_ADMIN_INTEGRATION_EDIT
\| \| 1Desk Instance \|
    AUTHORITY_ADMIN_ONE_DESK_INSTANCE_VIEWAUTHORITY_ADMIN_ONE_DESK_INSTANCE_EDIT
    AUTHORITY_ADMIN_DOMAIN_VIEW
\| \| Role \|
    AUTHORITY_ADMIN_VIEWAUTHORITY_ADMIN_RBAC
\| \| UI Bundle \|
    AUTHORITY_ADMIN_VIEWAUTHORITY_ADMIN_UI_BUNDLE_EDIT
    AUTHORITY_ADMIN_UI_BUNDLE_DEPLOY
\| \| User \|
    AUTHORITY_ADMIN_USER_VIEWAUTHORITY_ADMIN_USER_EDIT
\| \| User Group \|
    AUTHORITY_ADMIN_VIEWAUTHORITY_ADMIN_RBAC
\| \| Metrics \|
    AUTHORITY_METRICS_VIEWAUTHORITY_CONVERSATION_EXPORT
\| \| Virtual Host;(v4) \|
    AUTHORITY_ADMIN_VIRTUAL_HOST_VIEWAUTHORITY_ADMIN_VIRTUAL_HOST_EDIT
\|
# Usage
## Run the application
Once the Conductor CLI file is downloaded, type this command to run the application:
**Run the application**
``` text
java -jar conductor-engine-cli-<version>.jar
```
Running the application without any options will greet you with an interactive shell.
**Start interactive shell**
``` text
  ______   ______   .__   __.  _______   __    __    ______ .___________.  ______   .______                ______  __       __
 /      | /  __  \  |  \ |  | |       \ |  |  |  |  /      ||           | /  __  \  |   _  \              /      ||  |     |  |
|  ,----'|  |  |  | |   \|  | |  .--.  ||  |  |  | |  ,----'`---|  |----`|  |  |  | |  |_)  |     ______ |  ,----'|  |     |  |
|  |     |  |  |  | |  . `  | |  |  |  ||  |  |  | |  |         |  |     |  |  |  | |      /     |______||  |     |  |     |  |
|  `----.|  `--'  | |  |\   | |  '--'  ||  `--'  | |  `----.    |  |     |  `--'  | |  |\  \----.        |  `----.|  `----.|  |
 \______| \______/  |__| \__| |_______/  \______/   \______|    |__|      \______/  | _| `._____|         \______||_______||__|
                 o  o  O  O  O
            ,________  ____    O
            | IPsoft \_|[]|_'__Y
            |__________|__|_|__|}
=============oo--oo==oo--OOO\\====================
 :: Spring Boot ::   v2.2.6.RELEASE
 :: Conductor ::   v3.7-SNAPSHOT
 :: Amelia Core ::   v3.7-SNAPSHOT
2020-05-14 10:29:58,423 [main] INFO  -- StartupInfoLogger.java 55 - Starting ConductorCliApplication on ncorso-mbp2.local with PID 41018 (/Users/ncorsopassaro/workspace/conductor-engine-cli/build/libs/conductor-engine-cli-3.7-SNAPSHOT.jar started by ncorsopassaro in /Users/ncorsopassaro/workspace/conductor-engine-cli)
2020-05-14 10:29:58,428 [main] INFO  -- SpringApplication.java 651 - No active profile set, falling back to default profiles: default
2020-05-14 10:30:00,173 [main] INFO  -- StartupInfoLogger.java 61 - Started ConductorCliApplication in 2.525 seconds (JVM running for 3.468)
conductor-cli:>
```
## Commands
From the prompt running, typing the **help** command will display all of the available commands.
### **Basic Commands in Amelia 3.x and 4.x**
Commands Available in 3.x and 4.x
**Available Commands**
``` text
conductor-cli:>help
AVAILABLE COMMANDS
Amelia Aiml Command
        amelia-aiml-clean: Delete AIML files from an Amelia instance.
        amelia-aiml-export: Export a collection of AIML files from an Amelia instance.
        amelia-aiml-import: Import AIML files into an Amelia instance.
Amelia Authentication Command
        amelia-authentication-policy-export: Export a collection of authentication policies from an Amelia instance.
        amelia-authentication-policy-import: Import a collection of authentication policies into an Amelia instance.
        amelia-authentication-system-export: Export a collection of authentication systems from an Amelia instance.
        amelia-authentication-system-import: Import a collection of authentication systems into an Amelia instance.
        amelia-login: Login to an Amelia instance with a username and password.
        amelia-logout: Logout an existing session with an Amelia instance
Amelia Bpn Command
        amelia-bpn-clean: Delete a collection of BPNs from an Amelia instance. BPNs that reference BPNs to be deleted will be undeployed.
        amelia-bpn-export: Export a collection of BPNs from an Amelia instance.
        amelia-bpn-import: Import BPNs into an Amelia instance.
Amelia Classifier Command
        amelia-classifier-clean: Delete a collection of classifier models from an Amelia instance.
        amelia-classifier-export: Export a collection of classifier models from an Amelia instance.
        amelia-classifier-import: Import classifier models into an Amelia instance.
Amelia Domain Command
        amelia-domain-export: Export a collection of domains from an Amelia instance.
        amelia-domain-import: Import content from an Amelia instance.
Amelia Entity Command
        amelia-entity-clean: Clean a collection of entities from an Amelia instance. Requires BPNs to be undeployed before an entity can be deleted if it is used in an 'ask for the slot' task.
        amelia-entity-export: Export a collection of entities from an Amelia instance.
        amelia-entity-import: Import entities into an Amelia instance.
Amelia Escalation Command
        amelia-escalation-queue-clean: Delete collection of escalation queues from an Amelia instance.
        amelia-escalation-queue-export: Export a collection of escalation queues from an Amelia instance.
        amelia-escalation-queue-import: Import escalation queues into an Amelia instance.
        amelia-escalation-team-clean: Delete collection of escalation teams from an Amelia instance.
        amelia-escalation-team-export: Export a collection of escalation teams from an Amelia instance.
        amelia-escalation-team-import: Import escalation teams into an Amelia instance.
Amelia Grammar Command
        amelia-grammar-clean: Delete a collection of grammars from an Amelia instance.
        amelia-grammar-export: Export a collection of grammars from an Amelia instance.
        amelia-grammar-import: Import grammars into an Amelia instance.
Amelia Integration Command
        amelia-integration-asset-clean: Delete a collection of integration assets from an Amelia instance.
        amelia-integration-asset-export: Export a collection of integration assets from an Amelia instance.
        amelia-integration-asset-import: Import integration assets into an Amelia instance.
        amelia-integration-flow-clean: Delete a collection of integration flows from an Amelia instance. To undeploy and delete an integration flow, any BPNs that reference the flow will be undeployed.
        amelia-integration-flow-export: Export a collection of integration flows from an Amelia instance.
        amelia-integration-flow-import: Import integration flow into an Amelia instance.
        amelia-integration-property-set-clean: Delete a collection of integration property sets from an Amelia instance.
        amelia-integration-property-set-export: Export a collection of integration property sets from an Amelia instance.
        amelia-integration-property-set-import: Import integration property sets into an Amelia instance.
Amelia Intent Command
        amelia-intent-clean: Delete a collection of intents from an Amelia instance.
        amelia-intent-export: Export a collection of intents from an Amelia instance.
        amelia-intent-import: Import intents into an Amelia instance.
Amelia Metrics Command
        amelia-metrics-export: Export chat metrics from an Amelia instance for a given date range.
Amelia Multimedia Command
        amelia-multimedia-clean: Delete a collection of multimedia resources from an Amelia instance.
        amelia-multimedia-export: Export a collection of multimedia resources from an Amelia instance.
        amelia-multimedia-import: Import multimedia resources into an Amelia instance.
Amelia Nlu Command
        amelia-nlu-export: Export the NLU settings for a domain from an Amelia instance.
        amelia-nlu-import: Import the NLU settings for a domain into an Amelia instance.
Amelia Response Pool Command
        amelia-response-pool-clean: Delete a collection of response pools and their entries from an Amelia instance.
        amelia-response-pool-export: Export a collection of response pools and their entries from an Amelia instance.
        amelia-response-pool-import: Import response pools into an Amelia instance.
Amelia Script Command
        amelia-script-clean: Delete a collection of script libraries from an Amelia instance.
        amelia-script-export: Export a collection of script libraries from an Amelia instance.
        amelia-script-import: Import script libraries an Amelia instance.
Amelia Semnet Command
        amelia-semnet-clean: Delete SemNet documents from an Amelia instance.
        amelia-semnet-export: Export a collection of BPNs from an Amelia instance.
        amelia-semnet-import: Import SemNet documents into an Amelia instance.
Amelia Tabular Command
        amelia-tabular-clean: Delete tabular data from an Amelia instance.
        amelia-tabular-export: Export a collection of tabular data from an Amelia instance.
        amelia-tabular-import: Import tabular data into an Amelia instance.
Amelia Training Command
        amelia-training-clean: Deleting training documents from an Amelia instance.
        amelia-training-export: Export a collection of training documents from an Amelia instance.
        amelia-training-import: Import training documents into an Amelia instance.
Amelia UI Command
        amelia-ui-bundle-export: Export a collection of UI bundles from an Amelia instance.
        amelia-ui-bundle-import: Import UI bundles into an Amelia instance.
Amelia User Command
        amelia-user-clean: Delete users from an Amelia instance.
        amelia-user-export: Export a collection of users from an Amelia instance.
        amelia-user-group-clean: Delete user groups from an Amelia instance.
        amelia-user-group-export: Export a collection of user groups from an Amelia instance.
        amelia-user-group-import: Import user groups into an Amelia instance.
        amelia-user-import: Import users into an Amelia instance.
        amelia-user-role-export: Export a collection of user roles from an Amelia instance.
        amelia-user-role-import: Import user roles into an Amelia instance.
Built-In Commands
        clear: Clear the shell screen.
        exit, quit: Exit the shell.
        help: Display help about available commands.
        history: Display or save the history of previously run commands
        script: Read and execute commands from a file.
        stacktrace: Display the full stacktrace of the last error.
Git Repository Command
        git-add: Clone a git repository to a local directory
        git-clone: Clone a git repository to a local directory
        git-commit: Clone a git repository to a local directory
        git-push: Clone a git repository to a local directory
One Desk Command
        amelia-one-desk-export: Export a collection of 1Desk instances from an Amelia instance.
        amelia-one-desk-import: Import 1Desk instances into an Amelia instance.
One Rpa Command
        amelia-one-rpa-export: Export a collection of 1RPA instances from an Amelia instance.
        amelia-one-rpa-import: Import 1RPA instances into an Amelia instance.
```
### **Additional Commands in Amelia 4.x**
In Amelia V4, additional features have been added and there are additional commands in the 4.x versions of the CLI application to support these features.
Commands Only Available in 4.x
``` groovy
Amelia Aspect Command
        amelia-aspect-clean: Delete a collection of aspects from an Amelia instance.
        amelia-aspect-group-clean: Delete a collection of aspect groups from an Amelia instance.
        amelia-aspect-export: Export a collection of aspects from an Amelia instance.
        amelia-aspect-group-export: Export a collection of aspect groups from an Amelia instance.
        amelia-aspect-group-import: Import aspect groups into an Amelia instance.
        amelia-aspect-import: Import aspects into an Amelia instance.
Amelia Semantic Mapping Command
        amelia-semantic-mapping-clean: Delete a collection of semantic mappings from an Amelia instance.
        amelia-semantic-mapping-export: Export a collection of semantic mappings from an Amelia instance.
        amelia-semantic-mapping-import: Import semantic mappings into an Amelia instance.
Amelia Virtual Host Command
        amelia-virtual-host-clean: Delete a collection of virtual hosts from an Amelia instance.
        amelia-virtual-host-export: Export a collection of virtual hosts from an Amelia instance.
        amelia-virtual-host-import: Import a collection of virtual hosts into an Amelia instance.
One Store Command
        amelia-one-store-clean: Delete a collection of 1Store instances from an Amelia instance.
        amelia-one-store-export: Export a collection of 1Store instances from an Amelia instance.
        amelia-one-store-import: Import 1Store instances into an Amelia instance.
```
### **help Command Example**
Typing at a command line the **help** command followed by another command will display more information about that command including its available options and default values.
**help amelia-login**
``` text
conductor-cli:>help amelia-login
NAME
        amelia-login - Login to an Amelia instance with a username and password.
SYNOPSYS
        amelia-login [--url] string  [[--username] string]  [[--password] string]  [--ignore-cert-errors]  
OPTIONS
        --url  string
                [Mandatory]
        --username  string
                [Optional, default = ]
        --password  string
                [Optional, default = ]
        --ignore-cert-errors    
                [Optional, default = false]
```
### BPN import and deployment strategies
Different BPN import and deployment strategies are available in BPN import command in Conductor V3.7.12 onwards. Below is the description using help amelia-bpn-import command.
**help amelia-bpn-import**
``` groovy
conductor-cli:>help amelia-bpn-import
NAME
    amelia-bpn-import - Import BPNs into an Amelia instance.
SYNOPSYS
    amelia-bpn-import [--url] string  [--directory] string  [--domain-code] string  [[--names] string]  [[--ids] string]  [[--import-strategy] import-strategy]  [[--deploy-strategy] bpn-deploy-strategy]  [--with-dependencies] 
OPTIONS
    --url  string
        [Mandatory]
    --directory  string
        [Mandatory]
    --domain-code  string
        [Mandatory]
    --names  string
        [Optional, default = ,]
    --ids  string
        [Optional, default = ,]
    --import-strategy  import-strategy
        Following import strategies are available -
        ADD - import BPN only if it's not available in target.
        MERGE - import and updates the BPN if they are not same.
        OVERWRITE - import the BPN after deleting existing one if available.
        [Optional, default = MERGE]
    --deploy-strategy  bpn-deploy-strategy
    Following BPN deploy strategies are available to choose from :
    0 - No deployment of imported BPNs.
    1 - Attempts to deploy only specific BPNs that are imported. (Preserve source deployment status)
    2 - Attempts to deploy all specific BPNs that are imported. 
    3 - Deploys the latest revision of dependent BPNs (Preserve source deployment status of imported BPNs).
    4 - Deploys the latest revision of dependent BPNs (Attempts to deploy all imported BPNs).
    [Optional, default = 3]
    --with-dependencies
        Use this flag to import all dependencies associated with the BPN within the domain.
        (for eg. run the workflow tasks, escalation queue, script, integration flow, intent, entity, response pool and multimedia.)
        [Optional, default = false]
conductor-cli:>
```
## Scripts
Scripts can be written as a list of any of the commands from the previous section. A script file is a simple plain text file that can be created in any text editor. To run a script file, add it to the end of the command used to start the application starting with an **@** symbol before the file path.
**Run a script file**
``` text
java -jar conductor-engine-cli-<version>.jar @path/to/script/file
```
> [!warning]  
>
> Do not forget to start your file path with an **@** symbol.
> [!warning]  
>
> For any option that takes a directory as a value, do not forget to use your operating systems file path separator. This is usually a backslash **\\** on Windows or forward slash **/** on macOS and \*nix systems.

Scripts allows customization of Conductor processes to accomplish a variety of goals. An example script for exporting content from an Amelia instance can be found below.
> [!warning]  
>
> Scripts are very much just plaintext files, they do not require a specific file extension and do not have any ability to use variables or conditional logic, they do support comments using '//'. This feature uses the 'script' command built into Spring Shell, [read more here](https://docs.spring.io/spring-shell/docs/2.0.0.RELEASE/reference/htmlsingle/#script-command) at [docs.spring.io](http://docs.spring.io).

### **Export Amelia Knowledge Content and Domain Configuration**
**Script file to export all Amelia knowledge content and domain configuration**
``` groovy
//
// This script will export all of the most used knowledge content from an Amelia instance to a local file system directory.
// The domain configuration will also be exported with its dependencies.
// This script will also handle logging in and out of the instance and exiting the CLI application once finished.
//
// login to the specified Amelia instance
amelia-login https://Amelia_URL_path/Amelia
// export a domain and its dependencies. This command will also create directories and files for the dependencies of the domain
amelia-domain-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export AIML content
amelia-aiml-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export BPN content
amelia-bpn-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export NLU settings
amelia-nlu-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export classifier model content (To export latest revisions of classifier (by default: DEPLOYED) use the following : --revisionTarget LATEST)
// To exports classifier in bulk, use the following flag : --bulk
amelia-classifier-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export entity content
amelia-entity-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export grammar content
amelia-grammar-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export integration asset content
amelia-integration-asset-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export integration property set content
amelia-integration-property-set-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export integration flow content
amelia-integration-flow-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export intent content
amelia-intent-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export multimedia content in the content manager
amelia-multimedia-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export response pool content
amelia-response-pool-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export script library content (To export specific scripts or recursively, use the following (by default: SPECIFIC): --export-strategy  SPECIFIC/RECURSIVE)
amelia-script-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export semnet document content
amelia-semnet-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export tabular data content
amelia-tabular-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export training document content
amelia-training-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// export escalation queues and the escalation teams that are associated with it.
amelia-escalation-queue-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// log out of the Amelia instance
amelia-logout https://Amelia_URL_path/Amelia
// shut down the application, it is important to include this otherwise the CLI process will not finish and return control back to the parent shell
exit
```
The above script will log in to the Amelia instance specified by the **--url** option. Note, this will prompt for a username and password, those can be specified with the **--username** and **--password** options respectively to avoid being prompted.
> [!warning]  
>
> If you would like to run a script without being prompted and not include the username and password in the script file, outside values such as environment variables can be passed in like so:
>
> ``` groovy
> printf "email\npassword\n" | java -jar conductor-engine-cli-<version>.jar @path/to/your/script
> ```
>
> This assumes that both the username and password are not included.

This command must be executed first to allow any of the following commands to run using the same Amelia instance URL. Each following command will then be run in sequence.
### **Import a Domain with Content into an Amelia Instance**
Another script can be written to import the content that was exported into another instance.
**Import a domain with content into an Amelia instance**
``` groovy
//
// This script will import all of the most used knowledge content from a local directory into an Amelia instance.
// The local directory used should contain content that was previously exported with Conductor.
// The domain configuration will also be imported with its dependencies.
// The order in which commands are executed matters when importing so dependencies can be properly resolved.
// This example scripts follows the latest recommended import order.
// This script will also handle logging in and out of the instance and exiting the CLI application once finished.
//
// login to the specified Amelia instance
amelia-login https://Amelia_URL_path/Amelia
// import the domain configuration, this will create or update domain and import set of the dependencies required by the domain. 
// Give --parent-code to set the parent domain code for the domain which is getting imported.
// Authentication policy setting for the domain will be same if it is already available in target instance otherwise authentication system/policy gets imported. 
amelia-domain-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target --parent-code ncp_target_parent 
// import AIML content, no dependencies required
amelia-aiml-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import tabular data content, no dependencies required
amelia-tabular-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import semnet document content, no dependencies required
amelia-semnet-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import multimedia content, no dependencies required
amelia-multimedia-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import response pool content, no dependencies required
amelia-response-pool-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import grammar content, no dependencies required
amelia-grammar-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import entity content, dependant on grammars and tabular data
amelia-entity-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import intent content, dependant on entities
amelia-intent-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import training document content, dependant on intents and entities
amelia-training-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import NLU settings
amelia-nlu-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import classifier model content, dependant on intents, entities, and training documents
// To import classifier in bulk, use the following flag : --bulk
amelia-classifier-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import script library content
amelia-script-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import integration asset content
amelia-integration-asset-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import integration property set content
amelia-integration-property-set-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import integration flow content
amelia-integration-flow-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import escalation queues and the escalation teams that are associated with it.
amelia-escalation-queue-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import BPN content
amelia-bpn-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// import the domain configuration, this will update domain configuration. Give --parent-code to set the parent domain code for the domain which is getting imported.
amelia-domain-import --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target --parent-code ncp_target_parent
// log out of the Amelia instance
amelia-logout https://Amelia_URL_path/Amelia
// shut down the application, it is important to include this otherwise the CLI process will not finish and return control back to the parent shell
exit
```
The above script will log in to a different instance than the one used in the previous export script. These two scripts could even be combined into one, the application will allow a user to be logged in to multiple Amelia instances at a time. 
The next command will import the domain configuration, creating it if it does not already exist.
The subsequent commands import the various content types in an order that takes into account their dependencies.
> [!warning]  
>
> The order in which content is imported is very important! The example above is the recommended order taking into account content that may depend on each other, i.e. BPN should be the last thing imported since it may rely on several other types of content.

### **Clean Content from a Target Domain**
One more example script, this time for cleaning/deleting content in an Amelia instance.
**Clean content from a target domain**
``` groovy
//
// This script will clean (delete) all of the most used knowledge content in an Amelia instance.
// The order in which commands are executed matters when cleaning so dependencies can be properly resolved.
// This example script follows the latest recommended import order.
// This script will also handle logging in and out of the instance and exiting the CLI application once finished.
//
// login to the specified Amelia instance
amelia-login https://Amelia_URL_path/Amelia
// clean all BPN content, usually happens first because of the many potential dependencies
amelia-bpn-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all classifier model content, needs to happen before intents and entities
// Bulk clean can be used to delete all classifier models in a faster way. Use following flag : --bulk
amelia-classifier-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all entity content, needs to happen before tabular data
// Bulk clean can be used to delete all entities in a faster way. Use following flag : --bulk
amelia-entity-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all intent content, needs to happen before grammars
// Bulk clean can be used to delete all intents in a faster way. Use following flag : --bulk
amelia-intent-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all grammar content
amelia-grammar-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all integration flow content, needs to happen before assets and property sets
amelia-integration-flow-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all asset content
amelia-integration-asset-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all property set content
amelia-integration-property-set-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all multimedia content
amelia-multimedia-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all response pool content
amelia-response-pool-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all script library content
amelia-script-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all semnet document content
amelia-semnet-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all tabular data content
amelia-tabular-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all training document content
amelia-training-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all AIML content
amelia-aiml-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// clean all escalation queue from domain
amelia-escalation-queue-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// log out of the Amelia instance
amelia-logout https://Amelia_URL_path/Amelia
// shut down the application, it is important to include this otherwise the CLI process will not finish and return control back to the parent shell
exit
```
> [!warning]  
>
> The order in which content is deleted is also important. The above example is the recommended order, and you may notice that it is the reverse of the import order.
> [!warning]  
>
> Don't forget to include the 'exit' command at the end of every script file. If this is not present, the CLI application process will continue to run.

### Migrate Authentication Systems and Policies
Additional example scripts for system configuration settings are below.
**Migrate authentication systems and policies**
``` groovy
//
// This script exports authentication polcies and systems from one instance and imports them in another.
// This script will also handle logging in and out of the instances and exiting the CLI application once finished.
//
// log in to the specified Amelia instance
amelia-login https://Amelia_URL_path/Amelia
// export authentication policies and the authentication systems they depend on
amelia-authentication-policy-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source
// log out of Amelia instance
amelia-logout https://Amelia_URL_path/Amelia
// log in to another Amelia instance
amelia-login https://Another_Amelia_URL_path/Amelia
// import authentication polcicies and the authentication systems they depend on
amelia-authentication-policy-import --url https://Another_Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source
// log out of Amelia instance
amelia-logout https://Another_Amelia_URL_path/Amelia
// shut down the application, it is important to include this otherwise the CLI process will not finish and return control back to the parent shell
exit
```
### Escalation Queues and Teams Commands
**Commands for escalation queues and teams.**
``` groovy
//
// Below are the export, import and clean commands for escalation queues and teams.
//
// export escalation queues from the domain and the escalation teams they depend on
amelia-escalation-queue-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// import escalation queues and the escalation teams they depend on
amelia-escalation-queue-import --url https://Another_Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// clean escalation queues from target domain
amelia-escalation-queue-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// export all escalation teams from Amelia instance
amelia-escalation-team-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// import escalation teams in Amelia instance
amelia-escalation-team-import --url https://Another_Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// clean all escalation teams from Amelia instance
amelia-escalation-team-clean --url https://Amelia_URL_path/Amelia
```
### Users and User Groups Commands
**Commands for users and user groups.**
``` groovy
//
// Below are export, import and clean commands available for users and user groups in an Amelia instance.
// NOTE: Imported users will not have passwords set if using the Default Authentication policy, the system does not allow these passwords to be exported.
//
// export users as well as the groups, roles, and authentication polcies they depend on
amelia-user-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source
// import users as well as the groups, roles, and authentication polcies they depend on
// Use following option for choosing import strategy: --import-strategy  [user-import-strategy][Optional, default = 1]
// Following user import strategies are available to choose from :
//  0 - Import only users (maps with only default authentication policy).
//  1 - Import users and maps existing user group and auth policy only if it's present in target.
//  2 - Import users with dependencies (imports user group & authentication policy if they are not present in target).
amelia-user-import --url https://Another_Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target
// clean all users from target domain
amelia-user-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
// export user groups from source domain
amelia-user-group-export --url https://Amelia_URL_path/Amelia --domain-code ncp_source
// import user groups in target domain
amelia-user-group-import --url https://Another_Amelia_URL_path/Amelia --domain-code ncp_target
// clean all user groups from target domain
amelia-user-group-clean --url https://Amelia_URL_path/Amelia --domain-code ncp_target
```
### Migrate UI Bundles
**Migrate UI Bundles**
``` groovy
//
// This script exports UI bundles from one instance and imports them in another.
// This script will also handle logging in and out of the instances and exiting the CLI application once finished.
//
// log in to the specified Amelia instance
amelia-login https://Amelia_URL_path/Amelia
// export UI bundles
amelia-ui-bundle-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source
// log out of Amelia instance
amelia-logout https://Amelia_URL_path/Amelia
// log in to another Amelia instance
amelia-login https://Another_Amelia_URL_path/Amelia
// import UI bundles
amelia-ui-bundle-import --url https://Another_Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source
// log out of Amelia instance
amelia-logout https://Another_Amelia_URL_path/Amelia
// shut down the application, it is important to include this otherwise the CLI process will not finish and return control back to the parent shell
exit
```
### Migrate with Dependencies
**Migrate with dependencies**
``` groovy
//
// This script command exports BPNs or domains configuration along with all dependencies from one instance and imports it into another.
// NOTE: Only dependencies which are present in the domain mentioned in the command gets migrated.
// To enable this feature, following flag is required : --with-dependencies
// For migrating  specific BPNs using names or ids, use the following : --names {comma separated names} --ids {comma separated ids}
// This script will also handle logging in and out of the instances and exiting the CLI application once finished.
// NOTE: BPNs and Domains can have a lot of dependencies. It is likely that when running this script more than just a bpn or domain file will be exported.
// The files exported will only contain additional configurations required by the BPN or Domain, NOT the rest of the content that is in the domain. 
// The content specific commands are to be used for those activities, these commands are for migrating along with their dependencies.
// log in to the specified Amelia instance
amelia-login https://Amelia_URL_path/Amelia
// export domain configuration and all of its dependencies
amelia-domain-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source --with-dependencies
// log out of Amelia instance
// export BPN content
amelia-bpn-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source --with-dependencies
// log out of Amelia instance
amelia-logout https://Amelia_URL_path/Amelia
// log in to another Amelia instance
amelia-login https://Another_Amelia_URL_path/Amelia
// import a domain and all of its dependencies, give --parent-code to set the parent domain code for the domain which is getting imported.
amelia-domain-import --url https://Another_Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_source --parent-code ncp_parent --with-dependencies
// import BPN content
amelia-bpn-import --url https://Another_Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-code ncp_target --with-dependencies
// log out of Amelia instance
amelia-logout https://Another_Amelia_URL_path/Amelia
// shut down the application, it is important to include this otherwise the CLI process will not finish and return control back to the parent shell
exit
```
### Metrics Export
**Metrics export command**
``` groovy
//
// This script will export Amelia conversation metrics and transcripts from a list of domains for a given date range.
// This script will also handle logging in and out of the instances and exiting the CLI application once finished.
// To export metrics from list of domain, use comma separated domain codes like : --domain-codes domain1,domain2,domain3
// --start-date and --end-date should be in following date format: yyyy-MM-ddThh:mm:ssZ
// To include context, use following flag : --include-context
// To include escalation, use following flag : --include-escalation
// To include transcript, use following flag : --include-transcript
// To create Eddie replay test files for each conversation exported, use following flag : --replay
//
// log in to another Amelia instance
amelia-login https://Amelia_URL_path/Amelia
// export Amelia conversation metrics
amelia-metrics-export --url https://Amelia_URL_path/Amelia --directory /tmp/conductor/playgroundv4/ncp_source --domain-codes ncp_source --start-date 2021-01-01T10:15:30.00Z --end-date 2021-07-19T10:15:30.00Z --include-context --include-escalation --include-transcript --replay
// log out of Amelia instance
amelia-logout https://Amelia_URL_path/Amelia
// shut down the application, it is important to include this otherwise the CLI process will not finish and return control back to the parent shell
exit
```
## Thread Pool Configuration
Maximum threads in the thread pool can be customized in Conductor using the below command. By default, the thread pool size is set to 16.
**Thread pool setting**
``` groovy
// below command will increase the maximum thread in thread pool to 20
thread-pool-setting --threadCount 20
```
## Logging Configuration
Rather than having application-specific controls, the best way to customize the logging behavior is by supplying a configuration file as a system property when running the application. Using this file when running the application can be done like so:
**Run the application with a custom logging configuration file**
``` groovy
java -Dlogging.config=/path/to/logback.xml -jar /path/to/jar
```
More information about the available configuration options can be found [here](http://logback.qos.ch/manual/configuration.html).
# File System Output 
When running export commands, the following structure can be expected to be created under the directory root specified in the **--directory** option of the command. The corresponding import commands will look for dependencies in the same structure, so it is very important to not modify any files or their locations after they have been written to the file system.
``` text
<directory_root>/
    aiml/
        aiml_list.json - list of AimlObjectListModel metadata.
        *.aiml - There will be an XML file for each AIML file that can be imported into Amelia admin.
    bpn_migration/bpn/
        bpn_annotation_list.json - list of BpnAnnotationSystemInstanceModel metadata.
        bpn_model_list.json - list of BpnModel metadata.
        bpn_revision_list.json - list of BpnRevisionModel metadata.
        bpn_tree.json - list of BpnTreeNode metadata.
        bpn_validation_export.json - list of BpnValidationModel metadata after export.
        bpn_validation_import.json - list of BpnValidationModel metadata after import.
        . - The folder structure from the instance will be recreated with an XML file or each BPN that can be imported into Amelia admin.
    classifier/
        classifier_list.json - list of ClassifierModelListModel metadata
        . - There will be a ZIP file for each classifier model exported that can be imported into Amelia admin.
        bulk/
            classifier_bulk_list.json - bulk model metadata.
            domaincode.zip - compressed classifier resource.
        .- The folder structure is created upon using --bulk command during classifier export/import.
    consume_web/
         url_list.json - list of consume web url metadata.
         auth_list.json - list of consume web auth metadata.
         cert_list.json - list of consume web cert metadata.
         proxy_list.json - list of consume web proxy metadata.
    entity/
        entity_list.json - list of EntityListModel metadata.
        entity_question_list.json - list of EntityQuestionModel metadata.
        entites.json - entities JSON file can than be imported into Amelia admin.
    grammar/
        grammar_list.json - list of NluGrammarListModel metadata
        grammars.xml - grammars XML file that can be imported into Amelia admin.
    integration_asset/
        asset_list.json - list of IntegrationAssetModel metadata.
        . - There will be a binary file for each integration asset
    integration_property_set/
        set_list.json - list of IntegrationPropertySetModel metadata
        . - There will be a plain text .properties file for each property set.
    integration_flow_migration/integration_flow/
        flow_list.json - list of IntegrationFlowModel metadata
        . - There will be an XML file for each integration flow main context.
    intent/
        intent_faq_annotation_list.json - list of AnnotationSystemInstanceModel metadata
        intent_faq_utterance_list.json - list of IntentUtteranceModel metadata
        intent_list.json - list of  IntentListModel metadata
        intents.tsv - intents TSV file that can be imported into Amelia admin.
    metrics/
        metric_export_timestamp.json - Chat metrics in json format.
        tests/
            test-export-date.replay - Replay conversation file in json format.
    multimedia/
        bucket_list.json - list of ContentBucketModel metadata
        . - There will be a directory for each bucket, and in each directory will be resource_list.json file and a binary file for each resource.
            The resource_list.json file will be a list of ContentResourceMetadata metadata.
    response_pool/
        annotation_list.json - list of AnnotationSystemInstanceModel metadata
        group_list.json - list of  ResponsePoolGroupModel metadata
        pool_list.json - list of ResponsePoolModel metadata
        . - Directories will be created for each response pool group and response pool. 
            For each response pool directory there will be an entry_list.json file which is a list of ResponsePoolEntryModel metadata.
    script/
        script_model_list.json list of ScriptModel metadata
        script_tree.json - list of ScriptTreeNode metadata
        parent_script_list.json - list of parent script included metadata
        . - The folder sctructure from the instance will be recreated with a file for each script.
    semnet/
        semnet_list.json - list of SemnetDocumentModel metadata
        . - There will be a binary file for each SemNet document that can be imported into Amelia
    system/
        authentication_policy/
            policy_list.json - list of AuthenticationPolicyListModel metadata
        authentication_system/
            system_list.json - list of AuthenticationSystemModel metadata
        ui_bundle/
            bundle_list.json - list of UiBundleModel metadata
            . - There will be a ZIP file for the exported revision of each UI bundle that can be uploaded to Amelia admin.
        nlu/
            nlu_settings.json - NLU settings
        1Desk/
            instance_list.json - list of OneDeskInstanceModel metadata
        1RPA/
            instance_list.json - list of OneRpaInstanceModel metadata
        1Store/
            instance_list.json - list of OneStoreInstanceModel metadata
    escalation_migration/system/
        escalation_queue/
            queue_list.json - list of EscalationQueueModel metadata
        escalation_team/
            team_list.json - list of EscalationTeamModel metadata
    user_migration/system/
        user/
            user_list.json - list of AdminUserModel metadata
        user_group/
            group_list.json - list of UserGroupModel metadta
        user_role
            role_list.json - list of RoleModel metadata
    domain_migration/
        . - There can be additional folders inside for domain configuration like escalation_migration, user_migration, bpn_migration
        system/domain/
            domain_list.json - list of AdminDomainModel metadata
            . - There will be an additional JSON file for each domain which contains the subsystem responder metadata.
    tabular/
        tabular_list.json - list of TabularDataModel metadata
        . - There will be a CSV file for each tabular data table that can be imported into Amelia
    training/
        training_list.json - list of DocumentRevisionModel metadata
        . - There will be a JSON file for each training document with its annotations that can be imported into Amelia
```
# FAQs
## What version should I use?
The Conductor CLI application is versioned to match up with Amelia core. When you use the application with an Amelia instance, you should use the version that matches the Amelia instance. See the following chart to determine which version of the CLI should be used with which version of Amelia.

| Amelia/Conductor | 3.7.x | 4.0.x | 4.1.x | 4.2.x | 4.3.x |
| ----|----|----|----|----|----|
| 3.7.x |  |  |  |  |  |
| 4.0.x |  |  |  |  |  |
| 4.1.x |  |  |  |  |  |
| 4.2.x |  |  |  |  |  |
| 4.3.x |  |  |  |  |  |

Using mismatched versions can result in errors due to breaking changes made to the APIs as new features are added to Amelia. For example, using a 3.7 version of the CLI with a 4.2 version of Amelia could have errors because the CLI is not aware of new things in 4.2. In the opposite scenario, using a 4.2 version of the CLI with a 3.7 version of Amelia will cause errors because the CLI expects to see new things that are not there.
## Can I move content between major/minor versions of Amelia?
Yes, but there is a catch. Major and minor versions can include breaking API changes, this is why Conductor releases are versioned to match. The corresponding Conductor version is aware of that version's API, so using it with another version has the potential to cause issues. That being said, it would not be wise to use, for example, Conductor 4.3.0 to export content from your 3.7.x Amelia instance, and vice versa. To move content from a 3.7 instance to a 4.3 instance, content would be exported from the 3.7 instances with a 3.7 version of Conductor and then the content could be imported into a 4.3 Amelia instance with a 4.3 version of Conductor.
# Download
> [!info]  
>
> To run the V3 compatible versions Java 8 is required to be installed on the host machine. To run the V4 compatible versions Java 11 is required to be installed on the host machine. We build and test using the Amazon Corretto JDK, other JDK distributions should work but are not tested by the developers. If managing multiple Java versions is an issue it is recommended to use the Docker image instead.

[Conductor Engine CLI 4.3.10 for Amelia Core V4](https://artifactory.ipsoft.com/artifactory/libs-release/net/ipsoft/conductor/conductor-engine-cli-service/4.3.10/conductor-engine-cli-service-4.3.10.jar) - 03/23/2022
[Conductor Engine CLI 3.7.13 for Amelia Core V3](https://artifactory.ipsoft.com/artifactory/libs-release/net/ipsoft/conductor/conductor-engine-cli-service/3.7.13/conductor-engine-cli-service-3.7.13.jar) - 02/07/2022
