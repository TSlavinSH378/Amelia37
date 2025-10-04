{% version "3.x" %}
Access to Amelia V2 and V3 instances requires set up and use of Single Sign-On (SSO) authentication to connect and authenticate with client systems. Setup with clients requires collecting basic demographic information, for example, first and last names, and configuring Amelia. SSO options also have tradeoffs to consider when recommending options to clients.
# Collecting Client Information for SSO
Information collected from clients varies based on their SSO choice. SAML2 and LDAP are the most common with PKI lightly used.
Table. Required SSO Client Information

| Authentication Method | Required Client Information |
| ----|----|
| SAML2 | Encryption choice: SHA-1, SHA-256 (default), SHA-512Email address, first name, and last name needs to be passed. NameID must be their email or ID, otherwise we'll need the attribute name that the client is expecting us to use for email (ie. externalID)The IdP metadata XML is required and a certificate for IdP is optional. |
| LDAP | Connection to client authentication systemServer URL to handle requestsPort used: standard port 389 for Unsecure LDAP, 636 or 3269 for LDAPS, or a custom portEmail address, first name, and last name needs to be passed in NameID (email or ID) or as an attributeAdditional demographic data is possible but slows authentication process |

# SSO Options and Tradeoffs
Amelia’s authentication systems define where to store user credentials, as well as how to verify them.
Table. Amelia’s SSO Authentication Options

| Authentication Method | Description |
| ----|----|
| SAML2 | Amelia supports both Service Provider (SP) initiated and Identity Provider (IDP) initiated SAML2 authentication.As with all authentication methods supported by Amelia, SAML2 is integrated within the core Amelia authentication and authorization framework.; In the SAML2 case, support is provided by Spring Security SAML.SAML authentication is supported for web clients and mobile. |
| LDAP | When LDAP is configured, Amelia does not store user passwords (or hashes), but instead delegates password verification to the configured LDAP server. |

# SSO Configuration With Amelia
Single Sign-On authentication is configured through Amelia’s administration pages. In the case of SAML2, there are additional configuration file settings to check.
## Administration Pages
In Amelia instances, SSO configuration is available in the administration pages. In V2, click the dropdown list at the top left of the interface and select Admin. Then click the Authentication Systems tab on the left side. Select either an existing system from the list or click the New button to create an SSO option.
In V3, click the System Settings link at the left side of Amelia’s administration pages then click Authentication Systems link. The Authentication Systems workspace appears. Click the Notepad icon to the left of a system to edit details for that system. Or click the New Authentication System button at the top right of the workspace to create an SSO option.
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

## Configuration Files
SAML2 encryption also is configured in application files. In Amelia V2, the amelia-web/application.properties file includes an encryption setting. In V3, the amelia-user-web/application.properties for debugging only.
Table. Settings for /apps/IPsoft/amelia/amelia-web/application.properties File

| Configuration Setting | Description |
| ----|----|
| logging.level.org.springframework.security.saml=DEBUG | Used during initial setup/debug. Remove in all other cases. |
| amelia.saml.log-messages=true | Used during initial setup/debug. Remove in all other cases. |
| amelia.saml.superceding.target.url=/AmeliaCust/ | Optional. Used after SAML2 authentication when the user wants to use the custom UI instead of Amelia Core UI |

## Authentication Policies
Amelia’s authentication policies — which determine what users can see and do — are tied to SSO and other authentication systems. While authentication policies are not part of setting up SSO, they need to be defined and set up in parallel to the SSO access process.
## SSO and Custom UI Bundles
SSO integrations with the SAML2 identity provider (IP) allow for URL redirects after login. Amelia can route the user to a custom user interface (UI) and a specified domain. This is useful if a custom UI is not the default for an Amelia domain. If a custom UI is set as a domain default, redirecting to the /Amelia path will display the appropriate user interface.
The target URL to begin SSO SAML2 login must follow the https://hostname/Amelia/login?redirectPath=/Amelia/path/to/custom/ui structure, for example:
``` groovy
https://amelia.acme.com/Amelia/login?redirectPath=/Amelia/ui/AmeliaCust/&domainCode=sandbox
```
Without the /Amelia/login path, logins will be directed to /Amelia/login with no redirectPath or other parameters. The default interface will appear after successful login.
If the SAML2 redirect functionality is used, a logout link should be provided in the custom UI that points to a landing page with a login link to the unique custom UI login URL with redirectPath and any other parameters.
> [!warning]  
>
> The domainCode query string parameter is available only with some custom user interfaces and currently is not activated for the basic default Amelia V3.3.3 chat interface.

