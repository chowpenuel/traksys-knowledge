# Number and Date Format

When the Values Dictionary item specified by an expression is a DateTime, DateTimeOffset, Integer, Double, or Float, a format code can be specified to apply additional formatting to the item when processed. The format syntax is the standard .NET formatting syntax and the exhaustive list of formatting options can be found in MSDN references.

## Values Dictionary

StartDateTime = 2016-01-26 15:21:00

GoodProductionCount = 2400

SampleValue = 12.5891

## Expressions

`The line started on {StartDateTime:MMM-dd} at {StartDateTime:hh:mm}`

`The good production was {GoodProductionCount:N0}`

`The sample value was {SampleValue:N2}`

## Results

The line started on Jan-26 at 03:21

The good production was 2,400

The sample value was 12.59
