# Module Step

## Summary

### Entity Name

Module Step

### Database Table Name

`tModuleStep`

### API Object Name

`DbModuleStep`

### Entity Description

Module Steps represent distinct operations that can be configured to run under a parent Module. When the Data Management Service executes a Module, its Module Steps are run in sequence order. The Module is complete after the last Module Step is finished. There are several different types of Module Steps that can be configured. The common Module Step properties are described below followed by the step specific settings.

## Properties

`Module [ ModuleID ]`

Specifies the parent Module.

`Type [Type] : ETS.Core.Enums.ModuleStepType`

Specifies the type of Module Step.

**Script**

**Sql**

**MetricCalculator**

`Execute while True [ ShouldExecuteContent ]`

Specifies a TrakSYS expression which should return 1 or 0. If the expression returns 1, the Module Step will execute. If the expression returns 0, the Module Step will not execute and be skipped. The typical use for this field would be to evaluate an `{args}` value that was set in a previous Module Step.

`On Error [ OnErrorMode ] : ETS.Core.Enums.ModuleStepErrorMode`

Specifies the behavior of the parent Module execution in the event an un-handled error/exception occurs within the Module Step.

**Continue to Next Step** - The current Module Step stops execution and the next step in the sequence is started.

**Exit Module** - The current Module Step stops execution and the parent Module stops. No further Module Steps are executed.

`Step Sequence [ StepSequence ]`

Represents the sequence of step execution within the parent Module.
