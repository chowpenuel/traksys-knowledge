# Process Actions

The following sections describe common interactions with a Workflow Process. These descriptions contain conceptual summaries. Specific examples for referenced TrakSYS API calls can be found in the [API Reference](../api-reference).

## Testing

During the early stages of developing a Workflow Process Definition, it may be desireable to repeatably "run" or "execute" a Process to test its behavior. The following procedure can be used to start a new instance of a Process Definition during development.

* Make desired modifications to a Process Definition to be started.
* Restart the Workflow Service (so that the latest changes to the Process Definition are loaded).
* Navigate to the Item Slice for the Process Definition.
* Click the **New Process** link under the **Actions** section of the Item Slice.
* Provide appropriate values for the Process Start Sink message...
  * **Process Key** - An optional unique identifier for the Process.
  * **Process Step Definition** - An optional directive to "start" at a specific Start Step Type.
  * **Entity ID, Entity Key, Description and System** - Optional identifiers to help select or filter for specific Processes (reporting and troubleshooting).
  * **Process Sink Data** - A JSON object containing values for all defined Process Parameter Definitions.
* Clicking the OK button will submit a Start Sink message and the running Workflow Service will start a new Process.

{% hint style="info" %}
The Workflow Service will only load Process Definitions in the **Draft** State if the underlying license is a "development" version (Development, Partner, Consignment).
{% endhint %}

## Starting

Starting a new Process (an instance of a configured Process Definition) is done using a series of API calls. The sections below describe a simple/typical example of starting a Process from a TS Web page.

### Create Parameters Dictionary

Create and populate a Dictionary object with any Process Parameters (note these must match defined Process Parameters for the target Process Definition).

```csharp
var prms = new Dictionary<string, object>();
prms.Add("SystemID", 2);
prms.Add("JobID", 42);
```

### Create a DbProcessSink Start Object

Create a Sink message object using a Workflow API helper method. The Process Definition Key is required ("CO" in the example below).

```csharp
var res = this.Ets.Api.Workflow.CreateProcessSinkStartWithEntity("CO", job.ID, prms);
if (!res.Success) this.Ets.Debug.FailFromResultMessages(res.Messages);
var sink = res.Return;
```

### Additional Population of the DbProcessSink

Populate any optional fields in the Sink message.

```csharp
sink.Description = "Customer Order {0}".ToString(job.Name);
sink.ProcessKey = "CO_{0}".FormatWith(job.ID);
```

### Save the DbProcessSink

Use the standard API Insert method to save the Sink message. Once the Sink message is saved, the Workflow Service will start and create a Process for the requested Process Definition.

```csharp
this.Ets.Api.Data.DbProcessSinkStart.Save.InsertAsNew(sink);
```

## Killing

There are 2 methods of Killing an executing process as described below.

### Administrator Page

Standard TrakSYS pages within the **Administration** Section of TS Web allow for all executing Processes to be listed and viewed. The Process lists contain operations to issue a Kill command, notifying the Workflow Service to immediately cease execution of the specified Process.

* Navigate to **Administration | Services | WF**.
* Select the **Processes** link under **Related**.
* A list of executing Processes are listed.
* Select the Process to be stopped and click its **Kill** action.

### Using the API

An executing Process can be killed using API calls. Below is a simple/typical example of killing a Process from a TS Web page.

```csharp
// locate and load target process with Key = 123456
var process = this.Ets.Api.Data.DbProcess.Load.WithSql("SELECT * FROM tProcess WHERE ProcessKey = {0}".FormatWith("123456".ToSql()));

// call kill method
var res = this.Ets.Api.Workflow.KillProcess(process.ID);
if (!res.Success) this.Ets.Debug.FailFromResultMessages(res.Messages);
```

## Force Check

Some Workflow Step Types are designed to "wait" for a specific condition to occur. These Steps can be configured to "check" for the condition on a fixed interval (every 5 seconds, every 10 minutes, etc...). In some cases, the TrakSYS application may know that a specific condition has changed and it is desired for the Workflow Process (Step) to check its condition immediately, before the configured check interval has expired.

An executing Process Step can be "bumped" to force a check of its condition using API calls. Below is a simple/typical example of forcing a check from a specific Process Step from a TS Web page.

{% hint style="info" %}
The example below assumes that the target Process has at least one Step configured with a `Force Check Key` property set to "CHECK\_1". Any Step configured with a `Force Check Key` property set to "CHECK\_1" and is currently "waiting" will be forced to check its condition when this message is received.
{% endhint %}

```csharp
// locate and load target process with Key = 123456
var process = this.Ets.Api.Data.DbProcess.Load.WithSql("SELECT * FROM tProcess WHERE ProcessKey = {0}".FormatWith("123456".ToSql()));

// call force check method
var res = this.Ets.Api.Workflow.ForceStepCheck(process.ID, "CHECK_1");
if (!res.Success) this.Ets.Debug.FailFromResultMessages(res.Messages);
```
