# Event-Sub (Sub-Event)

## Summary

### Entity Name

Event-Sub (or Sub-Event)

### Database Table Name

`tEventSub`

### API Object Name

`DbEventSub`

### Entity Description

A Sub-Event is created each time an Event Definition is triggered. Sub-Events record the actual start and stop of every triggered Event Definition, where the Event (`tEvent`) records represent only the highest priority Event in progress for a System at a given time.

## Properties

`StartDateTime`

The date and time that the event started.

`EndDateTime`

The date and time that the event ended.

`EventID`

This is the unique identifier (primary key) for the parent Event that represents the actual causal or highest priority Event Definition in progress at the time.

`EventDefinitionID`

Specifies the parent Event Definition.
