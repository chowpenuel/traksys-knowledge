# MergeOeeData

```csharp
OeeData MergeOeeData(List<OeeData> source, [double nanValue])
```

This method returns a single OeeData object, which is an aggregation of multiple OeeData objects that are passed in as the `source` parameter.

If a calculation results in a divide by zero error (NaN), the value will be set to the `nanValue` parameter.

## Examples

### Merge multiple OeeData objects into a single OeeData object

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid OEE Calculation ID (from tOeeCalculation.ID)
    int oeeCalculationID = 18;
    // Provide Job ID values (from tJob.ID)
    int job1ID = 7;
    int job2ID = 8;
    int job3ID = 9;

    // Create a List to hold multiple OeeData objects
    List<ETS.Core.Api.Models.Kpi.OeeData> jobOeeData = new List<ETS.Core.Api.Models.Kpi.OeeData>();

    // Populate the List with OeeData objects
    jobOeeData.Add(this.Ets.Api.Kpi.LoadOeeDataByJobID(job1ID, oeeCalculationID).ThrowIfLoadFailed("JobID", job1ID));
    jobOeeData.Add(this.Ets.Api.Kpi.LoadOeeDataByJobID(job2ID, oeeCalculationID).ThrowIfLoadFailed("JobID", job2ID));
    jobOeeData.Add(this.Ets.Api.Kpi.LoadOeeDataByJobID(job3ID, oeeCalculationID).ThrowIfLoadFailed("JobID", job3ID));

    // Merge the multiple OeeData objects into a single, unified OeeData object
    // (Optional): Provide a NaN value for the nanValue parameter. 
    // This value will be returned if a divide by zero error occurs while loading data
    ETS.Core.Api.Models.Kpi.OeeData mergedOeeData = this.Ets.Api.Kpi.MergeOeeData(jobOeeData, nanValue);

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
