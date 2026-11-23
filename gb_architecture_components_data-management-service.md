# Data Management Service

The Data Management Service is a logic execution engine designed to process longer running non-real time business rules. Typical uses include pre-aggregation of data for improved report performance and automated transfers of data between TrakSYS and business systems. The Data Management Service also supports the creation of script based business rules that can execute longer operations without interfering with the time critical real-time data capture being done by the Logic Service.

## Modules

A Data Management Module is a collection of one or more Module Steps. Each Module represents specific functionality or business rules. There are several types of Module Steps which execute in a configured sequence. Modules can be executed manually via script or automatically based on a configured schedule.

Modules are typically written to interface with business systems, such as ERP systems, or to aggregate and run calculations on data periodically.
