# CalculateCp

```csharp
double CalculateCp(List<double> values, int samplesPerSubGroup, double usl, double lsl)
```

This method takes a list of values, the number of samples per sub group, and the Upper and Lower Specification Limits. Calculates the Mean and Sigma values and uses the CalculateC4Sigma method to determine constants needed to complete the standard CP formula of “Upper Specification minus Lower Specification, divide by six times the Sigma”, using the approximation of SigmaPopulation.
