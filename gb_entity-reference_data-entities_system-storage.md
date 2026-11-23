# System Storage

## Summary

### Entity Name

System Storage

### Database Table Name

`tSystemStorage`

### API Object Name

`DbSystemStorage`

### Entity Description

Each row in this table represents a layer of something that resides within a physical Storage System. The layer can be a specific Product, Material, Lot, or SubLot. A Storage System may contain multiple layers at the same time.

## Properties

`SystemID`

This is the unique identifier (primary key) for the Storage System for which the layer resides in.

`ProductID`

This is the unique identifier (primary key) for the Product that makes up the layer.

`MaterialID`

This is the unique identifier (primary key) for the Material that makes up the layer.

`Lot`

This is string identifier for the Lot makes up the layer.

`SubLot`

This is string identifier for the Sub-Lot makes up the layer.

`Quantity`

The quantity of substance that makes up the layer.
