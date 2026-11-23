# Latch Tag

## Summary

### Entity Name

Latch Tag

### Database Table Name

`tTag`, `tTagLatch`

### API Object Name

`DbTagLatchComposite`

### Entity Description

Latch Tags are similar to Compare Tags, except that they use different conditions for setting and resetting. A Latch Tag has two states: "Set" and "Reset". A Latch Tag is set when its Set Condition Tag evaluates to True, and is reset when its Reset Condition Tag evaluates to True.

An important distinction is that a Latch Tag will not automatically reset when its Set Condition Tag reverts to False, and will not automatically set when its Reset Condition Tag reverts to False. Once a Latch Tag sets, it remains set until its Reset Condition Tag evaluates to True; once a Latch Tag resets, it remains reset until its Set Condition Tag evaluates to True.

Tags or constant values may be used to specify what values a Latch Tag should return for its Set and Reset states .

## Properties

`Latch Set Condition [ LatchSetTagID ]`

A Boolean Tag whose value determines when the Latch should "Set." When True, the Latch will Set if it is currently Reset. When False, this Tag has no effect.

`Set Value [ SetTagID or SetConstant ]`

The value for the Latch to return when it is in the Set state, which may be a constant or the value of another Tag. This setting's data type must match the Latch's Data Type setting.

`Latch Reset [ LatchResetTagID ]`

A Boolean Tag whose value determines when the Latch should "Reset." When True, the Latch will Reset if it is currently Set. When False, this Tag has no effect.

`Reset Value [ ResetTagID or ResetConstant ]`

The value for the Latch to return when it is in the Reset state, which may be a constant or the value of another Tag. This setting's data type must match the Latch's Data Type setting.
