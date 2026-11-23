# CalculateB4Sigma

```csharp
double CalculateB4Sigma(int samplesPerSubGroup)
```

This method takes the integer count of Samples per SubGroup and returns the B4 constant that is utilized for calculating the Upper Control Limits associated with a Sigma chart. It uses hard-coded values for 2 to 10 groups, and approximated A2’s for groups of 11 and more.
