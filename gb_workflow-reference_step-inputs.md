# Step Inputs

Each Step Type exposes a set of Inputs (also referred to as Step Properties) that allow specification of Step behavior. These Properties may be set at configuration time by specifying fixed values, or dynamically at runtime by mapping to incoming **Process Values** entries.

## Property Entry

Specifying the value for most Step Inputs (properties) consist of setting a fixed value and an optional mapping to a **Process Value** Key. The UI for these Inputs consists of two entry fields laid out side by side.

### Constant

The first entry field allows the setting of a constant fixed value at configuration time. Some Inputs require a constant to be typed into a text field, while others expose a "picker" to select from a list of values.

### Values Key

The second entry field allows the mapping of a **Process Values** Key to the Input. When provided, the Workflow engine maps the specified value to the Input when the Step starts. If the specified Key cannot be located in the **Process Values**, the engine defaults back to the constant value configured int the first entry field.

## Special Properties

In some cases, Step Types expose custom editors and entry fields for some Properties. Examples include...

* **SQL Parameter Mapping**
* **SQL Statement**
* **Script Editor**
