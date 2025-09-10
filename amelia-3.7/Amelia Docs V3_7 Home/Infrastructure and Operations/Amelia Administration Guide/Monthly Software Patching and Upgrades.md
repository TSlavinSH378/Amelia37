To ensure that our systems are compliant and not vulnerable against threats, regular security patches will be deployed to all hosts in the same windows as standard product upgrades (for version compatibility). This will occur in two parts based upon the type of deployment, i.e., shared vs dedicated to ensure that the application downtime is kept to a minimum
For any client-hosted hosts/products, we shall provide training to customers to use our available playbooks for stopping/starting our applications, and will be available on stand-by in case of any issues. To accomplish this, clients would be required to share the patch details with us for validation, and any exceptions we would need to consider to ensure that the application downtime is kept to a minimum.
# Amelia Platform Upgrades - SaaS
Table. SaaS Amelia Platform Upgrade Details

|  |  |  |  |
| ----|----|----|----|
| Type of Update | Description | Non-Production (Dev/Stg/QA) | Production |
| Monthly Updates | Non-breaking updates that provide minor feature improvements, fixes for security related items, or minor fixes to address existing issues.; | Upgrades will be performed on the designated day (see below) of each month. Customers will have two weeks to test their workflows and integrations in their non-production environments.These upgrades are done in-place to non-production domains / virtual hosts and will only be reverted if there is a major issue encountered.; Minor issues will be addressed via hot-fixes which will be rolled into the next monthly release | Production will be upgraded two weeks after the designated upgrade day (see below).Once testing has completed, the upgrade is carried out on production instances and rolled back only in the case of major incident.; Standard polices include taking snapshots and backups of instance before upgrades occur. A rollback would incur larger downtime than usual, as it would need a full restoration from backups and time required for it would be based upon the size of the backup. |

# Upgrade/Patch
At the time of an upgrade, we will also apply any required security patches for the month against the instances. The time required for an upgrade + patches might vary and an expected downtime of maximum 2 hours would be taken into consideration for any reboot should that be required which if not, the downtime of 15 minutes at time of upgrade would be applicable. Please do note that there may not always be major security patche required to be applied, therefore a system reboot may not be always necessary.
Table. Upgrade/Patch Details by Location and Dates
|                       |          |                                    |                                    |                                       |                             |
|:----------------------|:---------|:-----------------------------------|:-----------------------------------|:--------------------------------------|:----------------------------|
| **Instance Location** | **Slot** | **Non-Production (Dev Instances)** | **Non-Production (Dev Instances)** | **Non-Production (Stg/QA Instances)** | **Production **             |
| US                    | Batch A  | First Wednesday of the Month       | Second Wednesday of the Month      | Third Wednesday of the Month          | Last Wednesday of the month |
|                       | Batch B  | First Thursday of the Month        | Second Thursday of the Month       | Third Wednesday of the Month          | Last Thursday of the month  |
| Europe                | Batch A  | First Wednesday of the Month       | Second Wednesday of the Month      | Third Wednesday of the Month          | Last Wednesday of the month |
|                       | Batch B  | First Thursday of the Month        | Second Thursday of the Month       | Third Wednesday of the Month          | Last Thursday of the month  |
| APAC                  | Batch A  | First Wednesday of the Month       | Second Wednesday of the Month      | Third Wednesday of the Month          | Last Thursday of the month  |
|                       | Batch B  | First Thursday of the Month        | Second Thursday of the Month       | Third Wednesday of the Month          | Last Thursday of the month  |
> [!warning]  
>
> Please note that, if there are any issues noticed with the first upgrade window – for example, any bugs found, a patch would be released against same and it would be applied on either the upcoming Monday or Thursday at same time windows mentioned below based upon how soon the bugs are fixed and a release made available.

Table. Upgrade/Patch Details by Software Product

|  |  |  |
| ----|----|----|
| Product | Time Slot 1 (US/LATAM) | Time Slot 2 (EU/APAC/Aus) |
| Amelia (V5)/Orchestrator/AIOps | 07:30 AM UTC / 2:30 AM EST | 7:30 PM UTC / 2:30 PM EST |
| 1Desk | 08:00 AM UTC / 3:00 AM EST | 1:30 PM UTC / 8:30 AM EST |
| 1RPA | 07:30 AM UTC / 2:30 AM EST | 2:00 PM UTC / 9:00 AM EST |
| Amelia (V3/V4) | 08:30 AM UTC / 3:30 AM EST | 2:30 PM UTC / 9:30 AM EST |

> [!warning]  
>
> UTC offset varies during the year due to time zone and clock changes, for example, US Daylight Savings Time. The current UTC offset for New York City is -4 hours during Daylight Savings Time and -5 hours during standard time. The Bangalore UTC offset is +5.5 hours, the United Kingdom is on UTC time, and a +1 hour UTC offset is used in Munich, Amsterdam, and Sweden. Please confirm the current UTC offset by searching online.

# Amelia Dedicated SaaS Instances
Customers with dedicated SaaS instances will be required to upgrade at least every quarter, to ensure software currency.  This is to address not only features and fixes, but also to ensure the security and integrity of the system. These instances will be managed through the respective EM/PM for the customer.  We will ensure that a Jira "CI" ticket is created for patches/security updates every month (for tracking/audit/compliance purposes), after confirming the date/time from the customer for downtime.  The same process will be used for product upgrades (both minor and major), either monthly or every 45 days - though it is mandatory to ensure that the latest version is available on an instance at the end of every quarter, to avoid issues with the product platform, as well as having features/fixes in place.
As for patching, we would need CI ticket opened every month with the date/time client would have chosen for us to apply security patches against the host OS. This is mandatory and not to be missed.
# Integration Notes
If you use the Amelia Integration Services Client (ISC) for integration, or Automata Lite (ALite) for automations, the updated client version should be upgraded and configured (if required) to ensure your version is compatibile with the core version of the platform. This is the responsibility of the EM/PM, to have the SA validate, based upon the release notes details to work with their clients and schedule, as needed.
# Emergency Changes
Please note that Emergency Changes or Upgrades may be required to address the stability or security of the product platform.  When this occurs, Amelia, LLC will provide as much notice as commercially and technically possible to our customers, informing them of the change. 
# Upgrade Types
It is to be noted that there are two types of Upgrade that would be considered for the auto-deploy windows and following explains the same with respect to version control.
-   Minor Upgrade
-   Major Upgrade
# Delivery Workflow – Mandatory Action Post Patching & Upgrade
-   Each client PM/EM/CPL will ensure that they keep their clients aware of the patching windows, and choose from the available slots indicated
-   If a change in the window is required, inform STech through a CI ticket, at least one week in advance
-   QA each instance post-patching to ensure no feature/functionality is broken, and report back if any concerns
