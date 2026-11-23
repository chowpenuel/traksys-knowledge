# RetryInterfaceTransaction

```csharp
Result<int> RetryInterfaceTransation(int interfaceTransactionID)
```

This method retriggers an Interface Definition based on the given `interfaceTransactionID`. The method is typically used in scenarios where the intial call fails and additional retries should be attempted.
