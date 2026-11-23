# Process Values

As a Workflow Process is executed, a mechanism is provided to pass values into and out of each Step in the progression. This mechanism is the **Process Values Dictionary** (may be abbreviated to **Process Values** or just **Values** in later descriptions).

The **Process Values** is very similar in concept to the **Values Dictionary** in the TS Web Page and Part framework. It is a .NET Dictionary object which can hold any number of objects referenced by a string Key. The **Values** is populated/managed by the Workflow engine and is passed around (in/out) of each Step as it is executed.

## Values Initialization

At the start of each Step, the Workflow engine creates a new **Values** set and initializes it with the following...

### Process Parameters

The current value of all Process Parameters are added to the **Values**. This may be the Parameter values that were set when the Process started, or it may be new values that have been written to the Process Parameters by a previous Step in the execution.

The **Values** Key for accessing a Process Parameters is `Process.<PPD_KEY>` where `<PPD_KEY>` is the Key specified for the Process Parameter Definition. For example, `Process.JobID` or `Process.TaskID`. The exact **Values** Keys can be found by selecting the picker control next to any Process Step property.

### Outputs from the Previous Step

All outputs from the previously executed Step are added and available in the **Values**. The specific Keys added are dependent on the behavior of the previous Step. Built-in Step Types have fixed output values that are always emitted, but may also create dynamic outputs (for example SQL Get Values, Get Entity Value, etc...). Script Step Types may insert any number of dynamic values into the **Process Values**.

### Workflow Engine Values

The Workflow engine provides some standard environmental values in every Step. There are two types of standard values provided (described below). The exact **Values** Keys can be found by selecting the picker control next to any Process Step property.

**Previous Step** - Every Step emits a consistent subset of outputs to the **Values**. They include Result states and execution start/end and duration.

**Standard** - These universal values are always maintained and provided throughout the execution process. The Keys for these are all prefixed with `ETS.`. They include entity IDs for the Process being executed, Site and current Date/Time.

## Consuming Values

**Values** may be consumed by any of the following methods...

### Direct Reference

Entering the **Values** Key into the Key input entry field for any Process Step property will map the value into that property at runtime.

### Picker Assignment

Selecting the "picker" icon next to the Key input entry field for any Process Step property will display a list of known **Values** entries to select from. Selecting an entry will assign the correct Key name into source Key input entry field.

### SQL Mapping

Within SQL Step editors, **Values** entries can be referenced by Key and mapped to a new SQL variable (useable within the SQL statement).

### Script

Within Script Step code, the **Values** may be referenced directly using the following syntax...

```csharp
int systemID = ets.Values.GetAsInt("SystemID");
```

## Writing to Values

Other than built-in, fixed Step Type outputs, **Values** may be created by any of the following methods...

### Step Dynamic Outputs

The following Step Types allow for the dynamic creation of **Values** entries based on the configured behavior...

* Entity Get Value
* SQL Get Values

### Script

Within Script Step code, items may be added or modified in **Values** using the following syntax...

```csharp
result.Outputs["TaskID"] = 23;
```

In the above example, a **TaskID** entry will be created in the **Values** that are passed to the next Step. If the `TaskID` entry already existed, this assignment would update its value.
