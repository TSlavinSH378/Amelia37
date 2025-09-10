-   [Create a Custom Whitelist Configuration File](#AppendixB:BPNScriptSandboxingandWhitelists-CreateaCustomWhitelistConfigurationFile)
    -   [Selecting Items to Import](#AppendixB:BPNScriptSandboxingandWhitelists-SelectingItemstoImport)
    -   [Sample whitelist.config File](#AppendixB:BPNScriptSandboxingandWhitelists-Samplewhitelist.configFile)
-   [Install a Custom Whitelist Configuration File](#AppendixB:BPNScriptSandboxingandWhitelists-InstallaCustomWhitelistConfigurationFile)
-   [Modify Application Properties to Enable a Whitelist](#AppendixB:BPNScriptSandboxingandWhitelists-ModifyApplicationPropertiestoEnableaWhitelist)
    -   [application.yml Example](#AppendixB:BPNScriptSandboxingandWhitelists-application.ymlExample)
    -   [application.properties Example](#AppendixB:BPNScriptSandboxingandWhitelists-application.propertiesExample)
-   [Restart Amelia Engine](#AppendixB:BPNScriptSandboxingandWhitelists-RestartAmeliaEngine)
-   [Troubleshooting](#AppendixB:BPNScriptSandboxingandWhitelists-Troubleshooting)
By default, all scripts within a BPN are executed within a secure sandbox within the Amelia engine, whether code that appears directly in a BPN Script task or a script library script. The sandbox prevents malfunctioning or malicious code from doing damage.
The sandbox constrains which:
-   Classes can be imported
-   Constructors can be invoked on imported classes
-   Instance methods can be invoked on imported classes
-   Static methods can be invoked on imported classes
-   Static fields (constants) can be accessed on imported classes
The default constraints are controlled by an internal *whitelist* configuration. Anything not in the whitelist cannot be used. If the default whitelist is too restrictive, however, the whitelist can be extended with a custom whitelist configuration file, as described below.
Sandboxing/Whitelist issues manifest themselves as script states that will not execute in BPNs. Issues can be identified by tailing the Amelia Engine logs then finding two messages, one after another:
``` groovy
Script is unsafe. 
Execution error detected. Error message: Groovy scripts are not allowed to call instance method <insert whatever bad thing you're trying to do here>
```
# Create a Custom Whitelist Configuration File
Adding packages, classes, and other code can be executed securely by creating a whitelist configuration file to Amelia's file system. The file name should be `whitelist.config` and be stored in the `/apps/IPsoft/amelia/amelia-common-config/scripting/groovy/sandbox/` folder, as described in the next section.
## Selecting Items to Import
Do not put whitelist items in the external config file unless the default one can't satisfy the requirement.
The import should always start from a narrower scoped import to a wider range import. For example: 
-   If any class in a package needs to be blacklisted, the starImport should not be used, instead, put all the remaining needed whitelisted classes under that package manually by usingclassImport. 
-   Similarly, if not all methods of a certain class are needed, do not use a whole classImport, put all needed whitelisted methods with corresponding parameters to the external config file by using staticMethod or method import.
-   There should be no overlapping in the configuration, otherwise the wider range import will override the more specific ones.
## Sample whitelist.config File
**Sample whitelist.config Whitelist Configuration File**
``` groovy
# Star imports (white list all classes under the package)
starImport java.util.regex
starImport java.util
# Concrete class imports (any interesting classes under not start-imported package must be whitelisted here)
classImport java.lang.Byte
classImport java.lang.CharSequence
# Static methods and fields, instance methods, and constructors
staticMethod com.cloudbees.groovy.cps.CpsDefaultGroovyMethods each java.util.Iterator groovy.lang.Closure
staticMethod groovy.json.JsonOutput prettyPrint java.lang.String
staticMethod groovy.json.JsonOutput toJson java.lang.Boolean
new groovy.json.JsonSlurper
new groovy.json.JsonSlurperClassic
method groovy.json.JsonSlurper parseText java.lang.String
method groovy.lang.Binding hasVariable java.lang.String
staticField groovy.lang.Closure DELEGATE_FIRST
staticField groovy.lang.Closure DELEGATE_ONLY
```
Possible script types are described in the table below. Formats are case-sensitive.
Table. Custom Whitelist Configuration File Format Options

| Element Type | Format | Example | Description |
| ----|----|----|----|
| Package | starImport<one space>packageName | starImport java.math | Whitelists all constructors, staticFields, staticMethods, and instanceMethods of all classes in a package |
| Class | classImport<one space>className | classImport java.lang.StringBuilder | Whitelists all constructors, staticFields, staticMethods, and instanceMethods of a class |
| Static Method | staticMethod<one space>className<one space>staticMethodName(<one space>parameter1ClassName<one space>parameter2ClassName) | staticMethod groovy.json.JsonOutput prettyPrint java.lang.String (1 parameter)staticMethod org.codehaus.groovy.runtime.DefaultGroovyMethods contains int[] java.lang.Object (2 parameters here: int[] and java.lang.Object) | Parameter is optional. Whitelists only specified staticMethods of a class. |
| Instance Method | method<one space>className<one space>methodName(<one space>parameter1ClassName<one space>parameter2ClassName) | method java.lang.String length (no parameter)method java.lang.String charAt int (1 parameter) | Parameter is optional. Whitelists only specified instanceMethods of a class. |
| Constructor | new<one space>className(<one space>parameter1ClassName<one space>parameter2ClassName) | new java.util.Date (no parameter)new java.util.Date long (1 parameter) | Parameter is optional. Whitelists only specified constructors of a class. |
| Static Field | staticField<one space>className<one space>fieldName | staticField java.util.Locale CANADA | Whitelists only specified staticFields of a class. |

# Install a Custom Whitelist Configuration File
Once a whitelist configuration file is defined, use a CLI tool to create a sandbox directory and configuration file then set permissions and restart two services.
> [!warning]  
>
> Before executing these steps, confirm the `scripting/groovy/sandbox` folder structure does not exist and the `whitelist.config` file is not in the `/sandbox` folder.

1.  Create a sandbox directory.
    ``` groovy
    mkdir -p /apps/IPsoft/amelia/amelia-common-config/scripting/groovy/sandbox
    ```
2.  In the sandbox directory, create a whitelist.config text file and add configuration settings, as described above.
3.  Change owner and permissions for directories and files as amelia:amelia.
    ``` groovy
    chown -R amelia:amelia /apps/IPsoft/amelia/amelia-common-config/scripting
    chown -R amelia:amelia /apps/IPsoft/amelia/amelia-common-config/scripting/groovy/sandbox/whitelist.config
    chmod 600 /apps/IPsoft/amelia/amelia-common-config/scripting/groovy/sandbox/whitelist.config
    ```
# Modify Application Properties to Enable a Whitelist
Depending on an instance setup, the application properties files may be listed as `application.yml`**` `**or `application.properties`**  
**Regardless of the file type, they should be located in the `/apps/IPsoft/amelia/amelia-common-config/` folder structure.
## application.yml Example
It's possible the `application.yml` file does not exist and will need to be created. Edit the `application.yml` file in the `/apps/IPsoft/amelia/amelia-common-config/` folder and add the following lines:
**application.yml Config Example**
``` xml
amelia:
  bpn:
    groovy:
      sandbox:
        conf:
          path: /apps/IPsoft/amelia/amelia-common-config/scripting/groovy/sandbox
        whitelist:
          filename: whitelist.config
```
> [!warning]  
>
> The hierarchy for the .yml file is likely already created. Therefore, add only the sections starting with `bpn` and below.

## application.properties Example
Edit the **application.properties **file and add the following lines:
**application.properties Config Example**
``` groovy
amelia.bpn.groovy.sandbox.conf.path=/apps/IPsoft/amelia/amelia-common-config/scripting/groovy/sandbox
amelia.bpn.groovy.sandbox.whitelist.filename=whitelist.config
```
# Restart Amelia Engine
Once the steps above are completed, restart Amelia Engine for the config changes to take effect. Restart `amelia-engine-service@p00x` (where x is the pod number) and then restart the `amelia-admin-web` service.
``` groovy
systemctl restart amelia-engine-service@p00x amelia-admin-web
```
# Troubleshooting
-   Test the script state for functionality after the whitelist is added and the engine-service and admin-web restarted.
-   The whitelist might need to be updated several times to ensure classes/modules are added appropriately as script states are tested.
-   Adding an entire class loads methods that may not be needed. Add specific additions to the whitelist before adding an entire class.
