# UpdateEventCategories

```csharp
Result<bool> UpdateEventCategories(int eventID, int eventCategoryID, [IUnitOfWork uow], [bool autoCalcUpdateRequest])
```

Updates the Event of the given Event ID with the provided Event Category ID (and preceding levels). The optional `uow` parameter can be used to ensure this statement is executed as part of a transaction. When true, the optional `autoCalcUpdateRequest` parameter will automatically re-calculate OEE for any intervals affected by the update in Event Categories (this parameter is true by default). The boolean return object conveys whether this method executed successfully.

{% hint style="info" %}
This method also updates the OEE Event Type and the Event Code ID of the Event record based on how the Event Category that is being set is configured.
{% endhint %}

## Examples

### Update an Event Category

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();

    // Add the transaction to the Unit of Work object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    // Provide a valid Event Category ID (from tEventCategory.ID) for the eventCategoryID parameter
    // (Optional): Provide a Boolean value to determine whether to recalculate OEE intervals affected by this update.
    this.Ets.Api.Events.UpdateEventCategories(eventID, eventCategoryID, uow, autoCalcUpdateRequest).ThrowIfFailed();

    // Execute Unit of Work and update the Event Category
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
