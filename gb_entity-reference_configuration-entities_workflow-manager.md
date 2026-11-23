# Workflow Service Instance

## Summary

### Entity Name

Workflow Manager

### Database Table Name

`tWorkflowManager`

### API Object Name

`DbWorkflowManager`

### Entity Description

A Workflow Service instance represents a single instance of the Workflow Service component, which creates, executes, and ends Workflow processes.

## Properties

`Computer Name [Host]`

Name of the computer where the Workflow Service will run.

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

`Script DLLs [ScriptDlls]`

A comma delimited list of DLL file names that will be loaded as references to any .NET Script within the Workflow Service. The list should contain file names only, and the DLLs must be present in the same directory as the WorkflowManagerService.exe.

`Stalled (Minutes) [StalledMinutes]`

If the Workflow Service is running and this number of minutes is exceeded while executing Processes, the service will considered stalled and any notifications configured for On Stalled will be sent.

`HA Timeout (Seconds) [HaTimeoutSeconds]`

This field determines how long the service will wait to failover if the primary machine goes down. The default value for this setting is 600 seconds (or 10 Minutes).

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

{% hint style="warning" %}
The value for this field should **not** be a very small value (e.g. 10\~30 seconds). Attempting to use a small value may cause the services to unnecessarily failover, which may cause interruptions in production data.
{% endhint %}
