# In Memory Tag

## Summary

### Entity Name

In Memory Tag

### Database Table Name

`tTag`, `tTagInMemory`

### API Object Name

`DbTagInMemoryComposite`

### Entity Description

In Memory Tags store their values in the memory of the Logic Service. This differs from most other Tag types that rely on the tTag table for value storage and changes. In Memory Tags can only be modified from with the Logic Service, making them useful for tag values that should only change by custom code.

Since the Tag's value is stored in memory, the value is temporary and will only be retained while the Logic Service is running. Once the service is stopped or restarted, the value is lost and will be reset when the service is started up again.
