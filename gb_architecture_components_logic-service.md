# Logic Service

The TrakSYS Logic Service is a Windows service that runs in the background (on the TrakSYS server) collecting inputs from automation (OPC), database and file data sources, processing business rules, recording transactional/KPI data and sending notifications to users and application devices.

The Logic Service loads its configuration from the TrakSYS database (upon service start/restart) and runs constantly in the background. Collected data and messaging is saved back to the TrakSYS database in real-time after each Logic Service scan (typically 1 second).
