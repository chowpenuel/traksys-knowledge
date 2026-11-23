# Recipe Step Definition Parameter

## Summary

### Entity Name

Recipe Step Definition Parameter

### Database Table Name

`tRecipeParameter`

### API Object Name

`DbRecipeParameter`

### Entity Description

Recipe Step Definition Parameters allow Recipe specific values to be assigned to pre-defined Function Definition Parameters defined in the equipment model (Areas and Systems). Values for RSD Parameters are assigned to the Tag defined in the Function Definition Parameter when the RSD starts.

## Properties

`Recipe [ RecipeID ]`

Specifies the parent Recipe.

`Recipe Step Definition [ RecipeStepDefinitionID ]`

Specifies the parent Recipe Step Definition.

`Parameter Definition [ ParameterDefinitionID ]`

Specifies the Parameter that the Value should be assigned to.

`Value`

This is the value that is assigned to the Function Definition Parameter Tag when the RSD starts.
