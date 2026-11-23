# Product Set

## Summary

### Entity Name

Product Set

### Database Table Name

`tProductSet`

### API Object Name

`DbProductSet`

### Entity Description

Product Sets list the available Products for a System and designate a Product Scheme. They may be flat lists of Products or contain hierarchies of Products arranged into Product Groups.

## Properties

`Product Scheme [ ProductSchemeID ]`

The Product Scheme that all Products under this set will use to define their Attributes.

`Default Product [ DefaultProductID ]`

Fall-back Product the Logic Service should use when it fails to find a matching Product in the Product Set for the Product Map's Product Code Tag value.

`Enforce Versioning [ EnforceVersioning ]`

When checked, Product and Recipe versioning menu options will be available. Products and Recipes can be created as Drafts, made Active and Retired as needed.
