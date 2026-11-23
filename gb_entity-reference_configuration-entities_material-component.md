# Material Component

## Summary

### Entity Name

Material Component

### Database Table Name

`tMaterialComponent`

### API Object Name

`DbMaterialComponent`

### Entity Description

A Material Component is a reference and quantity of another existing Material. They are used to construct compound Materials.

## Properties

`MaterialID [ MaterialID ]`

Specifies the parent Material.

`Material Component [ ComponentMaterialID ]`

The referenced sub-component Material.

`Quantity [ Quantity ]`

The quantity of the sub-component Material needed to make a specified amount of the parent Material.
