# Add

## Summary

`void Add(string sql)`

This queues up the `Sql` parameter for execution later. All queued statements will be executed when the [Execute](execute) method is run.

## Examples

### Simple Example

```csharp
var uow = api.CreateUnitOfWork();
uow.Add("UPDATE tArea Name = 'Not Yet Done' WHERE ID = 5");

var area = api.Data.DbArea.Load.ByID(5);
Console.WriteLine(area.Name); // will still be the original name.

uow.Execute();

area = api.Data.DbArea.Load.ByID(5);
Console.WriteLine(area.Name); // will now be 'Not Yet Done'.
```
