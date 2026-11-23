# Logic Service Scan Overview

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004188434-Logic-Service-Scan-Overview*
*Last updated: 2025-05-21T23:12:18Z*

---

Applies To | TrakSYS 10+

### **Summary**

The TrakSYS Logic Service architecture relies on a Scan to process TrakSYS structures and features. This article explains the order of execution of a Logic Scan and explains what an Overscan Log Message means as well as how it is displayed. 

### **Logic Service Scan**

Below is a brief explanation of a typical Logic Service Scan execution and the typical order of execution. In some instances, items may not appear or appear in different places based on configured TrakSYS settings. The Overscan Keys are displayed brackets.

  * Load Tag Configuration [ **InputEngineLoad**]: Handles all of the initial loading of tags into memory.
  * Compile Scripts [ **ScriptEngine.Load** ]: Compiles all Logic Service scripts. This also includes Script Tags.
  * Load Task Configuration [ **TaskEngineLoad** ]: Loads all of the initial Task Definition and Task-related configuration for the Logic Service.
  * Scan Initialization [ **ScanNormalInit**]: Initialize a new scan. This includes updating the Engine Datetime, Validating the License, and Load settings from the database.
  * OPC Initialization [ **OpcQueueMarking**]: Notify the OPC Server that a Scan has started. Prepare to read data from the OPC server.
  * Scheduling Pre-Scan [ **SchedulePreScan**]: Process Shift and Shift History information from the Schedules.
  * Scheduling Post-Scan [ **SchedulePostScan**]: Called after processing of Shift and Shift History information is complete.
  * Tag Engine Initialize [ **InputEngine.Scan**]: Initialize and sort the Tags for execution.
  * Load Virtual Tags [ **VirtualInputScan**]: Load Virtual Tag values from the database to be available for evaluation.
  * Load Smart Tags [ **SmartInputScan** ]: Load all Smart Tags assigned to the Logic Service. This marks any Smart Tag as bad quality if it has not received a value update in the past 30 seconds.
  * Load OPC Tags [ **OpcInputQueue**]: Load all OPC Tags that have changed since the last Scan.
  * Load Simulation Tags [ **OpcInputSimScan**]: Load OPC Tags in Simulation Mode if Simulation Mode is enabled.
  * OPC Tag Maintenance [ **OpcInputScan**]: Perform maintenance on Tag connections. This includes verifying Tag status, verifying connection status, performing Tag reconnects, etc.
  * Access Name Status Update [ **OpcInputSave**]: Evaluate Access Name status and update the TrakSYS database with the status information for use in the TrakSYS Web.
  * Execute Pre-Scan Scripts [ **ScriptEnginePreScan**]: Execute Pre-Scan scripts from the Logic Service scripting engine.
  * Load External Data Connector Tags [ **OleDbScan**]: Load External Data Connector Tags from the external database source.
  * Load OPC HDA Tags [ **OpcHdaScan**]: Load OPC HDA Tags from HDA sources.
  * Load Product Maps [ **ProductEngineScan** ]: Process Product information. Assign Product information, and process Product Mapping.
  * Load State Tags [ **StateScan**]: Load State Tags with TrakSYS state information.
  * Evaluate TrakSYS Tags [ **InputEngineEvaluateTags**]: Process TrakSYS Tags that rely on other trigger Tags. These include Counter Tags, Latch Tags, Switch Tags, Aggregate Tags, Calculation Tags, Script Tags, etc.
  * Write Tag Values to Database [ **SaveWritebackTags**]: Commit all Tag changes and values to the Database based on the Persist to Database Tag setting.
  * Save Queued Tags [ **SaveQueuedVirtualValues**]: Commit queued Virtual Tag values. These could be from other Assign Tags or scripting.
  * Process Jobs(s) [ **JobEngineScan**]: Process Job information. Start new Jobs, Close existing jobs, etc.
  * Process Batch(s) [ **BatchEngineScan**]: Process Batch information.
  * Process Event(s) [ **EventEngineScan**]: Process Events by starting, ending, and splitting Events. 
  * Process KPI Calculation(s) [ **OeeEngineScan**]: Process KPI Calculations by starting, ending and splitting KPI Intervals. Please note that Availability Loss, Performance Loss, and System Not Scheduled fields are no longer by default calculated in a scan. The spUpdateOeeInterval calls are now performed in a parallel process.
  * Process Task(s) [ **TaskEngineScan**]: Process Tasks include created and updated Tasks.
  * Process Transfer/Item(s) [ **TransferEngine**]: Process Location, Transfer Definitions and Item Definition related processes.
  * Process Sample Definitions[ **SampleEngineScan** ]: Processes configured Sample Definitions
  * Process Notifications[ **NotificationEngineScan**]:Queue Notifications to be sent. The TrakSYS Maintenance Service processes the queue and performs the sending of all alerts.
  * Process SignalR Notifications [ **WebEngineScan** ]: Process items that require change (e.g. Refresh Keys). The Logic Service makes Web API posts to the Web Servers notifying them that a Refresh Key requires a refresh.
  * Reconnect Access Name Status Update [ **InputEnginePostEvaluateScan**]: Evaluate Access Name reconnect settings and process Access Name reconnections.
  * Commit Remaining Queue [ **EngineDataCommit**]: Process remaining database statements from queue.
  * Execute Post-Scan Scripts [ **ScriptEngineEngineRunPostScan**]: Execute Post-Scan scripts from the Logic Service scripting engine.
  * Process Last Tag Values [ **UpdatingTagLastValues**]: Record Tag last values for reference in Tag Scripts and State Tags.
  * Update the Logic Manager Session [ **EngineSessionUpdate** ]: Updates the tLogicManagerSession table when tag values are updated after a Logic Scan.
  * Process All Remaining Queued [ **EngineFinalDbCommit**]: Make sure all database statements from queue are processed. This includes any that may have failed due to a database connectivity issue.
  * Cleanup Scan [ **EngineScanCleanup**]: Clear all queues and prepare the Logic Service for the next scan.
  * Scan Complete [ **FinishScan**]: Scan is complete.



