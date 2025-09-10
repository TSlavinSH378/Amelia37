# Overview
Text-to-speech (TTS) installation is a requirement for speech synthesis in Amelia. Multiple TTS voice engines may be installed to facilitate synthesis of audio to satisfy specified language requirements. Microsoft Internet Information Services (IIS) receives encoding requests and also serves the front-end content.
An Amelia instance running on Linux also needs a TTS-related property configured to point to the speech URL available on the IIS server.
# Minimum Server Specifications
Input/Output (I/O) performance is an important consideration. For both physical and virtualized servers, SSD backed storage is highly recommended to minimize audio encoding time.
Table.  Minimum Recommended Server Specifications

| OS |
| ----|
| Windows 2012r2 64bit |
| 8 |
| 8GB |
| 100GB |

# Prerequisites
-   Licensed TTS voice
-   Administrative rights
-   Port 443 (https) access for Amelia host
-   .NET framework 4.5+
-   SAPI 5.1+ (system default on w2k12)
-   IPsoft Centralized Installation package
-   Amelia instance available on a Linux server
Connectivity between the Amelia TTS server (Windows) and Amelia instance (Linux) must be configured for ports 443 and 80.
Property settings in Amelia’s application.properties file also must be configured. The file is located in the /apps/IPsoft/amelia/amelia-common-config folder.
-   The `amelia.tts.speech-base-url` property must be set to `https://${hostname}/Speech`.
-   If the default voice is not used, the `amelia.tts.<language_code>` property must be set to the Voice value for the language code of a location. For example, `amelia.tts.voices.en=Liv` sets the US English voice property to use the Norwegian voice. Language codes and Voices are listed below.
# Installation Package
The IPsoft base TTS installation package contains a batch file (.bat) that installs then enables Windows server features and copies binaries to the proper locations.
## Download Package
The package can be downloaded from artifactory.ipsoft.com using credentials used for docs.ipsoft.com. If login fails or the artifact is not visible, please contact your IPsoft Project Manager or Engagement Manager. The installation package can be downloaded here:
https://artifactory.ipsoft.com/artifactory/webapp/#/artifacts/browse/tree/General/amelia-tts/tts_iis_base_install.zip
## Zone Identifier File
NTFS filesystems add extra security metadata to the file in the form of a Zone.Identifier. This causes security problems with component installation downstream as unzipped files may inherit these restrictions.
For additional details on Zone.Identifier https://msdn.microsoft.com/en-us/library/dn392609.aspx
To determine if the Zone.Identifier file exists, in the cmd prompt, type:
``` groovy
dir /r <filename>
```
If the file has the extra metadata it will look like the following:
``` groovy
<filename>
<filename>:Zone.Identifier:$DATA
```
This will need to be removed before the installation process begins. Streams can be downloaded here to remove the Zone.Identifier <https://technet.microsoft.com/en-us/sysinternals/streams.aspx>.
``` groovy
usage example:
streams.exe -d -s <filename|directory>
```
Alternatively, the same can be done manually in Explorer. Right click the Zone.Identifier file to unblock:
Properties -\> General
      Security:  Unblock
> [!info]  
>
> Unlike streams which permanently deletes this metadata, Explorer does not permanently delete the Zone data and settings will not persist when copied to other filesystems.
> [!warning]  
>
> Unblock the zip `tts_iis_base_install.zip` file. The `Streams.exe` file also is included in the installation package.

