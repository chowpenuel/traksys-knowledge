# Recipe Step Definition Material

## Summary

### Entity Name

Recipe Step Definition Material

### Database Table Name

`tRecipeStepDefinitionMaterial`

### API Object Name

`DbRecipeStepDefinitionMaterial`

### Entity Description

A Recipe Step Definition Material a specific amount of a defined Material that must be added for the parent Step.

## Properties

`Recipe Step Definition [ RecipeStepDefinitionID ]`

Specifies the parent Recipe Step Definition.

`Material [ MaterialID ]`

Specifies the parent Material.

`Percentage`

The percentage of the overall Recipe quantity that is made up of the Material added at this Step. This is typically calculated through the built-in Configuration. The exact formula used for this property is shown below:

Percentage (Recipe Step Definition) = (User Input Quantity / ((tRecipe.PlannedBatchSize / tProduct.StandardSize) \* tProductMaterial.Quantity)) \* 100
