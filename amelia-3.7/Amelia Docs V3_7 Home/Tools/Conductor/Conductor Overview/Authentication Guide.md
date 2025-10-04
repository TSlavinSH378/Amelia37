{% version "3.x" %}
/\*\*/ Authentication Systems Default Authentication System LDAP Authentication System Setting a User's Authentication System
Conductor supports multiple authentication systems for logging in users. The default authentication system uses Conductor's application database to store user credentials. A commonly used alternative to this is to use an LDAP server to authenticate a user during login, while [authorization](Authorization%20Guide) is still handled by Conductor locally. 
# Authentication Systems
![](attachments/32510212/32510213.png)
Figure. List of Authentication Systems
# Default Authentication System
The default authentication system in Conductor is simply the application database containing the email address and password for each user. Passwords are salted and hashed before being stored in the database and are only ever decoded by the application during the authentication process. Nothing needs to be configured to set this up, however, this system can be disabled if another system is to be used instead.
![](attachments/32510212/32510214.png)
Figure. Default Authentication System Settings
The default authentication system can take advantage of a few settings:
-   Enabled Reset Password - if enabled, a user can reset their password from the login page or user profile page
-   Enabled Expire Password - if enabled, a password will expire and must be changed after a number of days
-   Password Expiry Days - if password expiry is enabled, a user will be forced to change their password this many days after it was last changed
# LDAP Authentication System
> [!warning]  
>
> This is currently a WIP feature. What is documented here will not be the final state.

An LDAP authentication system can be configured to authenticate users against an LDAP server before providing them access to the Conductor application. 
![](attachments/32510212/32510215.png)
Figure. LDAP Settings Workspace
An LDAP Authentication System has additional settings to configure.
Table. LDAP Settings

| Setting | Description |
| ----|----|
| Supports Auto-Create Users | If enabled, this authentication system can automatically create users when they attempt to log in |
| Enable Auto-Create Users | If enabled, when a user logs in that has never logged in before, their user account will automatically be created |
| User Search Filter | The LDAP search filter to use when looking for users |
| User Search Base | The LDAP search base for all users |
| LDAP Host URL | The LDAP URL of the server |
| LDAP Host Port | The LDAP port of the server |
| Manager DN | The manager username to access the LDAP server if required |
| Manager Password | The manager password to access the LDAP server if required |

# Setting a User's Authentication System
A [user](Authorization%20Guide) has a setting for which authentication system should be used when they log in. This setting can be changed when creating or editing a user. For any user that is auto-created by an authentication system, it will have that system set at their default.
> [!warning]  
>
> The IPsoft LDAP authentication system will automatically add users to the IPsoft Users group and assign them roles to access instances and migrations. This will be made configurable for other authentication systems in the future.

{% /version %}
