# Counter Tag

## Summary

### Entity Name

Counter Tag

### Database Table Name

`tTag`, `tTagCounter`

### API Object Name

`DbTagCounterComposite`

### Entity Description

Counter Tags allow a moving value to be monitored constantly by the Logic Service and its changes to be accumulated within TrakSYS. The Counter Tag behaves similarly to the production counters that exist within KPI Calculation entities but can be used to count any incrementing value for the inclusion in logic or capture.

## Properties

`Counter [ CounterTagID ]`

A Tag providing the Counter value.

`Source Units Multiplier [ SourceUnitsMultiplierConstant or SourceUnitsMultiplierTagID ]`

Floating-point multiplier to convert Source Units to another unit of measurement.

`Maximum Increment per Scan [ MaxPlusConstant or MaxPlusTagID ]`

The maximum number of (Counter) units the Counter may increment within a single scan. Set this to the maximum value the Counter can realistically increment to filter out unexpected large jumps in Counter values.

`Flow On Counter Units Count [ FlowOnCounterUnitsCountConstant or FlowOnCounterUnitsCountTagID ]`

Number of Counter Units that must pass through the Counter within the time specified by Flow On Period before the Counter is Flowing.

`Flow On Period Seconds [ FlowOnPeriodSecondsConstant or FlowOnPeriodSecondsTagID ]`

A period of seconds during which the number of units specified by Flow On Counter Units Count must pass through the Counter before it is Flowing. Note that the Counter can begin Flowing sooner if it reaches Flow On Counter Units Count in less time than the Flow On Period.

`Flow Off Delay Seconds [ FlowOffDelaySecondsConstant or FlowOffDelaySecondsTagID ]`

Delay after the Counter stops incrementing before it stops Flowing.

`Reset On True [ ResetOnTrueTagID ]`

If this Tag is specified, the internal Counter value will reset to zero when the referenced Tag flips from False to True. If the Reset on True Tag remains one (True), the Counter will continue to count without resetting. The reset only occurs after the Reset on True Tag goes from False to True.

`Increment While True [ IncrementWhileTrueTagID ]`

If this Tag is specified, the Counter only accumulates differences in the Counter Tag movement while the referenced Tag is True.
