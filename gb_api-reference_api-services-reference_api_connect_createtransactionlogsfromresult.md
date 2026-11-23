# CreateTransactionLogsFromResult

```c
Result<bool> CreateTransationLogsFromResult(IResult result, int interfaceTransactionID) 
```

Creates a new record in `tInterfaceTransactionLog` using the provided `InterfaceTransactionID`. Contains the contents of the `result` parameter passed in.
