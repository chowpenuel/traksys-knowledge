# LoadListByInt

## Summary

`List<T> LoadListByInt(int filterValue, Expression<Func<T, int>> prop)`

`List<T> LoadListByInt(int filterValue, string property)`

This method will dynamically build the Sql needed to query the table, automatically, considering a value of `-1` in the `filterValue` field to represent `IS NULL`. The method with the `Expression` parameter is used to create a compile time check when building custom SQL. This is recommended over the `string property`, as it minimizes any misspelling errors that may occur.

## Examples

### Shows both Calls

```csharp
int locID = 180;
var repo = api.Data.Util.Db.CreateDataRepository<DbItem>();
List<DbItem> itemList = repo.LoadListByInt(locID, x => x.LocationID);
// essentially the same statement as above
List<DbItem> itemList2 = repo.LoadListByInt(locID, "LocationID");
```
