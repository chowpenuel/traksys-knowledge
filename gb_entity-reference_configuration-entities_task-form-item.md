# Task Form Item

## Summary

### Entity Name

Task Form Item

### Database Table Name

`tTaskFormItem`

### API Object Name

`DbTaskFormItem`

### Entity Description

A Task Form Item represents a single piece of data that is to be recorded with a Task record. Task Form Items are grouped using Task Form Item Groups and then assigned to Task Definitions.

## Properties

`Key [ Key ]`

The unique string that identifies this Task Form Item.

`Data Type [ Data Type ] : ETS.Core.Enums.DataType`

Indicates that Data Type for the value specified for the Task Form Item.

`Prompt [ Prompt ]`

Specifies a text string that is displayed on the standard Task Forms as the label to the form input. If blank, the Name property is used as the prompt.

`Width [ WidhtBs ]`

Specifies a bootstrap width (1-12) used to size the label and input on the standard Task Form render.

`Default Value [ DefaultValue ]`

Specifies the default value that may appear in the entry field for this Task Form Item when displayed for input.

`Require Change [ ValidateChange ]`

Marks this item as requiring the user to change the value of this input to something different than the Default Value before saving. Note that is only a suggested setting, the actual user interface validation behavior must be implemented.

`Minimum / Maximum [ ValidateMinimum and ValidateMaximum ]`

Indicates the suggested minimum and maximum values for this input. Note these are only suggested settings; the actual user interface validation behavior must be implemented.

`Is Conditional [ IsConditional ]`

Specifies whether conditional statements will be applied to the Task Form Item.

`Condition [ Condition ]`

Contains the Conditional statements that will be used for the Task Form Item.

`Render Type [ RenderType ] : ETS.Core.Enums.TaskFormItemRenderType`

Specifies the UI control that will be used for the current Task Form Item.

`Render Custom Key [ RenderCustomKey ]`

Specifies the Custom Content Part Key that will be used to display the control. This option will only appear when the Render Type is set to Custom.

`Permission Key [ PermissionKey ]`

Allows users to specify a Permission Key to grant access or deny completion of specific Task Form Items on a per-user basis.
