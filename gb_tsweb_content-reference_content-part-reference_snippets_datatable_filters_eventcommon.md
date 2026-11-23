# Filters\_EventCommon

#### Filters | Sub-System

Specifies one or more **SubSystemID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

#### Filters | Event Definition

Specifies one or more **EventDefinitionID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

#### Filters | Event Category

Specifies one or more **EventCategoryID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

This filter is executed against the column **EventCategoryID**, which is the deepest selected **Event Category** for each **Event**.

#### Filters | Event Category01 - 10

Specifies one or more **EventCategoryID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

This filter is executed against the column **EventCategoryXXID**, where XX is 01 through 10.

#### Filters | Event Code

Specifies one or more **EventCodeID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

#### Filters | OEE Type None

When true, **Events** with OeeType = None (0) are included in the resultant dataset.

#### Filters | OEE Type Performance Loss

When true, **Events** with OeeType = Performance Loss (1) are included in the resultant dataset.

#### Filters | OEE Type Availability Loss

When true, **Events** with OeeType = Availability Loss (2) are included in the resultant dataset.

#### Filters | OEE Type System Not Scheduled

When true, **Events** with OeeType = System Not Scheduled (3) are included in the resultant dataset.

#### Filters | Event Isolation Type

Specifies the **EventIsolationType** to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).
