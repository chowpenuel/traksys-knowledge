# Recipe Step Definition

## Summary

### Entity Name

Recipe Step Definition

### Database Table Name

`tRecipeStepDefinition`

### API Object Name

`DbRecipeStepDefinition`

### Entity Description

A Recipe is made up of one or more Recipe Step Definitions (RSD). A Recipe Step Definition is the execution of one of the Batch System's Function Definitions for a specified duration.

Recipe Step Definitions are configured with a specific Start and End Sequence. The Sequence number is an arbitrary `integer` that represents the order in which the RSD starts and ends in relation to the other RSDs for the Recipe. When setting Sequence values, the following general rules should be observed.

* If Step A is set to end on Sequence 4 and Step B is set to start on Sequence 4, then Step B cannot start until Step A is complete.
* If Step A is set to end on Sequence 3 and Step B is set to start on Sequence 2, then Step B can start before or after Step A is complete.
* If Step A and Step B are set to start on Sequence 1 then the steps are parallel and they can start independently of each other.
* If Step A starts and ends on Sequence 1 and Step B starts and ends on Sequence 2, then Step B cannot start until Step A is complete.
* If Step A is set to start on Sequence 1 and end on Sequence 3, and Step B is set to Start on Sequence 2, Step B cannot start until Step A has started.

## Properties

`Recipe [ RecipeID ]`

Specifies the parent Recipe.

`Function Definition [ FunctionDefinitionID ]`

Specifies the Function Definition that will trigger this Step.

`Start Sequence [ StartSequence ]`

The Sequence that this RSD is set to start in.

`End Sequence [ EndSequence ]`

The Sequence that this RSD is set to end in.

`Planned Duration Seconds [ PlannedDurationSeconds ]`

The target duration for the RSD.
