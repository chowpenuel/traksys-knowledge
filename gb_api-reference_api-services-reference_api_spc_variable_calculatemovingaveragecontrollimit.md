# CalculateMovingAverageControlLimit

```csharp
double CalculateMovingAverageControlLimit(double standardDeviation, int groupSize)
```

This method takes the StandardDeviation and group size for a Moving Average or Weighted Moving Average chart to calculate the value to be added or subtracted from the mean to reach the Upper or Lower Control Limits for the two chart types. This uses the calculation of 3 times Standard Deviation, divided by the Square Root of the Group Size.
