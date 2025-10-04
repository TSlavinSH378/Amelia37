{% version "3.x" %}
Clients are a mechanism to allow multi-tenancy in Conductor. By default, the IPsoft client is always created in Conductor. Additional clients can be added to segregate access to a specified instance or migration resource that may be for a specific client. Users can be added to client groups to be allowed access to read and write to any restricted instance and migration resources for that client.
# Creating a Client
A new client can be created by going to the Clients list and pressing the blue button on the top right above the list.
![](attachments/32510225/32510226.png)
Figure. List of Clients Workspace
A client only contains two fields, its name and a Regex pattern for its instance URLs.
![](attachments/32510225/32510227.png)
Figure. Update Client Workspace
The name of a client should be unique to clearly identify which instances belong to them. The URL regex ensures that only the correct instances can be used with a client. Using this regex is optional, as it can just be made '.\*' to accept any URL.
> [!warning]  
>
> URL Regex functionality has not yet been implemented.

# Using Clients
Once a client is created, it can be selected when creating and editing [user groups](https://docs.amelia.com/display/AmeliaDocsV4/Authorization+Guide) and [instances](https://docs.amelia.com/display/AmeliaDocsV4/Instance+Guide). When creating a new client, also create at least one user group for it, otherwise, users will not be able to access any instances created with that client.
Selecting a client when editing a user group:
![](attachments/32510225/32510228.png)
Figure. Select Client When Editing a User Group
Selecting a client when editing an instance:
![](attachments/32510225/32510229.png)
Figure. Select Client When Editing an Instance
{% /version %}