# Batch File Installation
To install with the batch file script:
1.  Copy `tts_iis_base_install.zip` to the target server
2.  Unblock the ZIP file (if not blocked continue)
3.  Extract ZIP file locally on target server
4.  Open the extracted folder, and double-click on `install_amelia.bat`
5.  If User Account Control is turned on, a prompt to execute PowerShell in an elevated session will be displayed. Click Yes.
6.  The installer will execute a series of Powershell cmdlets. If .NET is upgraded reboot may be required. Let the install finish and reboot after.
The tasks in the batch file script are self-documented and perform these steps:
1.  Starts PowerShell.
2.  Runs `tts_base_install.ps1`.
3.  Installs or upgrades to latest available .NET 4.x version.
4.  Installs Webserver and application feature components.
5.  Copy files in `IPspeechResources\IPspeech` to `C:\inetpub\wwwroot\IPspeech`.
6.  Copy files in `IPspeechResources\IPsoft` to `C:\IPsoft`.
7.  Set ACL for IIS_IUSR (`r,w,x`) on `C:\IPsoft and C:\inetpub\wwwroot\IPspeech\speechonly`.
8.  Delete the Default Web Site that’s created when installing the Web Server role.
9.  Create the IPspeech website, and point it to `C:\inetpub\wwwroot\IPspeech`. Bind the website to port 80 and restarts IIS.
10. Create a scheduled task in task scheduler under `\IPsoft\IPspeech` to delete TXT, WAV, and JSON files in `C:\inetpub\wwwroot\IPspeech\speechonly\` directory that are older than 5 days. Task runs daily at 10PM.
# Manual Installation
If any of the above steps fail, the manual install steps are included below. In the event that the TTS licenses are not installed the audio files will be prepended with a demo statement.
**Install TTS Engines (setup.exe)**
1.  Generate Neospeech License File from Software Key at http://verification.neospeech.com.
2.  Enter License Key (20 digit key from vendor).
3.  Enter the primary NIC MAC address of the host the voice is installing on
    ``` groovy
    ipconfig /all
    ```
4.  Click Retrieve License and save to file. Copy this file to the install host.
**Install Neospeech Voices 32bit binary**
1.  Copy license `verification.txt` `$installdir\$voice\M16-SAPI5\data-common\verify\`
2.  For English we have a lexicon with custom word and IPA pronunciations. Copy `userdict_eng.csv` to `$installdir\Julie\M16-SAPI5\data-common\userdict\`
**  
**
**Install 32-bit binary Ivona Voices**
Using installer at the prompt for licensing – Use a license key (license key file provided by vendor)
**  
**
**Install FaceFx Binary**
1.  Copy `IPspeechResources\IPsoft\` to `C:\IPsoft\`
2.  Change Permissions on `C:\IPsoft` to IIS_USRS (allow write):  
    IIS_USRS (allow write)
**  
**
**Test one of the voices**
1.  Time and run test in PowerShell:
    ``` groovy
    cd \IPsoft\amelia\facefx\
    ```
2.  Time and run test in PowerShell:
    ``` groovy
    {start-process .\FxTTSAPI.exe '"VW Julie" test.txt' -WAIT}
    ```
    If TTS has a valid license the output wav should be ~44k. If it is significantly \>44k, then the TTS is unlicensed. If you listen to the WAV it should just say "Hello there."
    Unlicensed will have an additional demo message.
**Install .NET 4.5+**
``` groovy
Dism /online /Enable-Feature /FeatureName:NetFx4 /All
```
**Install Server Roles**
Window Server 2012
``` groovy
Install-WindowsFeature -name Application-Server, AS-NET-Framework, AS-Web-Support, NET-Framework-45-Core, Web-Server,Web-Dyn-Compression, Web-App-Dev, Web-Net-Ext45, Web-Asp-Net45 -IncludeManagementTools
```
Windows Server 2016
``` groovy
Install-WindowsFeature -name NET-Framework-45-Core, Web-Server, Web-Dyn-Compression, Web-App-Dev, Web-Net-Ext45, Web-Asp-Net45 -IncludeManagementTools
```
**Copy IPspeech files**
Copy the `IPspeechResources\IPspeech` files to `C:\inetpub\wwwroot\IPspeech`
**Website Configuration in IIS Manager**
Use IIS Manager to configure the IPspeech site and set permissions.
1.  Configure Site  
    IPspeech : 80
    -\> C:\inetpub\wwwroot\IPspeech  
2.  Change Permissions on `C:\inetpub\wwroot\IPspeech\speechonly`  
    IIS_USRS (allow write)  
3.  Restart IIS
**Configure cleanup scripts**
Use the Windows Scheduler to configure the cleanup scripts.
Daily
Remove (txt\|json\|wav) files older than 15 mins
# Additional Permissions/Validation
-   Anonymous authentication on WebSite uses AppPool identity.
-   Application Pool Identity is a system service account. In most cases
-   IIS `APPPOOL\DefaultAppPool` needs NTFS permissions to be setup:
    ``` groovy
    (Read) C:\inetpub\wwwroot\IPspeech
    (Modify) C:\inetpub\wwwroot\IPspeech\speechonly
    (Modify) C:\IPsoft\amelia\facefx
    ```
# Functional Verification from Browser
http://localhost/test.html
Voice: VW Julie
Text: any string
Response should be a JSON object similar to this example.
``` groovy
{ "id":"speech_6eee2864-5093-4439-b980-755b6fd0fca2",
"anim":"speech_6eee2864-5093-4439-b980-755b6fd0fca2.json",
"audio":"speech_6eee2864-5093-4439-b980-755b6fd0fca2.wav"
}
```
To listen to the audio file use the value for the audio key returned from the JSON object.
``` groovy
http://localhost/speechonly/speech_6eee2864-5093-4439-b980-755b6fd0fca2.wav
```
# Monitoring
Default Server + IIS and app server monitoring:
-   PING
-   CPU
-   DISK
-   MEM
-   Processes (IIS)
-   TCP (HTTP)
# Supported Languages
All voices are female.   
Table. Supported Voices and Languages

| 
 | Language | Language Code | Voice | Vendor | Legacy Voice | Legacy Vendor |
| ----|----|----|----|----|----|----|
| 1 | English (American) | en | VW Julie | Neospeech | VW Julie | NeoSpeech |
| 2 | Japanese | ja |  |  | VW Misaki | NeoSpeech |
| 3 | Chinese (Mandarin) | zh |  |  | VW Hui | NeoSpeech |
| 4 | Korean | ko |  |  | VW Yumi | NeoSpeech |
| 5 | French | fr | Céline | Ivona (Amazon) | Florence | Loquendo (Nuance) |
| 6 | French (Canadian) | fr | Chantal | Ivona (Amazon) |  |  |
| 7 | Swedish | sv | Astrid (US)Maja (EU) | Ivona (Amazon)rSpeak | Annika | Loquendo (Nuance) |
| 8 | Norwegian | no | Liv | Ivona (Amazon) | Vilde | Loquendo (Nuance) |
| 9 | Spanish (American) | es | Penélope | Ivona (Amazon) | Ximena | Loquendo (Nuance) |
| 10 | Spanish (Castilian) | es | Conchita | Ivona (Amazon) |  |  |
| 11 | Danish | da | Naja | Ivona (Amazon) | Frida | Loquendo (Nuance) |
| 12 | Arabic | ar |  |  | Laila | Loquendo (Nuance) |
| 13 | Russian | ru | Tatyana | Ivona (Amazon) | Olga | Loquendo (Nuance) |
| 14 | Dutch | nl | Lotte | Ivona (Amazon) | Saskia | Loquendo (Nuance) |
| 15 | Italian | it | Carla | Ivona (Amazon) | Silvana | Loquendo (Nuance) |
| 16 | Turkish | tr | Filiz | Ivona (Amazon) | Zeynep | Loquendo (Nuance) |
| 17 | Polish | pl | Maja | Ivona (Amazon) | Zoisa | Loquendo (Nuance) |
| 18 | Portuguese | pt |  | Ivona (Amazon) | Amalia | Loquendo (Nuance) |
| 19 | Portuguese (Brazilian) | pt | Vitória | Ivona (Amazon) |  |  |
| 20 | German | de | Marlene | Ivona (Amazon) | Katrin | Loquendo (Nuance) |
| 21 | Romanian | ro | Carmen | Ivona (Amazon) | Ioana | Loquendo (Nuance) |
| 22 | Icelandic | is | Dóra | Ivona (Amazon) |  |  |
| 23 | Welsh | cy | Gwyneth | Ivona (Amazon) |  |  |

# Windows 2012 Roles
To display the installed roles for a Windows 2012 server, use the get-windowsfeature command in PowerShell.
``` groovy
Display Name                                            Name                       Install State
------------                                            ----                       -------------
[X] Application Server                                  Application-Server             Installed
    [X] .NET Framework 4.5                              AS-NET-Framework               Installed
    [ ] COM+ Network Access                             AS-Ent-Services                Available
    [ ] Distributed Transactions                        AS-Dist-Transaction            Available
        [ ] WS-Atomic Transactions                      AS-WS-Atomic                   Available
        [ ] Incoming Network Transactions               AS-Incoming-Trans              Available
        [ ] Outgoing Network Transactions               AS-Outgoing-Trans              Available
    [ ] TCP Port Sharing                                AS-TCP-Port-Sharing            Available
    [X] Web Server (IIS) Support                        AS-Web-Support                 Installed
    [ ] Windows Process Activation Service Support      AS-WAS-Support                 Available
        [ ] HTTP Activation                             AS-HTTP-Activation             Available
        [ ] Message Queuing Activation                  AS-MSMQ-Activation             Available
        [ ] Named Pipes Activation                      AS-Named-Pipes                 Available
        [ ] TCP Activation                              AS-TCP-Activation              Available
