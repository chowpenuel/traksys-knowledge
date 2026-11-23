# SetNextSequenceToModel

```csharp
bool SetNextSequenceToModel(IIntKeyModel model)
```

This method sets the `model` argument's ID property to the next value in the `tSequence` table for that `model`'s type.

This method returns `false` if the specified model is `null` OR assigning the sequence value failed. It returns `true` if the specified model already has a sequence value OR assigning the sequence value was successful.

{% hint style="info" %}
If [Model Objects](../../../api-models-reference/api-models/data/db-entity) are being used to insert data from built-in TrakSYS tables, it is not necessary to use this method. The Model Object structure already provides the next ID in sequence for the new record.
{% endhint %}

## Examples

### Set the ID Property of a System with the next Sequence

```csharp
// set the ID of a DbSystem object to the next sequence
ETS.Core.Api.Models.Data.DbSystem system = new ETS.Core.Api.Models.Data.DbSystem();
system.Name = "New System";
system.AreaID = 2;
system.Enabled = true;
api.Util.Db.SetNextSequenceToModel(system);
```
