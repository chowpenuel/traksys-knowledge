# Span

This object model uses a .NET TimeSpan. It provides string values that are used for the [Timer Format Expression Syntax](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/tsweb/expression-syntax/Format/timer-format.md). The model takes in a parameter in seconds or as a TimeSpan to determine which text to output for the Timer Format.

## Properties

`string Ago`

Gets or Sets the string used for the time duration if it is positive. If seconds are used, the page will display something similar to `X Second(s) Ago`. If a TimeSpan is used, text will be outputted for greater measures of time (e.g., Hours, Days, etc.). For example, if hours are used, the page will display something similar to `X Hour(s) Ago`.

`string Duration`

Gets or sets the base string used for the duration. If seconds are used, the page will display something similar to `X Second(s)`. If a TimeSpan is used, text will be outputted for greater measures of time (e.g., Hours, Days, etc.). For example, if hours are used, the page will display something similar to `X Hour(s)`.

`double DurationAmount`

Gets or sets the duration number to be used for the Timer Format.

`string DurationUnitOfMeasure`

Gets or sets the unit of measure in time that will be used for the `DurationAmount` (e.g., Second(s), Minute(s), Hour(s), Day(s), etc.).

`bool DurationUnitOfMeasureIsSeconds`

This property returns a Boolean value that determines whether the `DurationUnitOfMeasure` property is in Second(s). A Boolean value of True (or 1) means that Second(s) is being used, while a value of False (or 0) means a different measure is being used.

`string Hms`

When used, this property applies the `Hms` format (e.g. 08:32:11) to the `DurationAmount` value.

`string In`

Gets or Sets the string used for the time duration if it is negative. If seconds are used, the page will display something similar to `In X Second(s)`. If a TimeSpan is used, text will be outputted for greater measures of time (e.g., Hours, Days, etc.). For example, if hours are used, the page will display something similar to `In X Hour(s)`.

`bool IsSpanNegative`

This property returns a Boolean value that determines whether the provided time duration is negative. A Boolean value of True (or 1) means that the duration is negative, while a value of False (or 0) means that it is positive.

`TimeSpan TimeSpan`

This property represents the `TimeSpan` object used to display the Timer Format.
