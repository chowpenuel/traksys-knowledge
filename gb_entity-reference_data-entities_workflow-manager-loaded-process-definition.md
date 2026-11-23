# Workflow Manager Loaded Process Definition

## Summary

### Entity Name

Workflow Manager Loaded Process Definition

### Database Table Name

`tWorkflowManagerLoadedProcessDefinition`

### API Object Name

`DbWorkflowManagerLoadedProcessDefinition`

### Entity Description

Each entry in this table represents loaded Process Definitions in the Workflow Service. As the service is started, entries will be added. As the service is ended, entries will be removed.

## Properties

`WorkflowManagerID`

This is the unique identifier (primary key) for the Workflow Manager which loads all active Process Definitions.

`ProcessDefinitionID`

Identifies the Process Definition associated with the Loaded Process Definition record.
