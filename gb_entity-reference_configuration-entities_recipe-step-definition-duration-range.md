# Recipe Step Definition Duration Range

## Summary

### Entity Name

Recipe Step Definition Duration Range

### Database Table Name

`tRecipeStepDefinitionDurationRange`

### API Object Name

`DbRecipeStepDefinitionDurationRange`

### Entity Description

A Recipe Duration Range helps specify the planned duration of the overall Recipe in relation to the Batch's planned size.

## Properties

`Recipe Step Definition [ RecipeStepDefinitionID ]`

Specifies the parent Recipe Step Definition.

`Batch Size Start Units [ RangeStartUnits ]`

The lower end of the size range for this entry.

`Batch Size End Units [ RangeEndUnits ]`

The upper end of the size range for this entry.

`Duration Seconds [ DurationSeconds ]`

If the Batch's planned size falls between the Start and End Units specified above, the planned duration of the Batch will be set with this value.
