# CalculateB3Sigma

```csharp
double CalculateB3Sigma(int samplesPerSubGroup)
```

This method takes the integer count of Samples per SubGroup and returns the B3 constant that is utilized for calculating the Lower Control Limits associated with a Sigma chart. It uses hard-coded values for 5 to 10 groups, and approximated A2’s for groups of 11 and more.
