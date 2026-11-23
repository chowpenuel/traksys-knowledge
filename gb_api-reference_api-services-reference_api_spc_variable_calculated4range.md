# CalculateD4Range

```csharp
double CalculateD4Range(int samplesPerSubGroup)
```

This method takes the integer count of Samples per SubGroup and returns the D4 constant that is utilized for calculating the Upper Control Limits associated with a Range chart. It uses hard-coded values for 2 to 10groups, and approximated A2’s for groups of 11 and more.
