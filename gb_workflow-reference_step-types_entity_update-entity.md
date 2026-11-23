# Update Entity

This Step Type allows for elements of a standard TrakSYS entity (row from a database table) to be updated with new values. Using the property settings below, up to 5 properties can be updated at once.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Entity Name

This string identifies the "type" of entity to be updated. The value specified should correspond to the database table being targeted, but without the "t" prefix. For example...

* tSystem - specify "System"
* tJob - specify "Job"
* tMaterial - specify "Material"
* Etc..

#### Entity ID

This integer specifies the `ID` value for the entity record to be updated. This value should correspond to the value in the database table's ID field.

### Property 01-05

#### Name

This string specifies the database column name for the entity, that should be updated. For example, if updating the `UserState` field for a `Job`, this property should be set to "UserState".

#### Value

This specifies the value to be updated to the field specified by the `Name` field above.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
