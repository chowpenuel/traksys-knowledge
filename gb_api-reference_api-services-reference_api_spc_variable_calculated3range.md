# CalculateD3Range

```csharp
double CalculateD3Range(int samplesPerSubGroup)
```

This method takes the integer count of Samples per SubGroup and returns the D3 constant that is utilized for calculating the Lower Control Limits associated with a Range chart. It uses hard-coded values for 5 to 10 groups, and approximated A2’s for groups of 11 and more.
