# Versioning

Parameter Definitions support the concept of **versioning**. As Processes are started and processed by the Workflow Service, the **version** of the Process Definition is saved and maintained. A Workflow Process will always complete its execution with the **version** configuration as it was started, regardless of Workflow Service restarts.

## Process Definition Family

A single Process Definition concept may end up having several Process Definition records at any given time (some in `Drafts`, and `Active` and possibly several `Retired`). The collection of related Process Definitions is commonly referred to as a **Family**.

## Version Numbers

Process Definition version numbers are whole integers and are automatically managed/incremented when new `Draft` records are created.

## Version States

### Draft

When a new Process Definition is created, it begins in the `Draft` state. It is expected that as a Process Definition is developed, it stays in the `Draft` state while being adjusted for testing and debugging. Once a stable, the Process Definition can be moved to the `Active` state.

`Draft` Process Definitions can be created in the following ways...

* When a new Process Definition is created for the first time, it starts in the `Draft` state.
* A new `Draft` can be created from the current `Active` Process Definition.
* A new `Draft` can be created from any `Retired` Process Definition.

There can be multiple `Draft` Process Definitions in existence at any point for a given Family.

### Active

Once a Process Definition is in an `Active` state, it is eligible for being started and (Processes created) in the Workflow Service.

An `Active` Process Definition can only be created by selecting an existing `Draft` and converting it to `Active`.

There can be only one `Active` Process Definition at any time for a given Family. When a `Draft` is converted to `Active`, the current `Active` Process Definition is automatically converted to `Retired`.

### Retired

`Retired` state Process Definitions are maintained for historical reference.

`Retired` Process Definitions can be created in the following ways...

* Selecting an `Active` Process Definition and converting it to `Retired`.
* When a `Draft` is converted to `Active`, the current `Active` Process Definition is automatically converted to `Retired`.

There can be multiple `Retired` Process Definitions in existence at any point for a given Family.

## Development Scenarios

Any Workflow Service running with a **Development** license (Partner, Consignment, or Non-Production) will be capable of loading and running `Draft` Process Definitions.

Conversely, a Production licensed Workflow Service will only load and run a Process if an `Active` Process Definition exists.

When a Development Workflow Service is restarted, any Processes based on `Draft` Process Definitions will be cleared/deleted based on the `Delete Draft Processes on Service Start` property.
