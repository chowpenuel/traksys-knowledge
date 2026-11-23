# SqlServerInfo

This object is used when retrieving information about the SQL Server instance used for the TrakSYS installation.

## Properties

`string DisplayVersion`

Specifies the full display version of the SQL Server instance. This includes the year (2017, 2019, 2022, etc.), the Release to Manufacturer (RTM) number (e.g. 16.0.1000.6), and the architecture used (32 or 64 bit).

`string Edition`

Specifies the Edition of SQL Server (e.g., Standard, Developer, Enterprise, etc.) and the architecture used (32 or 64 bit).

`int EngineEdition`

Specifies the Engine Edition number for the SQL Server installation.

`bool IsAlwaysOn`

Provides a Boolean value that specifies whether the Always On High Availability feature is being used in SQL Server with the TrakSYS database. A value of True (or 1) means High Availability in SQL Server is being used, while a value of False (or 0) means it is not enabled.

`bool IsClustered`

Provides a Boolean value that specifies whether the Clustering feature is being used in SQL Server with the TrakSYS database. A value of True (or 1) means that Clustering is being used, while a value of False (or 0) means it is not.

`bool IsEnterprise`

Provides a Boolean value that specifies whether the Enterprise edition of SQL Server is being used. A value of True (or 1) means that the Enterprise Edition is being used, while a value of False (or 0) means it is not.

`string Level`

Specifies the current type of SQL Server installation (e.g. Release to Manufacturing (RTM), Release Candidate (RC), Community Technology Preview (CTP), etc.).

`string VersionFull`

Specifies the full version of SQL Server and Windows Server that is used in the TrakSYS Installation. This includes the SQL Server year (2017, 2019, 2022, etc.), the Edition of SQL Server (e.g., Standard, Developer, Enterprise, etc.), the SQL Server architecture (32 or 64 bit), Windows Server year (e.g., 2016, 2019, 2022, etc.), Windows Server edition (e.g., Standard, Data Center, etc.), the Windows Server architecture (32 or 64 bit), and current Windows Server build number.

`string VersionNumber`

Specifies the raw version number for the SQL Server version (e.g., Release to Manufacturer (RTM) number (16.0.1000.6)).
