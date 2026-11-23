# Execute

## Summary

`bool Execute()`

This will actually attempt to commit all the queued up changes via the [Add](add) method to the database.

## Examples

`Parent Child Sample`

```csharp
// setup api object
var api = ApiService.GetInstance();

// create UnitOfWork
var uow = api.CreateUnitOfWork();

// create parent area
var area1 = new DbArea();
area1.Name = "Test";
area1 = api.Data.DbArea.Save.InsertAsNew(area1, uow).Return; // does not save to database yet, but does populate ID and DisplayOrder

// creates a child area
var area2 = new DbArea();
area2.Name = "Child Area to Test";
area2.ParentAreaID = area1.ID; // assigns parentArea to area2.
area2 = api.Data.DbArea.Save.InsertAsNew(area2, uow);  // does not save to database yet.

// now saves both areas to the database.
uow.Execute();
```

`Rollback Sample`

```csharp
// setup api object.
var api = ApiService.GetInstance();

// create UnitOfWork
var uow = api.CreateUnitOfWork();

// create area
var area1 = new DbArea();
area1.Name = "Good Area";
area1 = api.Data.DbArea.Save.InsertAsNew(area1, uow).Return; // does not save to database yet, but does populate ID and DisplayOrder

// creates the bad area
var area2 = new DbArea();
area2.Name = "This Area will not save";
area2.ParentAreaID = area1.ID + 50; // ForeignKey violation
area2 = api.Data.DbArea.Save.InsertAsNew(area2, uow); // does not save to database yet.

// result will be false, and area1 and 2 will NOT be saved to the database.
bool result = uow.Execute();
```
