# General\_States

#### States

The States grid allows for logic to be applied to Fields and Values within each row to dynamically render a color swatch and icon to the left side of the row.

#### States | Field

For each row, when the this Field from the part's data source matches the Value (specified below), the Icon and/or Color (specified below) will be applied to the row.

#### States | Value

For each row, when the Field (specified above) matches this Value, the Icon and/or Color (specified below) will be applied to the row.

#### States | Icon

Specifies the icon that will be applied to the row when the conditions (specified above) evaluate to true.

#### States | Color

Specifies the color swatch that will be applied to the row when the conditions (specified above) evaluate to true.

#### Icon

An expression or constant that specifies the glyphicon CSS class for a built-in icon that will be applied to each row. Note that when this property is used in conjunction with the conditional States (described above), the States are evaluated first, if none of the States are true, then the value for this property is used.

Through the user interface, the icon can be selected by using a search tool and visual selector. When setting this property through code, it is recommended that the visual interface is used to locate the desired icon and the text value be retrieved and copy/pasted into code.

#### Color

An expression or constant that specifies the color of the swatch that will be applied to each row. Note that when this property is used in conjunction with the conditional States (described above), the States are evaluated first, if none of the States are true, then the value for this property is used.

#### Anchor Name

Specifies the name of this section of Page (anchor tag name) so that this section can be directly navigated to using **#AnchorName** at the end of this Page's URL.
