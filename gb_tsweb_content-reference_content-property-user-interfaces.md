# Content Property User Interfaces

When configuring Content Pages and Parts, each property can be set via the Part/Page editor user interface. The special types and patterns of property input controls are described below.

## Setting / Value Pair

Most properties expose a user interface consisting of a pair of inputs. The first input (text-box or drop-down) is used to specify a fixed value for the property. The second input (decorated with a Key icon on the left edge of the input) is used to specify a Values Dictionary Key name. If a Values Key is specified, the Page or Part will attempt to set the property first by accessing the specified Key/Value in the Values Dictionary first. If the Key is not found, or the Values Key input is left blank, the property will be set using the fixed value from the first input.

## Expression

For some properties, it is desirable to set the value using a combination of a constant string with one or more Values Dictionary items inserted using the TrakSYS expression syntax. In these cases, it is not necessary to render a second Values Key input. Expression properties are configured with a text-box input that spans the entire 2 columns of the property interface and decorated with a script (\</>) icon on the left edge of the input.

## Text with Resource Picker

For some string type properties, it is possible to specify a Language Translation Resource reference instead of constant text. These properties allow for a picker to be launched where a Resource Translation reference string can be looked up from the TrakSYS database. These properties contain a picker icon on the right edge of the first text-box input.

## Icon Picker

Icon properties are set using a picker interface to search for and select an icon from a catalog. These properties contain a picker icon on the right edge of the first text-box input.

## Color Picker (Open)

Some color properties allow the selection of any color using a picker interface. These properties contain a picker icon on the right edge of the first text-box input.

## Color Picker (Standard)

Some color properties allow the selection of standard color from a pre-defined list using a picker interface. The standard palette contains foreground and background color combinations for elements with background and foreground content. These properties contain a picker icon on the right edge of the first text-box input.

## Pixel Width

Dimension properties designed to accept an integer pixel width are decorated with a (px) icon on the left edge of the input.

## Bootstrap Width

Dimension properties designed to accept an integer bootstrap width are decorated with a (1-12) icon on the left edge of the input.
