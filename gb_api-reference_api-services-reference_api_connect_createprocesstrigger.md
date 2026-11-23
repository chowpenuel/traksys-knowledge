# CreateProcessTrigger

```c
Result<DbProcessSinkStart> CreateProcessTrigger(ConnectWorkflowTriggerSettings wfSettings)
```

Create Task Sink record for the specified Process Definition specified in the `ConnectWorkflowTriggerSettings` object.

If the Inteface Definition is executed in the Process Definition and the Process Definition key is specified for the Interface Transaction that is executed, an additional Transaction Log is created with data consisting of the `InterfaceDefinitionID`, `InterfaceDefinitionKey`, and `InterfaceTransactionID`.