#### **Opening the Log**

The TrakSYS log can be viewed in two different areas: the TrakSYS Web and the TrakSYS Installation Manager. It is recommended to view the log in the TrakSYS Web by navigating to **Administration | Diagnostics | Log**.

However, if a user is unable to view the log in the TrakSYS Web, they may do so by opening the TrakSYS Installation Manager and clicking the Diagnostics tab. Then, clicking on the Log Viewer (DB) button to open the Log View window.

#### **Reading Scan Performance Log Entries**

Overscans will be a part of the Scan Performance Category and will contain a message similar to:
    
    
    Scan took 2.00 seconds, starting at 12/5/2017 11:45:38 AM -08:00M

  
In the TrakSYS Web, the details of the overscan are contained in the Data section of the overscan entry. In the Log View page of the TrakSYS Installation Manager, the details of the overscan are stored in the Data pane of the window. In both areas, the details of the overscan will contain a list of keys similar to what is shown above. An example of these details is shown below:
    
    
    -.--- [11:45:38.894]:StartScanNormal   
    -.--- [11:45:38.894]:ScanNormalInit   
    -.--- [11:45:38.894]:OpcQueueMarking   
    -.--- [11:45:38.894]:SchedulePreScan   
    -.--- [11:45:38.894]:SchedulePostScan   
    -.--- [11:45:38.894]:InputEngine.Scan   
    -.--- [11:45:38.894]:VirtualInputScan   
    -.--- [11:45:38.894]:OpcInputQueue   
    -.--- [11:45:38.894]:OpcInputSimScan   
    -.--- [11:45:38.894]:OpcInputScan   
    -.--- [11:45:38.894]:OpcInputSave   
    -.--- [11:45:38.894]:ScriptEnginePreScan   
    -.--- [11:45:38.894]:OleDbScan   
    -.--- [11:45:38.894]:OpcHdaScan   
    -.--- [11:45:38.894]:StateScan   
    -.--- [11:45:38.894]:InputEngineEvaluateTags   
    -.--- [11:45:38.894]:SaveWritebackTags   
    1.891 [11:45:40.784]:SaveQueuedVirtualValues   
    0.047 [11:45:40.831]:JobEngineScan   
    -.--- [11:45:40.831]:BatchEngineScan   
    -.--- [11:45:40.831]:EventEngineScan   
    -.--- [11:45:40.831]:OeeEngineScan   
    0.016 [11:45:40.847]:TaskEngineScan   
    -.--- [11:45:40.847]:TransferEngine   
    -.--- [11:45:40.847]:SampleEngineScan   
    -.--- [11:45:40.847]:NotificationEngineScan   
    -.--- [11:45:40.847]:WebEngineScan   
    -.--- [11:45:40.847]:InputEnginePostEvaluateScan   
    -.--- [11:45:40.847]:EngineDataCommit   
    -.--- [11:45:40.847]:ScriptEngineEngineRunPostScan   
    -.--- [11:45:40.847]:UpdatingTagLastValues   
    -.--- [11:45:40.847]:EngineSessionUpdate   
    0.047 [11:45:40.894]:EngineFinalDbCommit   
    -.--- [11:45:40.894]:EngineScanCleanup   
    -.--- [11:45:40.894]:FinishScan

Reading a Scan Performance log entry can be misleading. The time value for how long each scan item took is displayed in the line below the Scan Key. For example:

-.--- [11:45:38.894]:**SaveWritebackTags**  
**1.891** [11:45:40.784]:SaveQueuedVirtualValues

In the snippet above notice that the SaveWritebackTags and 1.891 are bolded. This is because the 1.891 seconds to execute the Scan Key section belongs to SaveWritebackTags and not SaveQueuedVirtualValues.
