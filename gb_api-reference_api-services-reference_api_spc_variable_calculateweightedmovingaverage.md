# CalculatedWeightedMovingAverage

```csharp
double CalculateWeightedMovingAverage(List<double> values)
```

This method takes a list of values, provides a linearly scaling weight for each point, with the oldest data point receiving the lowest weight, and the most recent receiving the highest weight. Averages those value according to the weights.
