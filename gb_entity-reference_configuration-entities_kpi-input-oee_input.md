# KPI Input (OEE Input)

## Summary

### Entity Name

KPI Input

### Database Table Name

`tOeeInput`

### API Object Name

`DbOeeInput`

### Entity Description

Each KPI Calculation contains exactly 3 KPI Input child records (Total, Good and Bad). The KPI Input is the parent record for KPI Counters.

## Properties

`OEE Calculation [ OeeCalculationID ]`

Specifies the parent entity in the configuration hierarchy.

`Type [ Type ] : ETS.Core.Enums.OeeCounterType`

An enum value specifying the type (Total, Good or Bad) of the KPI Input.

`Input Units [ InputUnits ]`

Label for the Input's units. This setting is for informational purposes only.

`Input Units to Calculation Units [ CalculationUnitsMultiplierTagID or CalculationUnitsMultiplierConstant or CalculationUnitsMultiplierSourceType / CalculationUnitsMultiplierSource ]`

Floating-point multiplier to convert the Input's Units to Calculation Units. If the Units are identical, specify 1.0. If all of the Counters use the same Units, this setting should specify the conversion to Calculation Units rather than setting identical conversions for each Counter.

`Flow On Input Units Count [ FlowOnInputUnitsCountTagID or FlowOnInputUnitsCountConstant ]`

Number of Input Units that must pass through the Input within the time specified by Flow On Period before the Input is Flowing.

`Flow On Period (Seconds) [ FlowOnPeriodSecondsTagID or FlowOnPeriodSecondsConstant ]`

A period of seconds during which the number of units specified by Flow On Input Units Count must pass through the Input before it is Flowing. Note that the Input can begin Flowing sooner if it reaches Flow On Input Units Count in less time than the Flow On Period.

`Flow Off Delay (Seconds) [ FlowOffDelaySecondsTagID or FlowOffDelaySecondsConstant ]`

Delay after the counters stop incrementing before this Input stops Flowing.
