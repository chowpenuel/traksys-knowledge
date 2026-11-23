# Process Parameters

Process Parameters can be optionally defined for a Process Definition. Process Parameter Definitions must be defined ahead of time and cannot be dynamically added during the runtime of a Process.

## Scenarios

The two main uses for Process Parameters are described below.

### Process Specific Start Values

In nearly every case, a Process will need to be initialized with some sort of instance specific information. Common examples may include a **JobID** for the Job that is being tracked, or a **TaskID** for the Task that is being monitored for escalation.

### Global Variables within a Process

Sometimes, it is necessary to pass information from one Process Step to another that is far down the diagram chain (not passing values to the next Step). In other cases, values may be required in many different Steps throughout the Process. In these situations, Process Parameters offer a "global" location to set and read variable values.

## Parameter Interaction

### Setting Parameters

There are two ways to set Process Parameter values. First, when a Process is started via the API, initial values can be written to any defined Process Parameters. In addition, during the execution of a Process any Step Output value may be written back to a Process Parameter.

### Reading Parameters

Any Process Parameters are automatically added to the **Process Values** dictionary that is available for initializing Step Inputs. The **Values** Key for accessing a Process Parameters is `Process.<PPD_KEY>` where `<PPD_KEY>` is the Key specified for the Process Parameter Definition. For example, `Process.JobID` or `Process.TaskID`. The exact **Values** Keys can be found by selecting the picker control next to any Process Step property.
