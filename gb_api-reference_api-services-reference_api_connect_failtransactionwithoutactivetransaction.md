# FailTransactionWithoutActiveTransaction

```c
Result<bool> FailTransactionWithoutActiveTransaction(int interfaceDefID, int parentInterfaceTransactionID, string errorMessage) 
Overload: Result<T> FailTransactionWithoutActiveTransaction(int interfaceDefID, int parentInterfaceTransactionID, string errorMessage, Result<T> r) 
```

Creates 2 `tInterfaceTransactionLog` records. The first is informational with a message of “Failed calling Child IntefaceDefID {IDValue}”. The second contains the contents of the `errorMessage` string parameter.
