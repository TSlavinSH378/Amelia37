In the SAML2 case, support is provided by Spring Security SAML
-   [Amelia High Level Architecture Design](#NOTUSEDAmeliaV3PlatformDesign-AmeliaHighLevelArchitectureDesign)
    -   [3-Node Cluster Architecture](#NOTUSEDAmeliaV3PlatformDesign-3-NodeClusterArchitecture)
    -   [6-Node Cluster Architecture](#NOTUSEDAmeliaV3PlatformDesign-6-NodeClusterArchitecture)
    -   [High Availability Architecture](#NOTUSEDAmeliaV3PlatformDesign-HighAvailabilityArchitecture)
    -   [Single Node Architecture](#NOTUSEDAmeliaV3PlatformDesign-SingleNodeArchitecture)
-   [Deployment Models](#NOTUSEDAmeliaV3PlatformDesign-DeploymentModels)
    -   [Amelia Hosted in IPsoft’s Cloud](#NOTUSEDAmeliaV3PlatformDesign-AmeliaHostedinIPsoft’sCloud)
    -   [Customer Premise / Cloud](#NOTUSEDAmeliaV3PlatformDesign-CustomerPremise/Cloud)
    -   [Online Deployment](#NOTUSEDAmeliaV3PlatformDesign-OnlineDeployment)
    -   [Offline Deployment Infrastructure Specifications](#NOTUSEDAmeliaV3PlatformDesign-OfflineDeploymentInfrastructureSpecifications)
-   [Hardware/Resource Recommendations](#NOTUSEDAmeliaV3PlatformDesign-Hardware/ResourceRecommendations)
    -   [CPU Requirements](#NOTUSEDAmeliaV3PlatformDesign-CPURequirements)
    -   [Storage Requirements](#NOTUSEDAmeliaV3PlatformDesign-StorageRequirements)
    -   [Disk IO](#NOTUSEDAmeliaV3PlatformDesign-DiskIO)
    -   [Clustered Setup](#NOTUSEDAmeliaV3PlatformDesign-ClusteredSetup)
    -   [Conversation Pods](#NOTUSEDAmeliaV3PlatformDesign-ConversationPods)
    -   [Single Host](#NOTUSEDAmeliaV3PlatformDesign-SingleHost)
    -   [VMware Oversubscription](#NOTUSEDAmeliaV3PlatformDesign-VMwareOversubscription)
    -   [VMware DRS Requirements](#NOTUSEDAmeliaV3PlatformDesign-VMwareDRSRequirements)
    -   [vMotion Requirements](#NOTUSEDAmeliaV3PlatformDesign-vMotionRequirements)
    -   [Memory Ballooning](#NOTUSEDAmeliaV3PlatformDesign-MemoryBallooning)
-   [Components of Amelia](#NOTUSEDAmeliaV3PlatformDesign-ComponentsofAmelia)
    -   [Operating System Requirements](#NOTUSEDAmeliaV3PlatformDesign-OperatingSystemRequirements)
    -   [External Load Balancers](#NOTUSEDAmeliaV3PlatformDesign-ExternalLoadBalancers)
    -   [HAProxy](#NOTUSEDAmeliaV3PlatformDesign-HAProxy)
    -   [MySQL / Percona XtraDB Cluster (PXC)](#NOTUSEDAmeliaV3PlatformDesign-MySQL/PerconaXtraDBCluster(PXC))
    -   [RabbitMQ](#NOTUSEDAmeliaV3PlatformDesign-RabbitMQ)
    -   [Redis Sentinel](#NOTUSEDAmeliaV3PlatformDesign-RedisSentinel)
    -   [Amelia Daemons](#NOTUSEDAmeliaV3PlatformDesign-AmeliaDaemons)
        -   [Amelia-Web](#NOTUSEDAmeliaV3PlatformDesign-Amelia-Web)
        -   [User Web](#NOTUSEDAmeliaV3PlatformDesign-UserWeb)
        -   [Engine Service](#NOTUSEDAmeliaV3PlatformDesign-EngineService)
        -   [Batch Service](#NOTUSEDAmeliaV3PlatformDesign-BatchService)
        -   [Escalation Service](#NOTUSEDAmeliaV3PlatformDesign-EscalationService)
        -   [Integration Service](#NOTUSEDAmeliaV3PlatformDesign-IntegrationService)
        -   [Duckling Service](#NOTUSEDAmeliaV3PlatformDesign-DucklingService)
    -   [Text to Speech (TTS)](#NOTUSEDAmeliaV3PlatformDesign-TexttoSpeech(TTS))
-   [Chat Integration](#NOTUSEDAmeliaV3PlatformDesign-ChatIntegration)
-   [Security](#NOTUSEDAmeliaV3PlatformDesign-Security)
    -   [Authentication Systems](#NOTUSEDAmeliaV3PlatformDesign-AuthenticationSystems)
        -   [Local Authentication](#NOTUSEDAmeliaV3PlatformDesign-LocalAuthentication)
        -   [LDAP / Active Directory (AD)](#NOTUSEDAmeliaV3PlatformDesign-LDAP/ActiveDirectory(AD))
        -   [Deny All](#NOTUSEDAmeliaV3PlatformDesign-DenyAll)
        -   [SAML 2](#NOTUSEDAmeliaV3PlatformDesign-SAML2)
            -   [Service Provider Initiated Authentication](#NOTUSEDAmeliaV3PlatformDesign-ServiceProviderInitiatedAuthentication)
            -   [Identity Provider Initiated Authentication](#NOTUSEDAmeliaV3PlatformDesign-IdentityProviderInitiatedAuthentication)
    -   [Anonymous Access](#NOTUSEDAmeliaV3PlatformDesign-AnonymousAccess)
    -   [SSL Certificates](#NOTUSEDAmeliaV3PlatformDesign-SSLCertificates)
    -   [Firewall Rules](#NOTUSEDAmeliaV3PlatformDesign-FirewallRules)
-   [Monitoring](#NOTUSEDAmeliaV3PlatformDesign-Monitoring)
-   [Backups](#NOTUSEDAmeliaV3PlatformDesign-Backups)
-   [Disaster Recovery](#NOTUSEDAmeliaV3PlatformDesign-DisasterRecovery)
-   [High Availability Configurations](#NOTUSEDAmeliaV3PlatformDesign-HighAvailabilityConfigurations)
    -   [Front End Services](#NOTUSEDAmeliaV3PlatformDesign-FrontEndServices)
    -   [Admin POD](#NOTUSEDAmeliaV3PlatformDesign-AdminPOD)
    -   [RabbitMQ Hosts](#NOTUSEDAmeliaV3PlatformDesign-RabbitMQHosts)
    -   [Conversation POD](#NOTUSEDAmeliaV3PlatformDesign-ConversationPOD)
    -   [General Notes about Hardware/Resource Recommendations](#NOTUSEDAmeliaV3PlatformDesign-GeneralNotesaboutHardware/ResourceRecommendations)
        -   [CPU](#NOTUSEDAmeliaV3PlatformDesign-CPU)
        -   [Disk](#NOTUSEDAmeliaV3PlatformDesign-Disk)
        -   [VMware](#NOTUSEDAmeliaV3PlatformDesign-VMware)
        -   [OS](#NOTUSEDAmeliaV3PlatformDesign-OS)
    -   [Scaling Amelia Components](#NOTUSEDAmeliaV3PlatformDesign-ScalingAmeliaComponents)
        -   [Databases](#NOTUSEDAmeliaV3PlatformDesign-Databases)
            -   [Scaling ADB and KDB](#NOTUSEDAmeliaV3PlatformDesign-ScalingADBandKDB)
            -   [Scaling CDB](#NOTUSEDAmeliaV3PlatformDesign-ScalingCDB)
            -   [Alternate CDB Design (Not recommended)](#NOTUSEDAmeliaV3PlatformDesign-AlternateCDBDesign(Notrecommended))
        -   [Rabbit MQ](#NOTUSEDAmeliaV3PlatformDesign-RabbitMQ.1)
        -   [Integration Services](#NOTUSEDAmeliaV3PlatformDesign-IntegrationServices)
> [!warning]  
>
> Content is hidden from GA per MikeG 11/3/2023. Content is outdated and/or not relevant to SaaS clients. 
> [!warning]  
>
> This document also is available in [PDF format](attachments/11940325/28476216.pdf).

# Amelia High Level Architecture Design
Amelia is the artificial intelligence platform that can understand, learn and interact as a human would to solve problems. Amelia reads natural language, understands context, applies logic, infers implications, learns through experience and even senses emotions. The diagrams below illustrate Amelia’s architecture..
Amelia V3 is designed with multiple shared services, including but not limiting to Administrative Services, Conversation Engine Pods, Integration Services, and a Database Shard Architecture.   The concept for this design is to separate very large JVMs, databases, daemons into smaller, faster, more easily managed fragments.  The below diagrams show the service architecture and data flow overviews of Amelia V3:
![](attachments/11940325/20808617.jpeg)
Figure: Service Architecture Diagram
The below sections will describe the infrastructure requirements and necessary components of Amelia V3.  Some hosts will have multiple middleware components to support Amelia and her functions.  Amelia supports clustering both for scaling and high availability.  It is recommended that all production environments be clustered with three Application servers and three Database servers.  When configured with clustering, there are no single points of failure within Amelia; any failure of a single component should at most result in a few seconds of intermittent faults.  Amelia V3 is only supported on LANs and where network split-brain between nodes is very unlikely. In the event of a network split-brain event, manual intervention may be required and data in-flight may be lost.
## 3-Node Cluster Architecture
IPsoft’s standard deployment model, a best practice, consists of three identical servers (see Figure 1).. When clustered, there are no single points of failure within Amelia and a failure of any single component should at most incur a few seconds of intermittent errors.
![](attachments/11940325/11940344.png)
Figure: Initial 3-Node Cluster Environment Diagram
> [!warning]  
>
> Connection options — for example, to IPcenter, LDAP/SSO/SAML2, or other technology — should be discussed with IPsoft in the planning process. 

## 6-Node Cluster Architecture
This configuration splits the application and database services into two network tiers.  As Amelia V3 uses a sharding/multiple shared services architecture, the various application and database services can be further split off into additional servers to provide separation of service requirements and for large volume use cases.
![](attachments/11940325/11940343.png)
Figure: 6-Node Cluster Environment Diagram
> [!warning]  
>
> Connection options — for example, to IPcenter, LDAP/SSO/SAML2, or other technology — should be discussed with IPsoft in the planning process.

## High Availability Architecture
Refer to the [High Availability Configuration](#NOTUSEDAmeliaV3PlatformDesign-HighAvailability) section below for more details about this configuration.
![](attachments/11940325/25462780.png)
Figure. Amelia Architecture Scaled for 1200 Concurrent Conversations
## Single Node Architecture
Amelia also supports single host architectures. Single-host configurations are meant for POC/Dev environments. 
![](attachments/11940325/11940342.png)
Figure: 1-Node Cluster Environment Diagram
> [!warning]  
>
> Connection options — for example, to IPcenter, LDAP/SSO/SAML2, or other technology — should be discussed with IPsoft in the planning process.

# Deployment Models
Amelia can be delivered in several deployment models, depending on customer/partner requirements. On-Premise deployments may require encrypted network connectivity between IPsoft and the clients/partners environments for installation of Amelia V3. Interconnectivity can be accomplished with dedicated communication circuits and/or site to site Virtual Private Network (“VPN”) tunnels across the public Internet.
IPsoft has developed a self-contained tool called Amelia Deployment Center (ADC) for deployment and configuration of Amelia V3 for remote servers to install Amelia on RHEL 7 family servers, which is used to automate and organize system configuration tasks.
## Amelia Hosted in IPsoft’s Cloud
Amelia can be hosted at IPsoft’s datacenters worldwide in IPsoft’s New York Metro and Amsterdam datacenters. In this model, IPsoft assumes all responsibility for deployment and scaling of Amelia for given clients and partners. This deployment will utilize IPsoft’s current hardware comprised of Dell servers, Compellent storage, VMware, and Cisco/Arista networking.
For security purposes, backend technologies and any integrations with Amelia are interconnected utilizing a secure delivery network, typically an IPsec VPN and/or MPLS.
![](attachments/11940325/11940341.png)
Figure. Amelia Hosted in IPsoft’s Cloud with IPsec VPN Tunnels
![](attachments/11940325/11940340.png)
Figure. Amelia Hosted in IPsoft’s Cloud
This figure shows a conceptual view of how clients and servers are communicating with Amelia in IPsoft-hosted environment.
## Customer Premise / Cloud
Amelia can also be deployed within a client’s/partner’s facilities, without IPsoft managing the hardware and network infrastructure. This type of deployment requires the involvement of Client/Partner Architects and IPsoft’s Service Design resources to develop a joint architecture for connectivity and sizing.
![](attachments/11940325/11940339.png)
Figure. Amelia Hosted in Customer’s Cloud
> [!warning]  
>
> Connection options — for example, to IPcenter, LDAP/SSO/SAML2, or other technology — should be discussed with IPsoft in the planning process.

## Online Deployment
With remote connectivity enabled, IPsoft will use ADC to deploy Amelia to automate the installation of Amelia and her dependencies.  Please refer to IPsoft’s Amelia Deployment Center (ADC) Guide for in-depth information.
The deployment and release of Amelia to remote server(s) is managed by IPsoft’s implementation of ADC.  Using job templates and ADC mechanism, IPsoft can show progress and monitor the status of Amelia being deployed.
Deployments in the public cloud (such as AWS/Azure) are considered on-premise deployments, as the roles and responsibility of the infrastructure is owned by the client/partner. IPsoft has done extensive testing within AWS for all support Operating Systems as described below in Section 3.1
At a minimum, each server should be deployed using the r4.4xlarge sizing; this does not include a backup partition if that is required. Client is responsible for any Elastic Load Balancing configuration and any OS/network security aspects.
As of this writing, Amelia is not supported using containers, for example, Docker.
## Offline Deployment Infrastructure Specifications
At times, remote connectivity will not be possible between IPsoft and client/partner for deployment of Amelia on remote server(s). IPsoft refers the lack of a persistent connection as an Offline Instances. IPsoft will continue to use ADC for deployments and the initialization of all playbooks will be maintained on the server(s) locally within the client’s/partner’s network.
For offline deployments, IPsoft can only provide specific SLAs based on available connectivity and access.
If considering an Offline deployment of Amelia, topics of discussion should include but are not limited to:
-   Backups – How are they performed? Schedule?
-   Monitoring – OS, Middleware, Amelia, Web Checks
-   Administration – Engineer access to Operating System
-   Upgrades – OS, Amelia
-   Support – Break/Fix, Root level access
-   Deployment Timeline– Procurement of servers/load balancers and/or access limitations
For offline deployments with a pre-existing IPcenter instance, contact IPsoft to discuss options.
# Hardware/Resource Recommendations
For deployments of Amelia on premise /cloud, there are several recommendations and requirements, depending on the type(s) of use cases and volume for each use case.  Amelia can be scaled up/out by increasing the number of CPUs, RAM, and disk capacity as well the number of Conversation PODs .  If Amelia is configured as a single node, It cannot be scaled-out with additional nodes.
Amelia deployments are supported in both physical and virtual environments.  For virtual deployments, it is recommended to enable Memory and Disk reservations for best performance; especially in highly utilized shared infrastructure. 
## CPU Requirements
Amelia does not perform well in virtual infrastructures with Memory ballooning and/or CPU scheduling issues.  Virtual machines (VMs) depend on available host resources (CPU, Memory), and the guest operating system consumes those resources. A problem with resource availability or scheduling inside or outside the virtual machine may cause it to become unresponsive.
Reviewing CPU performance metrics can be used to determine whether a guest operating system is actually running, whether the virtual machine monitor (VMM) is running, or whether there is scheduling contention.  The metrics is also leveraging insight into the responsiveness of a virtual machine or its Guest OS:
-   Run - Amount of time the virtual machine is consuming CPU resources.
-   Wait - Amount of time the virtual machine is waiting for a VMkernel resource.
-   Ready - Amount of time the virtual machine was ready to run, waiting in a queue to be scheduled.
-   Co-Stop - Amount of time a SMP virtual machine was ready to run, but incurred delay due to co-vCPU scheduling contention.
It is recommended Memory/CPU Hotplug is enabled to increase CPUs/RAM at any time to scale quickly.  Be mindful of the hardware configuration and NUMA settings, it is optimal for Amelia to access CPU/Memory resources on the same NUMA node.
Amelia should be utilizing at a minimum dual Intel® Xeon® Processor E5-2687W v3 (25M Cache, 3.10 GHz).
These are preferred processors, from newest to oldest.
Table. Preferred Processors
|                                                                                                                                                                   |       |         |                |                     |                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|---------|----------------|---------------------|------------------|
| Product Line/Processor Name                                                                                                                                       | Cores | Threads | Base Frequency | Max Turbo Frequency | Cache            |
| **Intel 2nd Gen Scalable Processors**                                                                                                                             |       |         |                |                     |                  |
| [Intel® Xeon® Gold 6246 Processor](https://ark.intel.com/content/www/us/en/ark/products/193969/intel-xeon-gold-6246-processor-24-75m-cache-3-30-ghz.html)         | 12    | 24      | 3.30 GHz       | 4.20 GHz            | 24.75 MB         |
| [Intel® Xeon® Gold 6242 Processor](https://ark.intel.com/content/www/us/en/ark/products/192440/intel-xeon-gold-6242-processor-22m-cache-2-80-ghz.html)            | 16    | 32      | 2.80 GHz       | 3.90 GHz            | 22 MB            |
| [Intel® Xeon® Platinum 8268 Processor](https://ark.intel.com/content/www/us/en/ark/products/192481/intel-xeon-platinum-8268-processor-35-75m-cache-2-90-ghz.html) | 24    | 48      | 2.90 GHz       | 3.90 GHz            | 35.75 MB         |
| **Intel Scalable Processors**                                                                                                                                     |       |         |                |                     |                  |
| [Intel® Xeon® Gold 6136 Processor](https://ark.intel.com/content/www/us/en/ark/products/120479/intel-xeon-gold-6136-processor-24-75m-cache-3-00-ghz.html)         | 12    | 24      | 3.00 GHz       | 3.70 GHz            | 24.75 MB L3      |
| [Intel® Xeon® Gold 6142 Processor](https://ark.intel.com/content/www/us/en/ark/products/120487/intel-xeon-gold-6142-processor-22m-cache-2-60-ghz.html)            | 16    | 32      | 2.60 GHz       | 3.70 GHz            | 22 MB L3         |
| [Intel® Xeon® Platinum 8158 Processor](https://ark.intel.com/content/www/us/en/ark/products/120500/intel-xeon-platinum-8158-processor-24-75m-cache-3-00-ghz.html) | 12    | 24      | 3.00 GHz       | 3.70 GHz            | 24.75 MB L3      |
| **Intel E5 V4 Processors**                                                                                                                                        |       |         |                |                     |                  |
| [Intel® Xeon® Processor E5-2687W v4](https://ark.intel.com/content/www/us/en/ark/products/91750/intel-xeon-processor-e5-2687w-v4-30m-cache-3-00-ghz.html)         | 12    | 24      | 3.00 GHz       | 3.50 GHz            | 30 MB SmartCache |
## Storage Requirements
Amelia’s response time (latency) is important for the user’s experience , handling of high concurrent connections, and scalability.  Amelia requires a low latency and high throughput storage tier.  IPsoft highly recommends using Solid State Drives (SSDs) for primary storage for all Amelia Servers.  SAS/SATA Storage can be used for backups if desired.
Customers and Partners can leverage existing storage platforms that are installed with SSDs.  Both All-Flash-Arrays and hybrid (SSDs and Spinning Disks) are viable solutions, taking into account the initial write lands on SSD storage tier.
Amelia’s databases and PODs require at minimum 10,000 IOPS, 15,000 to 20,0000 for larger deployments.
## Disk IO
Each VM must be able to sustain 1000 Read and 1000 Writes IOPS at \<10ms latency.
## Clustered Setup
For Production/DR deployments, it is highly recommended to deploy a clustered setup for high availability and scaling for performance, Amelia can be deployed on physical or virtual servers. As of this writing, the following are guidelines on the infrastructure requirements for a clustered Production/DR deployment. These requirements are for each server.
Table. 3-Node Clustered Setup Environment Resource Requirements

| 
 | Specifications per Host | 
 | Tier | CPU* |
| ----|----|----|----|----|
| Apps | 16 | 80 | 512 (not including OS) | 3 |
| TOTALS | 48 | 240 | 1.6TB | 3 |

\*Based on underlying server’s NUMA settings, multiple sockets may be suggested  
\*\*Additional RAM may be required for language pack support & gateways (2GB RAM/10 GB disk capacity for each pack)  
\*\*\*/apps is the required mount point; LVM and/or XFS file system is highly recommended. Slower disks can be utilized if slow performance is acceptable. Please see notes below regarding proper disk capacity sizing.
> [!warning]  
>
> The above table are requirements for each node of the cluster.

Table. 6-Node Clustered Production Environment Resource Requirements

| 
 | Specifications per Host | 
 | Tier | CPU* |
| ----|----|----|----|----|
| Apps | 12 | 64 | 300 | 3 |
| Database | 8 | 24 | 1024 (not including OS) | 3 |
| TOTALS | 60 | 264 | 3.88TB | 6 |

\*Based on underlying server’s NUMA settings, multiple sockets may be suggested  
\*\*Additional RAM may be required for language pack support & gateways (2GB RAM/10 GB disk capacity for each pack)  
\*\*\*/apps is the required mount point; LVM and/or XFS file system is highly recommended. Slower disks can be utilized if slow performance is acceptable. Please see notes below regarding proper disk capacity sizing.
> [!warning]  
>
> Clustering is only supported on LANs and where network split-brain between nodes is very unlikely. In the event of a network split-brain event, manual intervention may be required and data in-flight may be lost.
>
> Database sizes for both 3-node and 6-node clusters depends on the following:
>
> -   Data Retention Requirements/Compliance
> -   Local Database Backup(s)
> -   Use Cases
> -   Number of Conversation Pods

## Conversation Pods
Conversation Pods are used for additional capacity for higher concurrent conversations.  Conversation Pods are deployed in batches of 3 VMs to handle an additional 150 concurrent conversations.  There currently is no limit on the number of Pods that can be deployed with Amelia.  For deployments with high peaks, it is recommended to configure Amelia with the necessary sizing for those peaks and scale down if desired.
Table. Conversation POD Setup Environment Resource Requirements

| 
 | Specifications per Host | 
 | Tier | CPU* |
| ----|----|----|----|----|
| POD Node | 8 | 40 | 100 (not including OS) | 3 |
| TOTALS | 24 | 96 | 300 GB | 3 |

## Single Host
For deployments of Proof-of-Concepts, Development, User Acceptance Testing (UAT), and some limited Production environments, Amelia can be deployed on a single physical or virtual server. As of this writing, the following are guidelines on the infrastructure requirements for a single host deployment
Table. Single Host Environment Resource Requirements

| Resource | Quantity | Notes |
| ----|----|----|
| CPUs | 16 | Based on underlying server’s NUMA settings, multiple sockets may be suggested |
| RAM** | 80 GB |  |
| Disk Capacity | 300 GB | /apps is the required mount; LVM and/or XFS file system is highly recommended. Slower disks can be utilized if slow performance is acceptable. |

\*\*Additional RAM may be required for language pack support & gateways (2GB each pack)
## VMware Oversubscription
Do not oversubscribe CPUs and memory. One vCPU equals one Hyperthread.
## VMware DRS Requirements
VMware DRS (Distributed Resource Scheduler) is a utility that balances computing workloads with available resources in a virtualized environment.  With VMware DRS, users can define rules for the allocation of physical resources and placement among virtual machines. The utility can be configured for manual or automatic control. Resource pools can be easily added, removed or reorganized. If desired, resource pools can be isolated between different business units. If the workload on one or more virtual machines drastically changes, VMware DRS redistributes the virtual machines among the physical servers.
IPsoft recommends creating a DRS rule to separate Amelia VMs to ensure the VMs are not running on the same physical server.
## vMotion Requirements
VMware vMotion enables the live migration of running virtual machines from one physical server to another with zero downtime, continuous service availability, and complete transaction integrity. It is transparent to users.
Amelia virtual servers typically require significant amounts of RAM so it is recommended to have network connectivity between VMWare Hosts of at least 10Gbps to achieve successful migrations using vMotion.
## Memory Ballooning
Virtual memory ballooning is a memory reclamation technique used by a hypervisor in an attempt for the physical host system to retrieve unused memory from guest virtual machines (VMs) and share reallocate to others. Memory ballooning allows the total amount of RAM required by guest VMs to exceed the amount of physical RAM available on the host. When the host system runs low on physical RAM resources, memory ballooning allocates it selectively to VMs.
Using this technique would negatively impact Amelia’s performance and it should be avoided.
# Components of Amelia
An Amelia instance includes database, message transport, load balancers, and other components, as well as escalation and other processes and systems to set up.
## Operating System Requirements
Amelia is a Linux based Application and can be deployed onto a RHEL 7-family OS.  These are:
-   CentOS 7.x (Preferred OS)
    -   Licensing is provided via GPL
    -   Yum repository for software dependencies is provided by client or via Internet
    -   IPsoft’s images follows the Center for Internet Security® (<http://www.cisecurity.org/>) benchmarks, referred to as CIS.
-   Scientific Linux 7.x (SL)
    -   Licensing is provided by client at time of install
    -   Yum repository for software dependencies is provided by client at time of install
    -   IPsoft can provide SL CIS image if desired
-   RedHat Enterprise Linux 7.x (RHEL) (Preferred OS)  
    -   Licensing is provided by client at time of install
    -   Yum repository for software dependencies is provided by client at time of install
    -   IPsoft can provide RHEL CIS image if desired
-   Oracle Linux 7.x (RHEL)
    -   Licensing is provided via GNU General Public License (GPLv2). Support contracts are available from Oracle.
    -   Yum repository for software dependencies is provided by client or via Internet
    -   IPsoft does not provide a Oracle Linux image
IPsoft can provide an Open Virtualization Appliance (OVA) with the requisite OS, software dependencies, and Amelia herself. Leveraging IPsoft’s OVA provides a quick approach to standing up an Amelia instance. On request, IPsoft also can deploy the software dependencies and Amelia on a Client’s OS build.  Client is responsible for any licensing and yum repository access.
## External Load Balancers
Amelia clusters (can also be configured for single node deployments) leverage external load balancers to handle layer 7 (transport layer) traffic, including WebSockets. For Amazon customers, this requires configuration of an Amazon Application Load Balancer rather than the classic Amazon ELB. Load balancing this way will forward user/api traffic based on host and port availability.
Health Checks determines if a backend server is available to process requests. The default health check is to establish a TCP connection to the server on the configured hostname/IP and port then run one or more basic checks, for example, to check up status and/or check a page.
IPsoft recommends using the “least connections” algorithm because of the potential for longer sessions. Load balancers will forward https connections to the Amelia-Web services; any SSL certificates will be provided to IPsoft to decrypt the SSL traffic.
## HAProxy
HAProxy is normally used to handle external load balancing requests for web/application loads. IPsoft uses HAproxy for service checks and load balancing internal Amelia services and dependencies. This allows for better utilization of all servers and ensures availability. IPsoft configures HAProxy by binding the loopback IP address (127.0.0.x) as the frontend listening IP/port, forwards traffic via the “Round Robin” algorithm to the other servers, with the necessary health check.
## MySQL / Percona XtraDB Cluster (PXC)
The Knowledge Database (KDB) to store configuration parameters such as domain, authentication, FAQ, Grammar, transactions from SLUs/BPNs, classifiers. In addition, there is at least one slave of this database which is used at conversation time to query this information.  Writes to this database are only done through the admin daemons. 
The CDB (Conversation Database) is used for storing per-conversation data.  There may be multiple instances of the CDB database attached to multiple engines.  To support additional conversation throughput, additional instances can be added along with the associated engines.  These databases are not accessible from the admin daemons.
For more information regarding PXC, here is a web link to Percona: <https://www.percona.com/software/mysql-database/percona-xtradb-cluster>
## RabbitMQ
RabbitMQ is used for various messaging tasks and share data between the Amelia Engines and Web services as a three-node active/active/active cluster. It uses both Stomp and AMQP messaging protocols which are exposed on ports 13351 through 13354. Stomp and AMQP frontends are configured in HAProxy to distribute connections in RabbitMQ. Upon failure of a single node, the engine and web will reconnect and begin consuming and sending messages from one of the remaining nodes.
For more information regarding Rabbit MQ Clustering, here is a web link to RabbitMQ’s documentation: <http://www.rabbitmq.com/clustering.html>
## Redis Sentinel
Redis is a Key-Value In-Memory data structure store used for caching and configured with a single master and multiple slaves. Monitoring and automatic master promotion is handled by Redis Sentinel. Amelia connects to a Sentinel front-end in their local HAProxy to retrieve the current master Redis server information and then connect directly to that instance. Should the master Redis instance fail, a new master is elected and failover occurs automatically.
For more information regarding Redis Sentinel, here is a web link to Redis’ documentation:
<http://redis.io/topics/sentinel>
## Amelia Daemons
### Amelia-Web
Amelia-Web has a Spring Security layer to authenticate and authorize external connections to the system. Contains the REST APIs used by the UI and has read/write access to the KDB master database; no access to CDB.
### User Web
The end user and agent conversation interface.  Has read-only to a KDB slave and read/write to a CDB.
### Engine Service
Amelia Engine Packs (AEP) are bundled units of language, process, and server-side integrations to achieve conceptual objectives.
### Batch Service
The Batch Service provides metric calculation and other batch jobs.  Has read/write to the KDB master and no access to CDB.
### Escalation Service
Amelia can escalate during a conversation in the following manners:
-   Misunderstanding: Core dialog manager or a subsystem is unable to handle the user's response.
-   Explicit Escalation: Can occur only from BPN, through an "escalate" task.
-   Warm Handover: A special explicit escalation, where a reason is specified.
The Escalation Service has read/write to the KDB master and no access to CDB.
### Integration Service
The Integration Service is a process run separately from Amelia, potentially on another host or hosts, to allow Amelia to interface with external systems.  Integration Flows are Apache Camel contexts created in Amelia V3 admin tools and deployed to these remote processes over GRPC.  The Integration Service unpacks the bundle and deploys it in its own Spring application context separate from that of the parent context and of any other flows running on the Integration Service.  Integration Service relies on Spring Integration to handle Direct RPC-Style calls over RabbitMQ, and then internally hands off to Apache Camel to execute the given request.
Integration with Amelia is complex and can vary depending on the usage. Please reach out to your IPsoft’s Cognitive Lead for best practices involving integration with specific technologies.
### Duckling Service
Based on Facebook's open source Duckling project, this service is implemented it within Amelia to handle multi-lingual date normalization.  Duckling service uses probabilistic context free grammar based on rules consisting of patterns (regular expressions for character level and predicates for concept level matching) and productions/derivations.  The modules that parse temporal expressions in English, Spanish, French, Italian and Chinese.
## Text to Speech (TTS)
TTS may be used for speech synthesis in Amelia. Multiple TTS voice engines may be installed to facilitate synthesis of audio to satisfy specified language requirements. The TTS server receives encoding requests and also serves the front-end content.
The TTS runs on a Windows 2012 R2 server, ideally with a load balanced deployment of two or more Windows Servers in Active/Passive mode behind a provided Virtual IP (VIP) address. IPsoft recommends deploying a TTS server with a minimum of 8CPUs/16GB RAM/100GB disk capacity. Please inquire with RND on supported languages and licensing information.
TTS is not provided as part of Amelia Deployments; this is a separate, licensed installation.
# Chat Integration
Amelia can be integrated with external chat systems like LivePerson/LiveEngage, Skype for Business, Facebook Messenger.  Please reach out to your IPsoft’s Cognitive Lead for best practices involving integration with specific technologies.
![](attachments/11940325/11940338.png)
Figure. Chat Integration
# Security
## Authentication Systems
Authentication systems in Amelia define where the user credentials are stored, as well as how to verify credentials. All authentication systems have the following configurable properties. Specific, or custom authentication systems, may require additional configuration or custom development.
### Local Authentication
Passwords are stored hashed with [Bcrypt](http://docs.spring.io/spring-security/site/docs/4.0.3.RELEASE/apidocs/org/springframework/security/crypto/bcrypt/BCryptPasswordEncoder.html) in the Amelia database. Local Authentication is the default setting “out-of-the-box”.
### LDAP / Active Directory (AD)
For deployments leveraging LDAP, Amelia does not store user passwords (or hashes), but instead delegates password verification to the configured LDAP server or Windows Domain Controllers. The following additional configuration parameters are required to configure LDAP/AD properly.
### Deny All
The Deny All authentication system is used for required accounts that should not allow interactive login. Any attempt to authenticate to this authentication system will fail and no passwords or hashes are stored. This authentication system is used for the Amelia user by default.
### SAML 2
Amelia supports both Service Provider (SP) initiated and Identity Provider (IDP) initiated SAML2 authentication. As with all authentication methods supported by Amelia, SAML2 is integrated within the core Amelia authentication and authorization framework. In the SAML2 case, support is provided by Spring Security SAML. SAML authentication is supported for both web clients and mobile.
-   Service Provider (SP):  An application providing a service to an end-user. In this case, Amelia.
-   Identity Provider (IDP):  An application/service that manages user identities and provides authentication capabilities. For example, Microsoft Active Directory Federation Services (ADFS) or Ping Federate.
#### Service Provider Initiated Authentication
In SP initiated authentication, an end user first requests a resource within Amelia. If the resource requires authentication and the user is not yet authenticated with Amelia, the user will be sent to the IDP for authentication. Upon successful authentication, the IDP will send the user back to Amelia with a cryptographically secure assertion of their identity.
![](attachments/11940325/11940337.png)
Figure. Amelia and Service Provider Initiated Authentication
1.  An unauthenticated user attempts to access a protected resource in Amelia.
2.  Amelia generates an authentication request (signed AuthnRequest) and redirects the user's browser to the IDP with this request.
3.  The IDP determines the user's identity. This could involve one-time tokens, username and password, or other authentication methods. The exact mechanism is not important to the integration.
4.  Once the user is authenticated, the IDP generates a signed AuthnResponse carrying the user's identity, email, and other profile information as required. The IDP then redirects the user's browser back to Amelia with this response.
5.  Amelia verifies the signed response, and if valid, auto-creates (if required/configured) the user, and logs them into Amelia. Amelia then redirects the user's browser to the original protected resource they requested in step 1.
All communication takes place over TLS and is between the user's browser and the SP, and the user's browser and the IDP. No direct communication is done between the SP and IDP other than initial out of band sharing of metadata at configuration time (see below).
#### Identity Provider Initiated Authentication
Amelia supports IDP initiated authentication, however, SP initiated authentication should be preferred. In the IDP initiated scenario users must first authenticate to the IDP before accessing Amelia.
![](attachments/11940325/11940336.png)
Figure. Amelia and Identity Provider Initiated Authentication
1.  A user logs into the IDP directly. Normally by clicking a specially crafted link in some portal.
2.  The user selects the service provider from a list provided by the IDP. This step will often be skipped if the user started with a special link in step 1.
3.  The IDP generates and signed AuthnResponse and redirects the user's browser to Amelia.
4.  Amelia verifies the signed response, and if valid, logs in the user and redirects the user's browser to the default page.
## Anonymous Access
Anonymous access allows unauthenticated users to access Amelia. The unauthenticated user will be logged in as a special type of user, the Anonymous User. These users can be given access rights just like any other user in the system. The only difference between an anonymous user and any other user is that anonymous users will be auto-created when the user accesses the system and if anonymous access is enabled. Anonymous Users are given a default set of access rights based on a configured group. This group should have very minimal access rights. Most likely only End User for the anonymous domain.
Configuration of Anonymous access is a simple checkbox, which enables/disables the feature. This is also applied to the Amelia Escalation feature.
Using Anonymous Access are for specific use cases; please inquire with the Cognitive Team for specifics
## SSL Certificates
Amelia requires SSL certificates to keep sensitive information sent across the network encrypted so that only the intended recipient can understand. IPsoft recommends wildcard certificates for ease of installation and future growth. If a wildcard SSL certificate is not used, four individual certificates or one “Subject Alternative Name”, or SAN certificate must be created for each instance (except for DR).
Table. SSL Certificate Requirements

| Name | Description |
| ----|----|
| amelia.client.com | HTTP/HTTPS URL for Amelia |

## Firewall Rules 
Table. Firewall Rules
<table class="wrapped confluenceTable">
<tbody>
<tr class="header">
<th class="confluenceTh">Destination Port</th>
<th class="confluenceTh">Protocol</th>
<th class="confluenceTh">Purpose</th>
<th class="confluenceTh">Source</th>
<th class="confluenceTh">Destination</th>
</tr>
&#10;<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>haproxy</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>80</p></td>
<td class="confluenceTd"><p>HTTP</p></td>
<td class="confluenceTd"><p>Redirect to HTTPS</p></td>
<td class="confluenceTd"><p>Browser</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>443</p></td>
<td class="confluenceTd"><p>HTTPS and WebSockets</p></td>
<td class="confluenceTd"><p>User interaction</p></td>
<td class="confluenceTd"><p>Browser</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>1936</p></td>
<td class="confluenceTd"><p>HTTP</p></td>
<td class="confluenceTd"><p>Statistics</p></td>
<td class="confluenceTd"><p>Browser</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><strong>clamav</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">3310</td>
<td class="confluenceTd">TCP</td>
<td class="confluenceTd">Antivirus</td>
<td class="confluenceTd">ipsoft-av-gateway</td>
<td class="confluenceTd">clamav</td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-engine-service@p001</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4431</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p001</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4434</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p001</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4435</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p001</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4436</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC - All pods roundrobin</p></td>
<td class="confluenceTd"><p>amelia-user-web</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>44001</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC - Engine pod 001 roundrobin.</p></td>
<td class="confluenceTd"><p>amelia-user-web</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-user-web</strong></p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4441</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-user-web</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4444</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-user-web</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4449 (_only_ required for UI development)</p></td>
<td class="confluenceTd"><p>HTTPS</p></td>
<td class="confluenceTd"><p>UI Development</p></td>
<td class="confluenceTd"><p>developer machine</p></td>
<td class="confluenceTd"><p>webpack-dev-server</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-escalation-service</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4574</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-escalation-service</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-batch-service</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4584</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-batch-service</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-admin-web</strong></p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4601</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-admin-web</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4604</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-admin-web</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4609 (_only_ required for UI development)</p></td>
<td class="confluenceTd"><p>HTTPS</p></td>
<td class="confluenceTd"><p>UI Development</p></td>
<td class="confluenceTd"><p>deveveloper machine</p></td>
<td class="confluenceTd"><p>webpack-dev-server</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-admin-service</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4611</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-admin-service</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4614</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-admin-service</p></td>
</tr>
<tr class="even">
<td colspan="5" class="confluenceTd"><p><strong>amelia-engine-service@p002</strong></p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4621</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p002</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4624</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p002</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4625</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p002</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>44002</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>amelia-user-web</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-integration-service</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4634</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-integration-service</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4635</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-integration-service</p></td>
</tr>
<tr class="even">
<td colspan="5" class="confluenceTd"><p><strong>amelia-account-service</strong></p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4641</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-account-service</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4644</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-account-service</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4645</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-account-service</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4646</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>amelia-*</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-model-server</strong></p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4651</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-model-server</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4654</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-model-server</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4655</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-model-server</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4656</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>RPC</p></td>
<td class="confluenceTd"><p>amelia-*</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td colspan="5" class="confluenceTd"><p><strong>amelia-rest-gateway</strong> </p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>4661</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>REST Endpoints</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-rest-gateway</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>4664</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-rest-gateway</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><strong>amelia-client-gateways</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">4674</td>
<td class="confluenceTd">JMX</td>
<td class="confluenceTd">Monitoring</td>
<td class="confluenceTd">monitoring network</td>
<td class="confluenceTd">amelia-client-gateway</td>
</tr>
<tr class="odd">
<td class="confluenceTd">4684</td>
<td class="confluenceTd">JMX</td>
<td class="confluenceTd">Monitoring</td>
<td class="confluenceTd">monitoring network</td>
<td class="confluenceTd">amelia-client2-gateway</td>
</tr>
<tr class="even">
<td class="confluenceTd">4694</td>
<td class="confluenceTd">JMX</td>
<td class="confluenceTd">Monitoring</td>
<td class="confluenceTd">monitoring network</td>
<td class="confluenceTd">amelia-client3-gateway</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p><strong>mysql@amelia-kdb-master</strong></p></td>
<td class="confluenceTd"><p>Master Knowledge DB</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13304</p></td>
<td class="confluenceTd"><p>HTTP</p></td>
<td class="confluenceTd"><p>Cluster Check</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>xinetd</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13305</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>mysql@amelia-kdb-master</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13306</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>amelia-admin-service</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13307</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SST</p></td>
<td class="confluenceTd"><p>mysql@amelia-kdb-master</p></td>
<td class="confluenceTd"><p>mysql@amelia-kdb-master</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13308</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Group Communication</p></td>
<td class="confluenceTd"><p>mysql@amelia-kdb-master</p></td>
<td class="confluenceTd"><p>mysql@amelia-kdb-master</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13309</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>IST</p></td>
<td class="confluenceTd"><p>mysql@amelia-kdb-master</p></td>
<td class="confluenceTd"><p>mysql@amelia-kdb-master</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p><strong>mysql@amelia-kdb-slave</strong></p></td>
<td class="confluenceTd"><p>Slave Knowledge DB</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13314</p></td>
<td class="confluenceTd"><p>HTTP</p></td>
<td class="confluenceTd"><p>Slave Check</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>xinetd</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13315</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-kdb-slave</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13316</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>amelia-engine-service</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p><strong>mysql@amelia-cdb-p001</strong></p></td>
<td class="confluenceTd"><p>Pod 001 Conversation DB</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13324</p></td>
<td class="confluenceTd"><p>HTTP</p></td>
<td class="confluenceTd"><p>Cluster Check</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>xinetd</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13325</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p001</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13326</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p001</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13327</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SST</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p001</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p001</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13328</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Group Communication</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p001</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p001</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13329</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>IST</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p001</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p001</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p><strong>mysql@amelia-cdb-p002</strong></p></td>
<td class="confluenceTd"><p>Pod 002 Conversation DB. Only in dev-v3-ipsoft for testing multiple cdb. Normally on 1332* ports.</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13334</p></td>
<td class="confluenceTd"><p>HTTP</p></td>
<td class="confluenceTd"><p>Cluster Check</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>xinetd</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13335</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p002</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13336</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>amelia-engine-service@p002</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13337</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SST</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p002</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p002</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13338</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Group Communication</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p002</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p002</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13339</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>IST</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p002</p></td>
<td class="confluenceTd"><p>mysql@amelia-cdb-p002</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p><strong>mysql@amelia-adb</strong></p></td>
<td class="confluenceTd"><p>Account Database</p></td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13344</p></td>
<td class="confluenceTd"><p>HTTP</p></td>
<td class="confluenceTd"><p>Cluster Check</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>xinetd</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13345</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>mysql@amelia-adb</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13346</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SQL</p></td>
<td class="confluenceTd"><p>amelia-admin-service</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13347</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>SST</p></td>
<td class="confluenceTd"><p>mysql@amelia-adb</p></td>
<td class="confluenceTd"><p>mysql@amelia-adb</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13348</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Group Communication</p></td>
<td class="confluenceTd"><p>mysql@amelia-adb</p></td>
<td class="confluenceTd"><p>mysql@amelia-adb</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13349</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>IST</p></td>
<td class="confluenceTd"><p>mysql@amelia-adb</p></td>
<td class="confluenceTd"><p>mysql@amelia-adb</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p><strong>redis</strong></p></td>
<td class="confluenceTd"><p><br />
</p></td>
<td class="confluenceTd"><p><br />
</p></td>
<td class="confluenceTd"><p><br />
</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13341</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Datastore, Cache</p></td>
<td class="confluenceTd"><p>amelia-user-web, amelia-admin-web</p></td>
<td class="confluenceTd"><p>redis</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13342</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Redis Sentinel Cluster Management</p></td>
<td class="confluenceTd"><p>redis-sentinel, haproxy</p></td>
<td class="confluenceTd"><p>redis-sentinel</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13343</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Redis Sentinel VIP</p></td>
<td class="confluenceTd"><p>amelia-user-web, amelia-admin-web</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>rabbitmq</strong></p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13351</p></td>
<td class="confluenceTd"><p>AMQP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Messaging</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>rabbitmq</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13352</p></td>
<td class="confluenceTd"><p>AMQP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Messaging</p></td>
<td class="confluenceTd"><p>amelia-*</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13353</p></td>
<td class="confluenceTd"><p>STOMP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Messaging</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>rabbitmq</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13354</p></td>
<td class="confluenceTd"><p>STOMP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Messaging</p></td>
<td class="confluenceTd"><p>amelia-*</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13355</p></td>
<td class="confluenceTd"><p>HTTP (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>rabbitmq</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13356</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Clustering - Distribution</p></td>
<td class="confluenceTd"><p>RabbitMQ</p></td>
<td class="confluenceTd"><p>RabbitMQ</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13357</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Clustering - epmd</p></td>
<td class="confluenceTd"><p>RabbitMQ/epmd</p></td>
<td class="confluenceTd"><p>RabbitMQ/epmd</p></td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-tf-serving</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13361</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Datastore, Cache</p></td>
<td class="confluenceTd"><p>amelia-engine, amelia-model-server</p></td>
<td class="confluenceTd"><p>redis</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13371</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>Datastore, Cache</p></td>
<td class="confluenceTd"><p>amelia-engine, amelia-model-server</p></td>
<td class="confluenceTd"><p>redis</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>13381</p></td>
<td class="confluenceTd"><p>HTTPS (TLS 1.2)</p></td>
<td class="confluenceTd"><p>Web UI</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-model-server</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>13384</p></td>
<td class="confluenceTd"><p>JMX</p></td>
<td class="confluenceTd"><p>Monitoring</p></td>
<td class="confluenceTd"><p>monitoring network</p></td>
<td class="confluenceTd"><p>amelia-model-server</p></td>
</tr>
<tr class="even">
<td class="confluenceTd">13385</td>
<td class="confluenceTd">GRPC (TLS 1.2)</td>
<td class="confluenceTd">RPC</td>
<td class="confluenceTd">haproxy</td>
<td class="confluenceTd">amelia-model-server</td>
</tr>
<tr class="odd">
<td class="confluenceTd">13386</td>
<td class="confluenceTd">GRPC (TLS 1.2)</td>
<td class="confluenceTd">RPC</td>
<td class="confluenceTd">amelia-*</td>
<td class="confluenceTd">haproxy</td>
</tr>
<tr class="even">
<td colspan="5" class="confluenceTd"><strong>Date-time parser</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">14010</td>
<td class="confluenceTd">HTTPS</td>
<td class="confluenceTd">Date-time parser</td>
<td class="confluenceTd">amelia-engine-service</td>
<td class="confluenceTd">haproxy</td>
</tr>
<tr class="even">
<td class="confluenceTd">14011</td>
<td class="confluenceTd">HTTPS</td>
<td class="confluenceTd">Date-time parser</td>
<td class="confluenceTd">haproxy</td>
<td class="confluenceTd">amelia-duckling-service</td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><strong>AV Scan REST API</strong></td>
</tr>
<tr class="even">
<td class="confluenceTd">14020</td>
<td class="confluenceTd">HTTP (TLS 1.2)</td>
<td class="confluenceTd">AV scan REST API</td>
<td class="confluenceTd">amelia-*-web</td>
<td class="confluenceTd">haproxy</td>
</tr>
<tr class="odd">
<td class="confluenceTd">14021</td>
<td class="confluenceTd">HTTP (TLS 1.2)</td>
<td class="confluenceTd">AV scan REST API</td>
<td class="confluenceTd">haproxy</td>
<td class="confluenceTd">ipsoft-av-gateway</td>
</tr>
<tr class="even">
<td class="confluenceTd">14024</td>
<td class="confluenceTd">JMX</td>
<td class="confluenceTd">Monitoring</td>
<td class="confluenceTd">monitoring network</td>
<td class="confluenceTd">ipsoft-av-gateway</td>
</tr>
<tr class="odd">
<td colspan="5" class="confluenceTd"><p><strong>amelia-tf-syntaxnet</strong> </p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>14000</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>syntaxnet parser</p></td>
<td class="confluenceTd"><p>haproxy</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>14001</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>syntaxnet parser</p></td>
<td class="confluenceTd"><p>amelia-*</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>14009</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>syntaxnet parser</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>14090</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>syntaxnet parser</p></td>
<td class="confluenceTd"><p>haproxy-test</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet-test</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><p>14091</p></td>
<td class="confluenceTd"><p>GRPC</p></td>
<td class="confluenceTd"><p>syntaxnet parser</p></td>
<td class="confluenceTd"><p>amelia-*-test</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet-test</p></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><p>14099</p></td>
<td class="confluenceTd"><p>TCP</p></td>
<td class="confluenceTd"><p>syntaxnet parser</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet-test</p></td>
<td class="confluenceTd"><p>amelia-tf-syntaxnet-test</p></td>
</tr>
<tr class="even">
<td colspan="5" class="confluenceTd"><strong>amelia-h20</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd">54321</td>
<td class="confluenceTd">HTTP</td>
<td class="confluenceTd">Flow UI</td>
<td class="confluenceTd">haproxy</td>
<td class="confluenceTd">amelia-h20</td>
</tr>
<tr class="even">
<td class="confluenceTd">54322</td>
<td class="confluenceTd">TCP</td>
<td class="confluenceTd">H2) Internal Communication</td>
<td class="confluenceTd">amelia-h20</td>
<td class="confluenceTd">amelia-h20</td>
</tr>
</tbody>
</table>
# Monitoring
For IPsoft Hosted and Online deployments, all Amelia instances and supporting Operating Systems are monitored by IPcenter using IPmons. IPmons are configured to monitor each component of Amelia; each component having several individual checks to ensure thorough reporting and availability of each Amelia instance. Below is an example of the OS checks deployed:
![](attachments/11940325/11940335.png)
Figure. Example of OS Monitoring Checks Performed
Starting with Amelia v3, IPsoft is distributing *netdata* for insights into system and application performance.  It also provides a rudimentary level of monitoring and alerting.  These alerts do not currently come back to IPsoft, but my be directed at a clients email if desired.
![](attachments/11940325/11940334.png)
Figure. Example of OS Monitoring Checks Output
![](attachments/11940325/11940333.png)
Figure. Example of OS Monitoring Checks System Overview
# Backups
Backups for Amelia can be outfitted with the Customer/Partner’s Enterprise Backup solution. This allows the customer to roll Amelia backups into their current enterprise policies. Although most deployments leverage a virtual environment, backups of entire VM can cause a degraded or unresponsive system; it is highly recommended to disable the “virtual machine memory” and “Quiesce guest file system”.
File level backups would require a more unique solution. This would require standing up a new, fresh install of an Amelia host to replace an unrecoverable one, restoring the original's configuration and data from a remote backup. For a complete list of backup locations and uses, please contact the Service Technology team.
Defining Recovery Time Objective (RTO), Recovery Point Objective (RPO), and Geographic Redundancy Objective (GRO) should be considered when creating backup/recovery policy for Amelia.  For IPsoft Hosted Instances, non-production instances have a 24-hour RTO and no larger than 24-hour RPO.  For production instances, a 4-hr RTO and a 4-hour RPO.
# Disaster Recovery
In its current architecture, Amelia v3 current supports an Active/Passive approach, where web traffic would be directed to the "live" datacenter and replicated to a secondary datacenter.    The replication method can be achieved at either the middleware (native) or infrastructure level.
For native replication, Percona XtraDB Cluster would be replicating the databases across the WAN to the DR databases.  In this setup all Production and DR database nodes are configured as one large logical cluster.  Newer versions of Amelia, Language Packs, and Gateways would be performed separately for both the Production and DR instances; not as one upgrade to cover both instances.
Infrastructure replication can be achieved using 3<sup>rd</sup> party hardware/software vendors.  SAN based replication with orchestration tools (such as Zerto/VMware SRM) is a proven DR solution, as well as software based solutions such as Veeam and Veritas.  A Production instance is replicated without changing the hostnames of the VMs, however it is best to keep the IP addresses identical if possible using a stretched layer 2 network.
The length of time necessary to conduct a failover of Amelia will depend on the overall design and available automation processes.  Regarding Amelia specifically, all Amelia  processes can be started in parallel and can take up to 5 minutes for Amelia to be started in the secondary datacenter, assuming IP addresses are not altered.
For IPsoft Hosted instances, a 4-hr RTO and a 4-hour RPO.
# High Availability Configurations
A single Amelia deployment has can be scaled up to 8 conversation PODs, each handling 150 concurrent users for a total for 1200 concurrent conversations.
Each conversation POD contains 3 Amelia Conversation Engines and related services including Redis for session data, a Percona CDB database cluster, and a KBD Database slave.
Additional services such as user and Admin web front ends and Admin services are deployed on additional virtual machines. 
This configuration has been deployed in production handling \>200,000 daily conversations with end users.
![](attachments/11940325/25462779.png)
Figure. Amelia Deployment Scaled for 1200 Concurrent Conversations
## Front End Services
The front end services include the User Web Services, Admin Web Services and AntiVirus Gateway
Each of the front end service hosts are configure with a minimum of:

| CPU | Memory | Disk |
| ----|----|----|
| 8 vCPU | 32 GB Ram | OS + 100GB for application and logs |

## Admin POD
The Admin POD contains all admin services such a escalation, integration, batch and the account services as well as dedicated hosts for the KDB and ADB Percona clusters and dedicated RabbitMQ Hosts.
The Rabbit hosts also run Redis Sentinel which is responsible for Redis cluster management throughout the deployment.
Each of the Admin hosts are configured with a minimum of:

| CPU | Memory | Disk |
| ----|----|----|
| 8 vCPU | 64 GB Ram | OS + 300GB for application and logs |

Each of the Admin Database hosts are configured with a minimum of:

| CPU | Memory | Disk |
| ----|----|----|
| 8 vCPU | 64 GB Ram | OS + 1TB for databases, backups and logs |

## RabbitMQ Hosts
Each of the Admin RabbitMQ hosts are configured with a minimum of:

| CPU | Memory | Disk |
| ----|----|----|
| 8 vCPU | 16 GB Ram | OS + 100GB for applications and logs |

## Conversation POD
Each node in the conversation pod contains the Amelia engine as well as associated components such as the Model Server, Syntaxnet, Redis (for session data) and the duckling service.
The first two nodes contain 2/3 of the CDB cluster with 2 writers (only one is actively used at a time).  The 3rd node contains a CDB Garbd for maintaining cluster integrity as well as a KDB slave used for reading knowledge during conversations.
Each of the Conversation POD hosts are configured with a minimum of:

| CPU | Memory | Disk |
| ----|----|----|
| 8 vCPU | 64 GB Ram | OS + 300GB applications, databases, backups and logs |

## General Notes about Hardware/Resource Recommendations
### CPU
-   All Virtual CPUs are mapped to exactly 1 CPU core of an Intel E5-2687W v3 @ 3.10GHz of greater CPU.
-   No over-subscription is permitted.  CPUs must have a base frequency of 3Ghz.
### Disk
-   Disk space can be influenced by the number of conversations that are handled and size of each conversation and retention times. Observe average growth per day and plan accordingly.
-   It is suggested to utilize LVM for all application file systems to allow for easy growth as required.
-   Flash/SSD/NVMe based storage is required for Amelia to operate effectively.
-   IO Subsystems must be able to sustain a minimum of 1000 Mixed IOPS (80% write, 20% Read) per VM under load with a \<10ms response time to read and write requests.
-   Each VM will perform an average of 50MBps of write activity with an additional 10MBps of read, when Journey Analytics and detailed history are disabled.  IPsoft recommends sizing for 100MBps of Writes and 25MBps of reads per VM.
-   When Journey Analytics and detailed history are enabled, it is suggested to triple the disk IO figures.
### VMware
-   VMware's vMotion has the potential to adversely affect Amelia's performance and stability in certain situations. This includes synchronization of the RabbitMQ cluster as well as Percona database clustering.
-   It is suggested that if vMotion is required, it be scheduled to execute during quiet hours of operation. 
-   DRS can have the same effect as it used vMotion underneath. It is suggested to disable fully automated DRS or set to a less aggressive level.
### OS
-   Each VM has a minimum of 16GB Swap
## Scaling Amelia Components
Amelia was designed to be able to run each of its components on different OS Images for scaling/distribution of load and to meet security requirements.
### Databases
Databases may be isolated to dedicated hosts if required by information security requirements.  This includes KDB, ADB and CDB.
#### Scaling ADB and KDB
The reference architecture describers here is scaled appropriately for the 1200 concurrent user base.  No further scaling should be necessary.
#### Scaling CDB
We believe the proper distribution of services and databases for the CDB requirement is captured in the reference design. 
All databases are heavily used for both reads and writes (hence the minimum of 1000 IOPS requirement listed above)  during conversations and usage depends on the number of conversations occurring in the given POD
#### Alternate CDB Design (Not recommended)
IPsoft has tested performance of Amelia using 3 conversations PODs and 3 dedicated nodes for the CDB Database cluster in a 3x3 configuration

| Node 1 | Node 2 | Node 3 |
| ----|----|----|
| CDB01-Master | CDB01-Writer | CDB01-GarbD |
| CDB02-Writer | CDB02-GardB | CDB02-Master |
| CDB03-GarbD | CDB03-Master | CDB03-Writer |

This design appears to offer a limited to no benefit of lower CPU utilization on the conversation POD nodes. However, the CDB nodes usage becomes very CPU and network intensive due to the number of conversations being processed.
In a shared VMware environment the overall utilization remained constant in both configurations under load.
> [!info]  
> Currently, testing reveals no benefit from a conversations per POD perspective, or a conversation mean time to response perspective. Therefore, we do not recommend this configuration.

### Rabbit MQ
Dedicated RabbitMQ/Sentinel nodes are provided in the reference architecture to provide for necessary resources response time required by these services.
### Integration Services
Integration services run with the rest of the admin services.  We have observed up to 30 integration flows per second run in the configuration with a 75ms response time (inclusive of the back end systems). 
In a 1000 concurrent user configuration with a heavy reliance on integrations we generally see an average of 10 flows per second executing with minimal load on the integration servers.
Integration services may be scaled to their own VMs and may be added in batches of 3 nodes to provide additional scaling. 
Scaling of integration services is beyond the scope of this testing due to the variety of back end systems that may influence integration performance.
## Attachments:
![](images/icons/bullet_blue.gif) [IPsoft_Amelia_v3_Platform_Design_v1.3.pdf](attachments/11940325/20808641.pdf) (application/pdf)  
![](images/icons/bullet_blue.gif) [amelia_v3.5.x_system_arch-2018-0910.png](attachments/11940325/11940327.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia_v3.4.x_system_arch-2018-0418.png](attachments/11940325/11940328.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia_v3.4.x_system_arch-2018-0411.png](attachments/11940325/11940329.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia_v3.3.4_system_arch-2018-0330.png](attachments/11940325/11940330.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia_v3_system_arch-2018-0212a.png](attachments/11940325/11940331.png) (image/png)  
![](images/icons/bullet_blue.gif) [IPsoft_Amelia_v3_Platform_Design_v1.1.pdf](attachments/11940325/11940332.pdf) (application/pdf)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-38-8.png](attachments/11940325/11940333.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-37-44.png](attachments/11940325/11940334.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-36-39.png](attachments/11940325/11940335.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-35-37.png](attachments/11940325/11940336.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-34-57.png](attachments/11940325/11940337.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-34-30.png](attachments/11940325/11940338.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-29-28.png](attachments/11940325/11940339.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-27-28.png](attachments/11940325/11940340.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-27-11.png](attachments/11940325/11940341.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-26-38.png](attachments/11940325/11940342.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-26-4.png](attachments/11940325/11940343.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-12-19_10-25-37.png](attachments/11940325/11940344.png) (image/png)  
![](images/icons/bullet_blue.gif) [amelia_v3.7.x_system_arch-2019-0626.jpeg](attachments/11940325/20808617.jpeg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [IPsoft_Amelia_v3_Platform_Design_v1.3.pdf](attachments/11940325/11940326.pdf) (application/pdf)  
![](images/icons/bullet_blue.gif) [image2019-11-20_14-50-43.png](attachments/11940325/25462779.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-11-20_15-5-52.png](attachments/11940325/25462780.png) (image/png)  
![](images/icons/bullet_blue.gif) [IPsoft_Amelia_v3_Platform_Design_v1.4.pdf](attachments/11940325/28476216.pdf) (application/pdf)  
