# Webs

The Webs section of the TrakSYS Installation Manager displays information about the current IIS Web and TrakSYS Web configurations.

## Internet Information Services

### IIS Available

Displays whether or not IIS is available on the application server. If available, its version is shown.

### IIS Features

Displays whether or not IIS is configured correctly.

## TS Web

### App Pool

Shows the current TrakSYS Web App Pool name.

### Application

Show where the application resides within the web server hierarchy.

### URL

Displays the URL to TS Web (e.g - `http://{ServerName}/TS`)

## Actions

### Setup TS Web

Executes a script to install the TS Web Application in IIS. Results of the installation may be viewed and exported.

### Remove TS Web

Executes a script to remove the TS Web Application from IIS. Results of the process may be viewed and exported.

### Setup IIS

Executes a PowerShell script to install and configure Internet Information Services (IIS). Additionally, certain Server Roles and Services required to run TrakSYS are installed automatically. The PowerShell script executed by this button typically can be found under `...\Program Files\Parsec\TrakSYS\ps\SetupIis.ps1`.

{% hint style="info" %}
This button will only display in the TrakSYS Installation Manager if TrakSYS does not detect Internet Information Services (IIS) or if it is not correctly configured. If this action needs to be executed and the button does not display, the PowerShell script can be manually executed within Windows using PowerShell ISE.
{% endhint %}
