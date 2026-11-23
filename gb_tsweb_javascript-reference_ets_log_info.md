# info

```javascript
Boolean info(String msg, [String category])
```

This function makes a web service call to the TrakSYS server and creates a info type entry in the tLog table with the specified `msg` and `category` values.

The function always returns `false`.

## Parameters

```javascript
String msg
```

```javascript
String category = "js"
```

## Examples

### Simple Info Log

```javascript
ets.log.info('Object does not exists.', 'JS Page Init');
```
