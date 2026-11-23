# CalculatePp

```csharp
double CalculatePp(double standardDeviationS, double usl, double lsl)
```

This method takes a list of values, the number of samples per sub group, and the Upper and Lower Specification Limits. Calculates the Mean and Sigma values to complete the standard PP formula of “Upper Specification minus Lower Specification, divide by six times the Sigma”, using the approximation of SigmaSample.
