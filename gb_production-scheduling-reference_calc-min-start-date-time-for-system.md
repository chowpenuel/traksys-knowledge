# Calculate Minimum Start Date Time For System

This method is used to set the DateTime for the earliest a System is able to schedule Jobs. This method is done in the Initialization Steps before the main scheduling and scoring loop. This method is run X times where X is the number of systems that are configured to the Production Set.

## Context

`DateTimeOffset MinStart`

Gets or sets a DateTimeOffset value to mark the starting time when a system is first available time the System can run a Job.

`DateTimeOffset Now`

Gets the DateTimeOffset for the current time.

{% hint style="info" %}
This property is only available in the Discrete Job Production Scheduling Script.
{% endhint %}

`DbOeeCalculation OeeCalculation`

Gets the `DbOeeCalculation` model for the associated System.

{% hint style="info" %}
This property is only available in the Discrete Job Production Scheduling Script.
{% endhint %}

`DbSystem System`

Gets the `DbSystem` model that is being evaluated during this method call.
