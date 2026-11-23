# \<conditions>

The optional `<conditions>` part specifies logic that is evaluated in the order listed. The first condition that matches the `<identifier>`'s value will return its result as the value of the Expression. If there are no conditions specified, then the `<identifier>`'s value is returned as is. Conditions are separated with a semi-colon (;). There following describes the different types of conditions:

```html
value:result
```

If the Expression value matches the value part, the specified result is returned.

```html
[from_to]:result
```

If the Expression value falls between the from or to specified, the specified result is returned.

```html
[> < >= <= <> value]:result
```

If the comparison with the value specified is true, the specified result is returned.

```html
[null]:result
```

If the Expression returns null, the specified result is returned.

## Examples

```html
{args|AreaID|[null]:-1;}
```

Returns the value of the `args` key called AreaID. If the item does not exist (returns a null value), then the value of -1 will be returned instead.

```html
{tag|BL1.FILLER.TEMP|[25_50]:orange;[51_100]:red;|yellow}
```

Returns the string value orange if the BL1.FILLER.TEMP Tag value is between 0 and 50, red if the value is between 51 and 100, and yellow if it is any other value.

```html
{tag|BL1.FILLER.TEMP|[>50]:high;|normal}
```

Returns the string value high if the BL1.FILLER.TEMP Tag value is greater than 50 and normal if it is 50 or less.
