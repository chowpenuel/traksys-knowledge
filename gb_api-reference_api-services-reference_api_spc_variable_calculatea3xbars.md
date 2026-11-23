# CalculateA3XBarS

```csharp
double CalculateA3XBarS(int samplesPerSubGroup)
```

This method takes the integer count of Samples per SubGroup and returns the A3 constant that is utilized for calculating the Upper and Lower Control Limits associated with an XBar(S) chart. It uses hard-coded values for 2 to 10 groups, and approximated A2’s for groups of 11 and more.
