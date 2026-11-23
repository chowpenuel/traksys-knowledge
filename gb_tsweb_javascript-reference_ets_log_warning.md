# warning

```javascript
Boolean warning(String msg, Number warningLevel, [String category])
```

This function makes a web service call to the TrakSYS server and creates a warning type entry in the tLog table with the specified `msg` and `category` values.

The function always returns `false`.

## Parameters

```javascript
String msg
```

```javascript
Number warningLevel
```

If `warningLevel` is less than the TrakSYS application's MinWarningLevel, the entry will `NOT` be saved in tLog. Default MinWarningLevel = 5

```javascript
String category = "js"
```

## Examples

### Simple Warning Log

```javascript
ets.log.warning('Object does not exists.', 5, 'JS Page Init');
```
