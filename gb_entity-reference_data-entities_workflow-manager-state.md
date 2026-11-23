# Workflow Manager State

## Summary

### Entity Name

Workflow Manager State

### Database Table Name

`tWorkflowManagerState`

### API Object Name

`DbWorkflowManagerState`

### Entity Description

Each entry in this table contains the State and health of each configured Workflow Manager. This table can be used to verify each service (for troubleshooting purposes) by ensuring that the service contains the correct state and that the heartbeat is updating.

## Properties

`WorkflowManagerID`

Identifies the Workflow Manager associated with the Workflow Manager State record.

`State : ETS.Core.Enums.WorkflowManagerState`

This is an enumeration representing the State of the Service.

* **Stopped** = 0
* **Starting** = 1
* **Running** = 2
* **Stopping** = 3
* **Stalled** = 21

`IsLastRunContainer`

Contains a Boolean value that determines whether the service was last run in a Container. A value of 1 (or True) means that the service was run in a container, while a value of 0 (or False) means the service was run normally outside of a container.

`ContainerState : ETS.Core.Enums.ContainerServiceState`

This is an enumeration representing the State of the Container hosting the service.

* **UseServiceState** = 0
* **RestartingAsAContainer** = 1
* **RunningAsAContainer** = 2
* **StoppingAsAContainer** = 3

`ContainerRequest`

This is an enumeration representing the State of the current request sent to the Container service.

* **None** = 0
* **Restart** = 2
* **Stop** = 3

`ContainerRequestDateTime`

Specifies the Date/Time stamp of when the Container service request was made.

`HeartbeatDateTime`

Contains the date and time of the heartbeat value for the Service. This value should be constantly changing, which indicates that the service is actively running.

`HaHeartbeatDateTime`

Contains the date and time of the heartbeat value for the Service on the secondary failover machine. This value should be constantly changing, which indicates that the service is actively running and is ready for a failover if needed.

`HaHostMaster`

Contains the host name of the current, primary machine. The Service High Availability feature needs to be available to modify this setting.

`HaState : ETS.Core.Enums.HaState`

This is an enumeration representing the State of the Service on the secondary failover machine.

* **NotRunning** = 0
* **StartingHost** = 1
* **StartingHostHa** = 2
* **SwitchingToHost** = 3
* **SwitchingToHostHa** = 4
* **RunningAsHost** = 5
* **RunningAsHostHa** = 6
* **Stopping** = 7
* **Stopped** = 8

`HaRequest : ETS.Core.Enums.HaState`

This is an enumeration representing the High Availability request status of the Service.

* **None** = 0
* **Start** = 1
* **SwitchToHost** = 2
* **SwitchToHostHa** = 3
* **Shutdown** = 4
* **Stop** = 5
