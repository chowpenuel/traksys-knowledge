# CalculatePpk

```csharp
double CalculatePpk(List<double> values, double usl, double lsl)
```

This method takes a list of values, the number of samples per sub group, and the Upper and Lower Specification Limits. Calculates the Mean and Sigma values to complete the standard PPK formula of “return whichever is smaller, Upper Specification minus the Mean, divide by three times the Sigma, or the Mean minus the Lower Specification, divided by three times the Sigma”, using the approximation of SigmaSample.
