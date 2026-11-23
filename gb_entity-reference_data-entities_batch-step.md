# Batch Step

## Summary

### Entity Name

Batch Step

### Database Table Name

`tBatchStep`

### API Object Name

`DbBatchStep`

### Entity Description

Each Row in this table represents a specific Step in a Batch execution. Batch Steps are created as a result of the Batch's Recipe.

{% hint style="info" %}
Note that a Batch Step and a Recipe Step are not always 1 to 1. A single Recipe Step Definition could be run several times within a Batch, and produce multiple Batch Step records.
{% endhint %}

## Properties

`BatchID`

Specifies the parent Batch.

`StartDateTime`

The date and time that the Batch Step started.

`EndDateTime`

The date and time that the Batch Step ended.

`FunctionDefinitionID`

The unique identifier (primary key) of the Function Definition that triggered the Batch Step.

`PlannedDurationSeconds`

Number of seconds representing the expected length of the Batch Step. This is copied from the Recipe Step Definition that triggered the Step.

`StartSequence`

Identifies the Sequence that this Step was executed within the Batch's Recipe.

`IsExpected`

This value will be True (1) for any Steps that were executed in the expected sequence according to the Batch's Recipe. If a Batch Step is detected/triggered that is out of sequence, it will still be recorded, but this column value will be False (0).

`User`

Holds the name, initials or other unique identifier, of the User that completed or signed-off on the Batch Step. The actual context and use of this field is implementation dependent.

`Notes`

Contains any notes added from Batch Step form user interfaces.
