# Apps

The Apps section of the TrakSYS Installation Manager displays a list of installed TrakSYS Apps and provides App Management options.

## Installed Apps

Displays details regarding the App Name, Version, and File Status of currently installed Apps.

## Actions

### Manage

Displays a dialog to manage Apps. Each App listed will display the installed version and the latest available version. The right side of the dialog contains Install, Uninstall, and Update buttons to perform these operations on the selected App from the list. The Manage dialog includes the following sections:

* Browse - Search or browse for Apps to install from the local directory or the Parsec teaget repository.
* Installed - View a searchable list of installed Apps (this section is displayed by default when clicking Manage).
* Updates - View a searchable list of available updates for installed Apps.

### Resync

This option will resync the binary files for all currently installed TrakSYS Apps. This is normally done after a Database Transfer has been performed and a new version of one or more Apps were pushed to Production. This action should also be performed when a TrakSYS database is restored but the Apps and .dll files are not copied to the new installation.

### Install From File

This option installs TrakSYS Apps contained within an external NuGet or TeaGet package file.
