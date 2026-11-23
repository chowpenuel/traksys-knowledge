# Types of Logging in TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6827052105235-Types-of-Logging-in-TrakSYS*
*Last updated: 2026-07-22T21:06:13Z*

---

Applies To | TrakSYS 10+

When diagnosing issues in the TrakSYS software, several different types of logging are available. Each location will store different types of information depending on the issue and message logged. These locations include:

  * The TrakSYS Log File (tLog)
  * The tLogCustom table (TrakSYS 10.2.3+)
  * The Windows Event Viewer
  * Failed .sql files
  * The LogicManagerService.txt file
  * The Logic.txt file (TrakSYS 10.2.2+)



The following describes the different type of log files that are created, the type of information they provide, and where they are located.

#### **TrakSYS Log File (tLog)**

This is the primary TrakSYS log file where a large majority of messages are stored. Many system messages from all services (Logic, Historian, Data Management, Workflow, and Maintenance Services) are recorded here. Custom messages can also be logged here with the TrakSYS API using the LogUtilityService (such as `Api.Util.Log.`[`WriteError()`](https://docs.parsec-corp.com/api-reference/api-services-reference/api.util/api.util.log/writeerror)).

This log file can be viewed directly within the TrakSYS Web by navigating to **Administration | Diagnostics | Log**. It can also be accessed using the TrakSYS Installation Manager by going to the Diagnostics tab and clicking the "Log Viewer (DB)" button. The log file can also be exported directly from the TrakSYS Installation Manager as explained [**here**](https://portal.parsec-corp.com/hc/en-us/articles/115003466434-Exporting-the-TrakSYS-Log).

By default, the tLog table can contain up to 10,000 entries. Once this point is reached, the Maintenance Service will automatically delete log records starting with the oldest record until the row count reaches 10,000 records. The number of allowed entries can be changed by going into the TrakSYS Settings and modifying the MaxLogRows value under the Logging section. Changing these settings will not require any type of service restart.

**![](https://portal.parsec-corp.com/hc/article_attachments/16250943329555)**

**Note** : increasing the MaxLogRows value will require more disk space for logging purposes. It is strongly recommended to verify the available disk space before making this change.

#### **tLogCustom (TrakSYS 10.2.3+)**

This logging table is used to write custom messages for extensibility purposes. Nothing within TrakSYS will write log entries to the table automatically. Similar to the tLog table, custom messages are logged with the TrakSYS API using the CustomLogUtilityService (such as `Api.Util.LogCustom.Write()`). Unlike the tLog table, this table does not have a built-in log viewer. However, entries can still be queried with custom code or viewed in SQL Server Management Studio as needed.

By default, the tLogCustom table can contain up to 50,000 entries. Once this point is reached, the Maintenance Service will automatically delete log records starting with the oldest record until the row count reaches 50,000 records. The number of allowed entries can be changed by going into the TrakSYS Settings and modifying the MaxCustomLogRows value under the Logging section. Changing this setting will not require any type of service restart.

**![](https://portal.parsec-corp.com/hc/article_attachments/16250946821651)**

**Note** : increasing the MaxCustomLogRows value will require more disk space for logging purposes. It is strongly recommended to verify the available disk space before making this change.

Using this table for logging purposes is strongly recommended in scenarios where a large amount of custom logging will be performed. Since the tLogCustom table has a separate limit from tLog, this can prevent flooding of the tLog table. This allows auto-generated system and error messages to be maintained for a longer period of time before being removed by the Maintenance Service. It can also make finding specific, custom messages much easier as system-generated messages are excluded from this table.

#### **Windows Event Viewer**

Log entries are created in the Windows Event Viewer log when TrakSYS attempts to create entries in tLog, but fails. A large majority of these log entries will appear under **Windows Logs | Application**. In addition to errors and failed log entries, some types of system generated messages from the TrakSYS services can appear in this location. For example, every time the TrakSYS Web Application is started, entries will appear in the Event Viewer for this event.

#### **Failed .sql files**

These files are stored in CommonApplicationData (which is usually **C:\ProgramData**). Note that the ProgramData folder is typically hidden and can be displayed within the folder options of the Windows File Explorer. These files can contain failed query executions by the Logic Service for Event and OeeInterval operations. When the files are created, the file name will contain a format of `failed{now:yyyy-MM-dd HH}.sql`. These files can be created once per hour and will contain a list of queries that failed for that hour.

The Logic Service will attempt to execute these queries multiple times, but will stop after a certain number of tries. Instead of deleting the data, the queries are logged to the files. This allows users to open the .sql files and manually execute the queries at a later date. The queries will contain timestamps of when they failed for troubleshooting purposes.

#### **LogicManagerService.txt**

This file can be found in CurrentDirectory (which is usually **...\Program Files (x86)\Parsec\TrakSYS\logicmanagerservice.txt** for TrakSYS 11.2.5 and older or **...\Program Files\Parsec\TrakSYS\logicmanagerservice.txt** for TrakSYS 12). This file will contain error messages from the Logic Service when the application is not connected to the database. **Note** : if this file is not in the root TrakSYS folder, this means that there are no error messages that have met the criteria for being recorded in this file.

#### **logic.txt (TrakSYS 10.2.2+)**

This file can be found in CommonApplicationData (which is usually **C:\ProgramData**). The purpose of this file is to capture when the Logic Service is starting up or shutting down. This is done to notify any users troublehooting the Logic Service that the service has the appropriate write access to this folder.
