# FailTransactionFromResult

```c
Result<bool> FailTransactionFromResult(string errorMessage, IResult result, int interfaceTransactionID) 
Overload: Result<T> FailTransactionFromResult(string errorMessage, IResult result, int interfaceTransactionID, Result<T> r) 
```

Sets `tInterfaceTransaction.State` to failed (2) using the provided `InterfaceTransactionID`.

Creates a `InterfaceTransactionLog` record. Contains the contents of the `errorMessage` and `result` parameters passed in.
