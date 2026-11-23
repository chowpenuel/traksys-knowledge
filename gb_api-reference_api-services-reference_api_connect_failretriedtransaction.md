# FailRetriedTransaction

```c
Result<bool> FailRetriedTransaction(int sourceInterfaceTransactionID, string errorMessage) 
Overload: Result<T> FailRetriedTransaction(int sourceInterfaceTransactionID, string errorMessage, [Result<T> r]) 
```

Creates 2 `tInterfaceTransactionLog` records. The first is informational with a message of "Failed retrying Transaction". The second contains the contents of the `errorMessage` parameter passed in.
