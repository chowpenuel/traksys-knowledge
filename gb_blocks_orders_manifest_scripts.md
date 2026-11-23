# Scripts

## Shared

### Orders | Blocks Orders

This is the core class for the Blocks Orders API extensions. It contains the basic logic and structure for the other scripts and sets up the extension from the ApiService.

In most implementations, this script is not expected to be changed unless adding new elements to the overall structure.

This class defines the IOrderOperations interface used by the other classes in this Block.

The interface includes the following starting operations:

* ValidateForStart
* Start
* ValidateForEnd
* End
* EnsureBatchAndSteps

Each operation requires a DbSystem object, among other parameters. When calling any of these operations, the logic attempts to find a matching class based upon the related System. It selects the first match, checking for classes matching the naming convention in the following order:

* By the System’s Key \[ {BaseClass}_System_{SystemKey} ]
* By the System Type’s ScriptClassName01
* By the System Type’s Key \[ {BaseClass}_SystemType_{SystemTypeKey} ]
* By the System’s Production Type \[ Discrete or Batch ]

If successful, it returns the proper type and executes the requested operation.

### Orders Enums | Blocks Orders

This script contains the JobState enum.

These values are assigned to the UserState field of tJob records and are used by the **Orders Block** for filtering, validation, and Order processing logic.

### Orders Message | Blocks Orders

This script provides the message handling helpers for the **Orders Block**.

It uses the shared Blocks Message logic to send Order start and end messages for Batch and Discrete Orders.

The script supports the following message types:

* Batch Order Start
* Batch Order End
* Discrete Order Start
* Discrete Order End

Messages are processed with Order and URL replacement values. Order values are loaded from `_viewBlocks_Orders_Job`, and the Details URL is passed in by the calling logic.

Message targets are loaded from the Blocks Message configuration. Targets may be filtered by System Key before sending to configured channels or users.

In most implementations, this script only needs to be changed when adding new Order message types, adding replacement fields, or changing target filtering logic.

### Orders Operations | Blocks Orders

This is the base class for all Orders operation classes.

It contains the default logic for each operation. Logic can be overridden or extended in individual operation classes as needed, but each invokes the base class logic by default.

New System-specific or System Type-specific versions can be created using the proper naming convention and inheriting from this class or one of the Batch or Discrete operation classes.

### Orders Operations Batch | Blocks Orders

This is the base class for Batch Systems.

It contains the same operations as the base Orders Operations class, with Batch-specific logic and the option to override functionality as needed.

### Orders Operations Discrete | Blocks Orders

This is the base class for Discrete Systems.

It contains the same operations as the base Orders Operations class, with Discrete-specific logic and the option to override functionality as needed.
