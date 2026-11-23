# TagData

This class is primarily used to pass parameters to the `BulkTagOperations` class. The `ID` property should be unique when calling methods. The `Value` typically contains the `tTag.ID` for a given Tag, but it can be a different value if needed.

## Properties

```csharp
public int ID { get; set; }
public string ItemName { get; set; }
public object Value { get; set; }
```
