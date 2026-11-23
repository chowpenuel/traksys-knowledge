# Command Line Options

The TrakSYS Installation Manager includes several command line argument options that can be leveraged in order to automate deployments and other tasks.

## Format

```powershell
InstallationManager.exe <CommandName> [<CommandOptions>] [<StandardOptions>]
```

## Standard Options

### Normal UI Mode (Default)

The Installation Manager Graphical User Interface is launched as part of command execution. The specified command is run with its status displayed through the standard UI which is closed upon successful completion. If there are errors the UI will remain open. This mode is useful for running commands in an ad hoc manner.

#### Normal UI Mode Options

* `-ConfirmClose` - User Interface will not close following command execution even if successful.

### Silent Mode

`-Silent`

The Installation Manager Graphical User Interface is not launched as part of command execution, the main output will be to the Console.

#### Silent Mode Options

* `[-OutFile <path>]` - Logs the output to the specified file.
* `[-Verbose]` - Some commands can leverage Verbose logging. This is intended mainly for custom TeaGet Package installation scripts.

## Available Commands

```powershell
Add-CustomSequence -Sequence <sequenceName> [-MaxValue <maxValue:long= 2147483647>] [-StartingValue <startingValue:long=0>]

Debug-Echo -Echo <message:string>

Export-Config -File <exportFilePath:string> [ -All | -UI | -Config ] [-SiteID <siteID:int=-1>]

Import-Config -File <importFilePath:string>

Install-TeaGetPackage <PackageName> [-Version <version:string=latest>] [-Force]

Reset-Calendar

Reset-Sequence

Resync-TeaGetPackage [-All | -TsBin | -Root ]

Uninstall-TeaGetPackage <PackageName>
```

### Example

Executing the `Debug-Echo` command and logging the output to a file.

```powershell
InstallationManager.exe Debug-Echo -Echo "Hello World" -Silent -OutFile "C:\Logs\CliLog.txt"
```

## PowerShell

In order to facilitate the execution of command line arguments from PowerShell, a script file is included (relative path: \~\TrakSYS\ps\TsPowershellUtils.ps1). By referencing this script file, any of the commands listed above can be called from a custom PowerShell script via the `Invoke-TsInstallManCommand` function.

### Example

Executing the `Debug-Echo` command from a custom PowerShell file, without logging the output to a file.

```powershell
#Requires -RunAsAdministrator

. "C:\Program Files (x86)\Parsec\TrakSYS\ps\TsPowershellUtils.ps1"

Invoke-TsInstallManCommand -cliArgs "Debug-Echo -Echo ""Hello World"" -Silent" -cliName "Debug-Echo"
```

Resulting output:

```markdown
Running TrakSYS Debug-Echo

Creating Chore Debug-Echo...
The value of -echo is 'Hello World'.
```

### Available PowerShell Functions

In addition to `Invoke-TsInstallManCommand`, the TrakSYS PowerShell script file also provides several other common functions.

```powershell
Export-TsConfig -ExportFile <filename> [-LogFile <logfile>] [-SiteID <SiteID:int>] [-All] [-UI]

Import-TsConfig -ImportFile <filename> [-LogFile <logfile]

Reset-TsCalendar

Install-TeaGetPackage -PackageName <packagename> [-Version [<version>]] [-Force] [-Verbose]

Uninstall- TeaGetPackage -PackageName <packagename>

Clean-TsLibraries [-All|-Root|-TsBin]
```
