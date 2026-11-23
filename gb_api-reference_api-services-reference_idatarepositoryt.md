# IDataRepository\<T>

## Summary

The `IDataRepository<T>` classes handles all the basic CRUD (Create, Read, Update and Delete) data access operations all in one class. To maintain an easy to use class, the class only supports tables that have the primary key defined as its own unique ID.

## Examples

### Basic CRUD Operation

```csharp
var repo = api.Data.Util.Db.CreateDataRepository<DbArea>();
// try and find any root node areas
List<DbArea> areaList = repo.LoadListByInt(-1, x => x.ParentAreaID);
DbArea area;
Result<DbArea> result;
if (areaList.Count == 0) // create a new root area
{
    area = new DbArea();
    area.Name = "Root";
    result = repo.InsertAsNew(area);
}
else // update the first existing root area.
{
    area = areaList[0]; // first Area
    area.Description = "Is being modified";
    result = repo.UpdateExisting(area);
}
```
