# datetime

This is used to retrieve current and calculated date/time values.

### Examples

```html
{datetime|Time}
```

Returns the current date and time.

```html
{datetime|Date}
```

Returns the current date (at 12:00:00).

```html
{datetime|DateStart}
```

Returns the current date (at 12:00:00).

```html
{datetime|DateEnd}
```

Returns the current date (at 23:59:59).

```html
{datetime|MinuteStart}
```

Returns the current date/time at the start of the current minute.

```html
{datetime|MinuteEnd}
```

Returns the current date/time at the end of the current minute.

```html
{datetime|HourStart}
```

Returns the current date/time at the start of the current hour.

```html
{datetime|HourEnd}
```

Returns the current date/time at the end of the current hour.

```html
{datetime|WeekStart}
```

Returns the current date/time at the start of the current week.

```html
{datetime|WeekEnd}
```

Returns the current date/time at the end of the current week.

```html
{datetime|MonthStart}
```

Returns the current date/time at the start of the current month.

```html
{datetime|MonthEnd}
```

Returns the current date/time at the end of the current month.

```html
{datetime|YearStart}
```

Returns the current date/time at the start of the current year.

```html
{datetime|YearEnd}
```

Returns the current date/time at the end of the current year.

```html
{datetime|Date.AddHours(2).AddMinutes(-15).AddSeconds(3)}
```

Returns the current date and adds 2 hours, subtracts 15 minutes and adds 3 seconds.

```html
{datetime|Date.AddYears(-1).AddMonths(2).AddDays(3)}
```

Returns the current date and subtracts 1 year, adds 2 months and adds 3 days.
