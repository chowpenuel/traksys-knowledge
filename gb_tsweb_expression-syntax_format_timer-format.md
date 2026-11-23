# Timer Format

In some scenarios it is useful to display durations on the user interface that are actively changing, without constantly refreshing the page using server requests (AJAX). A special expression syntax allows for the formatting of a DateTimeOffset value to be rendered using a smart client side script (JavaScript), producing a running counter.

`timer-up` (`hms` format is implied) - Utilizes the Values item as the start and the current date/time as the end to calculate a span. Displays the duration using the `hms` format.

`timer-up:duration` - Utilizes the Values item as the start and the current date/time as the end to calculate a span. Displays the duration using the `duration` format.

`timer-up:relative` - Utilizes the Values item as the start and the current date/time as the end to calculate a span. Displays the duration using the `ago` format if the duration is positive, and the `in` format if the duration is negative.

`timer-down` (`hms` format is implied) - Utilizes the current date/time as the start and the Values item as the end to calculate a span. Displays the duration using the `hms` format.

`timer-down:duration` - Utilizes the current date/time as the start and the Values item as the end to calculate a span. Displays the duration using the `duration` format.

`timer-down:relative` - Utilizes the current date/time as the start and the Values item as the end to calculate a span. Displays the duration using the `in` format if the duration is positive, and the `ago` format if the duration is negative.

## Values Dictionary

EventStartDateTimeOffset = 2016-01-26 15:00:00

TaskDueDateTimeOffset = 2016-01-26 16:00:00

## Expressions

`Event Duration - {EventStartDateTimeOffset:timer-up}`

`Event Duration - {EventStartDateTimeOffset:timer-up:duration}`

`Event Duration - {EventStartDateTimeOffset:timer-up:relative}`

`Task Due - {TaskDueDateTimeOffset:timer-down}`

`Task Due - {TaskDueDateTimeOffset:timer-down:duration}`

`Task Due - {TaskDueDateTimeOffset:timer-down:relative}`

## Results (current time = 2016-01-26 15:25:00)

Event Duration - 00:25:00

Event Duration - 25.0 Minute(s)

Event Duration - 25.0 Minute(s) Ago

Task Due - 00:35:00

Task Due - 35.0 Minutes(s)

Task Due - In 35.0 Minute(s)
