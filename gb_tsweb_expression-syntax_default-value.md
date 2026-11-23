# Default Value

If an expression specifies a Values Dictionary item that does not exist, the page/script will error. In cases where the presence of a particular Values Dictionary item is in question, it is recommended to provide a default value to the expression. When a default value is provided, that value is returned by the expression when the Values Dictionary key specified cannot be located. The default value is specified in an expression using a **square bracket suffix**.

## Values Dictionary

\<empty>

## Expressions

`Data for {SystemName}`

`Data for {SystemName[No Line]}`

## Results

\<an error will be thrown on the page>

Data for No Line
