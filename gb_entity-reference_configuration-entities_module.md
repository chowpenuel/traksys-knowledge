# Module

## Summary

### Entity Name

Module

### Database Table Name

`tModule`

### API Object Name

`DbModule`

### Entity Description

A Module is a collection of business rules that can be executed by the Data Management service. A Module can contain one or more Module Steps with specific functionalities. Modules can be executed manually via script, or automatically based on a configured schedule.

## Properties

`Script DLLs [ ScriptDlls ]`

A list of .NET assembly DLLs to be used as references for any of the Module's code. Multiple DLLs can be specified separated by comma. The list should contain the file name of the DLL only (not the fill path). The actual DLL files should to be placed in TrakSYS installation root directory (`<Program Files>\Parsec\TrakSYS`).

`Trigger Key [ TriggerKey ]`

The unique string identifier used for manually triggering the Module execution. Modules can be triggered by inserting a new row into the tModuleTrigger table with the appropriate Key using the API or using direct SQL.

`Trigger Mode [ TriggerMode ] : ETS.Core.Enums.TriggerModeType`

Specifies when the Module is to be executed.

* **None** = 0
* **Periodic** = 1
* **Daily** = 2

**None** - In this mode, the Module is never automatically executed. This setting is used when the execution is to manually driven via API.

**Periodic** - In this mode, the Module is executed periodically based on the Trigger Period setting defined below.

**Daily** - In this mode, the Module is executed once daily at the time specified by the Period Time setting below.

`Trigger Time [ TriggerTime ]`

When the Trigger Module setting above is set to Daily, this property specifies the time of day when the Module will be executed.

`Execute on Days [ Mon ] [ Tue ] [ Wed ] [ Thu ] [ Fri ] [ Sat ] [ Sun ]`

When the Trigger Module setting above is set to Daily, this property specifies which days of the week this Module will be executed.

`Trigger Period [ PeriodicFrequency ] [ PeriodicInterval ]`

When the Trigger Module setting above is set to Periodic, this property defines when the Module will be executed. Options are Seconds, Minutes and Hours.