# Configuration Tools
In addition to Amelia’s administration web pages and configuration file settings, there are tools useful to setting up client SSO access.
## ldapsearch
This command-line utility locates and retrieves directory entries. The tool opens a connection to a specified server then performs a search with a specified search filter.
<https://www.centos.org/docs/5/html/CDS/ag/8.0/Finding_Directory_Entries-Using_ldapsearch.html>
## Sample User Group Script (Optional)
This script maps entries to user groups and domains.
``` bash
var code = credential.getAttributeAsString(entitlement_key);
var domainName = 'CompanyName';
//make sure the domains here match the default and all possible code cases in switch statement
var domains = ['domain1', 'domain2', 'domain3', 'domain4', 'domain5'];
if (code != null) {
      switch (code) {
             case '22':
                    domainName = 'domain1';
                    break;
             case '2':
                    domainName = 'domain2';
                    break;
             case '9':
                    domainName = 'domain3';
                    break;
             case '10':
                    domainName = 'domain4';
                    break;
             case '13':
                    domainName = 'domain5';
                    break;
      }
}
var groups = {};
if (domains.indexOf(domainName) > -1) {
      var add = domains.splice(domains.indexOf(domainName), 1) + ' End Users';
      var remove = [];
      for (var i = 0;i<domains.length;i++) {
             remove.push(domains[i] + ' End Users');
      }
      groups = {
             added: add,
             removed: remove
      }
}
groups;
```
## XML Metadata Example
``` bash
<EntityDescriptor
    xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
    entityID="loadbalancer-3.example.com">
    <IDPSSODescriptor
        WantAuthnRequestsSigned="false"
        protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
        <KeyDescriptor use="signing">
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
                <X509Data>
                    <X509Certificate>
MIICZDCCAg6gAwIBAgICBr8wDQYJKoZIhvcNAQEEBQAwgZIxCzAJBgNVBAYTAlVTMRMwEQYDVQQI
EwpDYWxpZm9ybmlhMRQwEgYDVQQHEwtTYW50YSBDbGFyYTEeMBwGA1UEChMVU3VuIE1pY3Jvc3lz
dGVtcyBJbmMuMRowGAYDVQQLExFJZGVudGl0eSBTZXJ2aWNlczEcMBoGA1UEAxMTQ2VydGlmaWNh
dGUgTWFuYWdlcjAeFw0wNzAzMDcyMTUwMDVaFw0xMDEyMDEyMTUwMDVaMDsxFDASBgNVBAoTC2V4
YW1wbGUuY29tMSMwIQYDVQQDExpMb2FkQmFsYW5jZXItMy5leGFtcGxlLmNvbTCBnzANBgkqhkiG
9w0BAQEFAAOBjQAwgYkCgYEAlOhN9HddLMpE3kCjkPSOFpCkDxTNuhMhcgBkYmSEF/iJcQsLX/ga
pO+W1SIpwqfsjzR5ZvEdtc/8hGumRHqcX3r6XrU0dESM6MW5AbNNJsBnwIV6xZ5QozB4wL4zREhw
zwwYejDVQ/x+8NRESI3ym17tDLEuAKyQBueubgjfic0CAwEAAaNgMF4wEQYJYIZIAYb4QgEBBAQD
AgZAMA4GA1UdDwEB/wQEAwIE8DAfBgNVHSMEGDAWgBQ7oCE35Uwn7FsjS01w5e3DA1CrrjAYBgNV
HREEETAPgQ1tYWxsYUBzdW4uY29tMA0GCSqGSIb3DQEBBAUAA0EAGhJhep7X2hqWJWQoXFcdU7eQ
        </KeyDescriptor>
        <KeyDescriptor use="encryption">
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
                <X509Data>
EwpDYWxpZm9ybmlhMRQwEgYDVQQHEwtTYW50YSBDbGFyYTEeMBwGA1UEChMVU3VuIE1pY3Jvc3lz
dGVtcyBJbmMuMRowGAYDVQQLExFJZGVudGl0eSBTZXJ2aWNlczEcMBoGA1UEAxMTQ2VydGlmaWNh
dGUgTWFuYWdlcjAeFw0wNzAzMDcyMjAxMTVaFw0xMDEyMDEyMjAxMTVaMDsxFDASBgNVBAoTC2V4
YW1wbGUuY29tMSMwIQYDVQQDExpMb2FkQmFsYW5jZXItMy5leGFtcGxlLmNvbTCBnzANBgkqhkiG
HREEETAPgQ1tYWxsYUBzdW4uY29tMA0GCSqGSIb3DQEBBAUAA0EAEgbmnOz2Rvpj9bludb9lEeVa
OA46zRiyt4BPlbgIaFyG6P7GWSddMi/14EimQjjDbr4ZfvlEdPJmimHExZY3KQ==
            </KeyInfo>
            </EncryptionMethod>
        </KeyDescriptor>
        <ArtifactResolutionService
            index="0"
            isDefault="1"/>
        <SingleLogoutService
            Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect"
        <SingleLogoutService
            Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP"
        <ManageNameIDService
            Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect"
            ResponseLocation="https://LoadBalancer-3.example.com:9443/
               amserver/IDPMniRedirect/metaAlias/idp"/>
        <ManageNameIDService
            Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP"
            Location="https://LoadBalancer-3.example.com:9443/amserver/
               IDPMniSoap/metaAlias/idp"/>
        <NameIDFormat>
            urn:oasis:names:tc:SAML:2.0:nameid-format:persistent
        </NameIDFormat>
        <NameIDFormat>
            urn:oasis:names:tc:SAML:2.0:nameid-format:transient
        </NameIDFormat>
        <SingleSignOnService
            Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect"
            Location="https://LoadBalancer-3.example.com:9443/amserver/
                SSORedirect/metaAlias/idp"/>
        <SingleSignOnService
            Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP"
            Location="https://LoadBalancer-3.example.com:9443/amserver/
                SSOSoap/metaAlias/idp"/>
    </IDPSSODescriptor>
</EntityDescriptor>
```
{% /version %}
