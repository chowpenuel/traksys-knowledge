# cp\[entityID]

This is used to access Custom Properties from a specified database entity. The entityID can be specified using the `args.NAME`.

## Examples

```html
{cp[args.SystemID]|System.ET.NODE.BUTTON.ID|[null]:-1}
```

Returns the value for the System Custom Property with a full key of ET.NODE.BUTTON.ID. The System entity for which the custom property is retrieved is specified by an `args` key called SystemID.
