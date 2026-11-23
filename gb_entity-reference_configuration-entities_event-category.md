# Event Category

## Summary

### Entity Name

Event Category

### Database Table Name

`tEventCategory`

### API Object Name

`DbEventCategory`

### Entity Description

Event Categories specify predefined values for operators to apply to Events. You may assign Event Categories to different hierarchical levels and create an Event Category Scheme to define each level.

## Properties

`Event Category Group [ EventCategoryGroupID ]`

Specifics the parent Event Category Group.

`Parent Event Category [ ParentEventCategoryID ]`

Specifics the parent Event Category, if any.

`Level`

Indicates the level in the Event Category hierarchy (an `integer` 1 - 10)

`Set Event Code [ EventCodeID ]`

Specifies the parent Event Code, if any.

`Event Code (Inherited) [ UseParentEventCodeID ]`

When inherited, specifies that this Event Category should inherit its Event Code from its parent Event Category. This does not apply to top-level Event Categories.

`Set OEE Type [ OeeEventTypeAssign ]`

Type of OEE loss this Event Category represents. This setting allows operators to override the Event Definition's OEE Event Type setting by assigning this Event Category to an Event. Select None to keep the Event Definition's OEE Event Type setting.

`OEE Type (Inherited) [ UseParentOeeEventTypeAssign ]`

When inherited, specifies that this Event Category should inherit its OEE Type setting from its parent Event Category. This does not apply to top-level Event Categories.

`Selectable`

When checked, specifies that operators may select this Event Category in a user interface. In hierarchical category schemes, you may want to prevent operators from selecting higher or top-level Event Categories, forcing them to choose lower-level, more detailed Event Categories.

`Icon`

Specifies an icon from the built-in TrakSYS icon library to the entity.

`Color CSS`

Specifies a CSS color class from the built-in TrakSYS color palette to the entity.

`Color`

Specifies a color to the entity. Both Hex and RGBA can be used to specify the color.
