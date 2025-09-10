To install the SSL Certificate in an Amelia deployment, follow these steps:
1.  Verify these items exist:
    -   The X.509 server certificate which is obtained using a CSR request. The certificate can be in CRT or PEM format. If the former see section [Create PEM File](#SSLInstallationGuide-CreatePEM) to generate a PEM file.
    -   The certificate private key
    -   If the certificate is signed by a Certificate Authority (CA), you need the CA certificate.
2.  Add custom CA certs: see section [Adding Custom CA Certs](#SSLInstallationGuide-AddCustomCert) below
3.  Install the certificate: see section [Installing SSL Certificate](#SSLInstallationGuide-InstallSSLCert)
4.  Verify the certificate is installed correctly: see section [Verify Certificate is Applied](#SSLInstallationGuide-VerifyCert)
# Useful SSL Commands
These commands perform tasks needed to install SSL certificates within the Amelia environment.
## Remove password from a password protected .key file
This openssl command will remove the password, however you WILL need to be provided the password by whoever generated it
``` bash
openssl rsa -in [file1.key] -out [file2.key]
```
To tell if the .key file is encrypted with a password, open up the .key file and if you see something similar to this, the file is encrypted:
``` bash
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED DEK-Info: DES-EDE3-CBC,
```
## Create PEM File
To create a .pem file from .crt and .key files, use the following command:
``` bash
cat <Your Private Key: your_domain_name.key> <Your Primary SSL certificate: your_domain_name.crt> <Your Intermediate certificate: DigiCertCA.crt> <Your Root certificate: TrustedRoot.crt> > <filename.pem>
```
> [!warning]  
>
> If intermediate/root certs are not available, they can be left out. It is also fine to copy/paste the contents of the file into the pem

## Verify Certificate is Applied
To check that certificate has been applied, use the following openssl command:
``` bash
openssl s_client -connect <url/hostname>:<port>
```
The output will look something like this:
``` bash
CONNECTED(00000003)
depth=2 C = US, O = "thawte, Inc.", OU = Certification Services Division, OU = "(c) 2006 thawte, Inc. - For authorized use only", CN = thawte Primary Root CA
verify return:1
depth=1 C = US, O = "thawte, Inc.", CN = thawte SSL CA - G2
verify return:1
depth=0 C = US, ST = New York, L = New York, O = "IPsoft, Inc.", OU = Operations, CN = *.ipcenter.ipsoft.com
verify return:1
---
Certificate chain
 0 s:/C=US/ST=New York/L=New York/O=IPsoft, Inc./OU=Operations/CN=*.ipcenter.ipsoft.com
   i:/C=US/O=thawte, Inc./CN=thawte SSL CA - G2
 1 s:/C=US/O=thawte, Inc./CN=thawte SSL CA - G2
   i:/C=US/O=thawte, Inc./OU=Certification Services Division/OU=(c) 2006 thawte, Inc. - For authorized use only/CN=thawte Primary Root CA
---
Server certificate
-----BEGIN CERTIFICATE-----
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
4T3l1KB8q3hZ0qWfpkbWu2vOjEaH8S4=
-----END CERTIFICATE-----
subject=/C=US/ST=New York/L=New York/O=IPsoft, Inc./OU=Operations/CN=*.ipcenter.ipsoft.com
issuer=/C=US/O=thawte, Inc./CN=thawte SSL CA - G2
---
No client certificate CA names sent
---
SSL handshake has read 2985 bytes and written 631 bytes
---
New, TLSv1/SSLv3, Cipher is AES256-SHA
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1
    Cipher    : AES256-SHA
    Session-ID: B5B591FE380236310462A90F6975E7E260563ED3C32D1A9131BEFC3253B92E15
    Session-ID-ctx:
    Master-Key: 6539F02AD1A0A186E63AA0DA25D7D0EEBF2B944F3D7FE88CCB4C72A06C4171A9650C346A96159320B1FE45F5A482534B
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    Start Time: 1490733314
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
220 mx2.ipcenter.ipsoft.com ESMTP Tue, 28 Mar 2017 20:36:27 +0000
```
# Adding Custom CA certs
Some clients require Amelia to trust internally generated certificates signed by their own CA infrastructure. The custom CA certs need to be addted to both OpenSSL and Java keystore as follows:
1.  Transfer the certificate (in PEM format) to the host(s)
2.  Import into Java keystore with this command:
    ``` bash
    /usr/java/latest/bin/keytool -storepass changeit -keystore /usr/java/latest/jre/lib/security/cacerts -alias "workit rootca" -import -file /tmp/WorkITRootCA.pem
    ```
3.  Copy the certificate to /usr/share/pki/ca-trust-source/anchors/
4.  Update OpenSSL CA trust with this command:
    ``` bash
    update-ca-trust
    ```
Step 2 allows all java processes to trust the client CA  and Steps 3-4 allow OpenSSL (curl and similar) to trust the client CA.
# Installing SSL Certificate
1.  Copy the pem files in /etc/haproxy folder
2.   Edit the /etc/haproxy/haproxy.cfg file to change the two instances of the */etc/haproxy/cert_and_key.pem* string to */etc/haproxy/certificate.pem*. For example, find these two lines:  
    ``` bash
    bind :443 ssl crt /etc/haproxy/cert_and_key.pem <options>
    ...
    bind :1936 ssl crt /etc/haproxy/cert_and_key.pem <options>
    ```
    and change the strings:
    ``` bash
    bind :443 ssl crt /etc/haproxy/certificate.pem <options>
    ...
    bind :1936 ssl crt /etc/haproxy/certificate.pem <options>
    ```
3.  Restart the* *haproxy service with this command:
    ``` bash
    systemctl restart haproxy.service
    ```
