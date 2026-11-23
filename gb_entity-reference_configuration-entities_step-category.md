# Step Category

## Summary

### Entity Name

Step Category

### Database Table Name

`tStepCategory`

### API Object Name

`DbStepCategory`

### Entity Description

Step Categories are reasons that can be applied to Batch Steps that exceed their planned duration that explain the overage. A Step Category is analogous to Event Category for Events.

## Properties

`Step Category Group [ StepCategoryGroupID ]`

Specifies the parent Step Category Group

`Parent Step Category [ ParentStepCategoryID ]`

Specifies the parent Step Category, if any.

`Level`

Indicates the level in the Event Category hierarchy (an `integer` 1 - 10)

`Step Code [ StepCodeID ]`

Specifies the parent Step Code, if any.

`Inherit Step Code From Parent [ UseParentStepCodeID ]`

When checked, specifies that this Step Category should inherit its Step Code from its parent Step Category. This setting does not apply to top-level Step Categories.

`OEE Type [ OeeStepTypeAssign ] : ETS.Core.Enums.OeeStepTypeAssign`

Type of OEE loss this Step Category represents. This setting allows operators to override the Function Definition's Overage OEE Step Type setting by selecting this Step Category from a user interface selection. Select None to keep the Function Definition's OEE Event Type setting.

* **None** = 0
* **PerformanceLoss** = 1
* **AvailabilityLoss** = 2
* **SystemNotScheduled** = 3

`Inherit OEE Type from Parent [ UseParentOeeStepTypeAssign ]`

When checked, specifies that this Step Category should inherit its OEE Type setting from its parent Step Category. This setting does not apply to top-level Step Categories.

`Selectable`

When checked, specifies that operators may select this Step Category in user interfaces. In hierarchical category schemes, you may want to prevent operators from selecting higher or top-level Step Categories, forcing them to choose lower-level, more detailed Step Categories.
