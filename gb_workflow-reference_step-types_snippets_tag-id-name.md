# tag-id-name

**ID**

If specified, this (integer) Tag `ID` is used to locate a Tag.

**Name Pre and Name Post**

The two `Name` properties are used together to create a `Tag Name` string that is used to locate a Tag.

The `Tag Name` use for lookup is a concatenation of the `Name Pre` and `Name Post` properties. There are two typical scenarios...

* A fixed Tag Name is required. In this case, use only the `Name Pre` property, provide the full Tag Name and leave the `Name Post` empty.
* A dynamically constructed Tag Name is required. In this case, the `Name Pre` property would be configured to retrieve a "Tag Name Prefix" from a **Process Values** `Key` (for example, the value "L1."). The `Name Post` would be configured with a fixed, post portion of the Tag Name (for example "LABEL\_JAM"). With these settings, the final Tag Name that would be used to locate a Tag would be "L1.LABEL\_JAM".
