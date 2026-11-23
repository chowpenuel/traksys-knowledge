# CompleteTransaction

```c
Result<bool> CompleteTransaction(string responsePayload, int InterfaceTransactionID) 
Overload: Result<bool> CompleteTransaction(int interfaceTransactionID) 
```

Inserts a response payload string into the Interface Transaction record specified in the `InterfaceTransactionID` parameter, and sets `tInterfaceTransaction.State` to complete (0).

Overload sets `tInterfaceTransaction.State` to complete (0) using the provided `interfaceTransactionID`.
