# KPI Interval Count (OEE Interval Count)

## Summary

### Entity Name

KPI Interval Count (also known as OEE Interval Count)

### Database Table Name

`tOeeIntervalCount`

### API Object Name

`DbOeeIntervalCount`

### Entity Description

Each row in this table holds the number of Calculation Units accumulated at a specific KPI Counter, over a specific KPI Interval.

## Properties

`OeeIntervalID`

The unique identifier (primary key) for each KPI Interval captured by TrakSYS.

`OeeCounterID`

The unique identifier (primary key) for the related KPI Counter.

`OeeCounterCategoryID`

The unique identifier (primary key) for the related KPI Counter Category. This is typically only used in cases where there are multiple counters for a specific type of Input (Good, Total, Bad). Also note that having this CategoryID field on this record allows re-categorization after production, when counts may be reconciled.

`InputUnitsMultiplier`

The multiplier that was used at the KPI Input level to convert the raw counter accumulation to Calculation Units. This can be used to reverse engineer the CalculationUnitsCount back to the units counted at the KPI Input.

`CalculationUnitsCount`

The actual quantity accumulated at the related KPI Counter for the specified KPI Interval.
