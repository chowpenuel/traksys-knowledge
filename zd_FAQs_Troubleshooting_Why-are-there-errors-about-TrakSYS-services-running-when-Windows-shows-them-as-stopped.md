# Why are there errors about TrakSYS services running when Windows shows them as stopped?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360005461294-Why-are-there-errors-about-TrakSYS-services-running-when-Windows-shows-them-as-stopped*
*Last updated: 2025-05-28T17:57:30Z*

---

Applies To | TrakSYS 10+

This scenario can happen when a backup of the database is taken while the TrakSYS Services are running and the database is restored. There are tables within the TrakSYS Database that keep track of the State (Running, Not Running, Starting, Stopping, etc.) for the Logic, Historian, Data Management, and Workflow Services.

If a backup of the database is taken while the TrakSYS Services are running, these State values will not be properly updated within the respective tables. This could prevent some operations from continuing (e.g. Upgrading a database to a newer version of TrakSYS). As a best practice, it is highly recommended to stop all TrakSYS Services before creating a backup of the database.

This article explains how to update the State for each of the TrakSYS Services.

#### **Logic Service**

The status of the Logic Service is stored within the State field of the tLogicManagerState table. To change the status to the service to "stopped," the field can be updated to contain a value of 0. The following query can be used to update the field:
    
    
    UPDATE tLogicManagerState
    SET State = 0
    WHERE LogicManagerID = --Insert LogicManagerID value here
    

#### **Historian Service**

The status of the Historian Service is stored within the State field of the tHistorianManagerState table. Setting the State field to 0 will set the status of the service to "stopped." The following query can be used to update the field:
    
    
    UPDATE tHistorianManagerState
    SET State = 0
    WHERE HistorianManagerID = --Insert HistorianManagerID value here
    

#### **Data Management Service Modules**

The status of each Module is stored within the State field of the tModuleState table. Setting the State field to 0 for each individual Module will set the status as "stopped." The following query can be used to update the field for an individual Module:
    
    
    UPDATE tModuleState
    SET State = 0
    WHERE ModuleID = --Insert ModuleID value here
    

#### **Data Management Service (TrakSYS 11.2.2+)**

The status of the Data Management Service is stored within the State field of the tModuleManagerState table. Setting the State field to 0 will set the status of the service to "stopped." The following query can be used to update the field:
    
    
    UPDATE tModuleManagerState
    SET State = 0
    WHERE ModuleManagerID = --Insert ModuleManagerID value here
    

#### **Workflow Service**

The status of the Workflow Service is stored within the State field of the tWorkflowManagerState table. Setting the State field to 0 will set the status of the service to "stopped." The following query can be used to update the field:
    
    
    UPDATE tWorkflowManagerState
    SET State = 0
    WHERE WorkflowManagerID = --Insert WorkflowManagerID here
    
    
