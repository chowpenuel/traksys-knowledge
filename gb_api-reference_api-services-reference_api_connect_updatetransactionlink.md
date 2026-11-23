# UpdateTransactionLink

```csharp
Result<bool> UpdateTransactionLink(string transactionLink, int interfaceTransactionID, [IUnitOfWork uow])
```

This method updates the `tInterfaceTransaction.TransactionLink` field for a given `interfaceTransactionID`. The optional `uow` argument can be used to include the modification as part of a transaction. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.
