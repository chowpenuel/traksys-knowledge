# DataDash

This grid specifies one or more key/value pairs that will be rendered to each element in the part. The key/value pairs are generated based on each row in the part's data source. Each row in the grid will generate an HTML attribute on the row element in the following format (the example below uses a for the element, but this may differ depending on the part)...

`<tr data-Key1="Value1" data-Key2="Value2">`

#### Key

Specifies the key that will be used to form the attribute name (data-Key).

#### Value

An expression or constant that will be used as the value of the attribute.
