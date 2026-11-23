# Material

## Summary

### Entity Name

Material

### Database Table Name

`tMaterial`

### API Object Name

`DbMaterial`

### Entity Description

A Material represents something that is consumed or produced by the manufacturing process. Materials can be simple "raw" ingredients or more complex combinations of several other defined Materials in a specific ratio.

## Properties

`Material Type [ MaterialTypeID ]`

A Material Type categorizing this Material (solely for organizational and reporting purposes).

`Material Group [ MaterialGroupID ]`

Specifies the parent Material Group.

`Material Code [ MaterialCode ]`

A string that identifies this Material. The Material Code must be unique within the entire TrakSYS configuration.

`Units [ Units ]`

A textual description of the unit of measurement for this Material.

`Planned Size [ PlannedSize ]`

If the Material is a compound made up of other Materials, this is an arbitrary quantity that helps contextualize the amounts of the sub-components. See also [Material Component](material-component).

`Consumption Method [ MaterialConsumptionMethodID ]`

Specifies the Consumption Method selected for the current Material.

`Version Fields`

See [Entity Version Properties](../entity-version-properties).

`Decimal Places [ DecimalPlaces ]`

An extensible property that specifies the preferred number of decimal places to be used when displaying a Material's quantity or to prompt for in a custom editor.
