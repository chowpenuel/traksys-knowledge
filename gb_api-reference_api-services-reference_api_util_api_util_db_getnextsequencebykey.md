# GetNextSequenceByKey

```csharp
int GetNextSequenceByKey(string key)
```

This method increments and returns the next sequence value in the `tSequence` table using the specified `key` argument. The `key` value is a `string` identifying which type of entity for which a sequence value is to be returned. To return the next sequence for the `tSystem` table, the `key` value passed in would be `SystemID`.

The sequence value is the next available primary key (ID) for the specified entity/table.

This method returns the next sequence value if it succeeds, and returns `-1` on failure.

{% hint style="info" %}
If [Model Objects](../../../api-models-reference/api-models/data/db-entity) are being used to insert data from built-in TrakSYS tables, it is not necessary to use this method. The Model Object structure already provides the next ID in sequence for the new record.
{% endhint %}

## Examples

### Get the next System ID

```csharp
// return the next System sequence number
int nextID = api.Util.Db.GetNextSequenceByKey("SystemID");
```
