# Database

The Database section of the TrakSYS Installation Manager displays current database connection details and provides key database operations.

## Connection Settings

Displays details regarding the Server Name, Database Name, Login Type, and Login.

## Connection Status

Displays whether or not TrakSYS is connected to the database.

## Versions

Displays the TrakSYS Software Version, the TrakSYS database Version, SQL Server Version, and SQL Server Edition.

## Historian Connection Status

Displays whether or not TrakSYS is connected to a Historian database as well as the Historian database version.

## Actions

### Edit Connection

Displays a dialog to enter the database server connection details and includes a button to test the connection. The Connect Timeout property determines how long (in seconds) to wait upon trying to connect to the database server before timing out. The Command Timeout property determines how long (in seconds) to wait upon command execution before timing out. The default Command Timeout is -1 which uses the default value configured in SQL Server (typically 30 seconds). A Command Timeout value of 0 will apply no timeout.

### Repair Logins

Provides a dialog to reset the default edbApp user given a login which has full administrative access to the database server. The Connect Timeout property determines how long (in seconds) to wait upon trying to connect to the database server before timing out. The Command Timeout property determines how long (in seconds) to wait upon command execution before timing out. The default Command Timeout is -1 which uses the default value configured in SQL Server (typically 30 seconds). A Command Timeout value of 0 will apply no timeout.

### Create Database

Provides a dialog to create an empty TrakSYS database on the local machine. The dialog prompts for a connection that has full administrative access to the SQL Server on the local machine. The Connect Timeout property determines how long (in seconds) to wait upon trying to connect to the database server before timing out. The Command Timeout property determines how long (in seconds) to wait upon command execution before timing out. The default Command Timeout is -1 which uses the default value configured in SQL Server (typically 30 seconds). A Command Timeout value of 0 will apply no timeout.

### Create Historian

Provides a dialog to create a TrakSYS Historian database based on the already configured TrakSYS database. The dialog prompts for a connection that has full administrative access to the SQL Server on the local machine. The Connect Timeout property determines how long (in seconds) to wait upon trying to connect to the database server before timing out. The Command Timeout property determines how long (in seconds) to wait upon command execution before timing out. The default Command Timeout is -1 which uses the default value configured in SQL Server (typically 30 seconds). A Command Timeout value of 0 will apply no timeout.

### Transfer Export

The Transfer Export dialog allows exporting of Configuration and User Interfaces. Configuration includes configured entities under the Configuration Section of the application, such as Systems, Tags, etc. User Interfaces include any Sections, Hubs, and Spokes created under the Development Section of the application. After selecting the type of Export, there is a prompt to determine where the Export file will be saved. Transfers are typically used to keep development (source) and production (target) environments in sync. Note: this transfer process has taken the place of the EDB Transfer tool from previous versions of TrakSYS.

### Transfer Import

The Transfer Import dialog simply prompts for the location of the file to be imported. Importing will overwrite values (Configuration and/or User Interfaces) in the target TrakSYS database. At the end of a Transfer Import, a Referential Integrity Check will be performed automatically. The results of the Transfer Import can be viewed in detail and even exported. Transfers are typically used to keep development (source) and production (target) environments in sync. Note: this Transfer process has taken the place of the EDB Transfer tool from previous versions of TrakSYS.

### Backup Database

Provides a simple prompt for backing up the current TrakSYS database. Note: Backup Database functionality cannot be performed if the TrakSYS database is on a remote SQL Server.

### Restore Database

Provides a simple prompt for restoring a TrakSYS database. Note: Backup Database functionality cannot be performed if the TrakSYS database is on a remote SQL Server.

### Create Audit Triggers

Provides a prompt to create SQL Server triggers to the provided SQL Server database in order for auditing to function correctly. The Command Timeout property determines how long (in seconds) to wait upon command execution before timing out. The default Command Timeout is -1 which uses the default value configured in SQL Server (typically 30 seconds). A Command Timeout value of 0 will apply no timeout. The results of this process can be viewed and exported.

### Referential Integrity Check

Although a Referential Integrity Check is done as part of the Transfer Export/Transfer Import processes, this Action can be used at any time as a verification step, typically after SQL Server maintenance. The prompt determines where the Referential Integrity Check Results CSV file will be saved. Upon completion, if the file is empty, there are no Referential Integrity issues.

### Cloud Settings

Provides a prompt to select a Cloud Database Mode if using a SQL Database that is either hosted in Azure or AWS RDS. This setting ensures that the TrakSYS license will be activated correctly if using a cloud-hosted database. The "Normal" option assumes the database is hosted either on the local server or network.
