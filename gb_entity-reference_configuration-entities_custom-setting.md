# Custom Setting

## Summary

### Entity Name

Custom Setting

### Database Table Name

`tCustomSetting`

### API Object Name

`DbCustomSetting`

### Entity Description

The tCustomSetting table is used to save custom configuration and UI settings to TrakSYS, and is purely for extensibility purposes.

## Properties

`Data Text [ DataText ]`

String configuration of data type nvarchar(max) is stored here. The ideal formats are json, xml or yaml.

`Data Binary [ DataBinary ]`

Varbinary(max) data type that is stored here.

`Is Ui [ IsUi ]`

Determines if this is a UI setting.

`Is Config [ IsConfig ]`

Determines if this is a configuration setting.

`Eval Order [ EvalOrder ]`

Determines the evaluation order of the setting.
