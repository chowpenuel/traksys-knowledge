# \<escape>

The optional part determines the type of character escaping that is applied to the return value of the Expression. Possible values are .js (JavaScript), .url (URL), .html (HTML), .htmlbr (HTML while preserving breaks) or .sql (SQL).

## Examples

```html
{args.sql|Notes}
```

Returns the value of the `args` key called Notes. The return value will be escaped based on SQL Server syntax. For example if the Notes value contains a single quote such as "It was Joe's Fault", the return value would be "It was Joe''s Fault".
