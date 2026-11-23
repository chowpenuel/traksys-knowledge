# CalculateEwMovingAverageControlLimit

```csharp
double CalculateEwMovingAverageControlLimit(int pointIndex, double standardDeviation, double lambda)
```

This method is used to calculate an Exponential Weighted Moving Average. It takes the point index, standard deviation, and lambda values of a point from an EWMA chart and calculates the value to be added or subtracted from the mean to reach the Upper or Lower Control Limits for the chart. This utilizes the standard formula, which can be described as follows:

3 times sigma, multiplied by the square root of a function that approaches lambda divided by 2 minus lambda as the point index increases. The function described above will typically level off around the 10th point index.
