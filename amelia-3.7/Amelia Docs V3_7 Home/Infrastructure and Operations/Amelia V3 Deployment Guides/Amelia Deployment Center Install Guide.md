
|  |  |  |  |  |
| ----|----|----|----|----|
| Author | Version | Date | Comments | Final Approval? |
| Service Technology | 1.0 | September 12, 2017 | Version change from Amelia V3 to Amelia V3.x | Yes |
| Service Technology | 1.1 | September 17, 2017 | Rework, bypass ssh root requirement between Amelia hosts proper | Yes |
| Service Technology | 3.0 | October 30, 2017 | Revamped ADC UI | Yes |
| Service Technology | 3.1 | November 15, 2017 | Revamped express.py to serve :8081 | Yes |
| Service Technology | 3.2 | November 24, 2017 | Target for final distribution version to hand to Documentation Dept | Yes |
| Service Technology | 3.2 | November 25, 2017 | Clarify prerequisites | Yes |
| Service Technology | 3.3 | December 6, 2017 | Merging prerequisites | Yes |
| R&D | 3.4 | December 12, 2017 | Documentation team review | Yes |
| Service Technology | 3.5 | January 23, 2018 | Updates for /etc/group requirements, centrify-like AD/LDAP | Yes |
| Service Technology | 3.6 | February 6, 2018 | Note about McAfee or other anti-virus slowing down installation30-90 normal speed | Yes |
| Service Technology | 3.7 | February 16, 2018 | Note that openssl 1.0.2k is required - for security compliance | Yes |
| Service Technology | 3.8 | March 10, 2018 | Updated filesize for ADC installation file, minor copy edits | Yes |
| Service Technology | 4.0 | June 20, 2018 | Changes for Amelia version 3.5 | Yes |
| Service Technology | 4.1 | July 4, 2018 | Antivirus user additions; web UI WIP | Yes |
| Service Technology | 4.2 | August 1, 2018 | Fixed uid/gid numbers to match | Yes |
| Service Technology | 4.3 | January 24, 2019 | Apache user/group | Yes |

