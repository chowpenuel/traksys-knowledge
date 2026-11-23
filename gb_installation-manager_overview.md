# Overview

The Overview section of the TrakSYS Installation Manager displays the status of the various elements of the installation. Additionally, there is an actions menu to interact with global settings of the installation.

## Database \[ {DatabaseServerName}.{DatabaseName} ]

Shows the current status of the database connection.

## License

Shows the current status of the TrakSYS License.

## Services

Shows the current status of the Services and whether they are installed.

## Webs

Shows whether TrakSYS webs and IIS are configured correctly.

## Sites

Shows whether the configuration of TrakSYS Sites is correct.

## Reporting Services

Shows whether SQL Server Reporting Services is reachable and available.

## Diagnostics

Displays any relevant diagnostic warnings or errors.

## Actions

### TrakSYS Settings

Global settings which impact all Sites of the TrakSYS installation. Description for each setting appear at the bottom of the settings dialog. Typically when saving these settings, an IIS restart or a TrakSYS Web Application restart may be needed. The main settings groups include:

* Audit
* Database Transfer
* General
* Historian
* Logging
* Notification
* Reporting Services
* Report Manager (This section is only available for installations that have the Legacy WEBTrak feature line on the TrakSYS license. As of TrakSYS 12.0.0, this section is no longer available)
* Web
* WebAuthOidc (TrakSYS 11.1.1+)
* WebAuthSaml (TrakSYS 12.0.2+)

### Server Expectations

Settings which determine how the Installation Manager will check the state of various components on this server to prevent status checks and inaccurate error messages.

#### Services

Determines which Services Installation Manager should check for upon startup.

#### Reporting Services

Determines if Reporting Services should be by Installation Manager upon startup.

### Version Information

Displays installation details and version information including:

* Database Server
* License Serial Number
* TrakSYS Version
* TrakSYS Database Version
* Host Information
* Server Name
* Outcome of TrakSYS Directory check
* Outcome of TrakSYS Directory\TS check

Additional details can be viewed by clicking the Results button in the bottom left. An export option is also available via the Export button in the bottom left of the Results dialog.
