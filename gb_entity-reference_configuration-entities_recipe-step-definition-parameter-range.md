# Recipe Step Definition Parameter Range

## Summary

### Entity Name

Recipe Step Definition Parameter Range

### Database Table Name

`tRecipeParameterRange`

### API Object Name

`DbRecipeParameterRange`

### Entity Description

RSD Parameter Range specifies a Parameter value for a specific Batch size (range).

## Properties

`Recipe Parameter [ RecipeParameterID ]`

Specifies the parent Recipe Parameter.

`Batch Size Start Units [ RangeStartUnits ]`

The lower end of the size range for this entry.

`Batch Size End Units [ RangeEndUnits ]`

The upper end of the size range for this entry.

`Value [ Value ]`

The value that will be assigned for the parent Parameter if the current Batch size falls between the configured Start and End Unit range.
