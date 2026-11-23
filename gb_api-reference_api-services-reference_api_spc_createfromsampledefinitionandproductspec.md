# CreateFromSampleDefinitionAndProductSpec

`csharp Result<SampleSubGroupData> CreateFromSampleDefinition(DbSampleDefinition sampleDef)`

This method retrieves the current configuration from the provided Sample Definition to create a new Sample record.

If the Sample Definition is not associated with a Product Specification Definition, process parameter constants from the Sample Definition are applied to the `SampleSubGroupData`. If the Sample Definition uses a Product Specification Definition, process parameters are expected to come from the Product Specification.

{% hint style="info" %}
This method only provides the base settings and configuration to create the Sample record. The `SampleSubGroupData` generated from this method must be passed into a method such as `Merge()` or `InsertAsNew()` in order to create the Sample record.
{% endhint %}
