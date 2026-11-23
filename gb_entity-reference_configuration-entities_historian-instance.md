# Historian Service Instance

## Summary

### Entity Name

Historian Service

### Database Table Name

`tHistorianManager`

### API Object Name

`DbHistorianManager`

### Entity Description

A Historian Service represents a single instance of the Historian Service component, which monitors and records changing Tag values for historical analysis.

## Properties

`Computer Name [ Host ]`

Name of the computer where Service will run.

`Generate Certificate [ GenerateCertificate ]`

Contains a Boolean value that determines if a certificate will be generated for the service. The actual certificate will be generated on the next service start.

`Certificate Lifetime (Months) [ CertificateExpirationMonths ]`

Specifies the duration (in months) in which the certificate will be valid.

`CertificateData`

Contains the raw certificate data that is used for secure OPC UA communication.

`Certificate Expiration Date [ CertificateExpirationDateTime ]`

Contains the DateTime value of when the generated certificate will expire.

`Certificate Last Modified [ CertificateDateTime ]`

Contains the DateTime value of when the certificate was last modified. This will typically contain the DateTime value of when the certificate was created if no modifications were made since its creation.

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

Contains the DateTime value of when the generated certificate will expire for the failover server.

{% hint style="info" %}
This field will only be populated if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Certificate Last Modified [ HaCertificateDateTime ]`

Contains the DateTime value of when the certificate was last modified for the failover server. This will typically contain the DateTime value of when the certificate was created if no modifications were made since its creation.

{% hint style="info" %}
This field will only be populated if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Enabled [HaEnabled]`

This setting determines whether the service will use the High Availability Services feature. When enabled, the service will attempt to failover to an instance of the same service on the secondary server if the primary machine goes down or if a manual failover occurs. Services with this option unchecked will not failover to an instance on the secondary server.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`Store and Forward Path [ StoreAndForwardPath ]`

The full path, on the local server running the Service, where data will temporarily be buffered in files, if the historian database is unavailable for recording. The account that the service is running under must have rights to create and update files in the specified directory.

`Settings [ Settings ]`

Advanced settings that can be passed into the service. The syntax for these settings is specific xml that must be supplied by TrakSYS support.

`HA Timeout (Seconds) [HaTimeoutSeconds]`

This field determines how long the service will wait to failover if the primary machine goes down. The default value for this setting is 600 seconds (or 10 Minutes).

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

{% hint style="warning" %}
The value for this field should **not** be a very small value (e.g. 10\~30 seconds). Attempting to use a small value may cause the services to unnecessarily failover, which may cause interruptions in production data.
{% endhint %}

`Simulation Mode [ SimulationModeActive ]`

Treats I/O Tags as Virtual Tags for troubleshooting purposes. will not attempt to establish any connections to I/O servers.

`Trace Enabled [ Trace Enabled ]`

When checked, this instance will write detailed trace data to the tTrace table in the TrakSYS database. This setting can be toggled and have an immediate effect in the without restarting the service.
