# Expression Use

Expressions can be used in a variety of places within the TrakSYS user interface development environment.

## Content Page/Part Expression Properties

Expressions can be used in any Page or Part Property that displays a "script" icon `</>` to the left of the text box. These properties can be specified with a combination of constant text and one or more expressions.

From the script code behind, these properties will all be exposed from the Page/Part object with property names ending in "Ex". Expression strings can be directly set to these properties, so long as it is done before the part is processed. For example, to set the Text property of a Header Part from code with a string using the `SystemName` element from the Values Dictionary…

`this.HeaderTop.TextEx = "Data for {LineName}";`

## Content Page/Part Expression Grid Properties

There are some Page/Part properties that are embedded in the grid editor user interfaces (table columns, list buttons, etc…). Some of these grid based properties allow expressions (see Page/Part reference for the use of each specific property). Expressions may be set to these elements either through the editor user interface or through script in the code page.

## Page/Part Script

In some cases, it may be desirable to construct and execute expression strings directly in script code. The `Ets.ProcessExpression()` method can be used to process and output the results of an expression directly.

`string headerText = this.Ets.ProcessExpression("Data for {SystemName}");`
