# CalculateEwWeightedMovingAverage

```csharp
double CalculateExWeightedMovingAverage(double lambda, double value, [double previousValue])
```

This method takes the previous value and the current value and weighs them using a percentage, lambda. A lambda value of 1 will return the current value. Using this method assumes that the previous points were calculated using the same method.
