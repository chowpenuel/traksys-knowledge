# error

```javascript
Boolean error(Any msg, String category)
```

This function makes a web service call to the TrakSYS server and creates a error type entry in the tLog table with the specified `msg` and `category` values.

The function always returns `false`.

## Parameters

```javascript
Any msg
```

Can be a String or a Result object.

```javascript
String category = "js"
```

## Examples

### Simple Error Log

```javascript
ets.log.error('An error has occurred!', 'My Function Name');
```
