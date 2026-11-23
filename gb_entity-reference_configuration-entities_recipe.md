# Recipe

## Summary

### Entity Name

Recipe

### Database Table Name

`tRecipe`

### API Object Name

`DbRecipe`

### Entity Description

A Recipe is a formula or a set of production directions for a specific Product on a specific Batch System. Recipes include many details and child entities.

## Properties

`System [ SystemID ]`

Specifies the System that this Recipe will be run on.

`Product [ ProductID ]`

Specifies the Product that is produced by this Recipe.

`Planned Number Of Batches [ PlannedNumberOfBatches ]`

The standard number of Batches that are run when this Recipe is used. This is a default and can be overridden in the actual run time application.

`Planned Batch Size [ PlannedBatchSize ]`

The standard size of each Batch when this Recipe is used. This is a default and can be overridden in the actual run time application.

`Planned Batch Size Units [ PlannedBatchSizeUnits ]`

The textual description of the units that are being produced in each Batch. This value is used primarily for display and reporting.

`Planned Batch Duration Seconds [ PlannedBatchDurationSeconds ]`

The overall planned length of the Batch. This is specified explicitly rather than being calculated by the planned durations of the Recipe Steps because of the potential for Recipe Steps to overlap each other in complex ways.

`Duration By Batch Size`

This table lists the Planned Batch Duration values as they vary based on the size of the Batch being run. If the Batch size is not found in the lookup table, then the Planned Batch Duration configured above will be used.

`Version Fields`

See [Entity Version Properties](../entity-version-properties).

`Planned Batch Size Minimum`

An extensibility field that determines the minimum amount for a given Batch when using the current Recipe. This field is purely for reference and is not enforced when a Job starts.

`Planned Batch Size Maximum`

An extensibility field that determines the maximum amount for a given Batch when using the current Recipe. This field is purely for reference and is not enforced when a Job starts.
