# Data Management Service Instance

## Summary

### Entity Name

Data Management Service

### Database Table Name

`tModuleManager`

### API Object Name

`DbModuleManager`

### Entity Description

A Data Management Service Instance represents a single instance of the Data Management Service component, which manages individual Modules.

## Properties

`Computer Name [ Host ]`

Name of the computer where the Data Management Service will run.

`Generate Certificate [ GenerateCertificate ]`

When enabled, the service will generate a certificate required for secure OPC UA communication on service start.

`Certificate Lifetime (Months) [ CertificateExpirationMonths ]`

Specifies the time (in months) of how long the generated certificate will be valid.

`CertificateData`

Contains the raw certificate data that is used for secure OPC UA communication.

`Certificate Expiration Date [ CertificateExpirationDateTime ]`

Contains the Date/Time stamp of when the generated certificate will expire.

`Certificate Last Modified [ CertificateDateTime ]`

Contains the Date/Time stamp of when the certificate was last generated.

`HA Computer Name [HaHost]`

Name of the secondary computer where the Data Management Service will run when a failover from the primary server occurs.

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

{% hint style="info" %}
This option will only be used if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Enabled [HaEnabled]`

This setting determines whether the service will use the High Availability Services feature. When enabled, the service will attempt to failover to an instance of the same service on the secondary server if the primary machine goes down or if a manual failover occurs. Services with this option unchecked will not failover to an instance on the secondary server.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Timeout (Seconds) [HaTimeoutSeconds]`

This field determines how long the service will wait to failover if the primary machine goes down. The default value for this setting is 600 seconds (or 10 Minutes).

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

{% hint style="warning" %}
The value for this field should **not** be a very small value (e.g. 10\~30 seconds). Attempting to use a small value may cause the services to unnecessarily failover, which may cause interruptions in production data.
{% endhint %}
