# CalculateA2XBarR

```csharp
double CalculateA2XBarR(int samplesPerSubGroup)
```

This method takes the integer count of SampleSubGroups and returns the A2 constant that is utilized for calculating the Upper and Lower Control Limits associated with an XBar(R) chart. It uses hard-coded values for 2 to 10 groups, and approximated A2’s for groups of 11 and more.
