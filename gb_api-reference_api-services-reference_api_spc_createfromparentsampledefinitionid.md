# CreateFromParentSampleDefinitionID

{% hint style="info" %}
This method was deprecated in version 12.0.3 and replaced with multiple newer versions to incorporate Product Specifications.
{% endhint %}

```csharp
SampleSubGroupData CreateFromParentSampleDefinitionID(int sampleDefinitionID, [bool shouldCalculateCurrentInfo])
```

This method retrieves the current configuration from an existing Sample Definition by `sampleDefinitionID` to create a new Sample record. The optional `shouldCalculateCurrentInfo` parameter determines if information from currently active, related entities should be included in the record.

{% hint style="info" %}
This method only provides the base settings and configuration to create the Sample record. The `SampleSubGroupData` generated from this method must be passed into a method such as [Merge()](merge) or [InsertAsNew()](insertasnew) in order to create the Sample record.
{% endhint %}
