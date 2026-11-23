# \<format>

The optional part is a standard .NET format string that is applied to the value of the content after it is calculated. Note that the underlying value must be of the appropriate data type for the formatting to work.

## Examples

```html
{data[0]|Efficiency:N1}
```

Returns the value of the column called Efficiency from the first row in the source data table formatted to 1 decimal point.
