# Sample Definition Rule Definition

## Summary

### Entity Name

Sample Definition Rule Definition

### Database Table Name

`tSampleDefinitionRuleDefinition`

### API Object Name

`DbSampleDefinitionRuleDefinition`

### Entity Description

A Sample Definition Rule Definition represents business rules that are applied to new Sample Sub-Groups recorded under the parent Sample Definition. As each new value is recorded, the Rule Definition Script is executed.

{% hint style="info" %}
A minimum of 30 Sample Sub Groups is required in order for built-in Rule Violations to trigger. If less than 30 are provided, the violations will not trigger and records will not be created in \`tSampleSubGroupRule\`.
{% endhint %}

## Properties

`Sample Definition ID [ SampleDefinitionID ]`

Specifies the parent Sample Definition.

`Rule Type [ RuleType ] : ETS.Core.Enums.SpcRuleDefinitionType`

Specifies the type of Rule that is being implemented.

* **CustomScript** = 0
* **CustomRule** = 1
* **FourteenConsecutivePointsAlternating** = 100
* **TwoOutOfLast3AboveSigma2** = 101
* **TwoOutOfLast3BelowNegativeSigma2** = 102
* **FourOutOfLast5AboveSigma1** = 103
* **FourOutOfLast5BelowNegativeSigma1** = 104
* **SixConsecutivePointsTrendingDown** = 105
* **SixConsecutivePointsTrendingUp** = 106
* **EightConsecutivePointsAboveCenterLine** = 107
* **EightConsecutivePointsBelowCenterLine** = 108
* **AnyPointAboveSigma3** = 109
* **AnyPointBelowNegativeSigma3** = 110

**CustomScript** - Provides access to the script, which acts as a single-assignment rule.

**CustomRule** - Allows the assignment of Script Class that inherits from SampleRuleDefinitionRunnerBase, which acts as a multi-assignable rule.

All other values represent built-in rule templates that do not have a Script component.

`Script [ Script ]`

If a built-in Rule Definition template is used, the value will be empty.

If a Custom Script is used, the script will be stored as the value.

If a Custom Rule is used, the Script Class Name is stored as the value.

When creating a custom Script or Rule, an array of recent Sample Sub-Group values is provided to determine whether a Rule has been violated. If the Script returns true, the Rule Definition is considered triggered (violated) and creates a record in tSampleSubGroupRule. Otherwise, no Rule is violated.
