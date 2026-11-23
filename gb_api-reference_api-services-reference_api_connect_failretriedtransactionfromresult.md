# FailRetriedTransactionFromResult

```c
Result<bool> FailRetriedTransactionFromResult(string errorMessage, IResult result, int sourceInterfaceTransactionID) 
Overload: Result<T> FailRetriedTransactionFromResult(string errorMessage, IResult result, int sourceInterfaceTransactionID, Result<T> r) 
```

Creates 2 `tInterfaceTransactionLog` records. The first is informational with a message of “Failed retrying Transaction”. The second contains the contents of the `errorMessage` and `result` parameters passed in.
