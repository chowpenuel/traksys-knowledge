# Product

## Summary

### Entity Name

Product

### Database Table Name

`tProduct`

### API Object Name

`DbProduct`

### Entity Description

Products represent what the equipment being monitored produces, and specify additional attributes such as theoretical rates and multipliers for KPI. Each Product has The unique identifying Product Code, which is often a SKU number.

Product Schemes define the Product Attributes associated with your Products, such as size, finish, and KPI theoretical rate. Products within the same Product Set must have the same Product Scheme.

Product Sets are complete lists of Products applicable to one or more Systems. If you have many Products in your Product Sets, you may wish to further divide your Sets into Product Groups for better organization.

Once you define your Product Sets and assign them to the appropriate Systems, you "map" your Product Sets to Product Tags using Product Maps. Product Maps relate a single Product Tag to the Product Codes of your Product Sets.

## Properties

`Product Set [ ProductSetID ]`

Specifies the parent Product Set.

`Product Group [ ProductGroupID ]`

Specifies the parent Product Group, if any.

`Product Code [ ProductCode ]`

The unique (within the Product Set) string identifying the Product.

`Material Produced [ ProducedMaterialID ]`

Specifies Material from the TrakSYS configuration that is produced when this Product profile is used during manufacturing.

`Standard Size [ StandardSize ]`

Specifies a baseline quantity of Product produced. This value is used for ratio calculations when extrapolating required Material quantities for different production run sizes. For example, if the Standard Size is 100 KGs and 20KGs of Material A is required, then production runs of 200KGs will require 40KGs of Material A.

`Standard Units Measure [ StandardUnitsMeasureID ]`

Specifies the Unit of Measure for a configured Measure (from the Measures and Conversions feature) that will be used for this entity. This is used for display purposes only and is not required.

`Standard Units [ StandardUnits ]`

Specifies the units of measurement for the Standard Size (used in reporting and display).

`Standard Units Measure [ StandardUnitsMeasureID ]`

Specifies the parent Units Measure, if any, for the Standard Units value. This can be used to standardize unit handling and conversions.

`Theoretical Rate (Units/Minute) [ TheoreticalRateCalculationUnitsPerMinute ]`

Specifies the theoretical production rate for this Product in units per minute, used for KPI calculations.

`Target Rate (Units/Minute) [ TargetRateCalculationUnitsPerMinute ]`

Specifies the target production rate for this Product in units per minute, used for KPI calculations.

`Product Set Gap Pre (Minutes) [ PsGapPreMinutes ]`

Specifies the number of minutes to treat as a gap before the Product Set is active (used by Production Scheduling logic and related calculations).

`Product Set Gap Post (Minutes) [ PsGapPostMinutes ]`

Specifies the number of minutes to treat as a gap after the Product Set is active (used by Production Scheduling logic and related calculations).

`Product Set Padding Pre (Minutes) [ PsPaddingPreMinutes ]`

Specifies the number of minutes to pad before the Product Set is active (used by Production Scheduling and related calculations).

`Product Set Padding Post (Minutes) [ PsPaddingPostMinutes ]`

Specifies the number of minutes to pad after the Product Set is active (used by Production Scheduling and related calculations).

`Product Changeover Family [ ProductCoFamilyID ]`

Specifies the parent Product Changeover Family, if any (used by Production Scheduling and related calculations).

`Product Attributes [ Attribute01 - Attribute20 ]`

Product Attributes hold configuration specific values for the Product item. The definition of what type of data is stored in each field is controlled by the Product Scheme related to this Product's parent Product Set.

`Version Fields`

See [Entity Version Properties](../entity-version-properties).
