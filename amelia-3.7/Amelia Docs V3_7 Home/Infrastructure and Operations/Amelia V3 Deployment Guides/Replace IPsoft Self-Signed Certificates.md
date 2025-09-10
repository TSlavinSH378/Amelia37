-   [Validating When Certificates Expire](#ReplaceIPsoftSelfSignedCertificates-ValidatingWhenCertificatesExpire)
    -   [Hosts Running HAproxy](#ReplaceIPsoftSelfSignedCertificates-HostsRunningHAproxy)
    -   [Shared and Pod Hosts](#ReplaceIPsoftSelfSignedCertificates-SharedandPodHosts)
-   [Running Ansible Playbook To Upgrade Certificates](#ReplaceIPsoftSelfSignedCertificates-RunningAnsiblePlaybookToUpgradeCertificates)
-   [Syntaxnet Certificates](#ReplaceIPsoftSelfSignedCertificates-SyntaxnetCertificates)
IPsoft's 1-click Amelia installer provides self-signed certificates for Amelia V3's HAProxy and Duckling services.  These certs are set to expire at 23:59:59 on September 8th, 2019.  Use the documented playbook to change the certificate to expire on May 19, 2036.  
The Ansible playbook listed below is also available at this Artifactory URL: <https://artifactory.ipsoft.com:443/artifactory/amelia-v3-install/replace-cert-for-haproxy-and-duckling.yml>
> [!warning]  
>
> If the **/etc/haproxy/cert_and_key.pem** and **/apps/IPsoft/amelia/amelia-duckling-service/conf/cert_and_key.pem** files on an Amelia host have been replaced with IPsoft's own certificates, there's no need to run this playbook.

# Validating When Certificates Expire
## Hosts Running HAproxy
On *hosts running haproxy*, run the following shell commands.  If duckling is not running on a host (which may be normal), it will return an error message which can be safely ignored.
**openssl expiry verification**
``` groovy
/bin/echo | /bin/openssl s_client -servername NAME -connect localhost:1936 2>/dev/null | /bin/openssl x509 -noout -dates | /bin/grep not
/bin/echo | /bin/openssl s_client -servername NAME -connect localhost:14010 2>/dev/null | /bin/openssl x509 -noout -dates | /bin/grep not
```
If the shell command output returns a **notAfter** setting with a datetime value in 2019, then run the Ansible playbook below.
``` groovy
notAfter=Sep 8 23:59:59 2019 GMT
```
## Shared and Pod Hosts
The easiest way to validate certificate expiration dates for shared and pod hosts is to run these shell commands:
**Per-host validation**
``` groovy
openssl x509 -noout -enddate -in /apps/IPsoft/amelia/amelia-duckling-service/conf/cert_and_key.pem | grep notAfter
openssl x509 -noout -enddate -in /etc/haproxy/cert_and_key.pem | grep notAfter
```
If the shell command output returns a **notAfter** setting with a datetime value in 2019, then run the Ansible playbook below.
# Running Ansible Playbook To Upgrade Certificates
On one or more Amelia deployment hosts, in the same location where  the **ansible-playbook -i \<inventory file\> main.yml** command was run, run the following playbook with the same root user and other details as run earlier.
``` groovy
ansible-playbook -i <inventory file> replace-cert-for-haproxy-and-duckling.yml
```
This playbook checks the expiration date of the HAproxy SSL certificate. If the certificate expires in 2019, the playbook will:
-   Copy an existing self-signed certificate which expires in 2036, for both haproxy and amelia-ducking-service
-   Reload (**not** restart) haproxy service
-   Restart amelia-duckling-service
The Ansible replace-cert-for-haproxy-and-duckling.yml playbook script is below.
**replace-cert-for-haproxy-and-duckling.yml**
``` groovy
- hosts: shared:admin:pods:Integration:rabbitmq:App
  gather_facts: false
  environment:
    PATH: /usr/sbin:/bin:$PATH:{{ ansible_env.PATH }}
  tasks:
# Do this only on hosts with /etc/haproxy/haproxy.cfg
  - name: Get certificate expiration for /etc/haproxy/cert_and_key.pem
    shell: openssl x509 -noout -enddate -in /etc/haproxy/cert_and_key.pem | grep notAfter | grep ' 2019 '
    register: haproxy_cert_expires_soon
    ignore_errors: true
  - block:
    - name: Get timestamp for backup files
      set_fact:
        timestamp: "{{ lookup('pipe', 'date +%Y%m%d-%H%M') }}"
    - name: Get stat of /etc/haproxy/cert_and_key.pem-OLD-CERT
      stat: path="/etc/haproxy/cert_and_key.pem-OLD-CERT"
      register: has_backup_of_old_haproxy_cert
      ignore_errors: true
    - name: Make named backup for /etc/haproxy/cert_and_key.pem
      command: /bin/cp /etc/haproxy/cert_and_key.pem /etc/haproxy/cert_and_key.pem-OLD-CERT
      when: has_backup_of_old_haproxy_cert.stat.exists == false
    - name: Copy 2035 cert named Amelia_Rabbit.pem to /etc/haproxy/cert_and_key.pem
      copy: src=roles/ipsoft-ameliav3.rabbitmq/files/Amelia_Rabbit.pem dest=/etc/haproxy/cert_and_key.pem owner=root group=root mode=0600 backup=yes
    - name: Reload running haproxy to not interrupt conversations
      systemd: name=haproxy enabled=true state=reloaded masked=false daemon-reload=true #"
    - name: Get haproxy certificate expiration for debug purposes
      shell: openssl x509 -noout -enddate -in /etc/haproxy/cert_and_key.pem | grep notAfter
      register: haproxy_cert_expiration_date
      ignore_errors: true
    - debug: var=haproxy_cert_expiration_date
    when: haproxy_cert_expires_soon is defined and haproxy_cert_expires_soon.rc == 0
  - name: Get certificate expiration for amelia-duckling-service from local file
    shell: openssl x509 -noout -enddate -in /apps/IPsoft/amelia/amelia-duckling-service/conf/cert_and_key.pem | grep notAfter | grep ' 2019 '
    register: duckling_cert_expires_soon
    ignore_errors: true
  - block:
    - name: Copy 2025 cert named Amelia_Rabbit.pem to /apps/IPsoft/amelia/amelia-duckling-service/conf/cert_and_key.pem
      copy: src=roles/ipsoft-ameliav3.rabbitmq/files/Amelia_Rabbit.pem dest=/apps/IPsoft/amelia/amelia-duckling-service/conf/cert_and_key.pem owner=amelia group=amelia mode=0600 backup=yes
    - name: Restart amelia-duckling-service
      systemd: name=amelia-duckling-service enabled=yes state=restarted
    - name: Get duckling certificate expiration for debug purposes
      shell: openssl x509 -noout -enddate -in /apps/IPsoft/amelia/amelia-duckling-service/conf/cert_and_key.pem | grep notAfter
      register: duckling_expiration_date
      ignore_errors: true
    - debug: var=duckling_expiration_date
    when: duckling_cert_expires_soon is defined and duckling_cert_expires_soon.rc == 0
 # May need to reload haproxy if not fully reloaded above
  - name: See if we need to reload haproxy
    shell: echo | openssl s_client -connect localhost:1936 2>/dev/null | openssl x509 -noout -dates | grep notAfter | grep ' 2019 '
    register: haproxy_needs_reloading
    ignore_errors: true
  - name: Reload running haproxy to not interrupt conversations
    systemd: name=haproxy enabled=true state=reloaded masked=false daemon-reload=true #"
    when: haproxy_needs_reloading is defined and haproxy_needs_reloading.rc == 0
 # May need to restart duckling if not fully reloaded above
  - name: See if we need to reload duckling
    shell: /bin/echo | /bin/openssl s_client -connect localhost:14010 2>/dev/null | /bin/openssl x509 -noout -dates | grep notAfter | grep ' 2019 '
    register: duckling_needs_reloading
    ignore_errors: true
  - debug: var=duckling_needs_reloading
  - name: Restart amelia-duckling-service
    systemd: name=amelia-duckling-service enabled=yes state=restarted
    when: duckling_needs_reloading is defined and duckling_needs_reloading.rc == 0
```
# Syntaxnet Certificates
If certificates for Syntaxnet need to be updated manually, replace these default files:
/apps/IPsoft/amelia/syntaxnet/server.crt  
/apps/IPsoft/amelia/syntaxnet/server.key
with appropriate certificate and key files. Both files are in pem format.
