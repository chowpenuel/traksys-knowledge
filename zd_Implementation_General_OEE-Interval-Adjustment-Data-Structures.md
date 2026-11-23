# OEE Interval Adjustment Data Structures

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824465725715-OEE-Interval-Adjustment-Data-Structures*
*Last updated: 2025-05-21T22:08:06Z*

---

Applies To | TrakSYS 10+

There are two types of OEE Interval Adjustments in TrakSYS: Single Interval and Interval Range. Single Interval adjustments affect one OEE Interval and are recorded in **tOeeIntervalAdjustment**. This adjustment is designed for scenarios where the exact time of the adjustment is known and can be applied to a specific single Interval. This adjustment can usually be made near real-time when the interval is currently active or has just ended. The out-of-the-box KPI Interval New/Edit (`ETS.Application.Kpi.KpiIntervalNewEdit`) Content Page can be used for this type of adjustment. Additionally, a Visual Page Definition version of this page is also available on the support site [**here**](https://portal.parsec-corp.com/hc/en-us/articles/360026615594-KPI-Interval-NewEdit).

Interval Range adjustments affect multiple OEE Intervals. The total adjustment is recorded in tOeeAdjustment and the specific intervals adjusted are recorded in **tOeeAdjustmentInterval** (as child entries under the same Adjustment ID). There is no out-of-the-box Content Page for this type of adjustment. However, there are multiple methods within the TrakSYS API can be used to create them. These methods are described in the [TrakSYS Reference Documentation ](https://docs.parsec-corp.com/)under **API Reference | API Services Reference | Api.Kpi | Adjustment**. Additionally, this article describes how to use the API to create an Interval-Range adjustment **[here](https://portal.parsec-corp.com/hc/en-us/articles/360005709414-How-To-Create-an-OEE-Adjustment-for-Multiple-Intervals-Using-the-API)**.  

