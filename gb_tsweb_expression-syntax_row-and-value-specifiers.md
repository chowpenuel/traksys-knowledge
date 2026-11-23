# Row and Value Specifiers

The source for the TrakSYS expression syntax is the Values Dictionary. However, in certain limited contexts, there can be an alternate source for the values referenced by expressions. When using expressions in a property on a part that renders multiple instances/rows, the individual datarow/object properties for the current record in the data source are also eligible to be referenced by the expression. Examples of Parts that allow this type of expression are…

* Lists
* Tables
* Tile Lists
* Charts
* Button Lists
* Etc…

When defining an expression in one of these Part properties, the source pool for the key lookup is a combination of the Values Dictionary, and the properties of the data source row for the current iteration. Note that if the expression key is present in both the Values Dictionary, and the current row, the value from the current row will take priority and be returned by the expression.

The source for evaluation can be forced by using the `r: (row source)` or `v: (values source)` prefixes before the key in the expression. If one of these prefixes is present, only the specified source is searched for a matching key.

## Values Dictionary

SystemName = Line 1

CategoryName = Operational

## Current Row

ID = 2

CategoryName = Mechanical

## Expressions

`System Name = {SystemName}`

`System Name = {v:SystemName}`

`System Name = {r:SystemName}`

`ID = {ID}`

`ID = {v:ID}`

`ID = {r:ID}`

`Category Name = {CategoryName}`

`Category Name = {v:CategoryName}`

`Category Name = {r:CategoryName}`

## Results (assuming all of these are called within the context of a part row)

System Name = Line 1

System Name = Line 1

System Name = \<an error will be thrown on the page>

ID = 2

ID = \<an error will be thrown on the page>

ID = 2

Category Name = Mechanical

Category Name = Operational

Category Name = Mechanical
