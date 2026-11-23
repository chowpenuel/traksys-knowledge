# resx

This is used to return values from compiled .NET Resource Files for the given key. This expression can only be used on specially compiled .NET Resource Files that can be added to an installation during customization.

## Examples

```html
{resx|DivMessage.DataOverflow}
```

Returns the translation value for the DataOverFlow resource in the DivMessage Resource File.
