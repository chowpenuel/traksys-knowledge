# State Tag

## Summary

### Entity Name

State Tag

### Database Table Name

`tTag`, `tTagState`

### API Object Name

`DbTagStateComposite`

### Entity Description

State Tags provide a means to access internal the Logic Service state information, such as the status of a System, what Event Definitions are active, and how long the Logic Service has been running.

## Properties

`Item Name [ ItemName ]`

The Property field is a string made of up 3 parts, the Entity Type, the Entity and the Attribute described below. Its value is set by the configuration user interface and is exposed as 3 separate entry fields.

**Entity Type** - The type of Configuration Entity to obtain state information from. Use the drop-down to select this value.

**Entity** - Which Entity to obtain state information from. Once you specify an Entity Type, Configuration provides a drop-down list of the available entities or an appropriate picker.

**Attribute** - The Attribute of the selected Entity to use for the Tag's value.
