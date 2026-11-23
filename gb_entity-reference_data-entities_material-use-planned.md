# Material Use Planned

## Summary

### Entity Name

Material Use Planned

### Database Table Name

`tMaterialUsePlanned`

### API Object Name

`DbMaterialUsePlanned`

### Entity Description

Each row in this table represents a type and amount of Material that should be consumed during a specific Job.

## Properties

`JobID`

The unique identifier (primary key) for the Job that the Material should be consumed for.

`BatchStepID`

The unique identifier (primary key) for the Batch Step that the Material should be consumed during.

`MaterialID`

The unique identifier (primary key) for the Material that should be consumed.

`Quantity`

The planned quantity of Material that should be consumed.