# 1. Introduction
This document describes how to install the Amelia Deployment Center (ADC), using it to configure and install Amelia software on one or more hosts. The ADC Installer includes patents as described here: <http://www.ipsoft.com/ctdmca#patents>.
# 2. ADC Overview
Amelia Deployment Center (ADC) is a lightweight stand-alone web interface that streamlines the installation of Amelia in your environment. With a minimum of information entered into the interface, Amelia can be deployed typically in 30 minutes.
The ADC runs with a Red Hat Ansible backend on RHEL 7-based distributions, currently RHEL 7, CentOS, Oracle Linux, and Scientific Linux 7. Use ADC to install a fully working single host Amelia instance on either the installation host itself or remotely, as well as installing an Amelia cluster.
ADC has two modes of operation:
-   **Fenced mode**: The target server has no connectivity to any resources beyond the LAN/ WAN environment where it is deployed.  There are no connections to any external software repositories of any kind. 
-   **Unfenced / network mode**:  The target server has connectivity to external software repositories as needed to perform upgrades and pull live content as required by Amelia and its related products. 
The ADC installation process automatically detects connectivity back to IPsoft yum repositories, and sets *fenced_mode* accordingly when the installation script is run. The installation host may be the actual host on which you install Amelia, or another RHEL 7 family host which has requisite access to Amelia host.
# 3. Install the ADC
> [!info]  
> Please pay special attention to [Installation Pre-Requisites](#AmeliaDeploymentCenterInstallGuide-Requirements). All prerequisites **must** be met before installation.

## Distribution Files
The ADC installer consists of one self-extracting *sh *archive, created by Makeself (<http://makeself.io/>).  The installer is available by either https or sftp downloads from a secure IPsoft site. A username and password is required to access these files. Please do not rename this files.
The installation file is shown in the table below. Sizes are approximate and subject to change; \<datestamp\> is of the form YYYYMMDD, indicating the latest build available. In all examples, the \<datestamp\> YYYYMMDD data is replaced with the actual date values.
**Table 1: ADC Distribution File**

| Name | Size | Required? | Function |
| ----|----|----|----|
| ameliav3installerameliav3-installer-<Amelia version>-<datestamp>.run | 10GB | Yes | Complete installation package - containing stand-alone webserver, UI, RPMs for ansible and required base for installation, ansible playbooks, configuration files, 3rd;party RPMs, all amelia rpms. Amelia version is in the form <major release.minor release.version>, such as 3.4.14, 3.5.1, etc. <datestamp> is in the form yyyymmdd |

## Install the Amelia Deployment Center
To install the ADC, you will need to download the file into a directory that has at least 20GB -- enough space for the installer + its extracted contents -- then run ./ameliav3installer-\<datestamp\>.run which automatically kicks off the configuration and installation process.
If you have not done so already, confirm your system has the pre-requisites needed to run ADC. See [Installation Pre-Requisites](#AmeliaDeploymentCenterInstallGuide-Requirements) for requirements.
### Download Appropriate Files on Target Server(s)
1.  Download files from IPsoft's yum repository at repo.svc.ipsoft.com if you have access over https. If you don't have access to IPsoft's yum repositories, please contact us for access and files.
    > [!info]  
    > After download, leave ameliav3installer-\<datestamp\>.run file intact. **Do not execute it now.**
2.  Access credentials will be provided to you by IPsoft.
3.  Download files to a directory with at least 10GB worth of space. This space is needed for installation only and can be subsequently released.  It is highly recommended you save the *inventory.fromweb* file that is created through your UI configuration.
> [!info]  
>
> **All commands below must be in a root shell**, via *sudo, pbrun bash, ss,* or the like, dependent on your internal privilege escalation methodology. The *id* command must return at least
>
> ``` bash
> # id
> uid=0(root) gid=0(root)
> ```
>
>   
> [!info]  
> Contents will be automatically extracted to the subdirectory ./amelia-v3-express.

### Installation Setup Script
The self-extracting ameliav3installer-\<datestamp\>.run file will automatically run the contained *bootstrap.sh *shell script.  Among other things, this prepares this host to run ADC by installing ansible and its requisite modules and creates a file named *fenced.repo* in your /etc/yum.repos.d/ directory.  This is mandatory to serve the needed RPMs which Amelia requires.  Note, this does not delete or modify any current entries in your /etc/yum.repos.d/ directory.
When the installer finishes running, it will display a screen similar to this one:
``` bash
 * Running on http://0.0.0.0:8081/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger pin code: 192-520-845
```
> [!warning]  
> *If you have any issues at this point please engage IPsoft.*

bootstrap.sh is a shell script, which performs the following functions:
1.  Unpacks all required files, ansible playbooks, configuration files, etc. 
2.  ADC notes if SELinux is set to **Enforcing**.  If so, ADC *temporarily *changes the policy to **Permissive** on the installation host during the installation.  In a future version, as a final act in the playbook, ADC will set SELinux mode back to Enforcing. Whether permissive or enforcing, the Amelia policy package and target enforcement files (*amelia.pp *and *amelia.te, respectively*) files will be copied to /tmp/, and will also be installed via *semodule*.
    > [!warning]  
    >
    > If you run a single-host installation where the ADC is run on a different server than where Amelia host software is installed, ensure that SELinux is set to permissive on the Amelia host before you start the installer.
3.  Verifies Perl is installed.
4.  Verifies if /apps (or the target /apps soft-link) is available with enough disk space.
5.  Adds a local yum repo, /etc/yum.repos.d/amelia-deployment-center.repo, with cost parameter of 20000. This ensures your own local repos are consulted first.
6.  Tries to connect to IPsoft's yum repo at repo.svc.ipsoft.com over https.
    1.  If it passes, required RPMs for Amelia functionality are downloaded from there.
    2.  If it fails -- aka *fenced installation, *the flag is set for a fenced offline installation, RPMs are untar'ed from ../ameliav2-installer-offline-fenced-.tgz.
7.  Ensures some base required RPMs are present for ADC to run.
8.  Lastly, bootstrap.sh starts the web installer processes /UI at http://\<installation host\>:8081
> [!warning]  
>
> Please ensure on your target installation hosts, that IPv6 localhost address in /etc/hosts is disabled (i.e., comment out ::1)
> [!info]  
>
> **I**f for any reason you need to restart the ADC user interface, run this command from the amelia-v3-express directory:
>
> ``` bash
> pkill -9 -u root -f '/usr/bin/python2 ./express.py'; ./express.py &
> ```
>
>   

**Table 2: Files in amelia-v3-express directory once the installation complete**

| Name | Usage |
| ----|----|
| ansible.cfg | Configuration file for ansible |
| ansible-json.cfg | Configuration file for ansible |
| asset/ | Misc. files for the ADC Web installer |
| auth.json | Configuration file for ansible |
| bootstrap.sh | This is automatically run once to set up installation files and web installer |
| mycaddy | Stand-alone web server for installer |
| Caddyfile | Configuration file for stand-alone web server |
| express.py | ADC Web installer written in python |
| FILENAME | Contains YYMMDD of current installer |
| index.html | Main web page for installer |
| install-me-first/ | Self-contained directory of RPMs and python modules needed for installation |
| inventory.fromweb | Configuration file created for Amelia install based on web installer input 
 SAVE THIS FILE |
| inventory.j2 | Jinja2 template file used to create inventory.fromweb |
| paddy | Stand-alone web server for installer |
| tmp | Local temporary directory for ansible installation logs |

# 4. Configure Amelia with The ADC
> [!warning]  
>
> Version 3.5 introduces a significant change in the way Amelia can be installed - providing the ability group via *Shared Services, Databases, Integration (Apache Camel) servers and Pods.  Updates to the 3.4 version of the ADC UI (described here) is a work in progress.  Current installation method is via a simple inventory file (also described below), via a single command line.*

From your browser navigate to http://\<installation host\>:8081. The ADC configuration screen will appear. Hover over individual form fields to view tooltips.
![](attachments/11940345/11940360.png)  
**Figure 1**:** Amelia Deployment Center Configuration Screen/Home Page**
## Host Settings
Amelia can be installed and configured for single host, 3-host cluster, and multi-tier host environments.
### Single Host
The single host configuration is primarily for development and testing purposes, not production.
1.  Click on *Single Host*. The Host Settings screen appears as shown in Figure 2.  
    ![](attachments/11940345/11940359.png)  
    **Figure 2**:** Host Settings on ADC Configuration Page For Single Node  
     **
2.  Enter the FQDN or IP address of the host on which you're installing Amelia.  If this host is the same host where you are running ADC, click the checkbox shown in Figure 3.  
    ![](attachments/11940345/11940358.png)  
    **Figure 3**:** ADC host is same as my target Amelia installation (bypasses ssh)  
    **This will change the display to additional configuration fields.**  
    ![](attachments/11940345/11940357.png)  
    Figure 4**:** Same-host ADC installation**
### **3-Host Cluster **
A 3-Host Cluster does not split the application tier from the database tier. As with a Multi-Tier hosting, there are **exactly** 3 database nodes.
Scroll down the ADC configuration page to complete the Host portion of the form shown in Figure 5. Cluster host settings are described below.
![](attachments/11940345/11940356.png)  
**Figure 5**:** Host Settings on ADC Configuration Page For 3-Host Cluster**
The default is installing Amelia on a single host. You also can install a 3-Host cluster or a Multi-Tier with the ADC installation software. To choose the 3-Hode Cluster option, click on *Host Clusters* and the top of the form changes from a single host entry field to three:
-   *Host cluster 1 *is the FQDN or IP address of the 1<sup>st</sup> host on which you're installing Amelia
-   *Host cluster 2 *is the FQDN or IP address of the 2<sup>nd</sup> host on which you're installing Amelia
-   *Host cluster 3 *is the FQDN or IP address of the 3<sup>rd</sup> host on which you're installing Amelia
> [!info]  
> During the validation run, if any of the tests fail, an error message is shown in the user interface. Deployment of Amelia is not possible. Please fix the problem(s) and validate again via the*Validate* button.
> [!info]  
> rabbitmq uses the *short hostname* of hosts (If your hostname is [abc123.subdomain1.subdomain2.com](http://abc123.subdomain1.subdomain2.com/), the short hostname is abc123). This is **critically important** to note.  
> When rabbitmq is in use -- for Single-Node, Cluster and Multi-Tier Amelia -- all hosts **must** be resolvable with both their FQDN *and* short hostnames. You can accomplish this with /etc/hosts or in your DNS. However, it is a base requirement for rabbitmq clustering to work. It's best practice to resolve both short hostnames and FQDNs.

### Multi-Tier Cluster
Click here to expand...
A Multi-Tier Cluster is a variation of the 3-Host Cluster, which splits off the application tier from the database tier.  With this setup, the application tier runs Amelia processes, the database tier runs PXC, rabbitmq and redis.  As with a 3-Host Cluster, there are exactly 3 database nodes.  There are a minimum of 2 application nodes required. To add additional nodes, click the **"+ Add More"** link.
![](attachments/11940345/11940355.png)
**Figure 6**:** Host Settings on ADC Configuration Page For Multi-Tier Cluster**
## Common Settings
Whether Single-Host, 3-Host Cluster or Multi-Tier, there are required configuration form fields common to all host configurations as shown in Figure 7.
![](attachments/11940345/11940354.png)  
**Figure 7**:** Common Settings Form Fields**
All fields on the Common Settings form are required.
**Table 3: Common Settings Form Fields**

| Field Name | Description/Notes |
| ----|----|
| External VIP FQDN (3-Host Cluster and Multi-Tier only) | The VIP name (or IP address) of your load balancer / VIP that you are using in your URL to access Amelia. For added security, Amelia will only allow web requests from its own FQDN, IP address, and localhost (via haproxy). 'localhost' is required for HTTP/1.0 health check requests (no host header) from the load balancer. Any requests sent with a Host header that does not match will be rejected (400).This field is mandatory when configuring a cluster, optional if the;"Single Host" is always the same host as the browser URL |
| Username | Should be set to;root; password-less ssh required only during installation timeIf deploying a cluster / multi-tier infrastructure, password-less ssh as root between the nodes from the ADC host, must be set up prior to install |
| Password | Password-less ssh is required only during installation time, as detailed above. You can set this to any value, it is unused |
| Base Directory | Controls where Amelia and Percona are installed. Currently only /apps directory is supported and this field is read only. |
| Company Code | A short name for your company without spaces, slashes, special characters, etc., used as an internal identifier. Normally lower-case |
| Environment Name | An abbreviated one-word code for what tier this is, also used as an internal identifier; common are poc, prod, dev, uat, qa, test, and the like. Normall lower-case, without spaces, slashes or special characters |
| Language Packs | Optional add-ons if you need localized language support (English is the supplied default); Language packs will be added when available. Speak with your IPsoft Cognitive Division lead before installing and for availability. Each installed language pack requires an additional 1GB disk space.
If additional language packs are installed, a predetermined Amelia version may be installed. |

## Login Credentials for Amelia
Complete the Login Credentials for Amelia portion of the ADC configuration form as shown in Figure 8.
![](attachments/11940345/11940353.png)  
**Figure 8**:** Login Credentials for Amelia Form Fields**
**Table 4: Login Form Fields  
**

| Field Name | Description/Notes |
| ----|----|
| First name and Last name | Used to personalize your user experience. No spaces |
| Email* | Administrative username you will use to log in to your Amelia instance. This is for Amelia login only, not tied to AD / LDAP |
| Password* | Password you will use to log in to your Amelia instance, and has no association with any existing passwords in your environment.Upon login, it is hightly recommended to change this password |
| Confirm Password | Same password as;Password, to ensure you typed the same. Please do not forget your username / password combination.Upon login, it is highly recommended to change this password |

> [!info]  
>
> -   \*Write down the Email and Password you set above, you will need it later. It is also stored in amelia-offline-installer/inventory.fromweb file. Keep this file secure.
> -   It is recommended you **change** your login password when you log in for the first time.
> -   The* ***checkbox **indicates your agreement to Amelia's Terms and Use. You must accept the terms, otherwise you cannot deploy / use Amelia. A PDF version is available in the assets/ ADC install directory, as well as from IPsoft directly. You may also review the Terms and Use by clicking on that link in the ADC UI.

## Validate and Deploy Amelia
The next steps are to validate your configuration details then deploy Amelia.
Once you have completed the ADC configuration form, click on the **Validate Environment** button. This uses ssh to connect to the target *Hostname* using the *Username* and *Password* you specified then validates Amelia can be installed on the specified host(s).  If you followed the requirements in this document (**password-less ssh as root from the ADC host to all the nodes must be set up prior to install)**, whatever you type in the password field is unused.
*Status* will either come back as Good!, allowing you to *deploy,* or report back any issue found which will need to be corrected before trying again, via Validation failed
For example, here we entered a bad *Hostname*, and clicking the *Validate Environment* button returned an error message, as shown in Figure 9.
![](attachments/11940345/11940352.png)  
**Figure 9**:** Sample Validation Error Example**
Once we changed the *Hostname* to a valid hostname, re-validation was successful. 
![](attachments/11940345/11940351.png)  
**Figure 10**:** Sample Validation Status:Good Example**
When *Status* is good, click on **Deploy Amelia** to install the software. This takes you to the progress screen. Please be sure you accept the Amelia Install Terms & Use by clicking the checkbox, otherwise the *Deploy Amelia* button will be greyed-out.
> [!info]  
> Please do not refresh, navigate away from using the back button, close, or in any way interrupt this screen during installation.

Now you'll see the **Progress Screen** as Amelia software is deployed and installed, shown in Figure 11.
![](attachments/11940345/11940350.png)  
**Figure 11**:** ADC Progress Screen**
The progress screen displays the Amelia installation process running via *A*nsible* *on your installation host. You view the FQDN / IP address of the host you entered on the configuration screen, what percentage of the installation has completed / how much is left, and a scrolling text box of the higher-level actions ansible is executing. This is abbreviated information. A complete log of the Ansible run will always be available to you at *\<installer path\>/amelia-v3-express/amelia-v3-installer/tmp/ansible.log*. This log does not get overwritten, only appended to.
You can copy / paste out of the scroll box if you wish.
Typical installation takes about 25 minutes; however, your installation may take longer, depending on
-   Underlying infrastructure configuration
-   Disk I/O, RAM, and/or CPU contention
-   Virtual resource groups, memory ballooning, etc.
-   Network connectivity to both internal Caddy web service and any YUM repositories
The progress meter will appear to pause during the installation. This is normal. (Again, please be patient, do not refresh, navigate away from, or close this screen.)
For example (all times and percentages approximate):
-   At around 3%, Percona RPMs are being installed and all databases configured
-   At around 60%, Percona role is completed
-   At around 63%, RabbitMQ and redis are installed
-   At around 70%, Postgres is being installed; the sql import can take several minutes
-   At around 73%, conceptnet is being installed; the data import can take several minutes
-   At around 75%, JDK and Amelia RPMs are being installed
-   At around 83%, the Amelia services are started up; this will take several minutes
The text box displays **Install has completed! **with the progress showing 100% when done, as shown in Figure 12 below. The QA process is described in [Appendix B: Amelia QA](https://docs.ipsoft.com/display/AmeliaDocsV3/Amelia+Deployment+Center+Install+Guide#AmeliaDeploymentCenterInstallGuide-AppendixB:AmeliaQA).
Click the link to access your Amelia instance; use the values input for *Email* as your login username, and *Password *as the login password. Click on the URL referenced under **Amelia is now ready** to open the link in another browser window.
> [!info]  
> URL DOESN'T WORK? If the URL presented in the ADC window doesn't work - are you working on a NAT'ed IP? Please make sure the IP address of the URL is the NAT'ed IP, if you are running the browser from your workstation. Also check if the host/VIP is in your DNS or local hosts file?

![](attachments/11940345/11940349.png)  
**Figure 12**:** ADC Amelia Ready Screen Output**
# Appendix A: Installation Pre-Requisites
> [!info]  
>
> **Please review this section; these requirements are for ADC installation, as well as to install, configure, and run Amelia software.**
> [!info]  
>
> If you are using an external IAM (Identify and Access Management Solution) such as *centrify, NetIQ, CA, BeyondTrust, etc. *- all the password and group memberships **must be created before Amelia V3 installation takes place**. Otherwise the installation will create local users on each Amelia host, with different uid/gid numbers and memberships, which is probably not what you want. See Appendix D for details before starting installation.

## File Requirements
**Table 5: ADC Distribution Files**

| Name | Size | Required? | Function |
| ----|----|----|----|
| ameliav3-installer-<Amelia version>-<datestamp>.run | 10GB | Yes | Complete installation package - containing stand-alone webserver, UI, RPMs for ansible and required base for installation, ansible playbooks, configuration files, 3rdparty RPMs. Amelia version is in the form <major release.minor release.version>, such as 3.4.14, 3.5.1, etc. <datestamp> is in the form yyyymmdd |

##  Environment  and Miscellaneous Requirements
Below are the minimum requirements to install, configure, and run Amelia software.
**Table 6: Environment and Miscellaneous Installation Requirements**
<table class="relative-table wrapped confluenceTable" style="width: 100.0%;">
<colgroup>
<col style="width: 19%" />
<col style="width: 80%" />
</colgroup>
<tbody>
<tr class="header">
<th class="confluenceTh"><strong>System</strong></th>
<th class="confluenceTh"><strong>Requirement</strong></th>
</tr>
&#10;<tr class="odd">
<td colspan="2" class="confluenceTd">Commands</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">All commands require a root shell, on both ADC host and target host</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><strong>password-less ssh as root from the ADC host to all the Amelia target hosts, must be set up prior to install. This is required only during installation</strong></td>
</tr>
<tr class="even">
<td colspan="2" class="confluenceTd"><strong>Environment</strong></td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">RHEL 7-family OS</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Minimum of 16 CPUs</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Minimum of 80GB RAM. For each language pack installed &amp; custom UI, you should increase this by 1GB</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Minimum of 150GB disk space in target (/apps) directory for a dev instance. As database backups are run nightly and stored on each database host, 200GB - 250GB is better for a POC/dev instance</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Minimum of 300GB disk space in target (/apps) directory for a production instance. As database backups are run nightly and stored on each database host, 80GB – 1TB is better for a production instance</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Minimum of 30GB disk space in root partition (/)</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Amelia should be deployed utilizing at a minimum dual Intel® Xeon® Processor E5-2687W v3 (25M Cache, 3.10 GHz) and Solid State Drives for primary storage (SAS/SATA Storage can be used for backups)</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Infrastructure is not over-subscribed; no memory ballooning, no CPU co-stop occurring, hypervisor memory utilization below 85%, for example.  To avoid this, for deployments in a virtual environment, it is recommended to enable Memory and Disk reservations for best performance; especially in highly utilized shared infrastructure. It is also recommended Memory/CPU Hotplug is enabled to increase CPUs/RAM at any time to scale quickly</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">amelia-* processes all should start up within 60-80 seconds</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">SELinux is set to not enforcing</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">The ADC host and all Amelia hosts must be resolvable to one another, whether that is done in your DNS or in local /etc/hosts files</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><p>The current ADC UI version requires <em>password-less root ssh access</em> from the ADC host → Amelia hosts</p>
<p>The next ADC version is targeted to allow a non-root user to be specified rather than <em>root</em> user, and allow alternate privilege escalation to root via various methods including <em>sudo</em> and <em>pbrun.</em> Currently this may be available via manual editing of the file <em>inventory.fromweb</em>, which is created when <strong>Validate</strong> is pressed in the ADC. This is for more experienced users who wish to install via a command-line (via privilege escalation)</p></td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd">Filesystem</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><p>Do not run the software out of /tmp if you have nodev or other restrictions set on filesystem mounts</p>
<p>Must have enough space for the installer + unpacked installation files. 10GB is minimum recommended on the installation host</p></td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd">Hosts</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">The ADC installation host can be the target host itself; the installation software does not conflict with Amelia installation</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Your /etc/hosts
<ul>
<li>::1 commented out</li>
<li>localhost is configured properly, i.e., <em>127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4</em></li>
<li>Must have an entry for your local IP address<em><br />
</em></li>
<li>The entry for your local IP must have the first entry as your hostname, then FQDN, after which any aliases / short names can be added</li>
</ul>
<p>For example, if the host IP is 10.1.20.12 and the hostname (as returned via the <em>hostname</em> or <em>hostnamectl</em> command) is <a href="http://ameliahost1.your.domain.com/">ameliahost1.your.domain.com</a>, /etc/hosts must be</p>
<p>10.1.20.12 <a href="http://ameliahost1.your.domain.com/">ameliahost1.your.domain.com</a></p>
<p>and then any other names on the same line. This is a requirement for both rabbitmq and MySQL to work properly - and it is best practice in general</p></td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">The installation host requires password-less ssh as root to the target Amelia host. This is for installation only, and can be disabled immediately after installation. However, this is not required if the ADC host is the same as the Amelia host (how to do this, is described below)</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">The default interface on the Amelia host, is the one that is used; for example, eth0, en01, etc.</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">If doing a remote install, ports 22, 5432 <strong>must</strong> also be open between the ADC host, and the target Amelia hosts. This is <strong>required only</strong> during installation</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">If doing a remote install, the remote host must be able to resolve the FQDN of the installation host - either via DNS, or via an /etc/hosts entry</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Ports 8081 is used web services for the webui</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Port 5000 is used for express.py, which does the installation</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">IPv6 is unused and commented out from the /etc/hosts file</td>
</tr>
<tr class="odd">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Note - the ADC web UI interface is self-contained</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">When rabbitmq is in use - for Single-Node, Cluster and Multi-Tier Amelia - all hosts must be resolvable via both their FQDN and short hostnames.</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd">Java</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Any existing versions of java will be removed on the Amelia host, as part of the installation. Replaced with the certified version that comes with the installer</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd">Logging</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><p>The installation modifies the configuration of rsyslog in order to provide local logging for Amelia and haproxy, which also restarts rsyslogd. Therefore, it is highly inadvisable to set your shell prompt using logger.</p>
<p>Amelia / haproxy now logs to /apps/IPsoft/log/ directory instead of /var/log. This is due to, in many client environments, /var/log residing on a small separate disk partition. If your configuration management tools modify /etc/rsyslog.conf, please be aware that your /var/log partition may fill and therefore prevent Amelia from functioning properly</p></td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd">Repo Settings</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd"><div class="content-wrapper">
<p>/etc/yum.repos.d/amelia-express.repo is added to ADC host, with a cost parameter of 2000, so it will be consulted last (as long as ADC host does not have an /etc/yum/repos* file with a cost &gt; 2000). There are individual entries with a cost of 10, reason being there are required, specific versions of RPMs which ADC provides; these local repos must be consulted first. These include Percona, Amelia, rabbitmq server and redis RPMs.<br />
If you have entries in /etc/yum.repos.d/ and they <em>do not work, </em>they may interfere with ADC and cause it to not work. This is due to the nature of yum - pointing at a repo on a network that is inaccessible, will cause timeouts. For example, having a Red Hat subscription listed (/etc/yum.repos.d/redhat.repo) which is inaccessible, causes yum install / update to fail for lack of connectivity. This isn't a problem with ADC, it's local to the ADC and Amelia target host(s). If you have this setup, we advise pre-installation to run these commands:</p>
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: groovy; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: groovy; gutter: false; theme: Confluence"><pre class="sourceCode groovy"><code class="sourceCode groovy"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a> mv <span class="op">/</span>etc<span class="op">/</span>yum<span class="op">.</span>repos<span class="op">.</span>d <span class="op">/</span>etc<span class="op">/</span>yum<span class="op">.</span>repos<span class="op">.</span>d<span class="op">-</span>save</span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a> yum clean all </span></code></pre></div>
</div>
</div>
<p><br />
</p>
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb2" data-syntaxhighlighter-params="brush: groovy; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: groovy; gutter: false; theme: Confluence"><pre class="sourceCode groovy"><code class="sourceCode groovy"><span id="cb2-1"><a href="#cb2-1" aria-hidden="true" tabindex="-1"></a> mv <span class="op">/</span>etc<span class="op">/</span>yum<span class="op">.</span>repos<span class="op">.</span>d<span class="op">-</span>save <span class="op">/</span>etc<span class="op">/</span>yum<span class="op">.</span>repos<span class="op">-</span>d </span>
<span id="cb2-2"><a href="#cb2-2" aria-hidden="true" tabindex="-1"></a> yum clean all</span></code></pre></div>
</div>
</div>
<p><br />
</p>
</div></td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd">System Software</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Amelia has certain certified, approved &amp; tested required software versions to run - for example, java, haproxy, redis and rabbitmq-server. Please do not replace these with your own / "latest and greatest"</td>
</tr>
<tr class="odd">
<td colspan="2" class="confluenceTd">System Software File Backup</td>
</tr>
<tr class="even">
<td class="confluenceTd"><br />
</td>
<td class="confluenceTd">Stash the file inventory.fromweb located at ./amelia-v3-express/amelia-v3-installer/inventory.fromweb somewhere safe. This file contains the configuration information you entered in the ADC UI. See the example below.</td>
</tr>
</tbody>
</table>
``` groovy
localhost              ansible_connection=local
[Integration]
singlehost-v3.amelia.mydomain.com
[App]
singlehost-v3.amelia.mydomain.com
[amelia-adb]
singlehost-v3.amelia.mydomain.com pxc_role=master
[amelia-kdb-master]
singlehost-v3.amelia.mydomain.com pxc_role=master
[amelia-kdb-slave]
singlehost-v3.amelia.mydomain.com
[amelia-cdb-p001]
singlehost-v3.amelia.mydomain.com pxc_role=master
[Database:children]
amelia-adb
amelia-kdb-master
amelia-kdb-slave
amelia-cdb-p001
[RemoveAmelia:children]
Database
App
[db:children]
Database
[all:vars]
ansible_user=root
ansible_ssh_pass=
client=ipsoft
client_environment=test-v3
location=EXT1
install_user=firstname.lastname@gmail.com
install_password=abc673XYZ
instance_name=ipsoft-test-v3
firstname=Firstname
lastname=Lastname
languagepacks=
fqdn=myexternalVIP.mydomain.com
fenced_instance=true
install_qa=false
pkg_amelia_web=
pkg_amelia_engine=
pkg_amelia_escalation=
pkg_amelia_batch=
pkg_amelia_locale-nl=amelia-locale-nl
pkg_amelia_locale-sv=amelia-locale-sv
pkg_amelia_locale-es=amelia-locale-es
pkg_amelia_locale-de=amelia-locale-de
pkg_amelia_locale-fr=amelia-locale-fr
pkg_amelia_locale-no=amelia-locale-no
pkg_amelia_locale-da=amelia-locale-da
pkg_jdk=jdk1.8
pkg_Percona_XtraDB-Cluster-server=
#Percona-XtraDB-Cluster-server-57-5.7.17-29.20.3.el7
pkg_rabbitmq_server=
pkg_redis=
pkg_haproxy=haproxy-1.7.8-1.el7
fenced_repo_port=5432
```
# Appendix B: Amelia QA
ADC comes with its own post-install validation software based on RobotFramework (RF), a generic test automation framework for acceptance testing and acceptance test-driven development (ATDD), with test libraries written in Java. ADC automatically runs RF, storing its output on your Amelia host(s) in /apps/amelia-qa/output/ directory. The post-install validation software can be run anytime or with a cron job if it is on the same target host as the ADC software.
Three files are in this directory:
-   report.html - entry point to the report
-   log.html - drill-down entries for each test
-   output.xml - low-level output from the report run
Copy these three html files to a host where you can launch a browser to review the output
Your report will look similar to this screen:
![](attachments/11940345/11940348.png)  
**Figure 13: ADC Validation Screen**
Note that under the Pass / Fail columns, there may be links in blue under the *Test Statistics* section at the top of the report. These are failed tests deemed to be non-critical. These are:
-   If you have firewalld running, or installed, ADC configures the ports in the default zone. firewalld is supported but not required for Amelia installation.  You can turn off firewalld at any time, should you require.
-   IPremote is IPsoft's client-side monitoring software, part of IPmon Remote Infrastructure Monitoring (RIM). It is not required to be installed.
-   Lastly, ADC installs its own SSL certificate for Amelia. Post-install, you should replace this with your own valid certificate.
Should any other test be marked critical, please contact IPsoft so we can review the issue.
![](attachments/11940345/11940347.png)  
**Figure 14: ADC Test Result Sample**
# Appendix C: Repositories Used For ADC 1-click Installation
An [external document contains a list of RPMs and files installed on both an ADC host, and an Amelia host](#).
# Appendix D: Users Created by Amelia Installation
This is not ADC-specific, though important to note here. These users are created and added to /etc/passwd as part of installing your Amelia environment. They may need to be added to your sssd / pam config / etc.
If these users are *pre-created* in your AD/LDAP, they will not be added to the local passwd/group files.
> [!info]  
>
> If you are using an external IAM (Identify and Access Management Solution) such as *centrify, NetIQ, CA, BeyondTrust, etc. *- all the password and group memberships, Table 8 and Table 9 below, **must be created before Amelia V3 installation takes place**. Otherwise the installation will create local users on each Amelia host, with different uid/gid numbers and memberships, which is probably not what you want.

**Table 8: Users Created by Amelia Installation**

| Username | Use | Sample /etc/password entry (to show homedir and login shell)
Note, epmd and amelia homedirs are not created |
| ----|----|----|
| mysql | owner of Percona (mysql) database files | mysql:x:106:106:MySQL server:/var/lib/mysql:/bin/bash |
| redis | redis owner | redis:x:105:105:Redis Database Server:/var/lib/redis:/sbin/nologin |
| rabbitmq | rabbitmq owner | rabbitmq:x:103:103:RabbitMQ messaging server:/var/lib/rabbitmq:/sbin/nologin |
| haproxy | haproxy owner | haproxy:x:188:188:haproxy:/var/lib/haproxy:/sbin/nologin |
| amelia | amelia owner | amelia:x:102:102:IPsoft Amelia:/var/lib/amelia:/sbin/nologin |
| exim | OPTIONAL for sending email - based on use case if mail is to be sentout as part of workflow. This is not created by the installer.mail owner | exim:x:93:93::/var/spool/exim:/sbin/nologin |
| netdata | from https://my-netdata.io/ - simple out-of-the-box monitoring & metrics collectionProvides basic information monitoring for Amelia and components on the installed host(s) | netdata:x:497:497:netdata:/usr/share/netdata:/sbin/nologin |
| ipsoft | user for default antivirus software, part of Amelia version >= 3.5 | ipsoft:x:991:991:ipsoft user for antivirus:/home/ipsoft:/bin/bash |
| clamupdate | antivirus definitions from ClamV, from;https://www.clamav.net/ | clamupdate:x:988:988:Clamav database update user:/var/lib/clamav:/sbin/nologin |
| clamscan | antivirus file upload scanning software ClamV, from;https://www.clamav.net/ | clamscan:x:986:986:Clamav scanner user:/:/sbin/nologin |
| apache | Only when an optional web server is put in front of amelia | apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin |

**  
**
**Table 9: /etc/group Requirements**

| Username | Use | Sample /etc/group entry, showing memberships |
| ----|----|----|
| mysql | group entry for mysql user | mysql:x:991: |
| redis | redis owner | redis:x:989: |
| rabbitmq | rabbitmq owner | rabbitmq:x:990: |
| haproxy | haproxy owner | haproxy:x:188: |
| amelia | amelia owner | amelia:x:1000:mysql,postgres,redis |
| exim | OPTIONAL for sending email - based on use case if mail is to be sentout as part of workflow. This is not created by the installer.mail owner | exim:x:93: |
| netdata | from;https://my-netdata.io/ - simple out-of-the-box monitoring & metrics collection
Provides basic information monitoring for Amelia and components on the installed
host(s) | netdata:x:497: |
| ipsoft | user for default antivirus software, part of Amelia version >= 3.5 | ipsoft:x:991 |
| virusgroup | group for antivirus software users | virusgroup:x:987:clamupdate,clamscan |
| clamscan | antivirus file upload scanning software ClamV, from;https://www.clamav.net/ | clamscan:x:986: |
| clamupdate | antivirus definitions from ClamV, from;https://www.clamav.net/ | clamupdate:x:988: |
| apache | Only when an optional web server is put in front of amelia | apache:x:48: |

# Appendix E: Files Removed By ADC 1-click Installation
On the Amelia hosts, the installation removes, among others
-   All versions of Percona
-   All versions of Erlang
-   All Java-related RPMs named
    -   \*openjdk\*
    -   \*javadb\*
    -   "mysql-community\*
-   /etc/security/limits.d/20-nproc.conf
-   All Percona RPMs named
    -   Percona-Server-shared-55
    -   Percona-Server-shared-56
    -   Percona-Server-client-55
    -   Percona-Server-client-56
    -   percona-xtrabackup
-   yum-cron
-   /etc/cron.daily/0yum-daily.cron
-   /etc/cron.hourly/0yum-hourly.cron
-   /etc/yum/yum-cron-hourly.conf
-   /etc/yum/yum-cron.conf
-   /usr/lib/systemd/system/yum-cron.service
-   /usr/sbin/yum-cron
-   /usr/share/doc/yum-cron-3.4.3
-   /usr/share/doc/yum-cron-3.4.3/COPYING
-   /usr/share/man/man8/yum-cron.8
These either conflict with specific required software versions / configurations that Amelia requires, or in the case of yum-cron, has been shown to negatively update those software versions / configurations.
# Appendix F: Troubleshooting Tips
**Table 10: Installation Troubleshooting Tips**

| Problem / Error Message | Possible Causes | What To Do |
| ----|----|----|
| Installation is very slow | McAfee or other anti-virus is examining all files including jars, causing installation to slow down anywhere from 30-90 times normal installation speed | Temporarily disable anti-virus for duration of installationWhite-list /apps/IPsoft/amelia and other files |
| Validate Environment->Status displays 
 Validation failed: SSH Error: data could not be sent to the remote host. Make sure this host can be reached over ssh | Hostname or IP address you entered in Hostname is not resolvable 
SSH is not open from your installation to that hostname / IP address 
Potential routing issue 
DNS and/or /etc/resolv.conf misconfigured 
There is a firewall on your installation host, target host, or on your network between the installation host and target host | from a terminal window, run host / dig / nslookup  ; ensure the name is resolvable 
 ping  ; check if target host is reachable 
 nmap -p22  ; ensure you can reach port 22 on target host 
 telnet  22; ensure you can reach port 22 on target host 
 iptables --list -vn on both hosts, look for discrepancies 
 netstat -rn on both hosts, check routing 
 check with your network adminstrator |
| Status spins forever | express.py is not running | cd amelia-deployment-center/ , run ./WEBSERVER ; then ps wauxww | grep -e express -e caddy to ensure both processes are running 
 Validate via ps waxuww | grep express, you should see these processes: /usr/bin/python2 -u ./express.py and /usr/bin/python2 ./express.py |
| Under Login Credentials for Amelia, Confirm Password is in RED | Passwords do not match | ensure you entered the same password in both fields |
| Deploy Amelia is greyed out | You have not successfully passed Validate Environment 
You have not accepted the Amelia Install Terms & Use | Click on Validate Environment, fix until it shows Status: Good! 
 Click on the checkbox on the left of Amelia Install Terms & Use |
| Going to :8081 in your browser displays This site can't be reached | caddy is not running on the ADC host 
 Your browser is firewalled off from the ADC host on port 8081 | cd amelia-deployment-center/ , run ./WEBSERVER ; then ps wauxww | grep -e express -e caddy to ensure both processes are running 
 Check your browser proxy settings; lsof -i:8081 on the ADC host to ensure the port is listening; iptables --list -vn ADC host, ensuring port is not blocked 
 Ensure the ADC  is resolvable from your workstation 
 Check if your browser is using a proxy which may be intercepting your http call 
 Check with your network adminstrator |
| Validate Environment→Status displays Validation failed: SElinix cannot be enforcing. Target node has enforcing. | Target host has SELinux mode set to Enforcing | SELinux must be set to Permissive; Enforcing is not allowed. Run setenforce 0 on the command line, and ensure permissive is permanently set. 
 Verify via sestatus | grep -i mode 
 Set SELINUX=permissive in /etc/selinux/config to ensure change survives reboots |
| Validate Environment→Status displays Validation failed: Not enough CPUs. Target node has X. Must have 16 or more. | Minimum requirement for an Amelia host is 16 CPUs | Ensure your target Amelia host has at least 16 CPUs |
| Startup of process(es) fail with User not known to the underlying authentication module 
 For example - "# rabbitmq-server -detached 
 su: User not known to the underlying authentication module" | Installation RPMs add entries to your /etc/passwd file, but your underlying OS authentication / authorization mechanisms, such as pam, su, kerberos, etc., requires additional configuration | Speak with your local *nix, infrastructure and / or security administrators |
| After installation, you are unable to browse to your Amelia instance at https://<fqdn>/Amelia/index.html | Your workstation is firewall'ed off on ports 80/443 from your Amelia instanceYour browser proxy settings, and/or your proxy host, are not allowing connections | Speak with your local *nix, infrastructure and / or security administrators |
| This is an FYI; if you run# cat /var/log/audit/audit.log |audit2allow
and see
[Errno 2] No such file or directory: '/etc/selinux/targeted/contexts/files/file_contexts.local' | This is a known Red Hat bug in RHEL 7.3 (https://access.redhat.com/solutions/2960851); it does not affect the proper functioning of Amelia | touch /etc/selinux/targeted/contexts/files/file_contexts.local

\| \| Percona (database) installs fail with  
\[ERROR\] WSREP: wsrep_load(): dlopen(): /usr/lib64/galera3/[libgalera_smm.so](http://libgalera_smm.so/): symbol SSL_COMP_free_compression_methods, version [libssl.so](http://libssl.so/).10 not defined in file [libssl.so](http://libssl.so/).10 with link time reference \| Your system is insecure - it is running an early version of openssl. \|
Ensure you update openssl and openssl-libs
openssl-libs-1.0.2k-8.el7.x86_64openssl-1.0.2k-8.el7.x86_64
\|
