# Sub-System

## Summary

### Entity Name

Sub-System, Sub-System (Discrete), Sub-System (Batch)

### Database Table Name

`tSystem`

### API Object Name

`DbSystem`

### Entity Description

Sub-Systems provide an additional level of grouping within normal Systems. This is useful for configuring Overview Systems; in these cases, Systems typically represent entire production lines while Sub-Systems represent equipment. With such a hierarchy you can easily relate line stoppages to the equipment and Event Definitions that caused them. The reports allow you to group your data by Sub-System, providing a clear view of the root cause for each interruption.

There are two variations of Sub-Systems in TrakSYS: Discrete Sub-Systems (or Work Cells in ISA-95) and Batch Sub-Systems (or Units in ISA-95). The sections below describe each of these Sub-System variations in more detail.

## Variations

### Sub-System (Discrete) Description

Discrete Sub-Systems (Work Cells in ISA-95) can be created under Discrete Systems. They may contain a sub-set of the properties and configuration entity children that the parent System supports.

### Sub-System (Batch) Description

Batch Sub-Systems (Units in ISA-95) can be created under Batch Systems. They may contain a sub-set of the properties and configuration entity children that the parent System supports.

## Properties

`Area [ AreaID ]`

Specifies the parent Area.

`Parent System [ ParentSystemID ]`

Specifies the parent System.

`Linked System [ LinkedSystemID ] | Discrete Sub-Systems Only`

When set, any event that is recorded under this Sub-System is also recorded with a link to the event that is currently active in the linked System. Reports allow the Event Definition from the linked System to be displayed in addition to the actual Event Definition.

`Location [ LocationID ]`

Relates Sub-the System to a specified Location in the TrakSYS configuration.

`Schedule [ ScheduleID ]`

This property will be NULL for all of the Sub-System variations.

`System Capture Scheme [ SystemCaptureSchemeID ]`

This property will be NULL for all of the Sub-System variations.

`Job Capture Scheme [ JobCaptureSchemeID ]`

This property will be NULL for all of the Sub-System variations.

`Event Category Scheme [ EventCategorySchemeID ]`

This property will be NULL for all of the Sub-System variations.

`Step Category Scheme [ StepCategorySchemeID ] | Batch Sub-Systems Only`

This property will be NULL for all of the Sub-System variations.

`Product Set [ ProductSetID ]`

This property will be NULL for all of the Sub-System variations.

`Product Code Tag [ ProductTagID ] | Batch Sub-Systems Only`

Specifies a Tag used to indicate the currently running Product from the related Product Set (by Product Code).

`Job Tag [ JobTagID ] | Batch Sub-Systems Only`

Specifies a Tag used to identify the current Job that is running on the Sub-System. The value returned from this Tag will be used to create or lookup a TrakSYS Job by its Name field.

`Batch Tag [ BatchTagID ] | Batch Sub-Systems Only`

Specifies a Tag used to identify the current Batch that is running on the Sub-System. The value returned from this Tag will be used to create or lookup a TrakSYS Batch by its Name field.

`Planned Size Tag [ PlannedSizeTagID ]`

This property will be NULL for all of the Sub-System variations.

`Actual Size Tag [ ActualSizeTagID ]`

This property will be NULL for all of the Sub-System variations.

`Split Event on Day Change [ SplitEventOnDayChange ]`

This property will be NULL for all of the Sub-System variations.

`Split Event on Shift Change [ SplitEventOnShiftChange ]`

This property will be NULL for all of the Sub-System variations.

`Split Event on Product Change [ SplitEventOnProductChange ]`

This property will be NULL for all of the Sub-System variations.

`Split Event on Job Change [ SplitEventOnProductChange ]`

This property will be NULL for all of the Sub-System variations.

`Split Event on Batch Change [ SplitEventOnProductChange ] | Batch Sub-Systems Only`

This property will be NULL for all of the Sub-System variations.

`Impact Tag [ ImpactTagID ] | Batch Sub-Systems Only`

Specifies a Tag to be used to indicate the current impact factor for Events recorded against the Sub-System. Impact determines how to weight Events for this Sub-System. The Logic Service will record the value of the Impact Tag at the start of each Event as weight. Certain reports use these weights to display weighted durations of Events. For example, if an Event lasts 10 minutes, but has an Impact of 0.5, the weighted duration is 5 minutes. The Tag specified should return a decimal value between 0 and 1. If this Tag is not specified, the Impact factor is considered to be 1.

`Suppress Events if True [ SuppressTagID ] | Batch Sub-Systems Only`

When set, the value of this `discrete` Tag is combined with the logic of all child Event Definitions. While the Suppress Tag is True, none of the child Event Definitions will evaluate to True. The Event Definition properties expose a property for each Event Definition that may override this behavior.

`Manual Data Entry [ IsManual ]`

This property will be NULL for all of the Sub-System variations.

`Template Tag Prefix [ TemplateTagPrefix ]`

This property will be empty for all of the Sub-System variations.

`ISA-95 System Type [ S95SystemType ] : ETS.Core.Enums.S95SubSystemType`

Specifies the variation type of the Sub-System entity. This property is managed and set internally by TrakSYS as new Systems are created.

`Storage Units [ StorageUnits ] | Storage Systems Only`

This property will be empty for all of the Sub-System variations.

`Maximum Capacity [ StorageMaximum ] | Storage Systems Only`

This property will be 0 for all of the Sub-System variations.

`Show For Acknowledge [ ShowForAcknowledge ]`

When checked, this Event will be eligible for display in a user interfaces which show Events requiring Attention. This value effects all child Event Definitions which inherit this setting.

`Display Delay Seconds [ DisplayDelaySeconds ]`

Number of seconds after an Event begins before it appears user interfaces which show Events requiring Attention. This value effects all child Event Definitions which inherit the ShowForAcknowledge setting.

`Acknowledge Duration Minutes [ AcknowledgeDurationMinutes ]`

Number of minutes users have to acknowledge an Event before it is considered auto-acknowledged and disappears from user interfaces which show Events requiring Attention. This value effects all child Event Definitions which inherit the ShowForAcknowledge setting.
