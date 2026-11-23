# Dynamic Date/Time Syntax

In certain Pages and Parts (as well as in some scripts), it is useful to specify date/time values as a "dynamic calculation". For example, the default Start and End Date properties of Filter part should always come up as Start Date = \<start of the week> and End Date = \<end of the week>. In these cases, it is not possible to specify a "hard coded" date for the default property. Pages and Parts that require this sort of Date/Time specification expose properties using a special TrakSYS data type called `DateTimeTs`. This string-based data type allows for specific date/times to be specified (such as 2016-07-04), or a special date/time calculation syntax that is evaluated at run-time. The following sections describe valid values for calculating a dynamic date/time...

## Standard Expressions

The following standard expressions can be used to calculate a date/time value.

### today

Returns the current date with 12:00:00 for the time.

### now

Returns the current date and time.

### hour

Returns the current date and time rounded down to the current hour. For example 2016-07-04 03:41:26 becomes 2016-07-04 03:00:00.

### minute

Returns the current date and time rounded down to the current minute. For example 2016-07-04 03:41:26 becomes 2016-07-04 03:41:00.

### second

Returns the current date and time rounded down to the current second. For example 2016-07-04 03:41:26 becomes 2016-07-04 03:41:26.

### weekstart

Returns the current date and time rounded down to the start of the current week (based on the TrakSYS Setting `WeekStartDay`). For example 2016-07-04 03:41:26 (a Monday) becomes 2016-07-03 / 2016-07-03 12:00:00 (the beginning of Sunday at the start of the week).

### weekend

Returns the current date and time rounded up to the end of the current week (based on the TrakSYS Setting `WeekStartDay`). For example 2016-07-04 03:41:26 (a Monday) becomes 2016-07-09 / 2016-07-10 12:00:00 (the end of Saturday at the end of the week).

### monthstart

Returns the current date and time rounded down to the start of the current month. For example 2016-07-04 03:41:26 becomes 2016-07-01 / 2016-07-01 12:00:00.

### monthend

Returns the current date and time rounded up to the end of the current month. For example 2016-07-04 03:41:26 becomes 2016-07-31 / 2016-08-01 12:00:00.

### yearstart

Returns the current date and time rounded down to the start of the current year. For example 2016-07-04 03:41:26 becomes 2016-01-01 / 2016-01-01 12:00:00.

### yearend

Returns the current date and time rounded up to the end of the current year. For example 2016-07-04 03:41:26 becomes 2016-12-31 / 2017-01-01 12:00:00.

## Calculating with Offsets

An addition or subtraction operation can be added to any of the standard expressions. The units being added or subtracted is relative based on the expression used..

### today - 1

2016-07-04 03:41:26 - 1 = 2016-07-03 12:00:00

### hour - 2

2016-07-04 03:41:26 - 2 = 2016-07-04 01:00:00

### minute - 10

2016-07-04 03:41:26 - 1 = 2016-07-03 03:30:00

### weekstart - 1

2016-07-04 03:41:26 - 1 = 2016-06-26 12:00:00

### monthstart - 1

2016-07-04 03:41:26 - 1 = 2016-06-01 12:00:00
