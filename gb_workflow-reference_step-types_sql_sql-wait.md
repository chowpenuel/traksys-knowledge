# SQL Wait For

This Step Type periodically executes a provided SQL SELECT statement and examines its results, matching them against some configured values. When the results match the condition, this Step will exit successfully.

Specifies an optional unique identifier (within the Process Definition) for the Step.

Allows for passing values into the SQL statement. The Parameters passed must exist in the **Process Values** passed into this Step.

* **Name** - Specifies the target SQL Parameter `Key`. This will result in a SQL variable being created and useable within the SQL statement below. For example, if **Name** is specified as "JobID", then a SQL variable will be available called `@JobID`.
* **Data Type** - Specifies the Data Type of the value being passed.
* **Default Value** - Specifies the default value to be passed if the actual value cannot be located using the **Key** specified below.
* **Key** - Specifies a `Key` from the **Process Values** to retrieve the value to be passed.

### SQL

Specifies a SQL SELECT statement that will return a single row of data to be examined for a specific condition.

#### Compare Field Name

Specifies a column name that should exist in the results returned by the SQL SELECT specified. The value in the first row for this column will be used as part of the condition evaluation.

Step Evaluation = **Compare Field Value** _Compare Operator_ **Compare to Value**

#### Compare Operator

Specifies a logical operator to be used as part of the condition evaluation.

Step Evaluation = **Compare Field Value** _Compare Operator_ **Compare to Value**

#### Compare to Value

Specifies a fixed value to be used as part of the condition evaluation.

Step Evaluation = **Compare Field Value** _Compare Operator_ **Compare to Value**

#### Output Prefix

This Step also returns the results to the **Process Values**. Each column of the first row returned will be placed into the **Process Values** structure that is passed to subsequent Steps. The `Key` for each value added will be equal to the column name.

When specified, the `Output Prefix` is concatenated to the beginning of the **Process Values** `Keys` that are added by the SQL SELECT specified. For example, if the SQL returns columns ID, Name, Description, and the `Output Prefix` is "Job.", then the following `Keys` are added to the **Process Values**...

* Job.ID
* Job.Name
* Job.Description

Specifies a span of time after which the Step will check/run its periodic execution. For instance, if **Hours** = 1, **Minutes** = 5, **Seconds** = 8, then a Step will execute every (1 \* 3600) + (5 \* 60) + 8 = 3908 Seconds.

## Hours

Specifies an (integer) number of hours.

## Minutes

Specifies an (integer) number of minutes.

## Seconds

Specifies an (integer) number of seconds.

## Force Check Key

Specifies a key that can be used to programmatically force a check.

Specifies a span of time after which a Step will **Timeout** and exit execution.

For example, if `Hours` = 1, `Minutes` = 5, `Seconds` = 8, then a Step will timeout (exit with a Timeout result) if it does not complete successfully after (1 \* 3600) + (5 \* 60) + 8 = 3908 Seconds.

## Timeout After

### Hours

Specifies an (integer) number of hours.

### Minutes

Specifies an (integer) number of minutes.

### Seconds

Specifies an (integer) number of seconds.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
