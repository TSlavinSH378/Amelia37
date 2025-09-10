Release notes for this tool track Amelia releases, for example, 3.7 are backwards compatible within their Amelia releases. A 3.7.0 and 3.7.1 Import Export Tool release both work with Amelia 3.7.0 to the latest 3.7.x Amelia release.
# 3.7.11
Release date: May 27, 2020
## Summary
A small release to fix a couple of bugs.
## Important highlights from this release
1.  BPNs that have shorter names contained in longer names will no longer be skipped when reading from the file system
2.  BPNs will no longer be undeployed at the start of an import. If a BPN needs to be moved or deleted for any other reason it will be undeployed with it's dependencies.
## Bug
AM3-13072 - Some BPNs can be skipped when names contain each other
AM3-13078 - All BPNs are being undeployed before an import
# 3.7.10
Release date: April 16, 2020
## Summary
One new feature and a couple bug fixes round out the final Impex release.
## Important highlights from this release
1.  Utterance annotations can now be moved for BPNs, intents, entities, and response pools. These will be moved as a part of the normal migration process, no additional options are required.  
    > [!warning]  
    >
    > Using this feature requires an Amelia core version of 3.7.43 or higher.
2.  Fixed a bug where Impex would try to import from a non existing source.
3.  Fixed a bug where training documents were not being imported correctly.
## Bug
AM3-12815 - Impex is not importing source training documents
AM3-12811 - Impex should not try to import if no source is given
## Defect (Client Requested)
AM3-11206 - HTML styles on lemmas are not transferred with BPN when moving to STG,PRD
# 3.7.9
Release date: March 23, 2020
## Summary
This release includes several major changes to available options and default behavior. The structure of the files that get written and read to the file system has changed and will not be compatible with previous versions of Impex.
## Important highlights from this release
1.  Exporting from the source and target is now multi threaded. This should reduce overall migration time by a noticeable amount. The option --threadPoolSize was added to control the amount of threads available.
2.  Internal response pool groups from the global domain can now be exported and migrated.
3.  Revision handling for BPNs and classifier models has been simplified. The --shallow and --revisionless options have been removed and the file system structure cleaned up.
4.  Integration content is now handle as 3 separate types. Instead of only including the integration type, it has been replaced by integration_flow, integration_asset, and integration_property_set. Migrating integration flows will still account for included assets and property sets, but will not migrate them.
## New Feature
AM3-9665 - Allow exporting internal response pools in global domain
AM3-9282 - Split integration assets and property sets into their own content types
## Enhancement (Client Requested)
AM3-11149 - Use threads for faster deployment
## Task
AM3-11602 - Deprecate the shallow/revisionless option
## Defect (Client Requested)
AM3-11865 - Impex 3.7.7 throws NullPointerException
# 3.7.8
Release date: February 7, 2020
## Summary
This is a small release that fixes a few bugs.
## Release Highlights
1.  Committing to a Git repository will now remove files that it sees are missing when exported.
2.  New BPNs with only one revision or no deployed revisions in the source can be deployed with the deploy argument.
3.  If Impex fails to login to an instance it will log an error and not continue trying to do things.
## Bug
AM3-12400 - New BPNs not being deployed
## Defect (Client Requested)
AM3-11879 - Remove old BPNs from GIT when exporting Amelia content to a GIT branch  
AM3-11683 - Git clone error not reported in the summary  
AM3-11642 - Impex continues to run after failing to login to an instance
# 3.7.7
Released October 24, 2019
## Summary
This release contains one new feature for Git repositories and two small bug fixes.
## New Stuff
AM3-11380 - This change adds support for checking out a Git tag when exporting content from a Git repository. This introduces a new option that can be used, '--gitTag \<tag\>.' A branch must still be specified when using this option.
AM3-8912 - This change updates an internal dependency to the latest version.
## Bugs Fixed
AM3-11604 - This change fixes an issue where a classifier model with multiple revisions that are newer than the deployed revision would not have the proper revision deployed in the target. This would occur specifically when using the '--revisions deployed' and '--revisionless' options at the same time. The warning for when a deployed revision does not exist for a classifier model when the '--revisions deployed' option is used is also now reported in the warning summary.
AM3-11349 - This change fixes an issue where a BPN could fail to be imported if using the '–search' option.
# 3.7.6
Released October 10, 2019
## Summary
This release contains several bug fixes to BPNs and a couple for other content types.
## New Stuff
None
## Bugs Fixed
AM3-10950 - This change fixes a bug where parsing a BPN XML was failing depending on the host machine default encoding.
AM3-11147 - This change fixes a bug where training documents that were deleted in the UI were still being exported by Impex.
AM3-11324 - This change ensures that UTF-8 encoding is used when writing AIML files to the filesystem to preserve foreign language characters.
AM3-11353 - This change fixes a bug where a BPN with an undeployed latest revision in the source would not get deployed in the target when using the \`--revisionless\` and \`--revisions deployed\` options in combination.
AM3-11354 - This change fixes a bug where the \`--revisonless\` option was not being applied to target file systems.
AM3-11437 - This change fixes a bug where some errors that could occur with classifier models were not being reported in the error summary.
# 3.7.5
Released September 19, 2019
## Summary
This release introduces new features supporting integrations as well as functional changes to how cleaning and deploying content works. Several bugs are also fixed, one creating a backward incompatibility.
## New Stuff
AM3-10916 - This change reorganized how content is cleaned and deployed when running a command. The first notable functional change is the deprecation of the --deploy option. This option should no longer be used when migrating content that needs to be deployed, now as the content is imported it will also be deployed (respecting any options or other factors that determine if it should be deployed). This change affects BPNs, classifier models, and integration flows.
For cleaning content, the first notable change is the order in which content is processed to ensure dependencies are handled correctly. 
Previous order: SCRIPT, TABULAR, MULTIMEDIA, SEMNET, RESPONSEPOOL, AIML, GRAMMAR, ENTITY, INTENT, TRAINING, NLU, CLASSIFIER, INTEGRATION, BPN
New order: NLU, AIML, SEMNET, GRAMMAR, TABULAR, MULTIMEDIA, SCRIPT, ENTITY, INTENT, CLASSIFIER, TRAINING, RESPONSEPOOL, INTEGRATION, BPN
This change in order is also reflected when exporting/importing content (the clean order is the reverse of the order shown above).
AM3-4717 - This change adds support for cleaning integration flows, they will now be handled by the --clean option.
AM3-4718 - This change adds support for cleaning integration assets, they will now be handled by the --clean option.
AM3-4719 - This change adds support for cleaning integration property sets, they will now be handled by the --clean option.
> [!warning]  
>
> When undeploying integration flows before deleting them an artificial delay of 5 seconds is in place. This is only until AM3-11104 is implemented and the request status can be more accurately tracked. Until then, cleaning integrations may take longer than expected. If any integration flow fails to be deleted, any assets or property sets used by that flow will also fail to be deleted.

## Bugs Fixed
AM3-10005 - This change fixes an issue where Semnet documents of the same name were being uploaded multiple times rather than replacing an existing document.
AM3-10880 - This change fixes an issue where the tabular data column option was being applied even if it wasn't supplied in the command.
AM3-10885 - This change fixes an issue where a BPN that contained a script task with no description would cause an uncaught exception and halt the running process.
AM3-10922 - This change fixes an issue with the response pool file system structure. Previously, the response pool files were all written to a flat structure under the "../responsepool" directory. This caused issues if a response pool with the same name existed in multiple response pool groups. To resolve this file structure was changed from flat to hierarchical similar to BPNs, scripts, and multimedia.
Previous structure:
![](attachments/11946083/25461069.png)
Figure. Previous Response Pool File System Structure
New structure:
Figure. New Response Pool File System Structure
> [!warning]  
>
> This change in structure is not backward compatible. Response pools exported with Impex versions before 3.7.5 will not be able to be imported with 3.7.5 and later.

AM3-11138 - This change improves performance when exporting BPNs by only querying the list of possible entity questions once before exporting the BPNs.
AM3-11147 - This change fixes an issue where training documents deleted in the UI were still being exported by Impex.
AM3-11221 - This change fixes an issue when exporting from a file system that contains empty content directories.
# 3.7.4
Released August 1, 2019
## Summary
This release contains several bug fixes and one new option for importing tabular data files.
## New Stuff
AM3-10459 - This change introduces the '--tabularColumn' option which can be provided any number of times with values such as "name"="String". This option allows a user to specify the name of a tabular data column and the data type that the column should be saved as. Previously, when a file is uploaded Amelia core will infer the column data type from its contents. In some scenario where the data could vary, the type would be inferred incorrectly and cause issues after being imported. This option will now allow users to ensure a column is always set to the correct data type.
## Bugs Fixed
AM3-9283 - This change fixes an issue where entities with multiple questions that are used in a BPN would not maintain the same question when being imported into the target. Note that this will extend the time it takes to migrate BPNs as additional API calls need to be executed to retrieve entity question details for each ask task that uses them in a BPN.
> [!warning]  
>
> For this fix to work between domains in the same instance it will require Amelia core 3.7.27, specifically because of AM3-10331.
> [!warning]  
>
> It is important to note that this change adds a dependency on entities being updated before BPNs. Impex will handle this import order itself if left to do so, however, if only BPNs are included in an import command, this may result in questions not matching the source if the entities were not updated first.

AM3-10330 - This change makes it so when an exception is encountered when deleting a script library it will properly be included in the clean summary.
AM3-10374 - This change fixes a regression that was introduced in the last release where the '--include' and '--exclude' options were no longer being recognized when provided. These options will now behave as expected.
AM3-10496 - This change addresses issues with special characters in the entity JSON file being exported to the file system. The file will now be written with UTF-8 encoding to preserve characters in their correct format.
# 3.7.3
Released July 8, 2019
## Summary
A small release featuring two minor changes.
## New Stuff
JIRA-10050 - This change adds a new command line option, --revisionless. This option has the same behavior as the --shallow option, however, when exporting to a filesystem the file created for the revision will not have the revision number in the file name (it is still in the metadata contained in the file). This is useful when exporting files to be committed to a Git repository as the same file name can be maintained and tracked more easily using Git diffs.
JIRA-10003 - This change makes the exit code produces by Impex more reliable so it can be used with other automation techniques/tools. Previously, Impex would always exit with an exit code of 0 is it was able to complete the process without any fatal errors or uncaught exceptions (which would result in an exit code of 1). After this change, any errors and warnings encountered while importing/exporting will influence the exit code. If Impex completes its job with no errors or warnings it will have an exit code of 0. If there are any errors fatal or otherwise the exit code will be 1. If there are any warnings (and no errors) the exit code will be 2.
## Bugs Fixed
None.
# 3.7.2
Released June 11, 2019
## Summary
This release contains several important changes to the available options and their behavior. Several critical bugs are also fixed.
## New Stuff
AM3-9951 - This change removed several options and replaces them with new ones. Options removed: --ameliaUser, --ameliaPass, --gitUser, --gitPass. Options added: --sourceUser, --sourcePass, --targetUser, --targetPass,--share-auth. With these new options, different credentials can be used for the source and target systems, regardless of what that system is. The --share-auth option can be used to only provide credentials for the source and they will also be applied to the target. If none of these options are provided they will still be prompted for during execution.
AM3-9667 - This change makes it so the following options are no longer applied to the target system: --search, --revisions, and --shallow. This was done because filtering the target in any way can cause issues when searching for dependencies or existing content to update.
AM3-9622 - This change brings the behavior of classifier model revisions in line with how BPN revisions are handled. Now, only classifier model revisions with a major version greater than 0 and a minor version equal to 0 will be imported (1.0, 2.0, 3.0, etc). The revision that was deployed in the source will automatically be deployed in the target after it is imported (--deploy no longer required). The revision options (--revisions and --shallow) both behave as expected to control which revision and how many revisions get moved.
AM3-9848 - This change overrides the import strategy used for intents and entities if MERGE is set to be used (either by being the global default or explicitly set as an option). This was done because the definition of MERGE in the context of Amelia core did not line up with the general definition Impex uses. When MERGE is used in Amelia core for intents and entities, settings will not be updated in the target if they are changed in the source, OVERWRITE must be used for these settings to be updated. This addresses the issues raised in AM3-9006 and AM3-9007.
AM3-9417 - This change suppresses 404 exceptions from appearing in the log when deleting an entity. This was done primarily due to parent/child entities and how they are handled by Amelia Core. If you delete a parent entity in Amelia core, it will automatically delete the child entities for you. In Impex, this resulted in the tool still thinking the child entities are still there and attempting to delete them. Until better logic is implemented to determine parent/child relationships, the tool will still attempt to delete the child but ignore the error produced when it can't find it.
AM3-9483 - This change will make it so the tool will not attempt to delete the builtin.fallbacks intent (because it can't).
AM3-9628 - This change will make it clearer if there is an issue getting the domain specified in the --sourceDomain or --targetDomain options.
AM3-9484 - This isn't a functional change, but a change to the test cases in the code base. They will now more accurately catch any issues when running.
## Bugs Fixed
AM3-9006 - Addressed an issue where the expected updates were not made to entities (see AM3-9848).
AM3-9007 - Addressed an issue where the expected updated were not made to intents (see AM3-9848).
AM3-9544 - Fixed a bug where only up to 100 revisions of a BPN could be exported.
AM3-9555 - Fixed a bug that would create an empty grammars.xml file when importing to a file system even if there were no grammars to export.
AM3-9603 - Fixed a bug that would cause script libraries to not have their included libraries set properly.
AM3-9826 - Fixed a bug that caused creating BPN/script folders/models to fail because of filtering being done on the target (resolved in AM3-9667).
AM3-9840 - Fixed a bug that caused Unicode characters to be converted to HTML safe representations in JSON files
# 3.7.1
Release May 16, 2019
## Summary
This release was mostly bug fixes and maintenance items, no new major functionality.
## New Stuff
AM3-9279 - Added a warning when exporting integration flows and property sets that contain encrypted properties. This warning will be displayed in the export summary when impex has finished running. This warning was added because encrypted properties cannot be decrypted and exported from an Amelia instance. These properties will be replaced with a value of "CHANGE_ME" to clearly indicate they need to be updated after being imported into the target Amelia instance.
## Bugs Fixed
AM3-8970 - Fixed a bug where integration property sets with encrypted properties did not get updated with the "CHANGE_ME" placeholder.
AM3-9331 - Fixed a bug where response pools were not imported to the proper groups.
AM3-9469 - Fixed a bug where JSON files were created for classifier models that were not actually supposed to be exported to the file system.
AM3-9439 - Fixed a bug where multimedia files exported from the content manager would be incorrectly written to the file system.
AM3-9356 - Fixed a bug where exporting entities from a file system would not import into an Amelia instance.
AM3-9429 - Fixed a bug where exporting intents from a file system would not import into an Amelia instance.
## Attachments:
![](images/icons/bullet_blue.gif) [image2019-9-23_10-13-36.png](attachments/11946083/25461069.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-9-23_10-14-35.png](attachments/11946083/25461070.png) (image/png)  
