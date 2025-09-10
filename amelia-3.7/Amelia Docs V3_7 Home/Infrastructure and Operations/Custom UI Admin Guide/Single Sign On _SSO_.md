As of Custom UI version 5.5.2, it is possible to use single sign on (SSO) to log in to a custom user interface regardless of the device.
# Non-Mobile Devices
If the ssoImmediateRedirect parameter in the config.json file is set to true, upon successful login the user will be returned to the original custom user interface. If the parameter is set to false, the user will see the login page.
# Mobile Devices
For mobile devices, there are a number of parameter settings in the config.json file.
-   To keep the user on the login page, set the mobileSSODisabled parameter to true.
-   To hide the login email and password fileds, set the hideLoginOnMobile parameter to true.
-   To provide the option to select anonymous Amelia domains, set the allowAnonymous parameter to true.
-   To prevent an immediate redirect to single sign on, set the ssoImmediateRedirect parameter to false.
-   To only show the single sign on button, set the showSSOButton parameter to true.
-   To hide domains from the login screen, set the showAnonymousDomains parameter to true.
Refer to Customize UI with config.json for details about how to hide login pages and anonymous domains.
