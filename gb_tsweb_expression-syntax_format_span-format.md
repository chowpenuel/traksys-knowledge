# Span Format

When the Values Dictionary item specified by an expression is an integer representation of a duration in seconds, a special format code can be specified to convert the seconds into a more human readable description of time. The format code `span`, followed by **one of 4 different format suffixes** can be specified to convert seconds to a text-based duration.

`hms` - Returns XX:YY:ZZ where XX = number of hours, YY = number of minutes, and ZZ = number of seconds.

`duration` - Returns a text representation of the seconds in the nearest logical units. < 60 seconds = N Seconds, < 60 minutes = N.1 minutes, < 24 hours = N.1 Hours, etc…

`ago` - Returns a format similar to duration (above), but the assumption is that the timespan is in relation to some fixed point in the past. So 1.4 Minute(s) Ago, or 4.5 Hour(s) Ago.

`in` - Returns a format similar to duration (above), but the assumption is that the timespan is in relation to some fixed point in the future. So In 1.4 Minute(s), or In 4.5 Hour(s).

## Values Dictionary

EventDurationSeconds = 120

SecondsSinceTaskStarted = 45

SecondsUntilTaskIsDue = 30

## Expressions

`Event Duration - {EventDurationSeconds:span:duration}`

`Event Duration - {EventDurationSeconds:span:hms}`

`Task Started - {SecondsSinceTaskStarted:span:ago}`

`Task Due - {SecondsUntilTaskIsDue:span:in}`

## Results

Event Duration - 2.0 Minutes(s)

Event Duration - 00:02:00

Task Started - 1.7 Minute(s) Ago

Task Due - In 30 Second(s)
