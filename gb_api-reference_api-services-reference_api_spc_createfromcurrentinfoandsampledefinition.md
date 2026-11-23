# CreateFromCurrentInfoAndSampleDefinition

```csharp
Result<SampleSubGroupData> CreateFromCurrentInfoAndSampleDefinition(DbSampleDefinition sampleDef)
```

This method retrieves the current configuration from the provided Sample Definition to create a new Sample record. It also calculates current info from the active system, such as the current Shift, current Job/Batch, and current process parameters.

If the Sample Definition is associated with a Product Specification Definition, process parameters are calculated from the current Product Specification. Otherwise, process parameters are calculated from current Tag info.

{% hint style="info" %}
This method only generates the `SampleSubGroupData` object. The returned object must be passed into a method such as `Merge()` or `InsertAsNew()` to create the Sample record.
{% endhint %}
