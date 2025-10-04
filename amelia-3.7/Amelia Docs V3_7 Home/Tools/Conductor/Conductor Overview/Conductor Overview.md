{% version "3.x" %}
This page describes the high-level perspective of the user functionality for Conductor. 
# Getting Started
After installing Conductor, the setup wizard will walk through the first steps of getting Conductor ready for regular use. This includes creating the first administrator account, creating the first client, and creating user groups to assign future users to that client. Once the setup is complete the home page will be the Migration Plans list, which should be empty. The next thing to do would be to create an instance or two and then create a migration plan to use the instance(s). The following sections will go into detail about the rest of the functionality in Conductor.
# Clients
Main article: [Client Guide](Client%20Guide)
Clients are a way to group instances and users. Before any instances or user groups can be created a client must exist first. Conductor always has the default IPsoft client, but more can be added to separate concerns in any way. Beware that deleting a client once it has been used can be a very destructive operation. Any instances and user groups that were associated with that client will also be deleted and no longer useable in migrations.
# User Groups
Main article: [Authorization Guide](Authorization%20Guide)
User groups are a way to associate a group of users with a client. This will give those users access to all instances associated with that client. If a user can edit any of the instances for a client is determined by their roles and authorities.
# Users, Roles, and Authorities
Main article: [Authorization Guide](Authorization%20Guide)
Conductor implements a fairly standard RBAC model for users and controlling what they are able to do in the application. Users can be assigned any number of roles, which can be made up of any number of authorities. An authority determines a user's access to view or edit a different part of Conductor.
# Instances
Main article: [Instance Guide](Instance%20Guide)
The most basic use case for Conductor is to move things from one instance of Amelia to another or from one domain to another in the same instance, however, this is not the only use case. Conductor can also be used to take content from other sources and deploy it to an Amelia instance. This includes content maintained in Git repositories and packaged Amelia content from services like Artifactory or locally uploaded to Conductor (note that this content is never stored in Conductor). Conductor fits best into a deployment pipeline where Amelia content is being deployed to production in versioned releases. In this scenario, a release branch from a Git repository or a published release artifact can be loaded into Conductor and deployed to any Amelia instance. 
In the reverse direction, when using Git as a content management repository there is the need to get incremental changes out of an Amelia instance where work is being performed and into a Git branch. This type of migration can be performed the same way by selecting an Amelia instance and domains as the source and a Git repository and branch as the target. 
# Migrations
Main article: [Migration Guide](Migration%20Guide)
The primary functionality of Conductor is to perform knowledge and configuration changes in Amelia instances. This is accomplished through the concept of migration. First are Migration Plans, which define the source and target and information such as domains involved in the migration. Then a Migration Request is created from that Migration Plan which includes the content to be migrated and any options to take into consideration such as import conflict and revision strategies. When viewing a Migration Plan, all of the Migration Requests previously executed can be seen as well as their status and progress.
{% /version %}
