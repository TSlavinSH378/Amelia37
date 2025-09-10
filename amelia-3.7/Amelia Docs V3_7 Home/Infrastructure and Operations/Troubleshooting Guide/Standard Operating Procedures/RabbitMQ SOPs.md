These operating procedures help debug possible RabbitMQ issues.
# RabbitMQ Users
An Amelia RabbitMQ instance requires 4 users to be present:
-   amelia
-   ipsoft
-   monitoring
The monitoring and ipsoft accounts belong to a group. If not sure, compare their account details to a working environment.
## List active users
Run this command to list active users:
``` bash
# rabbitmqctl list_users
Listing users ...
ipsoft  [administrator]
monitoring  [monitoring]
amelia  []
```
## Add a User
Run this command to add a user:
``` bash
# rabbitmqctl add_user monitoring <password>
```
> [!warning]  
>
> Do NOT assign random passwords. See below for instructions.  All passwords are unique for each user in every single environment, only monitoring uses the same password.

## Add User to Group
Run this command to add a user to a group:
``` bash
# rabbitmqctl set_user_tags monitoring monitoring
```
# List/Set Permissions
Run this command to list and set permissions:
``` bash
# rabbitmqctl list_permissions
Listing permissions in vhost "/" ...
monitoring  .*  .*  .*
ipsoft  .*  .*  .*
amelia  .*  .*  .*
# rabbitmqctl set_permissions -p / monitoring ".*" ".*" ".*"
```
# RabbitMQ Overview Alert
> [!info]  
>
> **Do not restart RabbitMQ unless you intend to restart ALL components of Amelia.**

This alert indicates several possible problems.
1.  List queues that are not empty.
    ``` bash
    # rabbitmqctl list_queues|grep queue.amelia.cache|grep -v 0$
    ```
2.  Check if there are any consumers for those queues.
    ``` bash
    # rabbitmqctl list_consumers|grep <queue name>
    ```
    > [!info]  
    >
    > **If the queue name does NOT begin with queue.amelia.cache DO NOT continue.**
3.  If the command returns nothing, then purge the queue.
    ``` bash
    # rabbitmqctl purge_queue <queue name>
    ```
