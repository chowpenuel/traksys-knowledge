# GeneralDateTimeRange

#### Date/Time Range | Key Prefix

By default, the part searches for date/time ranges using the standard naming (`SD`, `ED`, `SDT` and `EDT`). If a prefix is provided in this property, the prefix is concatenated to the beginning of the standard Values names. For example, if the prefix specified is `JOB.`, then the date/time Values items will be expected in `JOB.SD`, `JOB.ED`, `JOB.SDT` and `JOB.EDT`.

#### Date/Time Range | Use in Query

When true, this part will attempt to incorporate a start and end date/time range in the generated query (`WHERE` clause). Depending on the part, the range will be extracted from the Values items called `SD` and `ED` (Start Date and End Date), or `SDT` and `EDT` (Start Date/Time and End Date/Time). When false, the underlying query will be constructed with no date/time filter in the `WHERE` clause.