[X] Web Server (IIS)                                    Web-Server                     Installed
    [X] Web Server                                      Web-WebServer                  Installed
        [X] Common HTTP Features                        Web-Common-Http                Installed
            [X] Default Document                        Web-Default-Doc                Installed
            [X] Directory Browsing                      Web-Dir-Browsing               Installed
            [X] HTTP Errors                             Web-Http-Errors                Installed
            [X] Static Content                          Web-Static-Content             Installed
            [X] HTTP Redirection                        Web-Http-Redirect              Installed
            [ ] WebDAV Publishing                       Web-DAV-Publishing             Available
        [X] Health and Diagnostics                      Web-Health                     Installed
            [X] HTTP Logging                            Web-Http-Logging               Installed
            [ ] Custom Logging                          Web-Custom-Logging             Available
            [X] Logging Tools                           Web-Log-Libraries              Installed
            [ ] ODBC Logging                            Web-ODBC-Logging               Available
            [X] Request Monitor                         Web-Request-Monitor            Installed
            [ ] Tracing                                 Web-Http-Tracing               Available
        [X] Performance                                 Web-Performance                Installed
            [X] Static Content Compression              Web-Stat-Compression           Installed
            [X] Dynamic Content Compression             Web-Dyn-Compression            Installed
        [X] Security                                    Web-Security                   Installed
            [X] Request Filtering                       Web-Filtering                  Installed
            [X] Basic Authentication                    Web-Basic-Auth                 Installed
            [ ] Centralized SSL Certificate Support     Web-CertProvider               Available
            [X] Client Certificate Mapping Authentic... Web-Client-Auth                Installed
            [X] Digest Authentication                   Web-Digest-Auth                Installed
            [X] IIS Client Certificate Mapping Authe... Web-Cert-Auth                  Installed
            [X] IP and Domain Restrictions              Web-IP-Security                Installed
            [X] URL Authorization                       Web-Url-Auth                   Installed
            [X] Windows Authentication                  Web-Windows-Auth               Installed
        [X] Application Development                     Web-App-Dev                    Installed
            [ ] .NET Extensibility 3.5                  Web-Net-Ext                    Available
            [X] .NET Extensibility 4.5                  Web-Net-Ext45                  Installed
            [ ] Application Initialization              Web-AppInit                    Available
            [ ] ASP                                     Web-ASP                        Available
            [ ] ASP.NET 3.5                             Web-Asp-Net                    Available
            [X] ASP.NET 4.5                             Web-Asp-Net45                  Installed
            [ ] CGI                                     Web-CGI                        Available
            [X] ISAPI Extensions                        Web-ISAPI-Ext                  Installed
            [X] ISAPI Filters                           Web-ISAPI-Filter               Installed
            [ ] Server Side Includes                    Web-Includes                   Available
            [ ] WebSocket Protocol                      Web-WebSockets                 Available
    [ ] FTP Server                                      Web-Ftp-Server                 Available
        [ ] FTP Service                                 Web-Ftp-Service                Available
        [ ] FTP Extensibility                           Web-Ftp-Ext                    Available
    [ ] IIS Hostable Web Core                           Web-WHC                        Available
    [X] Management Tools                                Web-Mgmt-Tools                 Installed
        [X] IIS Management Console                      Web-Mgmt-Console               Installed
        [ ] IIS 6 Management Compatibility              Web-Mgmt-Compat                Available
            [ ] IIS 6 Metabase Compatibility            Web-Metabase                   Available
            [ ] IIS 6 Management Console                Web-Lgcy-Mgmt-Console          Available
            [ ] IIS 6 Scripting Tools                   Web-Lgcy-Scripting             Available
            [ ] IIS 6 WMI Compatibility                 Web-WMI                        Available
        [X] IIS Management Scripts and Tools            Web-Scripting-Tools            Installed
        [ ] Management Service                          Web-Mgmt-Service               Available
