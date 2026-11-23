# Function Definition

## Summary

### Entity Name

Function Definition

### Database Table Name

`tFunctionDefinition`

### API Object Name

`DbFunctionDefinition`

### Entity Description

A Function Definition defines a potential Batch System operation (it is only available under Batch Systems). When defining Batch Recipes, each step in the Recipe must be assigned to a Function Definition. A Recipe step is automatically started when its associated Function Definition becomes active based on its Trigger Tag logic.

## Properties

`System [ SystemID ]`

Specifics the parent System.

`Sub-System [ SubSystemID ]`

Specifics the parent SubSystem.

`Function Definition Group [ FunctionDefinitionGroupID ]`

Specifies the parent Function Definition Group.

`Function Definition Type [ FunctionDefinitionTypeID ]`

A Function Definition Type categorizing this Function Definition (solely for organizational and reporting purposes).

`Trigger Tag [ TriggerTagID ]`

A Discrete Tag which triggers this Function Definition. When True, the Function Definition is active; when False, the Function Definition is not active.

`Default Overage Step Category [ StepCategoryID ]`

Specifies an optional Step Category that is assigned by default any time the Function exceeds its planned duration (as defined in the Recipe Step Definition).

`Overage OEE Step Type [ OeeStepType ] : ETS.Core.Enums.OeeStepType`

Specifies an optional OEE Step Type that is assigned by default any time the Function exceeds its planned duration (as defined in the Recipe Step Definition). This OEE value is recorded for reporting only and is not used to calculate full OEE metrics (unlike discrete systems).
