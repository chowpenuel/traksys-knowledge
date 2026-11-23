# Keystroke Listener

## General

### Start Delimiter CSV

The Start Delimiter CSV allows for an **ASCII character code** to be configured to serve as the starting boundary for the data contained within a CSV file.

### End Delimiter CSV

The End Delimiter CSV allows for an **ASCII character code** to be configured to serve as the ending boundary for the data contained within a CSV file.

Example of setting Start Delimiter CSV to **`~~`** and End Delimiter CSV to **`*1`**:

```
Start Delimiter CSV = 126, 126
End Delimiter CSV = 42, 49
```

### On Complete JS Function

This field specifies a JS Function that is to be called once the keystroke listener has finished recording. This function should take a single parameter that should have a string type.

### Target Values Key

This setting configures the Values Dictionary key that will be used to contain the recorded keystrokes.

## Advanced

### Input Timeout (Milliseconds)

This field determines the allowable time frame (in milliseconds) for which the Keystroke listener will record for when active.

### Debug Output

Enabling this setting will allow for the recorded keystrokes to be displayed as output within the developer console contained within the web browser. Typically this console can be accessed via the developer tools (F12).

### Enabled

Specifies if this entity is actively considered within standard functionality. An entity is typically disabled when it is no longer required for future data collection or functionality, but is still required in order to contextualize historical data that has been captured against it (since deleting the entity from the database usually results in the clearing of any associated data).
