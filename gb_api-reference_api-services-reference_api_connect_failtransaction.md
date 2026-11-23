# FailTransaction

```c
Result<bool> FailTransaction(int interfaceTranssactionID, string errorMessage) 
Overload: Result<T> FailTransaction(int interfaceTranssactionID, string errorMessage, Result<T> r) 
```

Sets `tInterfaceTransaction.State` to failed (2) using the provided `InterfaceTransactionID`.

Creates a `InterfaceTransactionLog` record. Contains the contents of the `errorMessage` parameter passed in.
