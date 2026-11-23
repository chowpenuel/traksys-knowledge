# OeeData

Represents the building blocks and calculations for OEE and its related KPIs over a specific date range. This object is returned by many of the methods in the `ApiService.Kpi` section of the API.

## Properties

`double Availability`

Gets or sets the Availability value for the OeeData object.

`double Availability2`

Gets or sets the Availability2 value for the OeeData object. This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`bool Availability2IsNaN`

Provides a Boolean value that specifies whether the current Availability2 value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`double Availability2Teep`

Gets or sets the Availability2Teep value for the OeeData object. This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`bool Availability2TeepIsNan`

Provides a Boolean value that specifies whether the current Availability2Teep value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`bool AvailabilityIsNaN`

Provides a Boolean value that specifies whether the current Availability value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

`int AvailabilityLossSeconds`

Gets or sets the AvailabilityLossSeconds value for the OeeData object.

`int AvailabilityLossTeepSeconds`

Gets or sets the AvailabilityLossTeepSeconds value for the OeeData object.

`double AvailabilityTeep`

Gets or sets the AvailabilityTeep value for the OeeData object.

`bool AvailabilityTeepIsNaN`

Provides a Boolean value that specifies whether the current AvailabilityTeep value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

`int BadCalculationUnits`

Gets or sets the BadCalculationUnits value for the OeeData object.

`double BadDisplayUnits`

Gets or sets the BadDisplayUnits value for the OeeData object.

`DateTime EndDateTime`

Gets or sets the EndDateTime for the duration of the data in the OeeData object.

`int GoodCalculationUnits`

Gets or sets the GoodCalculationUnits value for the OeeData object.

`double GoodDisplayUnits`

Gets or sets the GoodDisplayUnits value for the OeeData object.

`int LegalLossSeconds`

Gets or sets the LegalLossSeconds value for the OeeData object.

`int NetOperationSeconds`

Gets or sets the NetOperationSeconds value for the OeeData object.

`double Oee`

Gets or sets the Oee value for the OeeData object.

`double Oee2`

Gets or sets the Oee2 value for the OeeData object. This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`bool Oee2IsNaN`

Provides a Boolean value that specifies whether the current Oee2 value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`bool OeeIsNaN`

Provides a Boolean value that specifies whether the current Oee value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

`double Performance`

Gets or sets the Performance value for the OeeData object.

`bool PerformanceIsNaN`

Provides a Boolean value that specifies whether the current Performance value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

`int PerformanceLossSeconds`

Gets or sets the PerformanceLossSeconds value for the OeeData object.

`DateTime ProductionDate`

Gets or sets the ProductionDate value for the OeeData object.

`int ProductionSeconds`

Gets or sets the ProductionSeconds value for the OeeData object.

`double Quality`

Gets or sets the Quality value for the OeeData object.

`bool QualityIsNaN`

Provides a Boolean value that specifies whether the current Quality value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

`int Seconds01 - 10`

Gets or sets the Seconds value from one of the SecondsXX fields for the OeeData object. These fields are used for extensibility purposes and are not normally used by default within TrakSYS.

`DateTime StartDateTime`

Gets or sets the StartDateTime for the duration of the data in the OeeData object.

`int SystemNotScheduledSeconds`

Gets or sets the SystemNotScheduledSeconds value for the OeeData object.

`double TaktSeconds`

Gets or sets the TaktSeconds value for the OeeData object.

`bool TaktSecondsIsNaN`

Provides a Boolean value that specifies whether the current TaktSeconds value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

`double TargetProductionCalculationUnits`

Gets or sets the TargetProductionCalculationUnits value for the OeeData object.

`double Teep`

Gets or sets the Teep value for the OeeData object.

`double Teep2`

Gets or sets the Teep2 value for the OeeData object. This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`bool Teep2IsNaN`

Provides a Boolean value that specifies whether the current Teep2 value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

This property uses a unit-based calculation for Availability, which can provide different results from the original Availability calculation (which is time-based). In general, the unit-based calculation is considered more accurate than the time-based one.

`bool TeepIsNaN`

Provides a Boolean value that specifies whether the current Teep value is Not a Number (NaN). A value of False (or 0) means it contains a valid number, while a value of True (or 1) means it is not a valid number. Scenarios where a value of True (or 1) is returned may occur in certain mathematical impossibilities such as dividing by zero or taking the square root of a negative number.

`double TheoreticalIntervalCalculationUnits`

Gets or sets the TheoreticalIntervalCalculationUnits value for the OeeData object.

`double TheoreticalIntervalTeepCalculationUnits`

Gets or sets the TheoreticalIntervalTeepCalculationUnits value for the OeeData object.

`double TheoreticalNetOperationCalculationUnits`

Gets or sets the TheoreticalNetOperationCalculationUnits value for the OeeData object.

`double TheoreticalProductionCalculationUnits`

Gets or sets the TheoreticalProductionCalculationUnits value for the OeeData object.

`int TotalCalculationUnits`

Gets or sets the TotalCalculationUnits value for the OeeData object.

`double TotalDisplayUnits`

Gets or sets the TotalDisplayUnits value for the OeeData object.

`int TotalSeconds`

Gets or sets the TotalSeconds value for the OeeData object.

`int TotalTeepSeconds`

Gets or sets the TotalTeepSeconds value for the OeeData object.
