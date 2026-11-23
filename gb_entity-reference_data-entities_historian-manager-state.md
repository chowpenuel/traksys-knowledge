# Historian Manager State

## Summary

### Entity Name

Historian Manager State

### Database Table Name

`tHistorianManagerState`

### API Object Name

`DbHistorianManagerState`

### Entity Description

Each entry in this table contains the State and health of each configured Historian Manager. This table can be used to verify each service (for troubleshooting purposes) by ensuring that the service contains the correct state and that the heartbeat is updating.

## Properties

`HistorianManagerID`

Specifies the Historian Manager associated with the current Historian Manager State record.

`State : ETS.Core.Enums.HistorianManagerState`

This is an enumeration representing the State of the Service.

* **Stopped** = 0
* **Starting** = 1
* **Running** = 2
* **Stopping** = 3
* **Unknown** = 1000

`StateDateTime`

Contains the Date/Time stamp of when the Service State was updated.

`OpcQueueCount`

Contains the number of OPC Tag changes queued to be processed for the next scan.

`MqttQueueCount`

Contains the number of MQTT Tag changes queued to be processed for the next scan.

`TagSaveQueueCount`

Specifies the number of Tag Saves queued for the next scan

`SfQueueCount`

Specifies the number of Tag History values queued in Store and Forward, which will be written to the database when immediate Tag value saves are not possible.

`TagChanges`

Specifies the number of Tag changes detected for the current scan.

`TagSaves`

Specifies the number of Tag Saves processed for the current scan.

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
