# tag\[prefix]

This is used to dynamically concatenate the starting portion of a Tag name with a fixed suffix.

## Examples

```html
{tag[args.SystemTagPrefix]|Manual.IsDown|0:START;1:END;|}
```

Returns the value of the `args` key called SystemTagPrefix and provides the value as input for the Tag Expression.
