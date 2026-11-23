# Get Entity Value

This Step Type allows for a standard TrakSYS entity (row from a database table) to be loaded and its field values to be injected into the **Process Values** passed to subsequent Steps.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Entity Name

This string identifies the "type" of entity to be loaded and returned. The value specified should correspond to the database table being targeted, but without the "t" prefix. For example...

* tSystem - specify "System"
* tJob - specify "Job"
* tMaterial - specify "Material"
* Etc..

#### Entity ID

This integer specifies the **ID** value for the entity record to be loaded. This value should correspond to the value in the database table's ID field.

#### Output Prefix

This prefix will be appended to the front of the column's name to create the Values `Key` inserted into the **Process Values**. For example, if a `System` entity is loaded, and the `Output Prefix` is provided as "Sys.", then the following entries will be added to the **Process Values**...

* Sys.ID
* Sys.Name
* Sys.AltName
* Sys.Enabled
* Etc...

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
