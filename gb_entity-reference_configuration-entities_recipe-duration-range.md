# Recipe Duration Range

## Summary

### Entity Name

Recipe Duration Range

### Database Table Name

`tRecipeDurationRange`

### API Object Name

`DbRecipeDurationRange`

### Entity Description

A Recipe Duration Range helps specify the planned duration of the overall Recipe in relation to the Batch's planned size.

## Properties

`Recipe [ RecipeID ]`

Specifies the parent Recipe.

`Batch Size Start Units [ RangeStartUnits ]`

The lower end of the size range for this entry.

`Batch Size End Units [ RangeEndUnits ]`

The upper end of the size range for this entry.

`Duration Seconds [ DurationSeconds ]`

If the Batch's planned size falls between the Start and End Units specified above, the planned duration of the Batch will be set with this value.
