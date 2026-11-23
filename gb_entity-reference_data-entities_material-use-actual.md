# Material Use Actual

## Summary

### Entity Name

Material Use Actual

### Database Table Name

`tMaterialUseActual`

### API Object Name

`DbMaterialUseActual`

### Entity Description

Each row in this table represents a quantity of Material that was consumed during the production of a Job.

## Properties

`JobID`

The unique identifier (primary key) for the Job in progress when the Material was consumed.

`SystemID`

This is the unique identifier (primary key) for the System for which the Material was consumed.

`DateTime`

The date and time the Material was consumed.

`Quantity`

The actual quantity of Material that was consumed.

`BatchStepID`

The unique identifier (primary key) for the Batch Step in progress when the Material was consumed.

`MaterialID`

The unique identifier (primary key) for the Material that was consumed.

`Lot`

A string identifier for the Material Lot that was consumed.

`SubLot`

A string identifier for the Material Sub-Lot that was consumed.

`Capture01 - 10`

These are developer-use-only field for extensibility. Any type of related data to the specific Material consumption can be stored in the Capture fields.

`User`

Holds the name, initials or other unique identifier, of the user that processed the Material consumption. The actual context and use of this field is implementation dependent.

`Notes`

Contains any notes added from Material consumption user interfaces.

`External Date Time [ ExternalDateTime ]`

An extensible field which is typically used to hold DateTime or DateTimeOffset values. This field is commonly used for integration with external systems.

`External State [ ExternalState ]`

An extensible field which is typically used to track States for the given entity. This field is commonly used for integration with external systems.

`External Data [ ExternalData ]`

An extensible field which is typically used to contain additional data for the current entity. This field is commonly used for integration with external systems.
