# State Machine Transition

## Summary

### Entity Name

State Machine Transition

### Database Table Name

`tStateMachineTransition`

### API Object Name

`StateMachine`

### Entity Description

Each row in this table represents a Transition between State Machine States.

## Properties

`State Machine ID [ StateMachineID ]`

The parent State Machine under which the Transition is configured.

`From State Machine State ID [ FromStateMachineStateID ]`

The State Machine State from which the Transition is occurring.

`To State Machine State ID [ ToStateMachineStateID ]`

The State Machine State to which the Transition is occurring.

`Prerequisite Script [ PrerequisiteScript ]`

Validation script used to check if the current Transition is possible.

`Execute Script [ ExecuteScript ]`

Script used to execute specific business rules when the Transition occurs.
