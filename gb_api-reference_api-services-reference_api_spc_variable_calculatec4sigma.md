# CalculateC4Sigma

```csharp
double CalculateC4Sigma(int samplesPerSubGroup)
```

This method takes the integer count of Samples per SubGroup and returns the C4 constant that is utilized for calculating the CP, PP, CPK and PPK metric values. It uses hard-coded values for 2 to 10 groups, and approximated A2’s for groups of 11 and more.
