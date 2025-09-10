This page describes the journey of creating and submitting a migration request to be executed.
# Sources and Targets
In Conductor different systems can act as sources of data to be deployed to a target Amelia instance. Conductor will also facilitate the process of moving content from a source Amelia instance to a target Git branch. To accomplish either of these workflows, application instances must first be registered with Conductor. See the [Instance Guide](https://docs.amelia.com/display/AmeliaDocsV4/Instance+Guide) for more information on registering instances with Conductor.
With at least one Amelia instance registered with Conductor a migration plan can be created to move knowledge from one domain to another. With multiple Amelia instances, knowledge and configuration can be moved across those instances.
# Creating a Migration Plan
To create a migration plan click the blue plus button above the list of plans.
![](attachments/32510238/32510239.png)
Figure. Migration Plans Workspace
This will open the migration plan modal that will go through the steps required to create the plan.
![](attachments/32510238/32510240.png)
Figure. Create a Plan Workspace
The first step is to define the source and target instances and which domains will be included.
## One Instance
With one instance of Amelia, Conductor will support knowledge migrations from a single domain to another single domain in that instance.
## Two Instances
With two instances of Amelia,  Conductor will support knowledge migrations from multiple domains in the source to the same set of domains in the target as well as configuration migrations from the source to the target.
> [!warning]  
>
> Multiple domain migrations have not yet been implemented.

Once the instance is selected, Conductor will fetch the domains that exist in that instance to choose from.
![](attachments/32510238/32510241.png)
Figure. Conductor Displays Source Domains in a Selected Instance
![](attachments/32510238/32510242.png)
Figure. Conductor Displays Target Domains in a Selected Instance
Once domains are selected, click the Save button to create the Migration Plan.
# Creating a Migration Request
Once a migration plan exists, migration requests can be created from it. A migration request can be created by clicking the Migration button on the migration plan (the two arrows). This will open up the content selection modal:
![](attachments/32510238/32510243.png)
Figure. Select Content Types to Include in Migration
Clicking the details button on each category will fetch that information from the source instance configured on the migration plan. That row can then be expanded to browse through the content and make selections:
![](attachments/32510238/32510244.png)
Figure. Click Details Button to Display Information about a Category
Once all of the content is selected, clicking the Start Migration button will submit the request to be executed.
> [!warning]  
>
> Viewing migration status/progress is not yet implemented.

## Attachments:
![](images/icons/bullet_blue.gif) [image2020-5-27_10-12-13.png](attachments/32510238/32510239.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-5-27_10-12-52.png](attachments/32510238/32510240.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-5-27_10-13-42.png](attachments/32510238/32510241.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-5-27_10-14-56.png](attachments/32510238/32510242.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-5-27_10-16-50.png](attachments/32510238/32510243.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2020-5-27_10-17-53.png](attachments/32510238/32510244.png) (image/png)  
