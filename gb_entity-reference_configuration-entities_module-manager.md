# Module Service Instance

## Summary

### Entity Name

Module Service

### Database Table Name

`tModuleManager`

### API Object Name

`DbModuleManager`

### Entity Description

A Module Service instance represents a single instance of the Module Service component. It hosts and executes TrakSYS modules and can optionally generate and store certificates used for secure communication. It also supports High Availability configuration via a secondary (failover) host.

## Properties

`Computer Name [ Host ]`

Name of the computer where the Module Service will run.

`Enabled [ Enabled ]`

When checked, this Module Service instance is active and will be used by the system.

`Generate Certificate [ GenerateCertificate ]`

When enabled, the service will generate a certificate on service start (used for secure communication where applicable).

`Certificate Lifetime (Months) [ CertificateExpirationMonths ]`

Specifies the time (in months) the generated certificate will be valid.

`Certificate Data [ CertificateData ]`

Contains the raw certificate data generated/stored for the primary host.

`Certificate Expiration Date [ CertificateExpirationDateTime ]`

Date/time when the primary certificate will expire.

`Certificate Last Modified [ CertificateDateTime ]`

Date/time when the primary certificate was last generated.

`HA Computer Name [ HaHost ]`

Name of the secondary computer where the Module Service will run when a failover from the primary server occurs.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Certificate Data [ HaCertificateData ]`

Contains the raw certificate data for the failover host.

{% hint style="info" %}
This option will only be used if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Certificate Expiration Date [ HaCertificateExpirationDateTime ]`

Date/time when the failover certificate will expire.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Certificate Last Modified [ HaCertificateDateTime ]`

Date/time when the failover certificate was last generated.

`HA Enabled [ HaEnabled ]`

Enables High Availability behavior for this service instance. When enabled, the service can fail over to the configured secondary host if the primary goes down or a manual failover is initiated.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

`HA Timeout (Seconds) [ HaTimeoutSeconds ]`

How long the service will wait before failing over if the primary host is unavailable.

{% hint style="info" %}
This option will only appear if the TrakSYS license has the High Availability Services feature line.
{% endhint %}

{% hint style="warning" %}
Avoid very small values (for example 10–30 seconds). Low timeouts can cause unnecessary failovers and interruptions.
{% endhint %}
