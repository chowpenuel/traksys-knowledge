# SQL Parameters

Allows for passing values into the SQL statement. The Parameters passed must exist in the **Process Values** passed into this Step.

* **Name** - Specifies the target SQL Parameter `Key`. This will result in a SQL variable being created and useable within the SQL statement below. For example, if **Name** is specified as "JobID", then a SQL variable will be available called `@JobID`.
* **Data Type** - Specifies the Data Type of the value being passed.
* **Default Value** - Specifies the default value to be passed if the actual value cannot be located using the **Key** specified below.
* **Key** - Specifies a `Key` from the **Process Values** to retrieve the value to be passed.
