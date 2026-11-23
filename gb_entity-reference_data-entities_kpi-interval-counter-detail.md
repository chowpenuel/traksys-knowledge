# KPI Interval Counter Detail (OEE Interval Counter Detail)

## Summary

### Entity Name

KPI Interval Counter Detail (OEE Interval Counter Detail)

### Database Table Name

`tOeeIntervalCounterDetail`

### API Object Name

`DbOeeIntervalCounterDetail`

### Entity Description

Each row in this table represents a KPI Counter's incremental value. A Counter Detail row is akin to historizing a KPI Counter and is most often used for debugging purposes. Note that when using this feature, it should be disabled after debugging use to avoid any performance issues.

## Properties

`OeeIntervalID`

The unique identifier (primary key) for the parent KPI Interval captured by TrakSYS. Since Intervals are often refreshed multiple times before they end, there may be multiple Counter Detail records belonging to the same Interval.

`OeeCounterID`

The unique identifier (primary key) for the KPI Counter which this record represents details for.

`DateTime`

The date and time of this Counter Detail record.

`Type : ETS.Core.Enums.OeeCounterDetailType`

Represents the type of Counter Detail record. Possible values include:

* **Normal** = 0
* **Rollover** = 1
* **ExceededMaxPlus** = 2
* **Quality Changed** = 4
* **FlowChanged** = 8

**Note**: While these are the only available enums, it is possible for this property to have a combination of values that represent multiple types. For example:

**1** (Rollover) + **2** (ExceededMaxPlus) = **3** (Rollover and ExceededMaxPlus)

**2** (ExceededMaxPlus) + **4** (Quality Changed) = **6** (ExceededMaxPlus and Quality Changed)

`Value`

Specifies the raw Counter value at the time the record was created.

`Delta`

Specifies the delta from the last count recorded (taking into account any multipliers).

`DeltaRaw`

Specifies the delta from the last raw count recorded (without any multipliers applied).

`Quality`

Specifies the OPC Tag Quality of the Counter Tag.

`QualityDescription`

Specifies the OPC Tag Quality Description of the Counter Tag.

`InputUnitsMultiplier`

The multiplier that was used at the KPI Input level to convert the raw counter accumulation to Calculation Units. This can be used to reverse engineer the CalculationUnitsCount back to the units counted at the KPI Input.

`Flowing`

Specifies whether or not the counter was flowing at the time this record was created.
