# GetNextSequenceLongByKey

```csharp
long GetNextSequenceLongByKey(string key)
```

This method increments and returns the next sequence value in the `tSequence` table using the specified `key` argument. The `key` value is a `string` identifying which type of entity for which a sequence value is to be returned.

The sequence value is the next available primary key (ID) for the specified entity/table.

This method returns the next sequence value if it succeeds, and returns `-1` on failure.

{% hint style="info" %}
If [Model Objects](../../../api-models-reference/api-models/data/db-entity) are being used to insert data from built-in TrakSYS tables, it is not necessary to use this method. The Model Object structure already provides the next ID in sequence for the new record.
{% endhint %}

{% hint style="warning" %}
This method is mainly used for implementation scenarios that leverage the tSequence table and require ID values or unique identifiers that go beyond the 32-bit Integer limit (2,147,483,647). This method should not be used with built-in TrakSYS tables as all ID fields are set to 32-bit Integers.
{% endhint %}
