# Databases

The TrakSYS database is the center of the software installation. It holds all configuration and data for the entire implementation, with the exception of historian data (discussed below). The TrakSYS database platform is Microsoft SQL Server. During installation, a new TrakSYS database is created containing the standard schema (table structures, views and stored procedures, etc…). During project implementation, the configuration will be completed and populated. During execution, the various TrakSYS components and user interfaces are used to monitor and collect data.

While the TrakSYS database can be named anything at the time of creation, it will be referred to as EDB throughout this documentation.

If the TrakSYS historian features are used, a separate TrakSYS database is provided to store the time series Tag history data. This database is automatically named the same as the main TrakSYS database with the suffix of \_Historian added. For the purposes of this documentation, it will be referred to as EDB\_Historian (although the name can be different depending on the specific name given when the database is created).

More detailed information on the TrakSYS databases can be found in the dedicated Reference Documentation section called [Database Reference](../../installation-manager/database).
