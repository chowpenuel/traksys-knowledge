# Material Produced

## Summary

### Entity Name

Material Produced

### Database Table Name

`tMaterialProduced`

### API Object Name

`DbMaterialProduced`

### Entity Description

Each row in this table represents a quantity of Material that was produced during the execution of a Job.

## Properties

`JobID`

The unique identifier (primary key) for the Job in progress when the Material was produced.

`SystemID`

The unique identifier (primary key) for the System where the Material was produced.

`BatchID`

The unique identifier (primary key) for the Batch associated with the produced Material, when applicable.

`MaterialID`

The unique identifier (primary key) for the Material that was produced.

`DateTime`

The date and time the Material was produced.

`UniqueID`

A unique identifier for the Material Produced record. This value is typically used to prevent duplicate inserts when records originate from external systems.

`Quantity`

The quantity of Material that was produced.

`Identifier`

A string identifier associated with the produced Material, such as a lot, serial, pallet, or container identifier.

`Capture01 - 10`

These are developer-use-only fields for extensibility. Any type of related data for the produced Material may be stored in the Capture fields.

`User`

Holds the name, initials, or other unique identifier of the user that recorded the Material production. The actual context and use of this field is implementation dependent.

`Notes`

Contains any notes associated with the Material Produced record.

`External Date Time [ ExternalDateTime ]`

An extensible field which is typically used to hold DateTime or DateTimeOffset values. This field is commonly used for integration with external systems.

`External State [ ExternalState ]`

An extensible field which is typically used to track States for the given entity. This field is commonly used for integration with external systems.

`External Data [ ExternalData ]`

An extensible field which is typically used to contain additional data for the current entity. This field is commonly used for integration with external systems.
