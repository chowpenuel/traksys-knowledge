# CalculateCpk

```csharp
double CalculateCpk(double standardDeviationS, double mean, int samplesPerSubGroup, double usl, double lsl)
```

This method takes a list of values, the number of samples per sub group, and the Upper and Lower Specification Limits. Calculates the Mean and Sigma values and uses the CalculateC4Sigma method to determine constants needed to complete the standard CPK formula of “return whichever is smaller, Upper Specification minus the Mean, divide by three times the Sigma, or the Mean minus the Lower Specification, divided by three times the Sigma”, using the approximation of SigmaPopulation
