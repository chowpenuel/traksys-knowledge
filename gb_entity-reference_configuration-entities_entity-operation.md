# Custom Operation

## Summary

### Entity Name

Custom Operation

### Database Table Name

`tEntityOperation`

### API Object Name

`DbEntityOperation`

### Entity Description

The `tEntityOperation` table stores custom operation data for a given entity name (optionally scoped to a site). It is primarily used for extensibility, where custom logic and/or UI features can persist a text payload and track when it was last modified.

## Properties

`Site ID [ SiteID ]`

Specifies the parent Site for the Operation.

`Entity Name [ EntityName ]`

The entity name this operation data is associated with (`nvarchar(100)`, not nullable). This determines where the operation appears in the standard configuration.

`Data [ Data ]`

Text payload for the custom operation (`nvarchar(max)`, not nullable) to define the Caption, Icon, Link, and Parameters in XML format.
