# Update Unavailable Times for System

This method is used for making changes to the unavailable times where a system cannot be run. This method can be used to remove or add unavailable times to the system. This method is run X times where X is the number of systems that are configured to the Production Set.

## Context

`DateTimeOffset MinStartDateTime`

Gets the DateTimeOffset object that represents the System's first available time to start scheduling jobs.

`int SystemID`

Gets the System's ID.

`string SystemKey`

Gets the System's string Key.

`string SystemName`

Gets the System's string name.

`List<PsUnavailableTime> UnavailableTimes`

Gets the List object of Unavailable times. This object holds information about the start and stop times of the system's times that it cannot schedule jobs. This object has functions to remove and add new `PsUnavailableTimes`.
