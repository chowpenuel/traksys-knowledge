# Event Category Group

## Summary

### Entity Name

Event Category Group

### Database Table Name

`tEventCategoryGroup`

### API Object Name

`DbEventCategoryGroup`

### Entity Description

Event Category Groups are sets of Event Categories that you can assign to Systems and Event Definitions for operator selection.

## Properties

`Scope [ ScopeType ] : ETS.Core.Enums.EventCategoryGroupScopeType`

Setting for whether this Event Category Group is normal or Global. Global Event Categories are available for selection for every Event; you do not need to explicitly assign Global Event Categories to Event Definitions or Systems. Select Global First if you would like the Global Event Category to appear at the top of the Event Category selection list in the user interface, or select Global Last if you would like it to appear at the bottom of the list. If the Scope is Normal, you must assign Event Categories for them to be available for selection.

* **GlobalFirst** = 0
* **Normal** = 1
* **GlobalLast** = 2

`Event Category Scheme [ EventCategorySchemeID ]`

Specifies the Scheme that all child Event Categories will be related to.
