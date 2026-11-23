# Logic Service Instance

## Summary

### Entity Name

Logic Service

### Database Table Name

`tLogicManager`

### API Object Name

`DbLogicManager`

### Entity Description

A Logic Service instance represents a single instance of the Logic Service component, which collects I/O, records KPI data, tracks production events, and dispatches event notifications to devices.

## Properties

`Computer Name [ Host ]`

Name of the computer where the Logic Service will run.

`Generate Certificate [ GenerateCertificate ]`

When enabled, the service will generate a certificate required for secure OPC UA and MQTT communication on service start.

`Certificate Lifetime (Months) [ CertificateExpirationMonths ]`

Specifies the time (in months) of how long the generated certificate will be valid.

`CertificateData`

Contains the raw certificate data that is used for secure OPC UA and MQTT communication.

`Certificate Expiration Date [ CertificateExpirationDateTime ]`

Contains the Date/Time stamp of when the generated certificate will expire.

`Certificate Last Modified [ CertificateDateTime ]`

Contains the Date/Time stamp of when the certificate was last generated.

`HA Computer Name [HaHost]`

Name of the secondary computer where the Logic Service will run when a failover from the primary server occurs.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HaCertificateData`

Contains the raw certificate data that is used for secure OPC UA communication for the failover server.

{% hint style="info" %}
This option will only be used if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Certificate Expiration Date [ HaCertificateExpirationDateTime ]`

Contains the Date/Time stamp of when the generated certificate will expire for the failover server.

{% hint style="info" %}
This option will only be used if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Certificate Last Modified [ HaCertificateDateTime ]`

Contains the Date/Time stamp of when the certificate was last generated for the failover server.

`HA Enabled [HaEnabled]`

This setting determines whether the service will use the High Availability Services feature. When enabled, the service will attempt to failover to an instance of the same service on the secondary server if the primary machine goes down or if a manual failover occurs. Services with this option unchecked will not failover to an instance on the secondary server.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`Scan in Milliseconds [ ScanMs ]`

Target scan rate of the Logic Service in milliseconds, which determines how frequently the Logic Service evaluates Tag changes and writes data to the database.

`Simulation Mode [ SimulationModeActive ]`

Treats I/O Tags as Virtual Tags for troubleshooting purposes. The Logic Service will not attempt to establish any connections to I/O servers.

`Trace Enabled [ TraceEnabled ]`

When checked, this Logic Service instance will write detailed trace data to the tTrace table in the TrakSYS database. This setting can be toggled and have an immediate effect without restarting the service.

`Database Connect Attempts [ DatabaseConnectAttempts ]`

The number of times the Logic Service will attempt to connect to the database before abandoning the current scan. This setting may help alleviate transient connectivity problems. Note that this setting works in conjunction with the Database Manager Connect Timeout setting.

`Virtual Tag Changed Delay in Seconds [ VirtualTagChangedDelaySeconds ]`

When greater than 0, this setting instructs the Logic Service to only examine Virtual Tags which have changed within the specified time limit. This optimizes the Logic Service to disregard Virtual Tags which have not changed recently. Setting this value to 0 instructs the Logic Service to examine all loaded Virtual Tags for possible value changes every scan.

`Load All Tags [ LoadAllTags ]`

This setting instructs the Logic Service to load every Tag in the database, regardless of whether or not the current configuration references all of them. The Logic Service will still load the configuration and collect Event and KPI data normally.

`Load Tags Only [ LoadTagsOnly ]`

This setting is similar to Load All Tags, but instructs the Logic Service to ignore the configuration. When this setting is active, the Logic Service will load every Tag in the database but will not load the configuration. Consequently, any State Tags dependent on configuration entities such as Event Definitions, Systems, and KPI Calculations will cease to function. A common use of this setting is to test I/O Tags before the configuration is complete, when the intent is not to collect any Event or KPI data.

`Overscan Buffer Milliseconds [ OverscanBufferMilliseconds ]`

This setting determines how far over the configured Scan time a scan must be before it is logged as an over-scan.

`Stalled Starting in Minutes [ StalledStartingMinutes ]`

If the Logic Service starts but exceeds this number of minutes before entering into a normal scan cycle, the service will be considered stalled and any notifications configured for Stalled Starting will be sent.

`Stalled Running in Minutes [ StalledRunningMinutes ]`

If the Logic Service is scanning and this number of minutes is exceeded between successful scans, the service will considered stalled and any notifications configured for Stalled Running will be sent.

`MaximumParallelExecutes [ MaximumParallelExecutes ]`

This setting controls the maximum number of threads that the Logic Service will use when executing operations in parallel.

`Async Empty in Seconds [ AsyncEmptySeconds ]`

The Logic Service executes some database updates asynchronously and independently of the scans. During heavy load, the scans may put more items into the queue for asynchronous execution that are being executed and cleared out over the same time interval. This setting controls the number of seconds that the asynchronous can be consecutively non-zero, before the Logic Service stops executing items asynchronous and switches to a synchronous execution mode to catch up.

`HA Timeout (Seconds) [HaTimeoutSeconds]`

This field determines how long the service will wait to failover if the primary machine goes down. The default value for this setting is 600 seconds (or 10 Minutes).

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

{% hint style="warning" %}
The value for this field should **not** be a very small value (e.g. 10\~30 seconds). Attempting to use a small value may cause the services to unnecessarily failover, which may cause interruptions in production data.
{% endhint %}

`Script Class Name [ ScriptClassName ]`

Specifies the .NET class name(s) (comma delimited) that will be associated with this Logic Service instance. The class names specified here must be defined in the Scripts | Logic section as Logic Service scripts.

`Script DLLs [ ScriptDLLs ]`

A comma delimited list of DLL file names that will be loaded as references to any .NET Script within the Logic Service. The list should contain file names only, and the DLLs must be present in the same directory as the LogicManagerService.exe.
