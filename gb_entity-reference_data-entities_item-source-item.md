# Item Source Item

## Summary

### Entity Name

Item Source Item

### Database Table Name

`tItemSourceItem`

### API Object Name

`DbItemSourceItem`

### Entity Description

The Item Source Item entity can be used to establish a many-to-many relationship between Items. While ParentAreaID can create a one-to-many relationship between items, the Item Source Item relationship can be used to create further traceability by allowing Items to be related and composed of multiple other Items.

### Properties

`SourceItemID`

The unique identifier (primary key) of the Source Item for this Item.

`ItemID`

The unique identifier (primary key) of the Item (created or sourced from the SourceItemID).
