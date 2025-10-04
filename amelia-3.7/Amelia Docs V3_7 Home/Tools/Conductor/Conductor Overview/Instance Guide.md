{% version "3.x" %}
This page describes the journey of registering and maintaining application instances in Conductor.
# Registering an Application Instance
To register a new application instance with Conductor, go to the Instances screen and click the blue button in the top right above the list.
![](attachments/32510231/32510232.png)
Figure. List of Instances Workspace
This will open the New Instance modal where the details of the application to be added need to be filled in.
![](attachments/32510231/32510233.png)
Figure. Create New Instance Workspace
Table. Create New Instance Workspace Elements

| Element | Description |
| ----|----|
| Instance Name | A friendly name to identify the instance |
| Client | The client that the instance will be associated with (only clients a user has access to will be displayed in this drop-down menu) |
| Instance Type | The identifier for what application this instance is, this will determine other fields that are required to add the instance |
| Instance URL | Common for any instance type, this is the URL to reach the application on the instance |
| Username | Common for any instance type, this is the username of an account used to login to the application |
| Password | Common for any instance type, this is the password of the account used to login to the application |
| Ignore Certificate Errors | Select to turn this on if the instance does not have a valid signed certificate |

To verify Conductor can make a connection, and validate the information entered, click the Check Connection button at the bottom left of the Create New Instance workspace. If the test is successful, click the Create button to save the instance for use in migrations.
# Amelia Instance Types
The available instance types for Amelia are currently, AMELIA36, AMELIA37, and AMELIA38. This identifies which core Amelia version the instance is running, which determines which Conductor engine should handle tasks involving that instance.
> [!info]  
>
> Use the Check Connection button before saving to verify Conductor can successfully login to the instance with the information provided.

**The user account configured for an Amelia instance should have full global permissions on that instance.** This assumes Conductor will be used to do all knowledge and configuration related changes.
Testing instance connection:
![](attachments/32510231/32510234.png)
Figure. Test the Instance Check Connection Feature
Successful connection:
![](attachments/32510231/32510235.png)
Figure. Check Connection Test is Successful
Failed connection:
![](attachments/32510231/32510236.png)
Figure. Check Connection Test Failed
> [!info]  
>
> This connection failed because the URL ended with **/admin** instead of **/Amelia**

# Git Instance Type
A Git application instance can be any flavor of Git repository such as GitHub, GitLab, Bitbucket, etc. All of these applications use the same Git protocol underneath and operate the same way from the perspective of Conductor.
> [!warning]  
>
> This functionality has not yet been implemented.

{% /version %}
