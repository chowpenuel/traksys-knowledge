# Product Variation

## Summary

### Entity Name

Product Variation

### Database Table Name

`tProductVariation`

### API Object Name

`DbProductVariation`

### Entity Description

Product Variations define differences in attributes of a given product to account for alternate Bill of Materials or varying production rates.

## Properties

`Standard Size [ StandardSize ]`

Specifies a baseline quantity of Product produced. This value is used for ratio calculations when extrapolating required Material quantities for different production run sizes. For example, if the Standard Size is 100 KGs and 20KGs of Material A is required, then production runs of 200KGs will require 40KGs of Material A.

`Theoretical Rate Calculation Units Per Minute [ TheoreticalRateCalculationUnitsPerMinute ]`

The maximum rate that the equipment can possibly run to make the product.

`Target Rate Calculation Units Per Minute [ TargetRateCalculationUnitsPerMinute ]`

The rate at which production should occur to meet goals or to hit an improvement target. This may differ slightly from the Theoretical Rate.