[X] .NET Framework 4.5 Features                         NET-Framework-45-Fea...        Installed
    [X] .NET Framework 4.5                              NET-Framework-45-Core          Installed
    [X] ASP.NET 4.5                                     NET-Framework-45-ASPNET        Installed
    [X] WCF Services                                    NET-WCF-Services45             Installed
        [ ] HTTP Activation                             NET-WCF-HTTP-Activat...        Available
        [ ] Message Queuing (MSMQ) Activation           NET-WCF-MSMQ-Activat...        Available
        [ ] Named Pipe Activation                       NET-WCF-Pipe-Activat...        Available
        [ ] TCP Activation                              NET-WCF-TCP-Activati...        Available
        [X] TCP Port Sharing                            NET-WCF-TCP-PortShar...        Installed
```
# Windows 2016 Roles
To display the installed roles for a Windows 2016 server, use the get-windowsfeature command in PowerShell.
``` groovy
Display Name                                            Name                       Install State
------------                                            ----                       -------------
[X] Web Server (IIS)                                    Web-Server                     Installed
    [X] Web Server                                      Web-WebServer                  Installed
        [X] Common HTTP Features                        Web-Common-Http                Installed
            [X] Default Document                        Web-Default-Doc                Installed
            [X] Directory Browsing                      Web-Dir-Browsing               Installed
            [X] HTTP Errors                             Web-Http-Errors                Installed
            [X] Static Content                          Web-Static-Content             Installed
            [ ] HTTP Redirection                        Web-Http-Redirect              Available
            [ ] WebDAV Publishing                       Web-DAV-Publishing             Available
        [X] Health and Diagnostics                      Web-Health                     Installed
            [X] HTTP Logging                            Web-Http-Logging               Installed
            [ ] Custom Logging                          Web-Custom-Logging             Available
            [ ] Logging Tools                           Web-Log-Libraries              Available
            [ ] ODBC Logging                            Web-ODBC-Logging               Available
            [ ] Request Monitor                         Web-Request-Monitor            Available
            [ ] Tracing                                 Web-Http-Tracing               Available
        [X] Performance                                 Web-Performance                Installed
            [X] Static Content Compression              Web-Stat-Compression           Installed
            [X] Dynamic Content Compression             Web-Dyn-Compression            Installed
        [X] Security                                    Web-Security                   Installed
            [X] Request Filtering                       Web-Filtering                  Installed
            [ ] Basic Authentication                    Web-Basic-Auth                 Available
            [ ] Centralized SSL Certificate Support     Web-CertProvider               Available
            [ ] Client Certificate Mapping Authentic... Web-Client-Auth                Available
            [ ] Digest Authentication                   Web-Digest-Auth                Available
            [ ] IIS Client Certificate Mapping Authe... Web-Cert-Auth                  Available
            [ ] IP and Domain Restrictions              Web-IP-Security                Available
            [ ] URL Authorization                       Web-Url-Auth                   Available
            [ ] Windows Authentication                  Web-Windows-Auth               Available
        [X] Application Development                     Web-App-Dev                    Installed
            [ ] .NET Extensibility 3.5                  Web-Net-Ext                    Available
            [X] .NET Extensibility 4.6                  Web-Net-Ext45                  Installed
            [ ] Application Initialization              Web-AppInit                    Available
            [ ] ASP                                     Web-ASP                        Available
            [ ] ASP.NET 3.5                             Web-Asp-Net                    Available
            [X] ASP.NET 4.6                             Web-Asp-Net45                  Installed
            [ ] CGI                                     Web-CGI                        Available
            [X] ISAPI Extensions                        Web-ISAPI-Ext                  Installed
            [X] ISAPI Filters                           Web-ISAPI-Filter               Installed
            [ ] Server Side Includes                    Web-Includes                   Available
            [ ] WebSocket Protocol                      Web-WebSockets                 Available
    [ ] FTP Server                                      Web-Ftp-Server                 Available
        [ ] FTP Service                                 Web-Ftp-Service                Available
        [ ] FTP Extensibility                           Web-Ftp-Ext                    Available
    [X] Management Tools                                Web-Mgmt-Tools                 Installed
        [X] IIS Management Console                      Web-Mgmt-Console               Installed
        [ ] IIS 6 Management Compatibility              Web-Mgmt-Compat                Available
            [ ] IIS 6 Metabase Compatibility            Web-Metabase                   Available
            [ ] IIS 6 Management Console                Web-Lgcy-Mgmt-Console          Available
            [ ] IIS 6 Scripting Tools                   Web-Lgcy-Scripting             Available
            [ ] IIS 6 WMI Compatibility                 Web-WMI                        Available
        [ ] IIS Management Scripts and Tools            Web-Scripting-Tools            Available
        [ ] Management Service                          Web-Mgmt-Service               Available
[X] .NET Framework 4.6 Features                         NET-Framework-45-Fea...        Installed
    [X] .NET Framework 4.6                              NET-Framework-45-Core          Installed
    [X] ASP.NET 4.6                                     NET-Framework-45-ASPNET        Installed
    [X] WCF Services                                    NET-WCF-Services45             Installed
        [ ] HTTP Activation                             NET-WCF-HTTP-Activat...        Available
        [ ] Message Queuing (MSMQ) Activation           NET-WCF-MSMQ-Activat...        Available
        [ ] Named Pipe Activation                       NET-WCF-Pipe-Activat...        Available
        [ ] TCP Activation                              NET-WCF-TCP-Activati...        Available
        [X] TCP Port Sharing                            NET-WCF-TCP-PortShar...        Installed
```
