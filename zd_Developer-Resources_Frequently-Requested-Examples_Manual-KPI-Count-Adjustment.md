# Manual KPI Count Adjustment

*Source: https://portal.parsec-corp.com/hc/en-us/articles/9714070791059-Manual-KPI-Count-Adjustment*
*Last updated: 2024-06-26T16:26:08Z*

---

### Introduction

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### Capability

Manual adjustments to the **OeeInterval** record are not intended, as **OeeInterval** records may be recalculated anytime a record related to the Interval is updated. Changes made directly to the Interval may be lost when the recalculation occurs.

This page shows an example of manually adjusting the Counts for a KPI Interval record by using the **OeeAdjustment** and **OeeAdjustmentInterval** records. The Adjustment records are intended to house manual adjustments that are aggregated for reporting by the **viewOeeInterval** view. 

The page requires a **JobID** and **SystemID** to function. An **OeeCalculationID** can optionally be provided. If not provided, the first OeeCalculation that is found the defined System will be used. It allows for new Good and/or Bad counts to be provided and will automatically adjust the Total count accordingly. Counts can be distributed across one or more intervals and are distributed using the "ByActualCounts" logic from the TrakSYS API. 

This is intended to mirror some of the functionality found on the **KpiIntervalListForJob** Content Page and can be linked to from the **JobDiscreteListForSystemCompleted** using the same QueryString parameters.

### Page Deployment

This example includes only one Page Definition, which can be deployed anywhere as needed without any additional supporting scripts.

#### Revisions

20th September 2022 - Initial Publication (v11.2.3)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
