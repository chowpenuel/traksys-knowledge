# Process Path Definition

## Summary

### Entity Name

Process Path Definition

### Database Table Name

`tProcessPathDefinition`

### API Object Name

`DbProcessPathDefinition`

### Entity Description

This entity defines a directional arrow connection between Steps in a Process Definition Workflow diagram.

## Properties

`Process Definition [ ProcessDefinitionID ]`

Specifies the parent Process Definition.

`From Process Step Definition [ FromProcessStepDefinitionID ]`

Specifies the Process Step Definition where the Path originates from.

`To Process Step Definition [ ToProcessStepDefinitionID ]`

Specifies the Process Step Definition where the Path enters into.

`Process Step Parameter Key [ ProcessStepParameterKey ]`

Specifies a `Key` from the **Process Values** being passed out of the originating Step to be used for evaluating a condition that determines if the Path is followed.

Follow Path = **Process Step Parameter Key** _Process Path Operator Type_ **Value**

`Process Path Operator Type [ ProcessPathOperatorType ] : ETS.Core.Enums.ProcessPathOperatorType`

Specifies a logical operator to be used for evaluating a condition that determines if the Path is followed.

Follow Path = **Process Step Parameter Key** _Process Path Operator Type_ **Value**

`Value [ Value ]`

Specifies a constant value to be used for evaluating a condition that determines if the Path is followed.

Follow Path = **Process Step Parameter Key** _Process Path Operator Type_ **Value**

`Process Path Label Mode [ ProcessPathLabelMode ] : ETS.Core.Enums.ProcessPathLabelMode`

Specifies how the Path label is rendered on the runtime render of a Workflow diagram.

* **Smart** - For comparisons with boolean values (where the **Value** is 0 or 1), the label will be rendered with only the `Process Step Parameter Key`.
  * For a `Key` of "Success" = **Value** of 1, the label would be rendered as "Success".
  * For a `Key` of "Success" = **Value** of 0, the label would be rendered as "! Success".
  * For cases where the **Value** is non 0 or 1, then the label will be rendered as the **Normal** setting described below.
* **Normal** - The label will be rendered as **Trimmed Process Step Parameter Key** _Process Path Operator Type_ **Value**. For a `Key` of "Job.UserState" the label would be "UserState = 2".
* **Verbose** - The label will be rendered as **Process Step Parameter Key** _Process Path Operator Type_ **Value**. For a `Key` of "Job.UserState" the label would be "Job.UserState = 2".

`Label [ Label ]`

When this property is non-empty, the Path diagram label will be rendered with this value. This overrides any label rendering behavior as described by the `Process Path Label Mode` property.
