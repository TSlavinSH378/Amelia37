-   [System Authentication](#AccessandPermissions-SystemAuthentication)
    -   [Authentication Systems](#AccessandPermissions-AuthSystemsAuthenticationSystems)
        -   [LDAP](#AccessandPermissions-LDAP)
        -   [Deny All](#AccessandPermissions-DenyAll)
        -   [SAML 2](#AccessandPermissions-SAML2)
        -   [Default Authentication Systems](#AccessandPermissions-DefaultAuthenticationSystems)
    -   [Authentication Policy](#AccessandPermissions-AuthPoliciesAuthenticationPolicy)
        -   [Deny All Pre-Configured Authentication Policy](#AccessandPermissions-DenyAllPre-ConfiguredAuthenticationPolicy)
        -   [Internal Pre-Configured Authentication Policy](#AccessandPermissions-InternalPre-ConfiguredAuthenticationPolicy)
-   [User Authentication and Permissions](#AccessandPermissions-UserAuthenticationandPermissions)
    -   [Authentication Process](#AccessandPermissions-AuthenticationProcess)
    -   [AuthFailure Process](#AccessandPermissions-AuthFailureProcess)
    -   [Authorization Process](#AccessandPermissions-AuthorizationProcess)
        -   [Example: Users with one User Group, Domain, Role and Permissions](#AccessandPermissions-Example:UserswithoneUserGroup,Domain,RoleandPermissions)
        -   [Example: Agent Users with one User Group, Domain, Role and Permissions](#AccessandPermissions-Example:AgentUserswithoneUserGroup,Domain,RoleandPermissions)
        -   [Example: User with Multiple User Group, Domains, Roles and Permissions](#AccessandPermissions-Example:UserwithMultipleUserGroup,Domains,RolesandPermissions)
    -   [Authorities](#AccessandPermissions-AuthorityDefsAuthorities)
    -   [Roles](#AccessandPermissions-RoleDefsRoles)
    -   [User Groups](#AccessandPermissions-UserGroupDefsUserGroups)
-   [Spring Security Framework](#AccessandPermissions-SpringSecurityFramework)
This section describes the technical details of Amelia's authentication system and user-related permissions.
# System Authentication
Each instance of Amelia has a range of authentication systems, policies, and other details documented in this section. Creating and modifying these elements is covered in the System Configuration section.
## Authentication Systems
Authentication systems in Amelia define where and how to store user credentials, and how to verify them.
All authentication systems have the following configurable properties.  Specific, or custom authentication systems, may require additional configuration or custom development.
Table. Authentication System Configurable Properties

| Name | Name of the authentication system |
| ----|----|
| Code | Short code for the authentication system. The code cannot be deleted, only disabled. |
| Type | The type of authentication system. By default, Amelia supports LDAP (or AD), Deny All, SAML2 and Internal authentication systems. |
| Password Change Supported? | Whether Amelia can, or is allowed to, change user passwords in this authentication system. |

The internal authentication system in Amelia is the default.  Passwords are stored hashed with [Bcrypt](http://docs.spring.io/spring-security/site/docs/4.0.3.RELEASE/apidocs/org/springframework/security/crypto/bcrypt/BCryptPasswordEncoder.html) in the Amelia database.Internal
### LDAP
When LDAP is configured, Amelia does not store user passwords (or hashes), but instead delegates password verification to the configured LDAP server.  LDAP configuration supports the following additional configuration parameters:
Table. Key LDAP Options

| Parameter | Description |
| ----|----|
| URL | The LDAP or LDAPS URL of the LDAP server including port. |
| Base DN | The root distinguished name to use. |
| Admin DN | User to authenticate against the LDAP server if anonymous read only is not allowed. |
| Admin Password | Password of the Admin DN user. |
| Email Field | Email field |
| UID Field | Unique user id field |
| First Name Field | Field containing user first name |
| Last Name Field | Field containing user last name. |
| Search Filter | Filter template to use when searching for user objects. The template may include the tokens from the user object by surrounding the token name with ${}. For example, to include email address as the uid:(&(uid=${email})(objectClass=person)) |

### Deny All
The Deny All authentication system is used for required accounts that should not allow interactive login.  Any attempt to authenticate to this authentication system will fail and no passwords or hashes are stored.  This authentication system is used for the amelia user by default.
### SAML 2
Amelia supports both Service Provider (SP) initiated and Identity Provider (IDP) initiated SAML2 authentication.
As with all authentication methods supported by Amelia, SAML2 is integrated within the core Amelia authentication and authorization framework.  In the SAML2 case, support is provided by Spring Security SAML.
SAML authentication is only supported for web clients (not mobile).
Table. Key SAML2 Options

| Field | Required | Default | Description |
| ----|----|----|----|
| SP Metadata Path | n/a |  | The path must be provided to the IDP at configuration time. Once configured, the Amelia SP metadata will be accessible at this URL. |
| IDP Metadata Provider | Yes | File | Where to load IDP metadata from. File should be used unless there is a specific reason to use HTTP. |
| IDP Metadata XML | If provider = File |  | The metadata from the IDP. Must be provided by the IDP administrator during configuration. |
| IDP SSL Certificate | If provider = HTTP |  | The certificate of the web server hosting the the IDP metadata. |
| SP Base URL | Yes |  | Should be the public URL of Amelia suffixed by /Amelia/api. For example:;https://amelia.acme.com/Amelia/api |
| SP Entity ID | No | net:ipsoft:amelia:sp:[auth system code] | The service provider entity ID. Generally speaking the auto-generated default is fine. |
| SP Certificate | No | A new self-signed certificate will be generated upon first save. | The certificate Amelia uses to sign AuthnRequests sent to the IDP. |
| SP Private Key | No | Will be auto-generated if the SP certificate is auto-generated. | The private key fro the SP certificate. |
| SP Private Key Password | No | Will be auto-generated if the SP certificate is auto-generated. | The password for the SP private key. |
| Sign SP Metadata | Yes | True | Whether to sign the SP provider metadata. Note, some IDPs may not support signed metadata. |
| IDP Metadata Trust Check | Yes | True | If the IDP metadata is signed, whether to verify the signature. |
| IDP Metadata Requires Signature | Yes | False | Whether we require metadata from the IDP to be signed. |
| Assertion Email Property | Yes | EmailAddress | The name of the property containing the user's email address from the IDP generated assertions. |
| Assertion First Name Property | Yes | FirstName | The name of the property containing the user's last name from the IDP generated assertions. |
| Assertion Last Name Property | Yes | LastName | The name of the property containing the user's last name from the IDP generated assertions. |
| Use External Id | Yes | False | If the NameId from the saml assertions is not the user's email address. |
| Auto Create Users | Yes | False | Whether to auto-create users |
| Associated User Group | No |  | The name of the group to add newly created users to. |

### Default Authentication Systems
Upon a new install of Amelia, the following authentication systems are pre-configured:
Table. Amelia Pre-Configured Authentication Systems

| Name | Code | Type | Password Change Supported? |
| ----|----|----|----|
| Deny All | denyall | DENY_ALL | false |
| Internal | internal | INTERNAL | true |

## Authentication Policy
Each domain in Amelia is associated with an authentication policy.  A user may also be directly associated with an authentication policy. If a user has an authentication policy it is used, if not, the authentication policy of the user's primary domain is used.
Each policy supports the following configuration parameters:
Table. Authentication Policy Configuration Parameters

| Parameter | Description |
| ----|----|
| Name | Policy name. |
| Authentication System | The authentication system to use with this policy. |
| Password Change Allowed? | Whether end-users can change their password. Regardless of this setting, if the associated authentication system does not allow changing passwords, users are not allowed to change their password. |
| Forgot Password Allowed? | Whether a user is allowed to use forgot password functionality. Note, it is not possible to know an unauthenticated user's authentication policy to hide the Forgot Password link in the UI. If a user attempts forgot password and their authentication policy prohibits it, they will be notified at that time. |
| Password Complexity Descriptions | Descriptions of password complexity requirements for this policy for each language supported in the instance. |
| Password Min Length | The minimum length of the users password. |
| Password Max Length | The maximum length of the users password. |
| Complexity Rules | Complexity Rules use regular expression to impose requirements on passwords, and are formed as follows:(regular expression1)::(min occurrences)::(regular expression2)::(min occurrences)To force a password to contain at least one lowercase letter, one uppercase letter, and one number, the rule would be:[a-z]::1::[A-Z]::1::[0-9]+::1 |
| Min Complexity Matches | The Min Complexity Matches allows you to define the number of rules that must be matched. A Min Complexity Match of 2 would mean that only 2 of the three above rules would need to succeed. If left blank, then all rules must be matched. |
| Rejection Rules | Rejection Rules are rules that the password may not;contain and are formed as follows:(regular expression1)::(min occurrences)::(regular expression2)::(min occurrences)These rules can use tokens to indicate values from the user's profile that are not allowed. A token is a property name surrouned by ${ and }. For example, to disallow spaces, or the user putting their first name or last name in their password, you could use these rules:[\s]::1::(?i)${firstName}::1::(?i)${lastName}::1 |
| Past Password Retention | The number of past password (hashes) to remember. Users are not able to reuse any of these passwords. |
| Password Expiration Days | The number of days after which a user must change their password on next login. |
| Password Expiration Warning Days | The number of days prior to password expiration where the user will be warned that their password is going to expire. |
| Minimum Password Age | How frequently (in days) a user is allowed to change their password. |
| Max Login Attempts | Number of failed login attempts allowed before locking an account. |
| Lockout Duration | Number of minutes since the last failed login to lock an account. |
| Inactivity Expiration | Number of days after which an account will auto-expire if not logged into. |

Upon a new install of Amelia, the following authentication policies are pre-configured for Deny All and Internal.
### Deny All Pre-Configured Authentication Policy

| Parameter | Description |
| ----|----|
| Name | System User Authentication Policy |
| Authentication System | Deny All |
| Password Change Allowed? | no |
| Forgot Password Allowed? | no |
| Password Complexity Description | blank (n/a) |
| Password Min Length | blank (n/a) |
| Password Max Length | blank (n/a) |
| Complexity Rules | blank (n/a) |
| Min Complexity Matches | blank (n/a) |
| Rejection Rules | blank (n/a) |
| Past Password Retention | blank (n/a) |
| Password Expiration Days | blank (n/a) |
| Password Expiration Warning Days | blank (n/a) |
| Minimum Password Age | blank (n/a) |
| Max Login Attempts | blank (n/a) |
| Lockout Duration | blank (n/a) |
| Inactivity Expiration | blank (n/a) |

### Internal Pre-Configured Authentication Policy

| Parameter | Description |
| ----|----|
| Name | Default User Authentication Policy |
| Authentication System | Internal |
| Password Change Allowed? | yes |
| Forgot Password Allowed? | yes |
| Password Complexity Description | en: Must be between 8 and 16 characters and contain at least one of 3 of the following 4 groups: lower case letters, uppercase letters, numbers, and special characters. Cannot contain the email, first name, last name, or white spaces (case insensitive). |
| Password Min Length | 8 |
| Password Max Length | 16 |
| Complexity Rules | [a-z]::1::[A-Z]::1::[\d]::1::[^a-zA-Z0-9]::1 |
| Min Complexity Matches | 3 |
| Rejection Rules | [\s]::1::(?i)${email}::1::(?i)${firstName}::1::(?i)${lastName}::1 |
| Past Password Retention | 25 |
| Password Expiration Days | 90 |
| Password Expiration Warning Days | 7 |
| Minimum Password Age | 1 |
| Max Login Attempts | 3 |
| Lockout Duration | 30 |
| Inactivity Expiration | 90 |

# User Authentication and Permissions
When a user logs in, their membership in groups defines what authorities they have. Authorities represent what a user can see or do, for example, all users have the authority to login. Users are grouped into roles that collect and reuse authorities. This section describes the technical details of these elements.
## Authentication Process
The default authentication credentials in Amelia are email and password.  The authentication process follows these steps:
1.  Credentials are sent from the client (browser) over TLS to the server.
2.  The user is looked up by email.  If not found, goto AuthFailure with status FAIL_NOT_FOUND.
3.  If the user is not enabled, go to AuthFailure with status FAIL_DISABLED.
4.  If the user is expired, go to AuthFailure with status FAIL_EXPIRED.
5.  If the user's primary domain is disabled, go to AuthFailure with status FAIL_DISABLED.
6.  Verify the provided password with the user's authentication system.
    1.  Internal authentication system: Compare with [BcryptPasswordEncoder](http://docs.spring.io/spring-security/site/docs/4.0.3.RELEASE/apidocs/org/springframework/security/crypto/bcrypt/BCryptPasswordEncoder.html) against the stored hash.  Go to AuthFail with status FAIL_AUTH comparison fails.
    2.  LDAP/AD authentication system: Lookup user and attempt to bind as that user with supplied credentials.  Go to AuthFail with status FAIL_AUTH if bind fails.
    3.  Deny All: Go to AuthFail with status FAIL_NOT_ALLOWED.
7.  If the user is currently locked, go to AuthFailure with status FAIL_LOCKED.
8.  At this point, the user has successfully authenticated to Amelia.
    1.  Their failed login attempts counter is reset to zero.  
    2.  Their last successful login timestamp is updated to the current date/time.
9.  Check for password expiration:
    1.  If the password has expired, the user is forced to change their password before interacting with Amelia.
    2.  If the password has the force expiration flag set to true, the user will be forced to change their password before interacting with Amelia.
    3.  If the password is nearing expiration the user is notified that their password is nearing expiration.  The user may dismiss this notification and continue interacting with Amelia.
10. Log the successful login.
11. User is logged in.
## AuthFailure Process
The user has failed to authenticate.  The behavior slightly varies based on why they failed to authenticate.  Care is taken to have the same response for authentication failures where the user did not supply valid credentials.
1.  If FAIL_LOCKED, the user is notified that their account is temporarily locked and to try again later.
2.  Otherwise:
    1.  Increment their failed login attempts by one.
    2.  Set their last failed login date to the current date/time.
    3.  The user is notified with a generic error message "Username or Password is invalid".
3.  Log the failed login attempt.
## Authorization Process
Amelia supports role based access control at a global (install/instance) and domain level.  This allows users to be granted authority to view, edit, and operate within a single domain but not for other domains.  The default installation of Amelia comes with a pre-configured set of Roles and Groups.  Significantly more complex configurations are possible, however, it is recommended to keep the RBAC configuration as simple as possible while still meeting deployment requirements.
Beginning with a visual example, here are three authorization examples.
Note Domain-\>User Group-\>Role-\>Authority.
### Example: Users with one User Group, Domain, Role and Permissions
![](attachments/11940292/11940295.png)
### Example: Agent Users with one User Group, Domain, Role and Permissions
![](attachments/11940292/11940294.png)
### Example: User with Multiple User Group, Domains, Roles and Permissions
![](attachments/11940292/11940293.png)
## Authorities
Authorities are granted to users upon login based on their group memberships.  An authority represents the ability to perform an action or view a something within Amelia.  The set of authorities is fixed and not configurable.
Table. Pre-Configured Authorities

| AUTHORITY_USER |
| ----|
| Most basic authority in the system. ;Allows user to login. |
| Allows user to have a conversation with Amelia as User. |
| Allows user to view active conversations. |
| Allows user to push new conversations to other users. |
| Allows user to pickup a conversation as an agent. |
| Allows user to steal a conversation from another agent. |
| Allows user to assign a conversation to an agent. |
| Allows user to observe a conversation. |
| Allows user to export a conversation. |
| Allows user to transfer a conversation to a queue. |
| Allows an agent to choose to auto-deploy learnt knowledge on conversation close. |
| Allows user to have a conversation on the 'Mind' page. |
| Allows user to have a conversation on the 'Mind 3D' page |
| Allows user to view administration area unless restricted by other more specific authority. |
| Allows user to view users. |
| Allows user to edit users. |
| Allows user to edit RBAC related entities (groups, members, roles). Having this globally should be restricted carefully as it allows granting authorities globally and configuring authentication policies and systems. |
| Allows user to create and edit a BPN. |
| Allows a user to deploy a BPN. |
| Allows a user to view a BPN. |
| Allows viewing general domain configuration. |
| Allows editing general domain configuration. |
| Allows editing of avatar voice. |
| Allows editing of translation configuration. |
| Allows viewing metrics. |
| Invalid authority. Is only used to handle cases where a new authority may exist in the database prior to this;enumeration being updated. |
| Authority to view integration templates. |
| Authority to edit integration templates. |
| Allows user to create and edit an Integration Flow or Asset. |
| Allows a user to deploy an Integration Flow. |
| Allows a user to view an Integration Flow or Asset. |
| Authority to execute integration flows directly in user-web. |
| Allows user to view escalation queues and escalation teams. |
| Allows user to edit escalation queues and escalation teams. |
| Allows user to view escalation teams. |
| Allows user to edit escalation teams. |
| Allows user to view one desk instances. |
| Allows user to edit one desk instances. |
| Allows access to the supervisor view. |
| Allows user to see the response pool. |
| Allows user to edit the response pool. |
| Allows user to execute "run the workflow" command. |
| Allows admin to view humanization resource files. |
| Allows admin to edit humanization resource files. |
| Allows the logged user to specify a different user to than themself to use for given APIs. For example, to;start a conversation as a different user. |
| Allows knowledge designers to see the training system related panel like intent, entity, training dashboard. |
| Allows knowledge designers to edit the train entities like intent, entity. |
| Allows knowledge designer to create training/annotation instance. |
| Allows knowledge designers to import, train and delete from real, live user conversation data. |
| Allows admin to edit other users face profile. |
| Allows admin to view UiBundles. |
| Allows admin to edit UiBundles. |
| Allows admin to deploy and undeploy UiBundles. |
| Allows admin to add new files to tabular data. |
| Allows admin to edit the tabular data metadata and content. |
| Allows admin to view tabular data. |
| Allows users to view AIML documents. |
| Allows users to create and edit AIML documents. |
| Allows users to delete AIML documents. |
| Allows users to view Semnet documents. |
| Allows users to create and edit Semnet documents. |
| Allows users to change Semnet thresholds and answer format. |
| Allows users to delete Semnet documents. |
| Allows users to configure and use Semnet transducer. |
| Allows users to view Content Manager. |
| Allows users to create and edit documents/buckets in Content Manager |
| Allows users to delete documents/buckets in Content Manager. |
| Allows user to test an already trained model. |
| Allows a user to view the audit event log. |
| Allows a user to export conversations. |
| Allows a user to cleanup conversation summaries and delete transcripts. |
| Allows users to view Journey Analytics. |
| Allow user to annotate misclassification during conversation. |
| Allows user to install content packs. |
| View one store instance attached to Amelia. |
| Edit one store instance properties. |
| Allows user to view one rpa instances. |
| Allows user to edit one rpa instances. |

## Roles
Roles allow defining collections of authorities and reusing these across multiple user groups.  Roles are configurable through the administration interface.
Amelia comes pre-configured with the following roles:
Table. Pre-Configured Roles

| Administrator |
| ----|
| AUTHORITY_ADMIN_AUDIT_VIEW, AUTHORITY_ADMIN_DOMAIN_EDIT, AUTHORITY_ADMIN_DOMAIN_EDIT_AVATAR_VOICE, AUTHORITY_ADMIN_DOMAIN_EDIT_TRANSLATION, AUTHORITY_ADMIN_DOMAIN_VIEW, AUTHORITY_ADMIN_ESCALATION_QUEUE_EDIT, AUTHORITY_ADMIN_ESCALATION_QUEUE_VIEW, AUTHORITY_ADMIN_ESCALATION_TEAM_EDIT, AUTHORITY_ADMIN_ESCALATION_TEAM_VIEW, AUTHORITY_ADMIN_FACE_EDIT, AUTHORITY_ADMIN_HUMANIZATION_RESOURCE_EDIT, AUTHORITY_ADMIN_HUMANIZATION_RESOURCE_VIEW, AUTHORITY_ADMIN_ONE_DESK_INSTANCE_EDIT, AUTHORITY_ADMIN_ONE_DESK_INSTANCE_VIEW, AUTHORITY_ADMIN_ONE_RPA_INSTANCE_EDIT, AUTHORITY_ADMIN_ONE_RPA_INSTANCE_VIEW, AUTHORITY_ADMIN_ONE_STORE_INSTANCE_EDIT, AUTHORITY_ADMIN_ONE_STORE_INSTANCE_VIEW, AUTHORITY_ADMIN_UI_BUNDLE_DEPLOY, AUTHORITY_ADMIN_UI_BUNDLE_EDIT, AUTHORITY_ADMIN_UI_BUNDLE_VIEW, AUTHORITY_ADMIN_USER_VIEW, AUTHORITY_ADMIN_VIEW, AUTHORITY_AUTO_DEPLOY_KNOWLEDGE, AUTHORITY_CONTENT_PACK_INSTALL, AUTHORITY_CONVERSATION_SUMMARY_CLEANUP, AUTHORITY_MISCLASSIFICATION_ANNOTATION, AUTHORITY_RESPONSE_POOL_EDIT, AUTHORITY_RESPONSE_POOL_VIEW, AUTHORITY_USER |
| AUTHORITY_ACTIVE_CONVERSATION_VIEW, AUTHORITY_CONVERSATION_OBSERVE, AUTHORITY_CONVERSATION_PICKUP, AUTHORITY_CONVERSATION_TRANSFER, AUTHORITY_JOURNEY_VIEW, AUTHORITY_USER |
| AUTHORITY_ACTIVE_CONVERSATION_VIEW, AUTHORITY_ADMIN_ESCALATION_QUEUE_EDIT, AUTHORITY_ADMIN_ESCALATION_QUEUE_VIEW, AUTHORITY_ADMIN_ESCALATION_TEAM_EDIT, AUTHORITY_ADMIN_ESCALATION_TEAM_VIEW, AUTHORITY_CONVERSATION_ASSIGN, AUTHORITY_CONVERSATION_OBSERVE, AUTHORITY_CONVERSATION_PICKUP, AUTHORITY_JOURNEY_VIEW, AUTHORITY_SUPERVISOR_VIEW, AUTHORITY_USER |
| AUTHORITY_CONVERSATION_START, AUTHORITY_RUN_THE_WORKFLOW, AUTHORITY_USER |
| AUTHORITY_ADMIN_INTEGRATION_DEPLOY, AUTHORITY_ADMIN_INTEGRATION_EDIT, AUTHORITY_ADMIN_INTEGRATION_TEMPLATE_EDIT, AUTHORITY_ADMIN_INTEGRATION_TEMPLATE_VIEW, AUTHORITY_ADMIN_INTEGRATION_VIEW |
| AUTHORITY_ACTIVE_CONVERSATION_VIEW, AUTHORITY_ADMIN_AIML_DOCUMENT_DELETE, AUTHORITY_ADMIN_AIML_DOCUMENT_EDIT,;AUTHORITY_ACTIVE_CONVERSATION_VIEW, AUTHORITY_ADMIN_AIML_DOCUMENT_DELETE, AUTHORITY_ADMIN_AIML_DOCUMENT_EDIT, AUTHORITY_ADMIN_AIML_DOCUMENT_VIEW, AUTHORITY_ADMIN_BPN_DEPLOY, AUTHORITY_ADMIN_BPN_EDIT, AUTHORITY_ADMIN_BPN_VIEW, AUTHORITY_ADMIN_CONTENT_MANAGEMENT_DELETE, AUTHORITY_ADMIN_CONTENT_MANAGEMENT_EDIT, AUTHORITY_ADMIN_CONTENT_MANAGEMENT_VIEW, AUTHORITY_ADMIN_DOMAIN_VIEW, AUTHORITY_ADMIN_SEMNET_CONFIG_EDIT, AUTHORITY_ADMIN_SEMNET_DOCUMENT_DELETE, AUTHORITY_ADMIN_SEMNET_DOCUMENT_EDIT, AUTHORITY_ADMIN_SEMNET_DOCUMENT_VIEW, AUTHORITY_ADMIN_SEMNET_TRANSDUCER_EDIT, AUTHORITY_ADMIN_VIEW, AUTHORITY_CONVERSATION_EXPORT, AUTHORITY_CONVERSATION_OBSERVE, AUTHORITY_CONVERSATION_START, AUTHORITY_JOURNEY_VIEW, AUTHORITY_METRICS_VIEW, AUTHORITY_MISCLASSIFICATION_ANNOTATION, AUTHORITY_RESPONSE_POOL_EDIT, AUTHORITY_RESPONSE_POOL_VIEW, AUTHORITY_RUN_THE_WORKFLOW, AUTHORITY_TABULAR_ADD, AUTHORITY_TABULAR_EDIT, AUTHORITY_TABULAR_VIEW, AUTHORITY_TRAINING_EDIT, AUTHORITY_TRAINING_REAL_CONVERSATION, AUTHORITY_TRAINING_TEST, AUTHORITY_TRAINING_TRAIN, AUTHORITY_TRAINING_VIEW, AUTHORITY_USER |
| AUTHORITY_ACTIVE_CONVERSATION_VIEW, AUTHORITY_ADMIN_BPN_VIEW, AUTHORITY_ADMIN_DOMAIN_VIEW, AUTHORITY_ADMIN_VIEW, AUTHORITY_CONVERSATION_EXPORT, AUTHORITY_CONVERSATION_OBSERVE, AUTHORITY_CONVERSATION_START, AUTHORITY_JOURNEY_VIEW, AUTHORITY_METRICS_VIEW, AUTHORITY_MIND3D_VIEW, AUTHORITY_MIND_VIEW, AUTHORITY_RESPONSE_POOL_VIEW, AUTHORITY_RUN_THE_WORKFLOW, AUTHORITY_USER |
| AUTHORITY_ADMIN_RBAC, AUTHORITY_ADMIN_USER_EDIT, AUTHORITY_ADMIN_USER_VIEW, AUTHORITY_ADMIN_VIEW, AUTHORITY_USER |

## User Groups
User groups in Amelia are the intersection of Users, Roles, Domains, and Authorities.  Groups have the following configurable properties:
Table. Configurable Properties for Groups

| Group Property | Description |
| ----|----|
| Domain | The domain for this group. |
| Name | Name of the group |
| Global | Whether this is a global group |
| Users | Users directly in this group |
| Member Groups | Groups included within this group. Users in these member groups are considered members of this group. |
| Roles | The roles associated with this group. |
| Authorities | Extra authorities granted by this group in addition to those granted by associated roles (if any). |

A group must either be global or have a domain associated with it.  A global group grants authorities to all domains.  A group with a domain associated grants authorities for that specific domain only.
Upon logging into Amelia, a user's authorities are calculated as follows:
1.  Define DA as the domain authorities for the user (initially empty).
2.  Define GA as the global authorities for the user (initially empty).
3.  Find all groups (GM) where the user is a direct member.
4.  For each group (G) in GM
    1.  Let A be all authorities associated directly with G and all authorities from roles directly associated with G.
    2.  If G is a global group, add A to GA.
    3.  If G is a domain group, add A to DA for the domain associated with G.
    4.  For each group where G is a member group, repeat from 4a (recursively process).
Amelia comes pre-configured with the following groups:
Table. Amelia's Pre-Configured Groups

| Name | Global | Domain | Roles | Users | Member Groups | Authorities |
| ----|----|----|----|----|----|----|
| Global Administrators | yes | none | Administrator | admin@ipsoft.com | none | none |
| Global Agents | yes | none | Agent | none | none | none |
| Global Agent Supervisors | yes | none | Agent Supervisor | none | none | none |
| Global End Users | yes | none | End Users | none | none | none |
| Global Integration Designers | yes | none | Integration Designer | none | none | none |
| Global Knowledge Designers | yes | none | Knowledge Designer | none | none | none |
| Global Knowledge Reviewers | yes | none | Knowledge Reviewers | none | none | none |
| Global Power Users | yes | none | Power User | none | none | none |
| Global RBAC Administrators | yes | none | RBAC Administrator | admin@ipsoft.com | none | none |

# Spring Security Framework
Amelia uses Spring Security (4.0.X) as its underlying security framework.  Spring security is a mature, battle-tested, Java based security framework.  To the greatest extent possible, Amelia utilizes all security features provided by this framework.
## Attachments:
![](images/icons/bullet_blue.gif) [image2017-3-24 16:26:8.png](attachments/11940292/11940293.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-3-24 16:26:24.png](attachments/11940292/11940294.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-3-24 16:26:35.png](attachments/11940292/11940295.png) (image/png)  
