# ExecuteAudit

## Summary

`bool ExecuteAudit([DbAuditHeader header])`

For installations with the Audit feature appropriately licensed and configured. This allows the entire `UnitOfWork` to be executed as a single Audit entry. If not Audit `header` is specified, this will be executed as if [Execute](execute) was called.
