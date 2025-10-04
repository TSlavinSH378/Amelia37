{% version "3.x" %}
Refer to the Amelia Deployment Center installation guide for details about installing the software files. The document describes how to install the Amelia Deployment Center (ADC) then use it to configure and install Amelia software on one or more hosts.
Once installed, setting up an Amelia instance requires several elements be configured first, in this order:
![](attachments/11940196/11940226.png)
All tasks are performed by an administrator as the final steps in the installation process.
# Step 1. Set Up a Domain
Domains organize into one knowledge set Amelia's interface, escalation system, humanization, decision making modules, FAQs, and other elements of her architecture.
The Domains workspace is available by clicking the System Settings heading then the Domains link on Amelia's left side administration pages navigation.
1.  To add a new domain, click the New Button button at the top right of the Domains workspace.
2.  Complete the New Domain form that appears on the right side of the interface.
# Step 2. Set Up a Group
Groups organize a set of users, roles, and authorities within a new domain. Once the first domain is created, the next step is to create a group.
1.  Click the System Settings heading then the Groups link on Amelia's left side administration pages navigation. The Groups workspace appears.
2.  To add a new group, click the New User Group button at the top right of the Groups workspace.
3.  Complete the Groups form that appears on the right side of the interface.
# Step 3. Set Up an Escalation Team
Escalation teams are collections of users and must be created before creating one or more escalation queues. With a group created, create an escalation team.
1.  Click the System Settings heading then the Escalation Teams link on Amelia's left side administration pages navigation. The Escalation Teams workspace appears.
2.  To add a new team, click the New Escalation Team button at the top right of the Escalation Teams workspace.
3.  Complete the New Team form that appears on the right side of the interface.
# Step 4. Set Up an Escalation Queue
Escalation queues can only be finalized when one or more escalation teams have been created. A default escalation queue also must be selected when setting up a domain.
1.  Click the System Settings heading then the Escalation Queues link on Amelia's left side administration pages navigation. The Escalation Queues workspace appears.
2.  To add a new queue, click the New Escalation Queue button at the top of the Escalation Queues workspace.
3.  Complete the New Queue form that appears on the right side of the interface.
# Step 5. Configure the Default Escalation Queue for the First Domain
The last setup step is to connect the escalation queue to the initial domain created for the Amelia system.
1.  Click the System Settings heading then the Domains link on Amelia's left side administration pages navigation. The Domains workspace appears.
2.  Type the domain name in the search box at the top of the Domains list page to display the domain name.
3.  Click the notepad edit icon to the left of the domain name. The Domain edit page appears.
4.  Find the Escalations box and dropdown list then select a queue name from the dropdown list.
5.  Click the Save button at the top of the domain edit page to save changes.
The rest of this document describes how to configure an Amelia system based on the purpose of the system, for example, to set up an authentication system, users, and additional domains to store and process knowledge.
{% /version %}
