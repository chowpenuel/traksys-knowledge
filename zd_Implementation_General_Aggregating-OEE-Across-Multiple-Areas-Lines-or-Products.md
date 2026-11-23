# Aggregating OEE Across Multiple Areas, Lines, or Products

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47519482908691-Aggregating-OEE-Across-Multiple-Areas-Lines-or-Products*
*Last updated: 2025-12-19T00:18:29Z*

---

### OEE as a Concept

Overall Equipment Effectiveness (OEE) is a standardized manufacturing metric composed of three defined sub-metrics: Availability, Performance, and Quality. Each sub-metric has a specific purpose and relies on a consistent underlying assumption about how time and production output relate to one another. When OEE is calculated for a single system operating at a fixed Theoretical Rate, these assumptions remain valid and the metric is well defined.

Availability measures how much of the scheduled production time was available for operation. In practice, this compares the time a system spent producing against the time it was expected to be capable of producing. In TrakSYS, this relationship is modeled by comparing Production Seconds to Net Operation Seconds, with additional loss categories accounting for unscheduled time and availability-related losses. Availability is, therefore, a purely time-based metric.

Performance measures how efficiently a system operated relative to its Theoretical Production Rate. It captures losses due to running below the expected speed. In TrakSYS, this is represented by comparing theoretical production quantities derived from the system’s defined rate against the quantities that would be expected if the system ran at that rate for the full duration of its productive time. Performance inherently mixes time and unit measurements, relying on the Theoretical Rate as the conversion between the two.

Quality measures how much of the produced output met quality standards. It compares Good production units to Total production units and is entirely unit-based. Time does not factor directly into the Quality calculation, only the ratio of acceptable output to total output.

These three components multiply cleanly into OEE only when a single, constant Theoretical Rate applies to the entire calculation window. Under that condition, the relationship between time and units remains consistent, and the mixed use of seconds and units does not introduce ambiguity. OEE can then be calculated accurately across any timeframe, regardless of its length.

#### Complexities with Multi-Rate Calculations

When the Theoretical Rate changes within the scope of a calculation, OEE can no longer be maintained under its original definition. This situation commonly occurs when aggregating OEE across multiple production lines, assets, or Products, each with different theoretical speeds. Availability remains time-based, Quality remains unit-based, and Performance depends on converting between the two. Once the conversion factor varies, the assumptions that allow these metrics to combine cleanly are no longer valid.

For this reason, OEE does not have a single standard definition when aggregated across assets with different Theoretical Rates. TrakSYS does not enforce a built-in solution for this scenario, as OEE was not designed to accommodate variable rates. Nevertheless, it is still possible to derive meaningful effectiveness metrics from the same underlying data, provided the calculation approach is explicitly defined. In these cases, there is no single correct answer, only different perspectives.

To calculate OEE across variable rates, the calculation must be balanced around either Production Time or Production Units. Both approaches are valid, but they answer different business questions. The key requirement is that all values must be converted to a common basis before aggregation.

In a time-weighted approach, all production units are converted into their equivalent time using each system’s Theoretical Rate. This produces a metric often referred to as Time-Weighted OEE or Time-Based OEE. The result emphasizes how effectively total available production time was used, regardless of how fast or slow individual assets are. This approach is commonly used for asset utilization analysis, maintenance effectiveness, and operational availability reporting.

In a unit-weighted approach, all time-based losses are converted into equivalent lost production units using the applicable Theoretical Rates. This produces what is commonly called Unit-Weighted OEE or Throughput-Weighted OEE. The result emphasizes how effectively the organization converted production opportunity into output. Faster assets naturally carry more influence, making this approach better aligned with throughput, delivery performance, and revenue-focused analysis.

As an example, consider two production lines operating for one hour. One line produces one unit per hour, while the other produces ninety-nine units per hour. If the slow line is down for the full hour and the fast line runs perfectly, ninety-nine units are produced out of a possible one hundred. From a unit-weighted perspective, effectiveness is ninety-nine percent. From a time-weighted perspective, half of the total available production time was lost, resulting in fifty percent effectiveness. Both results are accurate, but each reflects a different interpretation of performance.

#### General Conclusion

When aggregating OEE across multiple assets or lines with different Theoretical Rates, the chosen method **must** be stated explicitly. Time-Weighted OEE and Unit-Weighted OEE are both reasonable, defensible metrics, but they represent fundamentally different views of operational effectiveness. The correct choice depends on whether the analysis is intended to prioritize time utilization or production output.

### Implementation Note and Resource

An accompanying SQL script is provided to create an additional view layered on top of the standard `viewOeeInterval`. This view exposes each OEE interval in both time-based (seconds) and unit-based representations, using the interval’s Theoretical Rate as the conversion factor. Its purpose is to simplify downstream aggregation and reporting scenarios where either Time-Weighted OEE or Unit-Weighted OEE is required.

This view does not introduce new source data or alter the underlying OEE calculations. It relies entirely on the logic, adjustments, and suppression rules already defined within `viewOeeInterval`, and is intended to remain consistent with standard TrakSYS behavior at the individual interval level. The view functions solely as an analytical and semantic extension to support alternative aggregation approaches.

This implementation is provided as a reference pattern and is not an officially supported TrakSYS feature. Because OEE was not designed to aggregate across variable Theoretical Rates, the implementor should apply this view with care and ensure that the selected aggregation method aligns with the intended analytical objective. Any reporting or analytics built on top of this view should clearly communicate whether results are time-weighted or unit-weighted to avoid misinterpretation.

The implementor is responsible for validating performance, data volume, and usage considerations within their specific environment prior to deploying this view into production.
