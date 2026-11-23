# KPI Counter (OEE Counter)

## Summary

### Entity Name

KPI Counter

### Database Table Name

`tOeeCounter`

### API Object Name

`DbOeeCounter`

### Entity Description

KPI Counters track Total, Good, and Bad production counts. Rather than using the actual values of the Counter Tags, the Logic Service monitors the changes in their values to more accurately track their movement.

Flow provides a simple mechanism to track when a KPI Counter (and the line) is running. To prevent small, intermittent counter movement from activating a Counter's Flow status, the Logic Service uses a Flow On ratio to determine when to set the Counter's state to Flowing. For the Flow to activate, the Counter must increment by the Flow On Counter Units Count within the time specified by Flow On Period. Once a Counter is Flowing, it does not reset until the Counter stop incrementing for the time specified by Flow Off Delay.

For example, if the Flow On Counter Units Count is 5, the Flow On Period is 10 seconds, and the Flow Off Delay is 15 seconds, the KPI Counter must increment by 5 (Counter Units) within a 10 second span before Flow activates. Once Flowing, the Flow will remain active until the Counter stops incrementing for 15 consecutive seconds.

{% hint style="success" %}
The Flow status of a KPI Counter is available as a State Tag. The State Tag Properties dialog allows you to select the desired KPI Counter and state information.
{% endhint %}

## Properties

`OEE Input [ OeeInputID ]`

Specifies the parent Oee Input.

`Counter [ CounterTagID or CounterConstant ]`

Tag or constant providing the Counter value.

`Counter Units to Input Units Multiplier [ InputUnitsMultiplierTagID or InputUnitsMultiplierConstant or InputUnitsMultiplierSourceType / InputUnitsMultiplierSource ]`

Floating-point multiplier to convert Counter Units to Input Units. If the Units are identical, simply specify 1.0.

`Maximum Increment per Scan [ MaxPlusTagID or MaxPlusConstant ]`

The maximum number of (Counter) units the Counter may increment within a single scan. Set this to the maximum value the Counter can realistically increment to filter out unexpected large jumps in Counter values. Cycling the power on PLCs or uploading new programs may cause erratic Counter behavior that can severely impact OEE.

{% hint style="info" %}
Note that any time a Counter moves backward, the Logic Service >considers it a Rollover event (reset to 0) and uses this same setting >to determine whether or not to discard the change in Counter value (New Value – 0).
{% endhint %}

`KPI Count Category [ OeeCountCategoryID ]`

Specifies the KPI Count Category that will be assigned to Interval Count records recorded for this KPI Counter.

`Flow On Counter Units Count [ FlowOnCounterUnitsCountTagID or FlowOnCounterUnitsCountConstant ]`

Number of Counter Units that must pass through the Counter within the time specified by Flow On Period before the Counter is Flowing.

`Flow On Period Seconds [ FlowOnPeriodSecondsTagID or FlowOnPeriodSecondsConstant ]`

A period of seconds during which the number of units specified by Flow On Counter Units Count must pass through the Counter before it is Flowing. Note that the Counter can begin Flowing sooner if it reaches Flow On Counter Units Count in less time than the Flow On Period.

`Flow Off Delay Seconds [ FlowOffDelaySecondsTagID or FlowOffDelaySecondsConstant ]`

Delay after the Counter stops incrementing before it stops Flowing.

`Rollover [ RolloverTagID or RolloverConstant ]`

Maximum value at which the Counter rolls over to zero. Depending on the scan rate, the Logic Service may miss the maximum Counter value on some high-speed lines. If Rollover always occurs at a specific value, you can use this setting to ensure the Logic Service interprets the Rollover correctly. Note that the Maximum Increment per Scan setting overrides this setting, so if the Rollover is incorrect (i.e. too high) and the adjusted Counter change exceeds the Maximum Increment per Scan, the Logic Service will discard the change altogether.

For example, if a particularly fast Counter's Rollover occurs at 10, but the Logic Service only sees the values 9 and then 1, it will assume the Rollover occurred at 9 and interpret the change as +2. However, if you explicitly set Rollover to 10, the Logic Service will correctly adjust this to +3 to account for the missed Counter change from 9 to 10. Note that if the Maximum Increment per Scan setting is less than 3, the Logic Service will discard the Counter change. Therefore, it is important that Rollover be set correctly; otherwise, an incorrect value may make the data less accurate than not specifying Rollover at all.

`Record Detail [ RecordDetail ]`

When True, the Logic Service will record detailed tracking data every time the Counter changes. Use this setting to troubleshoot problematic Counters.

`Is Derived [ IsDerived ]`

Within each counter Type (Good, Bad or Total), one of the KPI Counters can be designated as "Derived" using this property. If the counter type is Derived (for instance the KPI Calculation is setup to calculate Total and Good : so Bad is derived), it is possible to setup distinct counters to specifically count some of the Bad units. However if the specific counters do not capture all of the Bad units, then the remainder will be automatically assigned to the Derived Bad KPI Counter. The following example demonstrates...

KPI Calculation (configured for counting Total and Good : Bad is derived)

* Total Units = Input counter to the Line
* Good Units = Output counter to the Line
* Bad Units = Derived (however some are counted specifically)
  * Bad from Filler = Reject counter at Filler
  * Bad from Labeler = Reject counter at Labeler
  * Other Bad = IsDerived

In a given interval, the following counts are captured...

* Total Units = 100
* Good Units = 75
* Bad Units = 25 (calculated by Total - Good)
  * Bad from Filler = 5
  * Bad from Labeler = 5
  * Other Bad = 15 (calculated by Total - Good - Bad from Filler - Bad from Labeler)
