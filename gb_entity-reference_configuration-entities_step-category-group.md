# Step Category Group

## Summary

### Entity Name

Step Category Group

### Database Table Name

`tStepCategoryGroup`

### API Object Name

`DbStepCategoryGroup`

### Entity Description

Step Category Groups are sets of Step Categories that can be assigned to Batch Sub-Systems and Function Definitions for user selection in a user interface.

## Properties

`Scope Type [ ScopeType ] : ETS.Core.Enums.EventCategoryGroupScopeType`

Setting for whether this Step Category Group is normal or Global. Global Step Categories are available for every Function Definition; you do not need to explicitly assign Global Step Categories to Function Definitions or Systems. Select Global First if you would like the Global Step Category to appear at the top of the Step Category selection list, or select Global Last if you would like it to appear at the bottom of the list. If the Scope is Normal, you must assign Event Categories for them to be available for selection.

* **GlobalFirst** = 0
* **Normal** = 1
* **GlobalLast** = 2

`Step Category Scheme [ StepCategorySchemeID ]`

Specifies the Scheme that all child Event Categories will be related to.
