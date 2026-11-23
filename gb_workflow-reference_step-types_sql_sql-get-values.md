# SQL Get Values

This Step Type allows for a SQL SELECT statement to be executed and the resulting data injected into the Output Values structure passed to subsequent Steps.

Specifies an optional unique identifier (within the Process Definition) for the Step.

Allows for passing values into the SQL statement. The Parameters passed must exist in the **Process Values** passed into this Step.

* **Name** - Specifies the target SQL Parameter `Key`. This will result in a SQL variable being created and useable within the SQL statement below. For example, if **Name** is specified as "JobID", then a SQL variable will be available called `@JobID`.
* **Data Type** - Specifies the Data Type of the value being passed.
* **Default Value** - Specifies the default value to be passed if the actual value cannot be located using the **Key** specified below.
* **Key** - Specifies a `Key` from the **Process Values** to retrieve the value to be passed.

### SQL

Specifies a SQL SELECT statement to be executed when this Step runs. The SELECT statement should return a single row of data. Each column of the first row returned will be placed into the Output Values structure that is passed to subsequent Steps. The `Key` for each value added will be equal to the column name.

#### Output Prefix

When specified, this string is concatenated to the beginning of the **Process Values** `Keys` that are added by the SQL SELECT specified. For example, if the SQL returns columns ID, Name, Description, and the `Output Prefix` is "Job.", then the following `Keys` are added to the **Process Values**s...

* Job.ID
* Job.Name
* Job.Description

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
