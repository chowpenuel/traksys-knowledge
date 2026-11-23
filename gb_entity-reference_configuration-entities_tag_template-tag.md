# Template Tag

## Summary

### Entity Name

Template Tag

### Database Table Name

`tTag`, `tTagTemplate`

### API Object Name

`DbTagTemplateComposite`

### Entity Description

The Template Tag is a special Tag type used as a placeholder for Tag properties in Template entities. For instance, when creating a Template Event Definition, the Trigger Tag can be set to a Template Tag instead of a real Tag. Besides being a non-functional Tag placeholder, the Template Tag also works in conjunction with the automatic Tag assignment functionality of Template to child entities. When using the Template Tag Prefix property in the Advanced tab of Template and child Systems, the Template Tag is available to be automatically replaced with a related real Tag when the automatic Tag assignment operation is run.

For example, A Template System is created called Template Bottle Line. Its Template Tag Prefix is configured as TBL\_. A Template Tag for the Product is created and named TBL\_Product and assigned to the System. A child System called Bottle Line 1 is created. Its Template Tag Prefix is configured as BL1\_. A Virtual Tag is created for the Bottle Line 1 Product and called BL1\_Product but not assigned to the System. When the Assign Tags from Template Parent operation is run on Bottle Line 1, the Template Tag Prefix settings are used and each Template Tag assigned to the parent triggers a search for a similarly named Tag (with the exception of the prefix). Tag matches are found and assigned to Bottle Line 1. The BL1\_Product Tag is located and automatically assigned as the Product Tag to Bottle Line 1.
