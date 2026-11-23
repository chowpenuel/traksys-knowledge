# Recipe Parameter

## Summary

### Entity Name

Recipe Parameter

### Database Table Name

`tRecipeParameter`

### API Object Name

`DbRecipeParameter`

### Entity Description

Recipe Parameters allow Recipe specific values to be assigned to pre-defined Batch System Parameters defined in the equipment model (Areas and Systems). Values for Recipe Parameters are assigned to the Tag defined in the Batch System Parameter when the Recipe starts.

## Properties

`Recipe [ RecipeID ]`

Specifies the parent Recipe.

`Recipe Step Definition [ RecipeStepDefinitionID ]`

Specifies the parent Recipe Step Definition, if any.

This field will be NULL for Recipe Parameters assigned directly to a Recipe. There will be a value when assigned to a specific Recipe Step Definition.

`Parameter Definition [ ParameterDefinitionID ]`

Specifies the Parameter that the Value should be assigned to.

`Value [ Value ]`

This is the value that is assigned to the Batch System Parameter Tag when the Recipe starts.
